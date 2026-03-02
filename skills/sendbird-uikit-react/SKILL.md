---
name: sendbird-uikit-react
description: Expert guidance for integrating and building chat applications with Sendbird UIKit for React, including channel components, message UI, authentication, and customization.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Sendbird UIKit for React

You are a frontend engineer specialized in building chat applications with Sendbird UIKit for React—a feature-rich and customizable chat UI kit with messaging, channel management, and user authentication.

## Core Concepts

Sendbird UIKit is a **component library** (not copy-paste like shadcn/ui) that provides:
- **Full-featured chat UI**: Ready-made conversation interfaces
- **Modular architecture**: Use individual components or full App
- **SDK integration**: Built on Sendbird Chat SDK
- **Customizable**: Style and behavior can be overridden

## Installation

### Prerequisites

- Node.js 18+
- npm 9+ or yarn 3+
- Sendbird Application ID (from Sendbird dashboard)

### Install Package

```bash
# Using npm
npm install @sendbird/uikit-react

# Using yarn
yarn add @sendbird/uikit-react
```

### Install Sendbird Chat SDK

```bash
npm install @sendbird/chat
```

## Quick Start

### 1. Basic Setup

```tsx
import '@sendbird/uikit-react/dist/index.css';
import { useState } from 'react';
import { App } from '@sendbird/uikit-react';

function ChatApp() {
  const [appId] = useState('YOUR_APP_ID');
  const [userId] = useState('USER_ID');
  const [nickname] = useState('NICKNAME');

  return (
    <App
      appId={appId}
      userId={userId}
      nickname={nickname}
    />
  );
}
```

### 2. Using Individual Components

```tsx
import { Channel, ChannelList, SendBirdProvider } from '@sendbird/uikit-react';

function CustomChat() {
  return (
    <SendBirdProvider appId="YOUR_APP_ID" userId="USER_ID">
      <div className="chat-container">
        <ChannelList />
        <Channel />
      </div>
    </SendBirdProvider>
  );
}
```

## Component Architecture

### Core Components

| Component | Description |
|-----------|-------------|
| **SendBirdProvider** | Context provider for SDK, wraps all other components |
| **App** | Full-featured group channel app (all-in-one) |
| **ChannelList** | List of channels user belongs to |
| **Channel** | Conversation view with messages |
| **ChannelSettings** | Channel configuration panel |
| **MessageSearch** | Search messages within a channel |
| **OpenChannel** | Open channel conversation |
| **OpenChannelSettings** | Open channel settings |

### Using sendBirdSelectors

```tsx
import { useSendbirdStateContext, sendBirdSelectors } from '@sendbird/uikit-react';

function CustomComponent() {
  const globalStore = useSendbirdStateContext();
  
  // Get current channel
  const currentChannel = sendBirdSelectors.getCurrentChannel(globalStore);
  
  // Get current user
  const currentUser = sendBirdSelectors.getUser(globalStore);
}
```

## File Structure

```
src/
├── components/
│   ├── ChatApp.tsx        # Full App component
│   ├── ChannelList.tsx    # Custom channel list
│   └── MessageList.tsx    # Custom message display
├── hooks/
│   └── useChat.ts         # Custom chat hooks
└── App.tsx
```

## Authentication

### User Authentication

```tsx
// Automatic user creation (if allowed in dashboard)
<App
  appId={appId}
  userId={userId}
  nickname={nickname}
/>

// With access token (recommended for production)
<App
  appId={appId}
  userId={userId}
  accessToken={accessToken}
  nickname={nickname}
/>
```

### SB Connect (External Auth)

```tsx
import { useMemo } from 'react';
import { SendBirdProvider } from '@sendbird/uikit-react';

function SBConnectExample() {
  const sb = useMemo(() => new SendbirdChat({
    appId: 'APP_ID',
    websocket: true
  }), []);

  return (
    <SendBirdProvider sdk={sb}>
      <App />
    </SendBirdProvider>
  );
}
```

## Channel Management

### Creating a Channel

```tsx
import { useGroupChannel } from '@sendbird/uikit-react/Channel/context';

function CreateChannelButton() {
  const { createChannel } = useGroupChannel();
  
  const handleCreate = async () => {
    const params = {
      name: 'Channel Name',
      coverUrl: 'https://example.com/image.jpg',
      customType: 'custom_type',
      data: { key: 'value' },
      inviteeIds: ['user1', 'user2'],
      isDistinct: false,
    };
    
    const channel = await createChannel(params);
  };
  
  return <button onClick={handleCreate}>Create Channel</button>;
}
```

### Channel Types

| Type | Description | Use Case |
|------|-------------|----------|
| **Group Channel** | 1-on-1 or group chat | Most chat apps |
| **Open Channel** | Public broadcast | Live streaming, Q&A |
| **Supergroup** | Large-scale group | Community forums |

## Message Features

### Sending Messages

```tsx
import { useChannel } from '@sendbird/uikit-react/Channel/context';

function MessageInput() {
  const { sendUserMessage, sendFileMessage } = useChannel();
  
  const sendText = async (text: string) => {
    const params = {
      message: text,
      customType: '',
      data: '',
    };
    await sendUserMessage(params);
  };
  
  const sendFile = async (file: File) => {
    const params = {
      file: file,
      fileName: file.name,
      fileSize: file.size,
      mimeType: file.type,
    };
    await sendFileMessage(params);
  };
}
```

### Message Types

- **UserMessage**: Text messages
- **FileMessage**: File/image attachments
- **AdminMessage**: System messages
- **MultipleStatusMessage**: Reactions, polls

## Customization

### Theme Customization

```css
/* Custom CSS variables */
.sendbird-theme--dark {
  --sendbird-primary-color-500: #6B46C1;
  --sendbird-secondary-color-500: #9F7AEA;
}
```

### Custom Components

```tsx
import { FileMessage, UserMessage } from '@sendbird/uikit-react/Channel/components';

function CustomMessage(props) {
  if (props.message.isUserMessage()) {
    return (
      <div className="custom-message">
        <UserMessage {...props} />
      </div>
    );
  }
  return <FileMessage {...props} />;
}

// Override in Channel
<Channel
  renderMessage={CustomMessage}
/>
```

### Custom Input

```tsx
function CustomMessageInput() {
  const { currentChannel } = useChannel();
  
  const sendMessage = (text) => {
    currentChannel.sendUserMessage({
      message: text
    });
  };
  
  return (
    <div className="custom-input">
      <input onKeyDown={(e) => {
        if (e.key === 'Enter') sendMessage(e.target.value);
      }} />
    </div>
  );
}
```

## Event Handling

### Listening to Events

```tsx
import { useEffect } from 'react';
import { useSendbirdStateContext } from '@sendbird/uikit-react';

function MessageListener() {
  const globalStore = useSendbirdStateContext();
  
  useEffect(() => {
    const sdk = globalStore?.stores?.sdkStore?.sdk;
    if (!sdk) return;
    
    const channelHandler = new sdk.ChannelHandler();
    
    channelHandler.onMessageReceived = (channel, message) => {
      console.log('New message:', message);
    };
    
    channelHandler.onTypingStatusChanged = (channel) => {
      console.log('Typing in channel:', channel);
    };
    
    sdk.addChannelHandler('UNIQUE_ID', channelHandler);
    
    return () => {
      sdk.removeChannelHandler('UNIQUE_ID');
    };
  }, [globalStore]);
}
```

## Common Patterns

### 1. Group Chat

```tsx
import { App } from '@sendbird/uikit-react';

function GroupChatApp() {
  return (
    <App
      appId={APP_ID}
      userId={USER_ID}
      nickname={NICKNAME}
      // Optional: configure UI
      showChannelList
      showChannelSettings
    />
  );
}
```

### 2. 1-on-1 Chat

```tsx
import { useState, useEffect } from 'react';
import { Channel, SendBirdProvider } from '@sendbird/uikit-react';

function OneOnOneChat({ otherUserId }) {
  const [channelUrl, setChannelUrl] = useState(null);
  
  useEffect(() => {
    // Create or get existing 1-on-1 channel
    const createChannel = async () => {
      const params = {
        isDistinct: true,
        invitedUserIds: [otherUserId],
      };
      // Use Sendbird SDK to create channel
    };
    createChannel();
  }, [otherUserId]);
  
  return channelUrl ? (
    <Channel channelUrl={channelUrl} />
  ) : (
    <div>Loading...</div>
  );
}
```

### 3. Open Channel (Live Streaming)

```tsx
import { OpenChannel } from '@sendbird/uikit-react';

function LiveStreamChat() {
  return (
    <OpenChannel
      channelUrl={CHANNEL_URL}
      onChatResized={(width, height) => {
        console.log('Chat resized:', width, height);
      }}
    />
  );
}
```

## Troubleshooting

### Import Errors

- Ensure `@sendbird/uikit-react` and `@sendbird/chat` are installed
- Import the CSS: `import '@sendbird/uikit-react/dist/index.css';`
- Check that your React version is 18+

### Connection Issues

- Verify app ID is correct
- Check network connectivity
- Ensure user ID format is correct (alphanumeric + special chars: - _ . @)

### Style Conflicts

- Override CSS using specific selectors
- Use `!important` sparingly
- Check z-index if UI appears behind elements

### Performance Issues

- Use virtualization for large message lists
- Lazy load components when possible
- Implement pagination for channels

## Validation and Quality

Before committing:
1. **Type check**: Run `tsc --noEmit`
2. **Lint**: Run linter to catch issues
3. **Test**: Verify chat functionality works
4. **Accessibility**: Test keyboard navigation
5. **Responsive**: Test on different screen sizes

## Resources

- [Sendbird UIKit Docs](https://sendbird.com/docs/uikit)
- [Sendbird Community](https://community.sendbird.com)
- [UIKit React Source](https://github.com/sendbird/sendbird-uikit-react-sources)
- [Storybook](https://sendbird.github.io/sendbird-uikit-react/)
