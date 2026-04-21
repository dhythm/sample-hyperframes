# Design — AI News Digest

## Style Prompt
Editorial tech-news aesthetic on a dark near-black canvas. Each of the three AI labs is introduced as a numbered section with a horizontal accent bar in its brand color. Typography is a single sans-serif family with strong weight contrast between display and body. Motion is precise and assertive: fast staggered entrances, long holds, crossfade transitions.

## Colors
- Background: `#0a0a0f`
- Surface line: `#1f1f27`
- Text primary: `#fafafa`
- Text secondary: `#c7c7d1`
- Text muted: `#71717a`
- OpenAI accent: `#10a37f` (green)
- Anthropic accent: `#d97757` (coral)
- Google accent: `#4285f4` (blue)
- Google trio: `#ea4335` / `#fbbc04` / `#34a853`

## Typography
- Inter — display (700), section name (600), body (500), labels (500 tabular)

## Motion
- Entrance eases: `expo.out` (headlines), `power3.out` (body), `power2.out` (labels)
- Scene crossfade: 0.5s on the incoming scene's opacity while outgoing scene still holds
- Accent bar: `scaleX` from 0 with `transformOrigin: left`, `expo.out`, 0.8s
- Stagger: 0.18s between news items

## What NOT to Do
- No `Math.random` or `Date.now`; no network fetches
- No per-scene exit animations (the crossfade is the exit) — final scene only
- No full-screen linear gradients on the dark canvas (H.264 banding)
- No drop-shadows on text; no emoji
- No `<br>` inside body copy — let text wrap via `max-width`
