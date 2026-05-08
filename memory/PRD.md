# BLAZEBOT — PRD

## Original problem statement
Convert a static cyberpunk AI character creator HTML prototype ("BLAZEBOT") into a fully functional personal-use app. Direct client-side API calls using user's keys for: DeepSeek R1 (chat), Fal.ai Z-Image Turbo (image gen), ElevenLabs (voice). Vanilla JS single-file architecture preserved by user request.

## Architecture
- Monolithic `/app/frontend/public/index.html` (vanilla HTML + Tailwind CDN + vanilla JS)
- No backend used. State in `localStorage` + JS memory
- Frontend served via CRA dev server (`yarn start`) → public/index.html as static template
- IMPORTANT: Frontend dev server caches public/index.html template at startup. After significant edits to public/index.html, restart frontend (`sudo supervisorctl restart frontend`) to surface changes.

## What's implemented
- DeepSeek R1 chat (1-on-1 + group)
- Fal.ai Z-Image Turbo generation (square_hd & portrait_16_9)
- ElevenLabs TTS playback
- Green Flame Skull theme + circuit backgrounds
- 3-step Character Creator (Identity / Image / Voice)
- Bot.ME persona management
- Group chat (Collective) with up to 5 bots + persona avatar selector
- 1-on-1 solo chat
- API key configuration UI

## Recently added (Feb 2026)
- **Two-image system**: full character image as solo-chat background; small circular avatar shown next to every bot bubble in both 1-on-1 and group chat
- **Avatar field in Character Creator (Step 2)**: upload face image OR "Use Generated Image" to derive avatar from full image
- **Per-bubble actions**: every bot message in solo + group chat has a speaker button (TTS for that exact text) and image-gen button (generates an in-context image using the bot's style + recent chat as prompt)
- **Custom group chat background**: Collective setup now has a "Group Chat Background" prompt + GENERATE BACKGROUND button. Image is used as the chat background (instead of auto-using a bot's image)
- **Full Character Creator form persistence**: name, gender, intro, visual prompt, style, ratio, voice prompt all save/restore across step navigation (back/forward) and tab switches; cleared only after `createCharacter()` finalizes

## Known / pending
- ElevenLabs voice "generation" uses TTS with a base voice + the description as text. True Voice Design API not implemented yet (user accepted simplified TTS approach for now)

## Roadmap (P1)
- Optional: implement true ElevenLabs Voice Design (`/v1/text-to-voice/create`) for custom voices from description
- Optional: per-character chat history persistence across sessions
- Optional: image-gen aspect ratio toggle inside chat bubble
