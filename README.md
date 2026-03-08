# Composio Composer | X Skill for OpenClaw

Post, retrieve, and delete tweets on Twitter/X through Composio's integration platform.

## Quick start

```bash
# Install to your OpenClaw skills directory
git clone https://github.com/RuneweaverStudios/composio-composer-xskill.git
cp -r composio-composer-xskill ~/.openclaw/workspace/skills/

# Install dependencies
pip install requests beautifulsoup4 python-dotenv
```

## Implemented features

- **Post tweets** -- Send text tweets (max 280 characters)
- **Retrieve tweets** -- Get tweet data by ID
- **Delete tweets** -- Remove tweets by ID

## Prerequisites

- Python 3.8+
- Composio account with Twitter/X integration
- Valid Composio credentials (see Configuration)

## Configuration

Create a `.env` file in the skill directory (do NOT commit this file):

```env
COMPOSIO_CLIENT_ID=your_client_id_here
COMPOSIO_API_KEY=your_api_key_here
COMPOSIO_SESSION_TOKEN=your_session_token_here
COMPOSIO_BEARER_TOKEN=your_bearer_token_here
COMPOSIO_USER_ID=your_user_id_here
COMPOSIO_API_BASE=https://backend.composio.dev/api/v1
```

## Usage

### Python API

```python
from composio_composer_xskill import post_tweet

# Post a tweet
result = post_tweet("Hello from OpenClaw!", composio_auth_token="your_token")
print(f"Tweet posted: {result['tweet_url']}")
```

### Retrieve a tweet

```python
from composio_composer_xskill import get_tweet

result = get_tweet("1234567890123456789", composio_auth_token="your_token")
print(result)
```

### Delete a tweet

```python
from composio_composer_xskill import delete_tweet

result = delete_tweet("1234567890123456789", composio_auth_token="your_token")
print(result)
```

## How it works

1. **Authentication**: Uses bearer token for Composio API requests
2. **Primary path**: Posts via Composio's REST API endpoint
3. **Fallback**: If the Composio API is unreachable, falls back to direct Twitter API v2 (experimental)
4. **Rate limiting**: Built-in request throttling (1 request/second minimum)

## Rate limits

- Twitter/X: 200 tweets per day (authenticated)
- Composio: Per API plan limits
- Respect rate limits to avoid account restrictions

## Troubleshooting

| Problem | Solution |
|---------|----------|
| Authentication errors | Verify credentials; session tokens expire after 2 hours |
| Rate limit (429) | Wait before retrying; implement exponential backoff |
| Connection errors | Check internet; verify Composio API status |

## License

MIT
