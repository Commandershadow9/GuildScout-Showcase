<p align="center">
  <img src="https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/Version-0.9.0-blue?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/License-Private-red?style=for-the-badge" alt="License">
</p>

<h1 align="center">GuildScout</h1>
<h3 align="center">Discord Guild Management Bot with Full-Featured Web Dashboard</h3>

<p align="center">
  <em>A production-ready Discord bot that ranks users based on activity, manages guild operations, and provides a modern real-time web dashboard for raid planning, member management, and analytics.</em>
</p>

---

## Screenshots

### Dashboard Overview
> Personalized dashboard with active raids, top rankings, quick actions, and live data updates via WebSocket.

![Dashboard](screenshots/dashboard.png)

### Raid Management
> Full raid planning system with category filters, role-based signups (Tank/Healer/DPS), live countdown timers, and progress tracking.

![Raids](screenshots/raids.png)

### Guild Management
> Complete ingame guild system with member tracking, rank hierarchy, Discord role sync, and officer tools (kick, ban, DM, notes).

![Guild Management](screenshots/guild-management.png)

### Guild Dashboard
> Per-guild dashboard with interactive stats, rank distribution chart, real-time activity feed, and quick action grid.

![Guild Dashboard](screenshots/guild-dashboard.png)

---

## Tech Stack

<table>
<tr>
<td align="center" width="150">
<strong>Backend</strong><br>
<img src="https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white" alt="Go"><br>
<img src="https://img.shields.io/badge/Fiber-333?style=flat" alt="Fiber"><br>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white" alt="PostgreSQL"><br>
<img src="https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white" alt="Redis">
</td>
<td align="center" width="150">
<strong>Frontend</strong><br>
<img src="https://img.shields.io/badge/React_19-61DAFB?style=flat&logo=react&logoColor=black" alt="React"><br>
<img src="https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white" alt="TypeScript"><br>
<img src="https://img.shields.io/badge/Tailwind-06B6D4?style=flat&logo=tailwindcss&logoColor=white" alt="Tailwind"><br>
<img src="https://img.shields.io/badge/Vite-646CFF?style=flat&logo=vite&logoColor=white" alt="Vite">
</td>
<td align="center" width="150">
<strong>Bot</strong><br>
<img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white" alt="Python"><br>
<img src="https://img.shields.io/badge/discord.py-5865F2?style=flat&logo=discord&logoColor=white" alt="discord.py"><br>
<img src="https://img.shields.io/badge/asyncpg-333?style=flat" alt="asyncpg">
</td>
<td align="center" width="150">
<strong>Infrastructure</strong><br>
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white" alt="Docker"><br>
<img src="https://img.shields.io/badge/Traefik-24A1C1?style=flat&logo=traefikproxy&logoColor=white" alt="Traefik"><br>
<img src="https://img.shields.io/badge/systemd-333?style=flat" alt="systemd">
</td>
</tr>
</table>

---

## Architecture

```
                    ┌──────────────────┐
                    │   React Dashboard │
                    │   (TypeScript)    │
                    └────────┬─────────┘
                             │ REST + WebSocket
                    ┌────────▼─────────┐
                    │     Go API       │
                    │    (Fiber)       │
                    └───┬────────┬─────┘
                        │        │
            ┌───────────▼──┐  ┌──▼───────────┐
            │  PostgreSQL  │  │    Redis      │
            │   (Data)     │  │  (Pub/Sub)    │
            └───────────▲──┘  └──▲───────────┘
                        │        │
                    ┌───┴────────┴─────┐
                    │   Discord Bot    │
                    │    (Python)      │
                    └──────────────────┘
```

**Key architectural decisions:**
- **Bidirectional sync** between Discord Bot and Web Dashboard via Redis Pub/Sub
- **Real-time updates** through WebSocket (no polling)
- **PostgreSQL** as single source of truth for all data
- **Bot runs on host** (systemd) while API runs in Docker (Traefik reverse proxy)

---

## Features

### Core
- **Activity-based ranking** with configurable weights (messages, voice, membership duration)
- **Real-time scoring** with percentile comparisons and visual rank cards
- **Multi-guild support** with Discord OAuth authentication
- **Internationalization** (DE/EN) for both dashboard and bot

### Raid System
- **Full lifecycle management**: Create, edit, lock, close, cancel raids
- **Template system**: Reusable raid configurations with role limits
- **Category & Mode system**: PvE, PvP, Guild Wars with different group sizes
- **Role-based signups**: Tank/Healer/DPS with auto-promote from bench
- **Weapon/Build system**: Per-signup weapon selection, displayed in Discord embeds
- **Guild War results**: Win/loss/draw tracking with MVP selection and rank points
- **iCal export**: Add raids to personal calendars
- **Push notifications**: Web Push + Discord DM with user preferences

### Guild Management
- **Ingame guild system**: Full CRUD for guilds, ranks, and members
- **Rank hierarchy**: Priority-based with Discord role auto-mapping
- **Member detail**: Event timeline, officer notes, Discord actions (kick/ban/DM/nickname)
- **Dashboard per guild**: Statistics, rank distribution, activity feed

### Permission System
- **5-tier hierarchy**: Owner > User Overrides > Discord Role Map > Legacy Roles > Member Roles
- **Per-user overrides**: Grant/deny individual permissions
- **Discord integration**: Automatic role sync on login and role changes

### Analytics
- **Activity charts**: Daily/hourly message and voice activity
- **Period filtering**: 30 days, 90 days, all-time
- **MVP leaderboard**: Top performers across guild wars
- **CSV export**: Full ranking data export

---

## Project Stats

| Metric | Value |
|--------|-------|
| **Total codebase** | ~40,000+ lines |
| **Go API** | ~8,000 lines |
| **React Dashboard** | ~20,000 lines |
| **Python Bot** | ~12,000 lines |
| **Database migrations** | 28 |
| **API endpoints** | 60+ |
| **Dashboard pages** | 15+ |
| **i18n namespaces** | 12 (DE + EN) |

---

## Status

This project is actively used in production on a Discord gaming community. The source code is in a **private repository**.

---

<p align="center">
  <em>Built by <a href="https://github.com/Commandershadow9">Commandershadow9</a></em>
</p>
