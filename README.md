# Stellar Party

A colorful multiplayer web game you can play with friends in the browser.

Collect glowing stars in a neon arena, chat, make rooms, send friend requests, and invite friends to your match. After every game a leaderboard shows who shone brightest. Your username is remembered in the browser.

Built for GitHub + [Render](https://render.com) — one Node.js web service, no extra database required.

## Features

- **Login and create account** (username + password, saved in this browser)
- **Taken usernames refresh from the server** — the login screen lists every name already used
- Private rooms with a shareable code
- **Friend search, requests, accept/decline**
- **Invite online friends** into your room
- **Lobby chat + room chat**
- **60-second star-collecting matches**
- **Live scores and post-match leaderboard**
- **Touch controls** on phones
- Kid-friendly: collect stars, no combat

## How to play

1. Create an account or log in (password is at least 4 characters)
2. Create a room or join with a code
3. Add friends and invite them
4. Host presses **Start Match**
5. Move with **WASD** or arrow keys
6. Grab white/blue stars (10 pts) and gold stars (30 pts)
7. Highest score after 60 seconds wins

## Run locally

Needs Node.js 18+.

```bash
git clone https://github.com/YOUR_USERNAME/stellar-party.git
cd stellar-party
npm install
npm start
```

Open [http://localhost:3000](http://localhost:3000).

Open two browser windows (or a normal window and a private window) to test multiplayer on one computer.

## Deploy on Railway

The line `npm warn config production Use --omit=dev instead` is only a warning. It is not an error. Railway prints it, then installs packages. That install can sit quietly for a few minutes.

If it stays on that line for more than 10 minutes:

1. Do not upload `node_modules`. Delete that folder before you deploy.
2. In the Railway service settings set:
   - **Build command:** `npm install --omit=dev --no-audit --no-fund`
   - **Start command:** `npm start`
3. Redeploy. A good log looks like install finishing, then `Stellar Party running on port ...`.
4. Open the Railway URL. `/health` should say `{"ok":true}`.

## Deploy on Render

1. Push this folder to a GitHub repository.
2. Go to [Render Dashboard](https://dashboard.render.com) → **New** → **Web Service**.
3. Connect the GitHub repo.
4. Settings:
   - **Runtime:** Node
   - **Build command:** `npm install`
   - **Start command:** `npm start`
   - **Instance:** Free is fine for testing
5. Deploy. Render sets `PORT` for you — the server already reads it.

The first time this version starts, it refreshes the taken-username list and clears old name-only accounts so everyone can create a real login. After that, names stay taken until you delete `data/users.json` and `data/meta.json` and restart.

## Project layout

```
stellar-party/
├── server.js          # Express + Socket.io (rooms, friends, game loop)
├── package.json
├── public/
│   ├── index.html
│   ├── css/style.css
│   └── js/
│       ├── app.js     # UI, chat, friends, rooms
│       └── game.js    # Canvas renderer + particles
└── data/              # created at runtime
```

## Notes

- One username can only be signed in on one tab at a time.
- Rooms hold up to 8 players.
- The host can start a match even with one player (good for testing).

MIT license — remix it, skin it, add new maps.
