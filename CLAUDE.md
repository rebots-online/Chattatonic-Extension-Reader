Refresh and follow all conventions in `/home/robin/Admin-Manual`, the global single source of truth.

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository status

Greenfield. No stack, package manager, build, lint or test tooling exists yet, so there are no commands to list. When the scaffold lands, add the real build / lint / test / single-test commands here; do not guess them.

The repo is in the screens-first phase (TC12). Stitch exports are frozen under `LIBS/UI/STITCH/` but are **not yet cleared by the operator**. Until they are cleared, `ARCHITECTURE.md` may not be started; until `ARCHITECTURE.md` is complete and approved, no `CHECKLIST.md` and no code may be written. Once `ARCHITECTURE.md` exists it supersedes the brief below.

Decisions and research from the init sessions are in KStore (search "chattatonic-reader").

## Product

Chattatonic Reader (pronounced "catatonic"; the name comes from the Chatterbox and Supertonic TTS models) is a commercial product that reads content aloud so the user does not have to read it. Two user-facing surfaces share one reading engine:

- **Web app** for uploaded content (PDF and other documents).
- **Chrome extension** for DOM-aware reading of the page the user is on.

## Reading engine invariants

- **The sentence is the base unit.** TTS is rendered per sentence, the read-ahead buffer is sized in whole sentences, and highlighting advances sentence by sentence. Segmentation, synthesis, buffering and highlighting must agree on the same sentence boundaries and IDs.
- **Synthesis is on-device**, in the browser, in worker threads, ahead of playback. Playback starts as soon as the first unit is ready.
- **Two on-device engines behind one interface.** Supertonic is the baseline. Chatterbox is the alternative where the device supports it. A self-built ONNX model is a later option. Both upstream repos are archived, so no code may depend on one engine directly.
- **Calibration** runs on first install and on demand. It measures the machine per engine, decides which engines that device can run, and sets worker count and read-ahead depth. It must actually load and time an engine, not infer support from hardware hints.
- **Karaoke highlighting, two render paths.** DOM-aware content is highlighted in the page. PDF and other content without usable DOM text gets a glow drawn on a canvas layer over the content.

### Reference implementation

`github.com/rebots-online/astronatally` (`src/voice/index.ts`, `src/atelier-original/services/supertonic.worker.ts`, `voiceService.ts`) runs Supertonic in the browser with gapless playback. Reuse its worker loading, pinned model revision, WebGPU-to-WASM fallback, real-time-factor measurement, cancellation and gesture-gated audio. It differs from this product in ways that must not be copied: it uses one serialised worker, prefetches only one chunk ahead, packs several sentences into a chunk, and starts each chunk on the previous one's `onended` rather than on the audio clock.

## Tiers and pricing rules

- **Free:** one voice, limited use.
- **Passes** (day, month, year, lifetime) unlock everything that runs on the user's own device. They pay for the software, not for compute, and do not auto-renew. Call them passes, never subscriptions.
- **Render credits** meter anything that runs on hosted inference, at full cost. A pass never includes unmetered hosted usage. There is no subsidised flat-rate inference.
- Whether a feature is pass or credits follows from where it runs.
- Paid features: multiple voices per document section, intelligent layout preprocessing (VLM, Surya and similar), voice cloning for content producers' voiceovers.
- Prices are data from the billing provider, not constants in code.

## Voice cloning consent

- The consent script is assembled at consent time from randomly chosen component phrases. The grantor reads it aloud; the recording is stored; that same recording is the cloning sample.
- Consent recordings may be uploaded, to support third-party grantors.
- Consent gates release, not rendering: a job may render before consent arrives, but no media file is released until a valid consent is on record.
- The stored consent is due-diligence evidence, not proof of identity.

## Model licence duties

Supertonic weights are under BigScience OpenRAIL-M. It allows commercial use but requires: no impersonation without consent; generated audio must be disclosed as machine generated; the use restrictions must be passed on to users in our terms; recipients of the model must be given a copy of the licence. Chatterbox code is MIT and watermarks every output; its weights licence has not been checked yet.

## Commerce

- **Billing is Polar.sh.** No WooCommerce.
- The apps never talk to the billing provider directly. Our own entitlement check sits between them, and feature gating is decided from that entitlement, not from client-side flags.

## Identity and licensing of this repo

- **Everything identifying is build-time `.env` configuration** (TC17): app name, namespace, URLs, extension name, billing IDs, support and legal links. The same code must be able to run under a different banner.
- An unconfigured build must not present itself as the operator's product, so a misconfigured clone cannot impersonate it. Billing IDs, signing keys and service URLs are never committed.
- The repo starts under a proprietary licence, with open-sourcing kept possible. Record each dependency's licence as it is added.

## UI

- Everything user-facing must be beautiful, modern and flashy. The design system is `LIBS/UI/STITCH/DESIGN.md`.
- The Stitch exports under `LIBS/UI/STITCH/screens/<slug>/index.html` are the UI. Do not edit them by hand, redraw them, or have a coder re-implement a screen; integrate the export. Each screen's `meta.md` lists where Stitch departed from the prompt.
