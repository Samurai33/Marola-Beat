<div align="center">

<img src="marolabeat_logo.png" alt="Marola Beat" width="200">

# Marola Beat

### Self-hosted Discord music bot for the Marola RP community

Slash commands, a shared queue and YouTube + SoundCloud playback, in a small TypeScript codebase
that is easy to read and extend.

[![Website](https://img.shields.io/badge/n3xus.dev-0B1220?style=for-the-badge&logo=googlechrome&logoColor=14B8A6)](https://n3xus.dev)
[![Community](https://img.shields.io/badge/Marola%20RP-marolaroleplay.com.br-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://marolaroleplay.com.br)
[![License](https://img.shields.io/badge/License-MIT-F59E0B?style=for-the-badge)](LICENSE)

[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=flat-square&logo=typescript&logoColor=white)](tsconfig.json)
[![discord.js](https://img.shields.io/badge/discord.js-14-5865F2?style=flat-square&logo=discord&logoColor=white)](package.json)
[![discord-player](https://img.shields.io/badge/discord--player-7-111827?style=flat-square)](package.json)
[![Sources](https://img.shields.io/badge/sources-YouTube%20%C2%B7%20SoundCloud-FF0000?style=flat-square&logo=youtube&logoColor=white)](src/player.ts)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat-square&logo=nodedotjs&logoColor=white)](package.json)

</div>

---

## Table of Contents

- [Overview](#overview)
- [Commands](#commands)
- [Architecture](#architecture)
- [Quickstart](#quickstart)
- [Repository structure](#repository-structure)
- [Current status](#current-status)

---

## Overview

**Marola Beat** plays music in the voice channels of the Marola RP Discord. It was written to be boring in the
good way: one process, slash commands only, nothing stored, and it leaves the channel when nobody is listening.

It is built for:

- community servers that want their own music bot instead of a shared public one;
- developers learning `discord.js` + `discord-player` from a small, typed example;
- self-hosting on a VPS or in a container next to other community services.

---

## Commands

| Command | What it does |
|---|---|
| `/play <query>` | Search or paste a URL; adds the track or playlist to the queue |
| `/skip` · `/stop` | Skip the current track · stop and clear the queue |
| `/pause` · `/resume` | Pause or resume playback |
| `/queue` · `/nowplaying` | Show the queue · show the current track |
| `/shuffle` | Shuffle the remaining tracks |
| `/loop <off\|track\|queue>` | Set the repeat mode |

---

## Architecture

```mermaid
flowchart LR
  U["Discord user<br/>slash command"] --> GW["discord.js client"]
  GW --> CMD["src/commands/*"]
  CMD --> PL["discord-player<br/>queue per guild"]
  PL --> EX["Extractors<br/>YouTube · SoundCloud"]
  PL --> VC["Voice channel"]
  PL -. "empty channel / queue" .-> LEAVE["auto-leave"]
```

---

## Quickstart

Requires Node.js 18+ and a Discord application with a bot user.

```bash
git clone https://github.com/Samurai33/Marola-Beat.git
cd Marola-Beat
cp .env.example .env        # DISCORD_TOKEN, DISCORD_APP_ID, GUILD_ID
npm install
npm run register            # registers the slash commands in your guild
npm run dev
```

Production:

```bash
npm run build
npm start
```

---

## Repository structure

| Path | What it is |
|---|---|
| `src/index.ts` | Bot entry point and command routing |
| `src/player.ts` | discord-player setup, extractors and auto-leave events |
| `src/commands/` | One file per slash command |
| `src/register-commands.ts` | Registers the commands for `GUILD_ID` |
| `.env.example` | Required environment variables |

---

## Current status

| | |
|---|---|
| **Stage** | Working v1, open source |
| **Successor** | A private v2 runs in production for Marola RP (Docker image + Coolify) |
| **Not included** | Persistence, web dashboard, tests |

---

<div align="center">

**Need something built, secured or kept online?** → [contato@n3xus.dev](mailto:contato@n3xus.dev) · [n3xus.dev](https://n3xus.dev)

MIT © Thiago "Samurai" Rangel · [N3XUS](https://n3xus.dev)

</div>
