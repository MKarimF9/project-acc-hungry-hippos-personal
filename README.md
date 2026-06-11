[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=19552926)
<div align="center">

# The Hungry Hippos Project
[![Report Issue on Jira](https://img.shields.io/badge/Report%20Issues-Jira-0052CC?style=flat&logo=jira-software)](https://temple-cis-projects-in-cs.atlassian.net/jira/software/c/projects/DT/issues)
[![Deploy Docs](https://github.com/ApplebaumIan/tu-cis-4398-docs-template/actions/workflows/deploy.yml/badge.svg)](https://github.com/ApplebaumIan/tu-cis-4398-docs-template/actions/workflows/deploy.yml)
[![Documentation Website](https://img.shields.io/badge/-Documentation%20Website-brightgreen)](https://capstone-projects-2025-spring.github.io/project-acc-hungry-hippos/docs/intro )


![Gameplay Demo](https://github.com/MKarimF9/project-acc-hungry-hippos-personal/blob/066bfebda6f3b817244804a9ba51103068510822/Demo.gif)

</div>

A web-based multiplayer game inspired by *Hungry Hungry Hippos*, built with accessibility at its core. The game integrates an **AAC (Augmentative and Alternative Communication)** interface so individuals with speech or motor impairments can fully participate as the game conductor alongside up to four hippo players.

---

## Table of Contents

1. [Keywords](#keywords)
2. [About the Project](#about-the-project)
3. [How to Play](#how-to-play)
4. [High Level Requirements](#high-level-requirements)
5. [Tech Stack](#tech-stack)
6. [Architecture](#architecture)
7. [Getting Started](#getting-started)
8. [Project Structure](#project-structure)
9. [Running Tests](#running-tests)
10. [Required Resources](#required-resources)
11. [Documentation](#documentation)
12. [Collaborators](#collaborators)
13. [License](#license)


---

## Keywords

Section #701 — JavaScript · TypeScript · React · Phaser · Web Game · Accessibility · AAC · Multiplayer · Physics-based · Educational Technology

---


## About the Project

Many existing web games are designed primarily for able-bodied users, leaving out players who rely on AAC devices. This project was inspired by the desire to **merge play, inclusivity, and technology**, ensuring children and individuals with communication challenges can participate in social, fast-paced gameplay.

The original *Hungry Hungry Hippos* was a tactile, turn-based game. Modernizing it with bouncing physics, interactive traps, and digital control unlocks a new level of engagement. Integrating accessible design principles and playful interaction fosters **joyful shared experiences**, especially in educational or therapeutic settings.

Players are divided into two roles:

- **AAC Game Conductor** — selects fruits, launches traps, and directs the flow of the game using an AAC-compatible interface.
- **Hippo Players** — up to four players control cartoon hippos stationed at screen edges, sliding along their borders to catch fruits using movement keys or touch input.

Fruits and traps bounce around the arena with physics-based behavior, creating a dynamic and exciting environment. The goal is to collect as many correct fruits as possible while avoiding traps. This game emphasizes **inclusivity, real-time decision-making**, and **competitive play** in a fun, accessible format.

> **What is AAC?** Augmentative and Alternative Communication refers to tools and strategies that support communication for people who cannot rely on speech alone — including symbol boards, speech-generating devices, and eye-gaze technology. This game is designed so that an AAC user can be a full, active participant, not a spectator.

---
## How to Play

The game supports **5 simultaneous players** across separate devices or browser tabs.

### Role 1 — AAC Game Conductor (1 player)
- Uses the AAC interface to select which fruits appear on the board
- Launches traps to challenge hippo players
- Controls the pace and flow of the round
- Can be played via touch, AAC device, or keyboard

### Role 2 — Hippo Players (up to 4 players)
- Each player controls a cartoon hippo at one edge of the arena (top, bottom, left, right)
- Slide your hippo to catch falling fruits and avoid traps
- Catch fruits with default open mouths; close your mouth to deflect incorrect fruits or traps
- Deflected fruits and traps bounce away with physics
- Controlled via keyboard arrows or touch swipe
- Scores update in real time

The game ends after a time or round limit. The hippo player with the most correct fruits wins.

---


## High Level Requirements

### AAC Game Conductor
- Select target fruits (e.g., "Apples only")
- Launch fruits and traps from the screen center
- Assign initial launch direction for traps
- Reset and start new rounds
- View real-time score updates
- Receive visual and auditory feedback on all actions

### Hippo Players
- Each hippo is assigned to a unique screen edge
- Slide left/right or up/down along their edge
- Catch fruits with default open mouths
- Close mouths to avoid incorrect fruits or traps
- Deflect fruits and traps with physics when not eaten
- Game ends after time or round limit

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend Framework | React 19 + TypeScript |
| Styling | Tailwind CSS |
| Game Engine | Phaser 3 |
| Bundler | Vite |
| Backend | Express 5 + Node.js |
| Database | PostgreSQL |
| Routing | React Router DOM 7 |
| Testing | Vitest + React Testing Library |
| Linting | ESLint |
| Deployment | Vercel |

---

## Architecture

The app runs as two processes simultaneously:

```
Browser Clients (up to 5)
        |
        | HTTP / WebSocket
        v
  Express API Server          <-- npm run api
  (session management,
   game state, player sync)
        |
        v
   PostgreSQL Database

  React + Phaser Frontend     <-- npm run dev
  (renders game, handles
   AAC input, player input)
```

- The **API server** manages game sessions, synchronizes player state across devices, and persists scores.
- The **frontend** runs Phaser 3 for physics and rendering inside a React app, with React handling menus, the AAC board, and all UI outside the game canvas.
- Players join a shared session via QR code or URL — no accounts needed.

---

## Getting Started

### Prerequisites

- Node.js v18 or higher
- npm v9 or higher
- PostgreSQL (for session persistence)

### Installation

```bash
git clone https://github.com/MKarimF9/project-acc-hungry-hippos-personal.git
cd project-acc-hungry-hippos-personal/Hungry-Hippo-Game
npm install
```

### Running the App

Open **two terminal windows**:

**Terminal 1 — API server:**
```bash
npm run api
```

**Terminal 2 — Frontend:**
```bash
npm run dev
```

Open `http://localhost:5173` in your browser. For a full 5-player game, open the app on 5 separate devices or browser tabs and assign one as the conductor.

### Production Build

```bash
npm run build
```

Output goes to `dist/`. The project is configured for Vercel deployment via `vercel.json`.

---

## Project Structure

```
project-acc-hungry-hippos-personal/
├── Hungry-Hippo-Game/          # Main application
│   ├── src/                    # React + Phaser source code
│   ├── public/                 # Static assets (images, sounds)
│   ├── server-backend/         # Express API server
│   ├── index.html
│   ├── package.json
│   ├── tsconfig.json
│   ├── vitest.config.ts
│   └── vercel.json
├── documentation/              # Docusaurus docs site
├── Instructions.md             # Original project brief
└── README.md
```

---

## Running Tests

```bash
npm run test
```

With coverage:

```bash
npm run coverage
```

Tests use Vitest and React Testing Library. Test files live alongside source files in `src/`.

---

## Required Resources

### Software

| Resource | Purpose | Required? |
|---|---|---|
| Node.js | Runtime environment | Yes |
| npm | Package manager | Yes |
| React | UI library | Yes |
| Phaser 3 | 2D game engine | Yes |
| TypeScript | Static typing | Yes |
| Tailwind CSS | Styling and layout | Yes |
| Vite | Dev server and bundler | Yes |
| Git / GitHub | Version control | Yes |
| PostgreSQL | Session persistence | Yes |
| Visual Studio Code | Recommended editor | No |

### Hardware

| Device | Use | Required? |
|---|---|---|
| Desktop or Laptop | Development and playtesting | Yes |
| Tablet or Touchscreen | AAC interface simulation | Yes |
| Multiple Devices (2–5) | Simultaneous testing (1 conductor + 4 players) | Yes |

---

## Documentation

Full technical documentation — including API specs, component diagrams, and AAC design decisions — is maintained as a Docusaurus site in the `/documentation` folder.

To run the docs site locally:

```bash
cd documentation
yarn install
yarn start
```

---

## Collaborators

<table>
<tr>
    <td align="center">
        <a href="https://github.com/tun67213">
            <img src="https://www.gravatar.com/avatar/?d=mp&s=200" width="100;" alt="ArvindhVelrajan"/>
            <br />
            <sub><b>Arvindh Velrajan</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/MKarimF9">
            <img src="https://www.gravatar.com/avatar/?d=mp&s=200" width="100" alt="Mohammed Karim"/>
            <br />
            <sub><b>Mohammed Karim</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/tug74295">
            <img src="https://www.gravatar.com/avatar/?d=mp&s=200" width="100" alt="Kostandin Jorgji"/>
            <br />
            <sub><b>Kostandin Jorgji</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/jdoooodler">
            <img src="https://www.gravatar.com/avatar/?d=mp&s=200" width="100" alt="Jasmine Liu"/>
            <br />
            <sub><b>Jasmine Liu</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/tun70323">
            <img src="https://www.gravatar.com/avatar/?d=mp&s=200" width="100" alt="Omais Khan"/>
            <br />
            <sub><b>Omais Khan</b></sub>
        </a>
    </td>
</tr>
</table>

---

## License

MIT — see [LICENSE](Hungry-Hippo-Game/LICENSE) for details.


[//]: # ( readme: collaborators -end )
