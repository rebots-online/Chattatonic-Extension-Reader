# Chattatonic Reader — design system

Stitch project: `projects/81951782971452349` ("Chattatonic Reader").
Status: elucidation in progress. Not yet cleared by the operator (TC12 rule 9).

## Product in one line

Chattatonic Reader reads web pages, PDFs and uploaded documents aloud with on-device voices, highlighting each sentence as it is spoken.

The name is written "Chattatonic" and pronounced "catatonic". It comes from the TTS model families the product is built on.

## Mood

Night-studio, luminous, confident. The signature visual is **the glow**: the sentence being read is lit from behind, as if the words were giving off light. That same glow is reused for primary buttons, the play control, progress and focus, so the whole product feels like one instrument.

Modern and flashy, never noisy: one glowing thing per view.

## Colour

Dark mode is the default and the only mode designed.

| Token | Value | Use |
|---|---|---|
| `bg-base` | `#0B0A14` | page background |
| `bg-raised` | `#14122A` | cards, panels |
| `bg-glass` | `rgba(255,255,255,0.06)` with 20px backdrop blur | player bar, popup, overlays |
| `border-subtle` | `rgba(255,255,255,0.10)` | hairlines on glass |
| `primary` | `#8B5CF6` (violet) | primary actions, active states |
| `secondary` | `#22D3EE` (cyan) | progress, buffered audio, links |
| `tertiary` | `#F472B6` (pink) | accents, paid-feature badges |
| `glow-gradient` | `#8B5CF6` → `#F472B6` → `#22D3EE` at 120° | hero, play button, current-sentence glow |
| `text-high` | `#F5F3FF` | headings, body |
| `text-mid` | `#B4B0D0` | secondary text |
| `text-low` | `#6E6A8F` | hints, disabled |
| `success` | `#34D399` | ready, licence active |
| `warning` | `#FBBF24` | limit approaching |
| `danger` | `#F87171` | errors, expired |

Each reader voice has its own hue for multi-voice sections: violet, cyan, pink, amber `#FBBF24`, green `#34D399`. A section's left edge and its sentence glow take the voice's hue.

## Type

- Headings: **Bricolage Grotesque**, weights 600–800, tight tracking (-0.02em) at display sizes.
- Body and UI: **DM Sans**, 400/500/700.
- Reading surface: DM Sans 20px, line height 1.7, max width 68 characters.
- Numbers (timers, prices, credit balances): tabular figures.

## Shape and depth

- Radius: 12px controls, 20px cards, fully round for the play button and pills.
- Depth comes from light, not shadow: raised things get a soft outer glow in their own colour, not a black drop shadow.
- Glass panels have a 1px `border-subtle` hairline.

## Signature components

- **Current-sentence glow.** The spoken sentence sits on a soft, blurred gradient halo with brighter text. Sentences already read drop to `text-mid`. Upcoming sentences that are already synthesised carry a faint cyan underline (the read-ahead buffer made visible).
- **Player bar.** Glass bar docked at the bottom: previous sentence, large round gradient play/pause, next sentence, speed pill, voice avatar pill, a progress track with two layers (played in the gradient, buffered in cyan), time remaining.
- **Voice chip.** Round avatar in the voice's hue with an animated waveform ring while that voice speaks.
- **Pass card.** Pricing card for a pass; the recommended one has an animated gradient border.
- **Credit meter.** Pill showing hosted render credit balance with a small lightning icon; pink when a paid hosted feature will spend credits.
- **Paid badge.** Small pink "PASS" pill on features that need a pass; a cyan "CREDITS" pill on features that spend hosted credits.

## Motion

- Sentence glow cross-fades to the next sentence in 180ms.
- Play button breathes (slow 3s glow pulse) while playing.
- Calibration shows a live animated gauge.
- Respect `prefers-reduced-motion`: glows stay, movement stops.

## Vocabulary

- Paid time-based access is a **pass** (Day Pass, Month Pass, Year Pass, Lifetime Pass). Never "subscription"; passes do not auto-renew.
- Metered hosted usage is **render credits**.
- The free tier is **Free**.
- Buttons say what they do: "Read this page", "Add a document", "Get a pass", "Buy credits", "Run calibration".

## Sample commerce data shown on screens

Prices and limits on the screens are sample WooCommerce product data, not fixed design content:
Free (1 voice, 20 minutes a day), Day Pass $2, Month Pass $8, Year Pass $49, Lifetime Pass $99, render credits 100 for $5.

## Anti-patterns

- No light theme, no white cards.
- No black drop shadows, no neumorphism.
- No more than one gradient-filled element competing with the current-sentence glow in a reading view.
- No stock-photo people. Use abstract waveforms, light and type.
- No "subscribe" or "unlimited AI" wording.
