# matrix-cms-bot

A Matrix bot that lets you publish blog posts and upload mushroom photos to a static GitHub Pages / Firebase site by sending DMs.

## Commands

| Command | Description |
|---|---|
| `!blog <title>` | Start a new blog post — bot will prompt for the body |
| `!mushroom [title]` | Add a mushroom photo — bot will prompt for the image |
| `!cancel` | Abort the current pending command |
| `!status` | Show bot status and config |
| `!help` | List all commands |

After `!blog <title>`, send the post body as a single follow-up message. Markdown is supported.

After `!mushroom`, attach an image (jpg/png/gif/webp) as your next message. The bot downloads it from Matrix media, uploads it to `public/assets/mycology/` in the GitHub repo, and updates `mushrooms-data.js`.

## Setup

### 1. Register a bot user on your Synapse homeserver

```bash
register_new_matrix_user -c homeserver.yaml -u cms --no-admin http://localhost:8008
```

Or use the shared-secret registration endpoint.

### 2. Configure environment

Copy `.env.example` to `.env` and fill in values:

```
MATRIX_HOMESERVER  — your Synapse URL
MATRIX_USER_ID     — @cms:yourdomain.com
MATRIX_TOKEN       — bot's access token
OWNER_USER_ID      — your personal Matrix ID (only this user can command the bot)
GITHUB_TOKEN       — personal access token with repo write scope
GITHUB_REPO        — owner/repo of your website repository
GITHUB_BRANCH      — branch to commit to (e.g. Main or main)
```

### 3. Run

```bash
docker compose -f docker-compose.example.yml up -d
```

Or locally:

```bash
pip install -r requirements.txt
source .env
python bot.py
```

### 4. Invite the bot

DM `@cms:yourdomain.com` in Element. The bot auto-accepts invites from `OWNER_USER_ID`.

## Expected repo structure

The bot expects your website repo to have:

- `public/blog-data.js` — `window.BLOG_ENTRIES = [...]`
- `public/mushrooms-data.js` — `window.MUSHROOMS_DATA = [...]`
- `public/assets/mycology/` — directory where mushroom images are stored
