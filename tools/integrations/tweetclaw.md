# TweetClaw

OpenClaw plugin and npm package for X/Twitter automation through Xquik API endpoints. Use it when an agent needs to search tweets, search tweet replies, post tweets, post tweet replies, export followers, look up users, handle media, monitor accounts, receive webhooks, or run giveaway draws.

## Capabilities

| Integration | Available | Notes |
|-------------|-----------|-------|
| API | ✓ | Xquik REST API for X/Twitter read and write workflows |
| MCP | - | Use the OpenClaw plugin or Xquik API path |
| CLI | - | No standalone CLI |
| SDK | ✓ | npm package `@xquik/tweetclaw` for OpenClaw agents |

## Authentication

- **Type**: Xquik API key for account-backed actions
- **Header**: `Authorization: Bearer {api_key}`
- **Install**: Add `@xquik/tweetclaw` to an OpenClaw setup
- **Note**: Store API keys in the agent runtime or OpenClaw configuration. Never paste tokens in prompts, docs, commits, or issue text.

## Common Agent Operations

### Search tweets for campaign research

Use tweet search before drafting launch posts, competitor commentary, customer research summaries, or community response plans.

```bash
GET https://xquik.com/api/v1/x/tweets/search?q={query}&limit=20
Authorization: Bearer {api_key}
```

### Search tweet replies

Use reply search to find questions, complaints, objections, testimonials, and high-intent discussion under a tweet.

```bash
GET https://xquik.com/api/v1/x/tweets/{tweet_id}/replies
Authorization: Bearer {api_key}
```

### Post tweets and post tweet replies

Use write actions after the agent has the final approved copy, account context, and media requirements.

```bash
POST https://xquik.com/api/v1/x/tweets
Authorization: Bearer {api_key}
Content-Type: application/json

{ "account": "@example", "text": "Launch update copy" }
```

```bash
POST https://xquik.com/api/v1/x/tweets
Authorization: Bearer {api_key}
Content-Type: application/json

{ "account": "@example", "text": "Approved reply copy", "reply_to_tweet_id": "1234567890" }
```

### Export followers and look up users

Use user lookup, follower export, and verified follower export for audience research, influencer lists, community segmentation, and campaign targeting.

```bash
GET https://xquik.com/api/v1/x/users/{username}
Authorization: Bearer {api_key}
```

```bash
GET https://xquik.com/api/v1/x/users/{user_id}/followers
Authorization: Bearer {api_key}
```

### Monitor accounts and receive webhooks

Use monitors and webhooks when a marketing agent needs fresh tweets, replies, mentions, or campaign signals without polling manually.

```bash
POST https://xquik.com/api/v1/monitors
Authorization: Bearer {api_key}
Content-Type: application/json

{ "username": "example", "eventTypes": ["tweet.new", "tweet.reply"] }
```

### Run giveaway draws

Use giveaway draws when a campaign requires transparent selection from replies, likes, reposts, or follower criteria.

```bash
POST https://xquik.com/api/v1/draws
Authorization: Bearer {api_key}
Content-Type: application/json

{ "tweetUrl": "https://x.com/example/status/1234567890", "winnerCount": 1 }
```

## API Pattern

TweetClaw wraps Xquik REST endpoints for OpenClaw. Read operations return structured JSON for agent workflows. Write operations should use explicit approval, account selection, and clear final copy before sending.

## Key Data

- Tweet search results: tweet ID, text, author, timestamps, engagement metrics
- Reply search results: reply text, author, conversation context, timestamps
- User lookup: profile metadata, follower counts, verification signals
- Follower export: follower handles and profile fields for audience research
- Media workflows: media upload and download metadata
- Monitors and webhooks: fresh tweet, reply, mention, and account events

## Parameters

Common parameters depend on the endpoint:

- `q` - Search terms, operators, handles, hashtags, or URLs
- `tweet_id` - Tweet ID for replies, engagement, media, or draw workflows
- `username` - X/Twitter handle for user lookup
- `user_id` - X/Twitter user ID for follower export
- `account` - X/Twitter account handle or account ID for write actions
- `text` - Approved tweet or reply copy
- `media_ids` - Uploaded media IDs for posts with media
- `webhook_url` - Destination for monitor events

## When to Use

- Scrape tweets or search tweets for customer research and campaign planning
- Search tweet replies for objections, praise, support needs, or testimonials
- Post tweets or post tweet replies from an approved agent workflow
- Export followers for audience research and creator outreach
- Look up users before personalization or segmentation
- Upload or download media for social campaigns
- Monitor tweets, replies, mentions, and accounts with webhooks
- Run giveaway draws from X/Twitter engagement

## Rate Limits

Follow the limits shown by the Xquik API response headers and account plan. Handle HTTP 429 with backoff and avoid duplicate write retries without idempotency.

## Relevant Skills

- social-content
- launch-sequence
- customer-research
- community-marketing
- social-proof
