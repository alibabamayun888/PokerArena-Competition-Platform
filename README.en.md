# PokerArena | Texas Hold'em SNG, MTT and Tournament Platform

[简体中文](README.md) | [繁體中文](README.zh-TW.md) | [English](README.en.md) | [Project Website](https://alibabamayun888.github.io/PokerArena-Competition-Platform/en/)

<p align="center">
  <img src="https://img.shields.io/badge/Client-Unity3D-000000?logo=unity&logoColor=white" alt="Unity3D Texas Hold'em client">
  <img src="https://img.shields.io/badge/Game_Server-C%2B%2B17-00599C?logo=c%2B%2B&logoColor=white" alt="C++17 game server">
  <img src="https://img.shields.io/badge/Admin-Java%2017-ED8B00?logo=openjdk&logoColor=white" alt="Java 17 admin backend">
  <img src="https://img.shields.io/badge/Tournament-SNG%20%7C%20MTT-C62828" alt="SNG and MTT poker tournaments">
</p>

**PokerArena Competition Platform** is a Texas Hold'em tournament system for Sit & Go (SNG), Multi-Table Tournament (MTT), competitive rankings, and online-to-live event qualification. Its architecture combines a **cross-platform Unity3D client, a real-time C++ game server, and a Java operations backend** for registration, identity verification, table play, blind levels, elimination, ranking, settlement, and live-event ticket redemption.

The project is relevant to poker tournament platform development, real-time multiplayer game research, online qualifiers, live-event registration, and tournament operations. The repository presents the product and technical design; verify available modules, dependencies, and compliance requirements against the current source revision before deployment.

## Contents

- [Overview](#overview)
- [Tournament Formats](#tournament-formats)
- [Architecture](#architecture)
- [Core Features](#core-features)
- [Unity Client](#unity-client)
- [C++ Game Server](#c-game-server)
- [Java Admin Backend](#java-admin-backend)
- [Identity and Security](#identity-and-security)
- [Online and Live-Event Tickets](#online-and-live-event-tickets)
- [Screenshots](#screenshots)
- [Repository Structure](#repository-structure)
- [Build and Deployment](#build-and-deployment)
- [FAQ](#faq)
- [Compliance](#compliance)
- [Contact](#contact)

## Overview

PokerArena connects online Texas Hold'em tournaments, tournament scheduling, player eligibility, identity and face verification, rankings, and live-event ticket management in one workflow.

```text
Publish → Register → Verify identity and eligibility → Seat players
        → Increase blinds → Eliminate and balance tables → Final table
        → Settle rankings, points, or tickets → Redeem at live event
```

| Layer | Technology | Responsibility |
| --- | --- | --- |
| Client | Unity3D 2021.3 LTS | iOS / Android UI, lobby, registration, table, and results |
| Client networking | WebSocket | Real-time messaging, heartbeat, reconnection, and recovery |
| Game server | C++17 / Boost.Asio | Game state, player actions, tournament scheduling, and synchronization |
| Admin backend | Java 17 / Spring Boot 3.x | Tournament settings, user review, tickets, operations, and risk controls |
| Data services | MySQL 8.0 / Redis 7.x | Persistence, caching, online state, and rankings |
| Identity | Third-party identity and face-verification service | Liveness, identity checks, and player eligibility |

## Tournament Formats

### Multi-Table Tournaments (MTT)

- Run multiple tables and dynamically break or balance tables as the field changes.
- Configure blind levels, antes, late registration, rebuys, and add-ons.
- Track eliminations, live standings, payout positions, and final-table results.

### Sit & Go (SNG)

- Start automatically when the configured number of players has registered.
- Suitable for fast single-table competition and fixed-field qualifiers.
- Configure eligibility, starting chips, blind speed, and winning positions.

### Competitive Rankings

- Support tournament points, seasonal leaderboards, and qualification rules.
- Connect online results with eligibility for live poker events.
- Suitable for tournament series, qualifiers, and branded competitions.

## Architecture

```text
┌───────────────────────────────────────────┐
│               Unity3D Client              │
│ Lobby · Registration · Table · Tickets    │
└───────────────────┬───────────────────────┘
                    │ WebSocket / API
┌───────────────────▼───────────────────────┐
│               C++ Game Server             │
│ State · Dealing · Validation · Scheduling │
└───────────────────┬───────────────────────┘
                    │ Internal APIs / Events
┌───────────────────▼───────────────────────┐
│             Java Admin Backend            │
│ Events · Users · Rankings · Tickets · Risk│
└───────────────────┬───────────────────────┘
                    │
┌───────────────────▼───────────────────────┐
│ MySQL · Redis · Messaging · Identity      │
└───────────────────────────────────────────┘
```

The client handles presentation and interaction. Critical game state, randomness, action validation, and tournament results must remain server-authoritative. The admin backend manages tournaments and operations through controlled interfaces and does not participate directly in card dealing.

## Core Features

| Feature | Description |
| --- | --- |
| Tournament lobby | Lists registering, running, and completed SNG, MTT, and ranked events |
| Registration | Manages schedules, capacity, eligibility, waiting lists, and cancellation |
| Blind engine | Configures blind levels, intervals, antes, and breaks |
| Tournament scheduling | Opens, breaks, balances, and merges tables and manages eliminations |
| Real-time tables | Synchronizes actions, pots, side pots, all-ins, and game state |
| Rankings and points | Updates finishing positions, seasonal points, and qualification |
| Settlement | Produces rewards, points, or eligibility according to event rules |
| Ticket center | Handles point exchange, ticket claims, status, and live redemption |
| Identity verification | Integrates identity review, liveness, and face matching |

## Unity Client

The Unity3D client targets iOS and Android and includes the tournament lobby, event details, registration, waiting, real-time tables, standings, results, player profile, qualification cards, tickets, reconnection, and localization support.

## C++ Game Server

The C++ game server owns the Texas Hold'em state machine, action validation, server-side dealing, pot and side-pot calculation, connections, SNG/MTT lifecycle, blind progression, table balancing, elimination, advancement, and settlement events.

Concurrency and latency depend on the exact source revision, hardware, compiler settings, and benchmark method. This README does not make fixed performance claims without a published reproducible benchmark.

## Java Admin Backend

| Module | Purpose |
| --- | --- |
| Tournament management | Templates, schedules, blinds, field size, and reward rules |
| User management | Profiles, identity review, restrictions, and participation records |
| Ticket management | Qualification cards, inventory, issue, claim, and redemption records |
| Content management | Announcements, banners, activities, and client configuration |
| Reporting | Participation, retention, registration, and completion statistics |
| Risk and audit | Events, device/account relationships, logs, and manual review |
| Access control | Roles, least privilege, and approval for sensitive operations |

## Identity and Security

The platform can integrate identity and face verification for account checks, important event registration, ticket claims, and on-site redemption.

- Explain the purpose and obtain separate consent before collection.
- Protect face images and biometric templates as sensitive personal data.
- Give the C++ server only the minimum eligibility status; do not store raw face images there.
- Define retention, withdrawal, deletion, and manual-review processes.
- Authenticate, rate-limit, and audit admin, verification, registration, and reward APIs.
- Use TLS and never commit production keys or credentials to a public repository.

## Online and Live-Event Tickets

1. A player enters an online SNG, MTT, or points competition.
2. The event awards a qualification card or live-event ticket under published rules.
3. The player views and claims the qualification in the client.
4. The backend verifies identity and eligibility.
5. The organizer redeems a secure credential or QR code on site.
6. The result is recorded for audit and support.

## Screenshots

### Live Event Lobby

![PokerArena live Texas Hold'em event lobby](docs/Assets/Screenshots/dating.jpg)

### Tournament Registration

![PokerArena poker tournament registration list](docs/Assets/Screenshots/baoming.jpg)

### Competition Table

![PokerArena Texas Hold'em competition table](docs/Assets/Screenshots/bisai.jpg)

### Qualification Card Exchange

![PokerArena points exchange for live-event qualification](docs/Assets/Screenshots/duihuanka.jpg)

## Repository Structure

```text
PokerArena-Competition-Platform/
├── Clinet/
├── Doc/
├── Unity-iPhone Tests/
├── UnityFramework/
├── docs/
│   ├── index.html
│   ├── en/index.html
│   ├── zh-TW/index.html
│   └── Assets/Screenshots/
├── README.md
├── README.zh-TW.md
└── README.en.md
```

> `Clinet/` is the directory name currently visible in the online repository. Rename it to `Client/` only in a separate, tested change that also updates Unity references.

## Build and Deployment

The repository root does not currently expose complete C++ server, Java backend, and database deployment entry points, so this README does not invent commands. When those modules are published, add verified Unity build instructions, C++ deployment, Java deployment, protocol compatibility, benchmark methodology, and a secret-free `.env.example`.

## FAQ

### Which tournament formats does PokerArena support?

The platform is designed for SNG, MTT, ranked competition, online qualifiers, and live-event ticket integration.

### What technologies are used?

The client uses Unity3D, the real-time game server uses C++, and the tournament operations backend uses Java and Spring Boot.

### Does it support iOS and Android?

The online project describes iOS and Android targets. Confirm supported builds and minimum OS versions against the current Unity project and build tests.

### Is face verification mandatory?

Not necessarily. Use it only when event rules and applicable law justify it, with clear notice, consent, data minimization, and deletion controls.

### Is it ready for commercial operation?

Commercial readiness depends on code completeness, licensing, third-party SDK rights, security testing, and local law. Complete code review, load testing, privacy assessment, and legal review before launch.

## Compliance

This project is intended for software development, tournament management, and technical research. Operators must comply with applicable laws concerning online games, competitions, age restrictions, consumer protection, biometrics, and data protection.

Do not use it for unauthorized gambling operations, identity misuse, privacy violations, match manipulation, or other illegal activity. See [PRIVACY.md](PRIVACY.md), [SECURITY.md](SECURITY.md), and [RESPONSIBLE-USE.md](RESPONSIBLE-USE.md).

## License

The current repository root does not show a standard `LICENSE` file. This README therefore makes no MIT or other licensing claim. The copyright owner should add the chosen license before distribution; until then, copyright remains reserved by default.

## Contact

| Channel | Address |
| --- | --- |
| Email | <ttpoker40@gmail.com> |
| Telegram | [@alibabama401](https://t.me/alibabama401) |
| Issues | [PokerArena GitHub Issues](https://github.com/alibabamayun888/PokerArena-Competition-Platform/issues) |
