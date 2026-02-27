# API Reference - {{API Name}}

{{Brief description of the API}}

## Base URL

```
{{base-url}}
```

## Authentication

{{Authentication method description}}

```{{language}}
// Example authentication
{{auth-example}}
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `Authorization` | Yes | Bearer token |
| `Content-Type` | Yes | `application/json` |
| `Accept` | No | Response format |

---

## Endpoints

### {{Endpoint Category}}

#### `{{METHOD}} {{endpoint-path}}`

{{Endpoint description}}

**Parameters:**

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `{{param1}}` | {{type}} | Yes | {{Description}} |
| `{{param2}}` | {{type}} | No | {{Description}} |

**Request Body:**

```json
{
  "{{field1}}": "{{type}}",
  "{{field2}}": "{{type}}"
}
```

**Response:**

```json
{
  "success": true,
  "data": {
    "{{field1}}": "{{value}}",
    "{{field2}}": "{{value}}"
  }
}
```

**Status Codes:**

| Code | Description |
|------|-------------|
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | Not Found |
| 500 | Server Error |

**Example:**

```{{language}}
// Request example
{{request-example}}
```

---

## Error Handling

### Error Response Format

```json
{
  "success": false,
  "error": {
    "code": "{{ERROR_CODE}}",
    "message": "{{Human-readable message}}",
    "details": {}
  }
}
```

### Error Codes

| Code | Description | Resolution |
|------|-------------|------------|
| `{{ERROR_CODE_1}}` | {{Description}} | {{Resolution}} |
| `{{ERROR_CODE_2}}` | {{Description}} | {{Resolution}} |

---

## Rate Limiting

{{Rate limiting description}}

| Tier | Requests/minute | Requests/day |
|------|-----------------|--------------|
| Free | {{X}} | {{Y}} |
| Pro | {{X}} | {{Y}} |
| Enterprise | {{X}} | {{Y}} |

### Rate Limit Headers

| Header | Description |
|--------|-------------|
| `X-RateLimit-Limit` | Maximum requests allowed |
| `X-RateLimit-Remaining` | Requests remaining |
| `X-RateLimit-Reset` | Time when limit resets |

---

## Pagination

{{Pagination description}}

### Query Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `page` | integer | 1 | Page number |
| `limit` | integer | 20 | Items per page |
| `sort` | string | `created_at` | Sort field |
| `order` | string | `desc` | Sort order |

### Response Format

```json
{
  "success": true,
  "data": [],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "totalPages": 5
  }
}
```

---

## Versioning

{{API versioning strategy}}

Current version: `{{version}}`

---

## SDKs & Libraries

| Language | Repository | Version |
|----------|------------|---------|
| JavaScript | {{repo-url}} | {{version}} |
| Python | {{repo-url}} | {{version}} |
| Go | {{repo-url}} | {{version}} |

---

## Changelog

### Version {{version}}

- {{Change 1}}
- {{Change 2}}

---

## Support

- **Documentation**: {{docs-url}}
- **API Status**: {{status-url}}
- **Support Email**: {{support-email}}
