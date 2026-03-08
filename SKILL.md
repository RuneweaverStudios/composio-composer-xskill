---
name: composio-composer-xskill
displayName: Composio Composer for X
description: Post, retrieve, and delete tweets on Twitter/X through Composio's integration platform.
version: 1.1.0
---

# Composio Composer | X Skill

Post, retrieve, and delete tweets on Twitter/X through Composio's integration platform.

## Tool definitions

### post_tweet

Posts a tweet to Twitter/X using Composio.

```python
def post_tweet(content: str, composio_auth_token: str) -> dict:
```

**Parameters:**
- `content` (str): The tweet content (max 280 characters)
- `composio_auth_token` (str): The Composio authentication token

**Returns:**
- `dict` with `success` (bool), `tweet_id` (str), `tweet_url` (str), or `error` (str)

**Example:**
```python
from composio_composer_xskill import post_tweet

result = post_tweet(
    content="Hello from OpenClaw!",
    composio_auth_token="your_token"
)
# {'success': True, 'tweet_id': '123...', 'tweet_url': 'https://twitter.com/i/status/123...', 'content': 'Hello from OpenClaw!'}
```

### get_tweet

Retrieves a tweet by ID.

```python
def get_tweet(tweet_id: str, composio_auth_token: str) -> dict:
```

**Parameters:**
- `tweet_id` (str): The tweet ID to retrieve
- `composio_auth_token` (str): The Composio authentication token

**Returns:**
- `dict` with `success` (bool) and `tweet` data or `error` (str)

### delete_tweet

Deletes a tweet by ID.

```python
def delete_tweet(tweet_id: str, composio_auth_token: str) -> dict:
```

**Parameters:**
- `tweet_id` (str): The tweet ID to delete
- `composio_auth_token` (str): The Composio authentication token

**Returns:**
- `dict` with `success` (bool) and `message` or `error` (str)

## How it works

1. **Primary**: Sends requests to Composio's REST API (`/twitter/tweets`)
2. **Fallback**: If Composio is unreachable, attempts direct Twitter API v2 (experimental -- requires valid OAuth2 bearer token)
3. **Rate limiting**: Built-in 1-second minimum interval between requests

## Configuration

Required environment variables:

| Variable | Description |
|----------|-------------|
| `COMPOSIO_BEARER_TOKEN` | Bearer token for Composio API |
| `COMPOSIO_API_KEY` | Composio API key |
| `COMPOSIO_CLIENT_ID` | Composio client ID |
| `COMPOSIO_SESSION_TOKEN` | Session token (expires after 2 hours) |
| `COMPOSIO_USER_ID` | Your Composio user ID |

## Setup

```bash
pip install requests beautifulsoup4 python-dotenv
```

Configure credentials in a `.env` file or system environment variables.

## Notes

- Rate limits apply per Twitter/X and Composio policies
- Session tokens expire after 7200 seconds (2 hours)
- The direct Twitter API fallback is experimental and may not work without proper OAuth2 setup
