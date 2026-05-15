[![Buy Me A Coffee](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://buymeacoffee.com/hackatoa)

# matrix-cms-bot

A Matrix bot that lets you publish blog posts and upload mushroom photos to a static site by sending DMs — no web UI, no browser needed.

## Commands

| Command | Description |
|---|---|
| `!blog <title>` | Start a new blog post — bot prompts for the body |
| `!mushroom [title]` | Add a mushroom photo — bot prompts for the image |
| `!cancel` | Abort the current pending command |
| `!status` | Show bot status and config |
| `!help` | List all commands |

After `!blog <title>`, send the post body as a follow-up message. Markdown is supported.

After `!mushroom`, attach a jpg/png/gif/webp image. The bot downloads it from Matrix media, uploads to `public/assets/mycology/` in your GitHub repo, and updates `mushrooms-data.js`.

## Setup

### 1. Register a bot user

```bash
register_new_matrix_user -c homeserver.yaml -u cms --no-admin http://localhost:8008
```

### 2. Configure environment

Copy `.env.example` to `.env`:

```
MATRIX_HOMESERVER  — your Synapse URL
MATRIX_USER_ID     — @cms:yourdomain.com
MATRIX_TOKEN       — bot's access token
OWNER_USER_ID      — your Matrix ID (only this user can command the bot)
GITHUB_TOKEN       — personal access token with repo write scope
GITHUB_REPO        — owner/repo of your website repository
GITHUB_BRANCH      — branch to commit to (e.g. Main)
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

- `public/blog-data.js` — `window.BLOG_ENTRIES = [...]`
- `public/mushrooms-data.js` — `window.MUSHROOMS_DATA = [...]`
- `public/assets/mycology/` — mushroom image directory

---

[hackatoa.com](https://hackatoa.com) · [GitHub](https://github.com/Hackatoan) · [Buy Me A Coffee](https://buymeacoffee.com/hackatoa)
