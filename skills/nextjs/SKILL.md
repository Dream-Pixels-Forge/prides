---
name: nextjs
description: Expert guidance for building production-ready applications with Next.js 14+, including App Router, Server Components, data fetching, API routes, authentication, and performance optimization.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Next.js - React Framework

You are a frontend expert specialized in building production-ready applications with Next.js—the React framework that enables server-side rendering, static site generation, and more.

## Core Concepts

### What is Next.js?

- **React Framework**: Full-stack React framework
- **Server Components**: Default in App Router
- **Multiple Rendering**: SSR, SSG, ISR, CSR
- **File-based Routing**: Directory-based routing
- **API Routes**: Backend in your app
- **Optimizations**: Built-in image, font, script optimization

### App Router vs Pages Router

| Feature | App Router | Pages Router |
|---------|------------|-------------|
| **Routing** | `app/` directory | `pages/` directory |
| **Components** | Server by default | Client by default |
| **Data Fetching** | async/await in components | getStaticProps, getServerSideProps |
| **Layouts** | Built-in layouts | _app.js, _document.js |
| **Streaming** | Built-in with Suspense | No |
| **Error Handling** | error.tsx | _error.js |

## Installation

### Create New Project

```bash
# Interactive
npx create-next-app@latest my-app

# Non-interactive
npx create-next-app@latest my-app \
  --typescript \
  --tailwind \
  --eslint \
  --app \
  --src-dir \
  --import-alias "@/*" \
  --use-npm
```

### Available Options

| Flag | Description |
|------|-------------|
| `--typescript` | TypeScript |
| `--javascript` | JavaScript |
| `--tailwind` | Tailwind CSS |
| `--eslint` | ESLint |
| `--app` | App Router (default) |
| `--src-dir` | Use `src/` directory |
| `--import-alias` | Import alias (default `@/*`) |
| `--use-npm` | Use npm |
| `--use-yarn` | Use yarn |
| `--use-pnpm` | Use pnpm |
| `--no-turbopack` | Don't use Turbopack |

## Project Structure

```
my-app/
├── src/
│   ├── app/                    # App Router
│   │   ├── layout.tsx          # Root layout
│   │   ├── page.tsx            # Home page
│   │   ├── globals.css         # Global styles
│   │   ├── loading.tsx         # Loading UI
│   │   ├── error.tsx           # Error UI
│   │   ├── not-found.tsx       # 404 UI
│   │   ├── (group)/            # Route groups
│   │   │   └── page.tsx
│   │   ├── dashboard/          # Nested routes
│   │   │   └── page.tsx
│   │   └── api/                # API routes
│   │       └── route.ts
│   ├── components/             # React components
│   ├── lib/                    # Utilities
│   ├── hooks/                  # Custom hooks
│   └── types/                   # TypeScript types
├── public/                     # Static files
├── next.config.js              # Next.js config
├── tailwind.config.ts          # Tailwind config
├── tsconfig.json               # TypeScript config
└── package.json
```

## App Router

### Root Layout

```tsx
// src/app/layout.tsx
import type { Metadata } from 'next';
import { Inter } from 'next/font/google';
import './globals.css';

const inter = Inter({ subsets: ['latin'] });

export const metadata: Metadata = {
  title: 'My App',
  description: 'Description here',
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body className={inter.className}>
        <header>
          <nav>Navigation</nav>
        </header>
        <main>{children}</main>
        <footer>Footer</footer>
      </body>
    </html>
  );
}
```

### Page Component

```tsx
// src/app/page.tsx
export default function HomePage() {
  return (
    <div>
      <h1>Welcome to Next.js</h1>
      <p>Get started by editing src/app/page.tsx</p>
    </div>
  );
}
```

### Server Components

```tsx
// Server Component (default) - data fetching directly
async function getData() {
  const res = await fetch('https://api.example.com/data');
  if (!res.ok) throw new Error('Failed to fetch');
  return res.json();
}

export default async function ServerComponent() {
  const data = await getData();
  
  return <div>{data.title}</div>;
}
```

### Client Components

```tsx
// Client Component - use 'use client'
'use client';

import { useState } from 'react';

export default function ClientComponent() {
  const [count, setCount] = useState(0);
  
  return (
    <button onClick={() => setCount(c => c + 1)}>
      Count: {count}
    </button>
  );
}
```

### Mixing Server and Client

```tsx
// Server Component
export default function Page() {
  return (
    <div>
      <ServerData />
      <ClientCounter />
    </div>
  );
}

// Client Component (separate file)
'use client';
export function ClientCounter() {
  // interactive logic
}
```

## Data Fetching

### Server-Side Fetching

```tsx
// Fetch with caching (default)
async function getData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'force-cache', // default
  });
  return res.json();
}

// Dynamic fetching (no cache)
async function getDynamicData() {
  const res = await fetch('https://api.example.com/data', {
    cache: 'no-store',
  });
  return res.json();
}

// Revalidate every 60 seconds
async function getRevalidatedData() {
  const res = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 },
  });
  return res.json();
}
```

### Route Handlers (API)

```ts
// src/app/api/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const data = { message: 'Hello, World!' };
  return NextResponse.json(data);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  
  // Process data
  
  return NextResponse.json({ success: true, data: body });
}
```

### Query Params

```ts
// src/app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';

export async function GET(request: NextRequest) {
  const searchParams = request.nextUrl.searchParams;
  const page = searchParams.get('page') || '1';
  const limit = searchParams.get('limit') || '10';
  
  // Fetch from database
  
  return NextResponse.json({
    users: [],
    page: Number(page),
    limit: Number(limit),
  });
}
```

## Routing

### Dynamic Routes

```tsx
// src/app/blog/[slug]/page.tsx
export default function BlogPost({
  params,
}: {
  params: { slug: string };
}) {
  return <div>Blog post: {params.slug}</div>;
}

// Generate static params
export async function generateStaticParams() {
  const posts = await getPosts();
  
  return posts.map((post) => ({
    slug: post.slug,
  }));
}
```

### Optional Parameters

```tsx
// src/app/[...slug]/page.tsx
export default function CatchAll({
  params,
}: {
  params: { slug: string[] };
}) {
  return <div>Path: {params.slug.join('/')}</div>;
}
```

### Route Groups

```tsx
// (marketing)/about/page.tsx - doesn't affect URL
// (dashboard)/settings/page.tsx - doesn't affect URL

export default function AboutPage() {
  return <h1>About</h1>;
}
```

### Parallel Routes

```tsx
// @modal slot
// src/app/@modal/(.)photo/[id]/page.tsx
export default function PhotoModal({ params }) {
  return (
    <dialog open>
      <img src={`/photos/${params.id}.jpg`} />
    </dialog>
  );
}

// Intercepting routes
// (.)photo/[id] - intercepts /photo/[id]
```

## Navigation

### Link Component

```tsx
import Link from 'next/link';

export function Navigation() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/about">About</Link>
      <Link href="/blog/nextjs-guide">Blog Post</Link>
      <Link href="/products/123" scroll={false}>
        Product (no scroll to top)
      </Link>
    </nav>
  );
}
```

### useRouter Hook

```tsx
'use client';

import { useRouter, usePathname, useSearchParams } from 'next/navigation';

export function NavigationComponent() {
  const router = useRouter();
  const pathname = usePathname();
  const searchParams = useSearchParams();
  
  const handleNavigation = () => {
    router.push('/dashboard');
    // or
    router.replace('/dashboard'); // no history
    // or
    router.refresh(); // refresh data
  };
  
  // Read params
  const page = searchParams.get('page');
  
  return <button onClick={handleNavigation}>Go</button>;
}
```

### Intercepting Routes

```tsx
'use client';

import Link from 'next/link';

export function PhotoLink({ id }) {
  return (
    // (.) enables intercepting
    <Link href={`(.)/photos/${id}`} scroll={false}>
      <img src={`/photos/${id}.jpg`} />
    </Link>
  );
}
```

## Server Actions

### Defining Actions

```ts
// src/app/actions.ts
'use server';

export async function createPost(formData: FormData) {
  'use server';
  
  const title = formData.get('title');
  
  // Database operation
  await db.post.create({ title });
  
  // Revalidate
  revalidatePath('/posts');
  
  return { success: true };
}
```

### Using Actions

```tsx
// src/app/page.tsx
import { createPost } from './actions';

export default function Page() {
  return (
    <form action={createPost}>
      <input name="title" type="text" />
      <button type="submit">Create</button>
    </form>
  );
}
```

### With useFormState

```tsx
'use client';

import { useFormState } from 'react-dom';
import { createPost } from './actions';

const initialState = { message: '' };

export function CreatePost() {
  const [state, formAction] = useFormState(createPost, initialState);
  
  return (
    <form action={formAction}>
      <input name="title" type="text" />
      <p>{state.message}</p>
      <button type="submit">Submit</button>
    </form>
  );
}
```

## Styling

### Tailwind CSS

```tsx
// src/app/page.tsx
export default function Page() {
  return (
    <div className="min-h-screen bg-gray-100 p-8">
      <h1 className="text-4xl font-bold text-gray-900">
        Hello World
      </h1>
      <button className="bg-blue-500 hover:bg-blue-700 text-white px-4 py-2 rounded">
        Click me
      </button>
    </div>
  );
}
```

### CSS Modules

```tsx
// Button.module.css
.button {
  background: blue;
  color: white;
  padding: 8px 16px;
  border-radius: 4px;
}

// Button.tsx
import styles from './Button.module.css';

export function Button() {
  return <button className={styles.button}>Click</button>;
}
```

### Global CSS

```css
/* src/app/globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --primary: #0066ff;
}

body {
  font-family: system-ui, sans-serif;
}
```

## Optimizations

### Image Component

```tsx
import Image from 'next/image';

export function MyImage() {
  return (
    <Image
      src="/hero.jpg"
      alt="Hero"
      width={800}
      height={600}
      priority       // Load immediately
      placeholder="blur"
      blurDataURL="data:image/..." // or remotePatterns
      sizes="(max-width: 768px) 100vw, 50vw"
    />
  );
}
```

### Font Optimization

```tsx
import { Inter, Roboto_Mono } from 'next/font/google';

const inter = Inter({
  subsets: ['latin'],
  display: 'swap',
  variable: '--font-inter',
});

const robotoMono = Roboto_Mono({
  subsets: ['latin'],
  variable: '--font-roboto',
});

export default function Layout({ children }) {
  return (
    <html className={`${inter.variable} ${robotoMono.variable}`}>
      <body>{children}</body>
    </html>
  );
}
```

### Script Optimization

```tsx
import Script from 'next/script';

export function Analytics() {
  return (
    <>
      <Script
        src="https://example.com/script.js"
        strategy="lazyOnload" // 'beforeInteractive', 'afterInteractive', 'lazyOnload', 'worker'
      />
      <Script
        dangerouslySetInnerHTML={{
          __html: `console.log('inline script')`,
        }}
      />
    </>
  );
}
```

## Authentication

### With NextAuth.js

```ts
// src/app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import GoogleProvider from 'next-auth/providers/google';

const handler = NextAuth({
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    }),
  ],
  callbacks: {
    async session({ session, token }) {
      session.user.id = token.sub!;
      return session;
    },
  },
});

export { handler as GET, handler as POST };
```

### Using Session

```tsx
// Server Component
import { getServerSession } from 'next-auth';

export default async function Dashboard() {
  const session = await getServerSession(authOptions);
  
  if (!session) {
    redirect('/api/auth/signin');
  }
  
  return <div>Welcome, {session.user.name}</div>;
}

// Client Component
'use client';

import { useSession, signIn, signOut } from 'next-auth/react';

export function AuthButton() {
  const { data: session } = useSession();
  
  if (session) {
    return <button onClick={() => signOut()}>Sign out</button>;
  }
  
  return <button onClick={() => signIn()}>Sign in</button>;
}
```

## Middleware

```ts
// src/middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(request: NextRequest) {
  // Check auth
  const token = request.cookies.get('auth-token');
  
  if (!token && !request.nextUrl.pathname.startsWith('/login')) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
  
  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*', '/profile/:path*'],
};
```

## Deployment

### Build

```bash
# Development
npm run dev

# Production build
npm run build

# Start production server
npm start

# Lint
npm run lint
```

### Environment Variables

```env
# .env.local
DATABASE_URL=postgresql://...
API_KEY=secret
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### Output

- Static export: `npm run build` → `out/`
- Server: `npm run build` → `.next/`

## Troubleshooting

### Hydration Errors

```tsx
// Use useEffect for client-only rendering
'use client';

import { useEffect, useState } from 'react';

export function ClientOnly({ children }) {
  const [mounted, setMounted] = useState(false);
  
  useEffect(() => setMounted(true), []);
  
  if (!mounted) return null;
  
  return children;
}
```

### 404 in Production

- Check `next.config.js` has `output: 'export'` for static
- Verify `trailingSlash` setting

### Build Errors

```bash
# Clear .next cache
rm -rf .next

# Rebuild
npm run build
```

## Validation

Before deployment:
1. **Build**: `npm run build`
2. **Lint**: `npm run lint`
3. **Type check**: `npx tsc --noEmit`
4. **Test**: Verify all pages load

## Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js Learn](https://nextjs.org/learn)
- [Next.js GitHub](https://github.com/vercel/next.js)
