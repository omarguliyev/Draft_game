# Anime Draft

Anime character auction game with two modes:

- **Friends Mode:** one device, 2–5 players, no backend required.
- **Online Room:** one host creates a six-character room code; each player joins with their own phone and receives a live bidding interface.

## GitHub Pages

Upload `index.html` to a GitHub repository and enable GitHub Pages. The friends mode works immediately.

## Online mode / Supabase

Online mode uses Supabase Realtime Broadcast. Supabase's Realtime service supports low-latency Broadcast and Presence for multiplayer applications. The browser uses the project's publishable/anon key; never put a Supabase secret/service-role key in this repository.

The game currently does **not** require a database table. Room state is held by the host and synchronized through Realtime Broadcast. This keeps setup simple for the first public version.

1. Create a Supabase project.
2. Enable/configure Realtime as needed for your project.
3. Copy the project URL and publishable key from the Supabase Connect settings.
4. Open Anime Draft → Online Room → Supabase settings and paste them.
5. Create a room and send the generated invite link.

The app stores these two client-side configuration values in localStorage. Only use a public/publishable/anon key in the browser.

## Important MVP limitation

The host is authoritative. If the host closes the page or loses connection, the room stops. A future production version should move authoritative game actions to a server/Edge Function and persist rooms in Postgres.

## Character images

Character images are fetched on demand from AniList's public GraphQL API and cached in the browser. If an image API is unavailable, the game still works and shows a placeholder.
