# TypeScript Sapphire Bot example

This is a basic setup of a Discord bot using the [sapphire framework][sapphire] written in TypeScript

## Getting Started

### Prerequisites

- Node.js (v18 or higher recommended)
- A Discord bot token (see [Creating a Discord Bot](#creating-a-discord-bot) below)

### Installation

1. Clone this repository
2. Install dependencies:

```sh
npm install
```

3. Generate Prisma client:

```sh
npx prisma generate
```

4. Set up the database (run migrations):

```sh
npx prisma migrate deploy
```

Or for development with a fresh database:

```sh
npx prisma migrate dev
```

### Creating a Discord Bot

Before you can run the bot, you need to create a Discord application and get a bot token:

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications)
2. Click **"New Application"** and give it a name
3. Navigate to the **"Bot"** section in the left sidebar
4. Click **"Add Bot"** (if you haven't already) and confirm
5. Under the **"Token"** section, click **"Reset Token"** or **"Copy"** to get your bot token
    - ⚠️ **Important**: Never share your bot token publicly! Treat it like a password.
6. Enable the following **Privileged Gateway Intents** (if needed for your bot):
    - **Message Content Intent** (required for message commands)
    - **Server Members Intent** (if you need member information)
    - **Presence Intent** (if you need presence information)

### Environment Setup

This project uses two separate `.env` files for different purposes:

#### 1. Root `.env` - Database Configuration

Copy the root example file:

**On Linux/macOS:**

```sh
cp .env.example .env
```

**On Windows (PowerShell):**

```powershell
Copy-Item .env.example .env
```

**On Windows (Command Prompt):**

```cmd
copy .env.example .env
```

Open the root `.env` file and configure your database connection:

```env
# Database Configuration
# For SQLite (default), use: file:./prisma/dev.db
# For PostgreSQL: postgresql://user:password@localhost:5432/database
# For MySQL: mysql://user:password@localhost:3306/database
# For Supabase: postgresql://user:password@db.xxxxx.supabase.co:5432/postgres
DATABASE_URL=file:./prisma/dev.db

# Node Environment
NODE_ENV=development
```

#### 2. `src/.env` - Discord Bot Token

Copy the example file in the `src` directory:

**On Linux/macOS:**

```sh
cp src/.env.example src/.env
```

**On Windows (PowerShell):**

```powershell
Copy-Item src\.env.example src\.env
```

**On Windows (Command Prompt):**

```cmd
copy src\.env.example src\.env
```

Open `src/.env` and add your Discord bot token:

```env
# Discord Bot Token
# Get your bot token from: https://discord.com/developers/applications
DISCORD_TOKEN=your_actual_bot_token_here

# Node Environment
NODE_ENV=development
```

**Example `src/.env` file:**

```env
DISCORD_TOKEN=YOUR_BOT_TOKEN_HERE
NODE_ENV=development
```

### Inviting Your Bot to a Server

1. In the Discord Developer Portal, go to the **"OAuth2"** → **"URL Generator"** section
2. Select the following scopes:
    - `bot`
    - `applications.commands` (for slash commands)
3. Select the bot permissions you need (e.g., "Send Messages", "Read Message History", etc.)
4. Copy the generated URL and open it in your browser
5. Select a server and authorize the bot

## How to use it?

### Development

This example can be run with `tsc-watch` to watch the files and automatically restart your bot.

```sh
npm run watch:start
```

### Production

You can also run the bot with `npm run dev`, this will first build your code and then run `node ./dist/index.js`. However, this is not the recommended way to run a bot in production.

For production, you should:

1. Build the project: `npm run build`
2. Run the compiled code: `npm run start`
3. Use a process manager like PM2 or systemd to keep the bot running

## License

Dedicated to the public domain via the [Unlicense], courtesy of the Sapphire Community and its contributors.

[sapphire]: https://github.com/sapphiredev/framework
[Unlicense]: https://github.com/sapphiredev/examples/blob/main/LICENSE.md
