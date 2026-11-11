Refresh and follow all conventions in `/home/robin/Admin-Manual`, the global single source of truth.

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository status

Greenfield. As of the first commit the repo contains only `README.md` (title: "Chattatonic-Extension-Reader"). No stack, package manager, build, lint or test tooling has been chosen yet, so there are no commands to list. When the scaffold lands, add the real build / lint / test / single-test commands here; do not guess them.

Everything below is the product brief from the owner. Treat it as requirements, not as a description of existing code. It is the input to `ARCHITECTURE.md`, which does not exist yet; under the Architecture Law no `CHECKLIST.md` and no code may be written until that snapshot is complete and operator-approved. Once `ARCHITECTURE.md` exists it supersedes this brief.

## Product

Chattatonic Reader is a commercial SaaS that reads content aloud so the user does not have to read it. It ships as two user-facing surfaces that share one reading engine:

- **Web app** for uploaded content (PDF and other documents).
- **Chrome extension** for DOM-aware reading of the page the user is on.

## Reading engine invariants

These span every surface and are the parts that are easy to break by working on one file in isolation.

- **The sentence is the base unit.** TTS is rendered per sentence, the read-ahead buffer is sized in whole multiples of sentences, and highlighting advances sentence by sentence. Segmentation, synthesis, buffering and highlighting must all agree on the same sentence boundaries and IDs.
- **Read-ahead pipeline.** Synthesis runs multithreaded in the background, ahead of playback, so audio for upcoming sentences is ready before the playhead reaches them. Playback starts as soon as the first unit is ready rather than waiting for the whole document.
- **Calibration.** On first install, and again whenever the user triggers it, the app benchmarks the machine and uses the result to set the balance between background rendering and read-ahead depth (worker count, buffer size). Calibration results are per device and must be re-runnable.
- **Karaoke highlighting, two render paths.**
  - DOM-aware content: highlight the current sentence in the page.
  - PDF and other screen content with no usable DOM text: draw the highlight as a glow on a canvas layer overlaid on the content in the browser.
- **Content sources.** Uploaded content and DOM-aware live page content both feed the same sentence pipeline.

## Tiers and entitlements

- **Free demo:** single reader voice, limited use.
- **Paid:**
  - multiple voices reading different sections of web content;
  - intelligent document layout preprocessing (VLM, Surya and similar) before segmentation;
  - voice cloning, aimed at content producers making voiceovers.
- **Plans:** daily, monthly, annual, and an unlimited lifetime option, priced in line with competitors. Actual prices are not set yet.

Feature gating must be decided from the licence/entitlement state, not from client-side flags alone, in both the web app and the extension.

## Operator decisions (2026-11-11)

- **Main TTS synthesis runs on-device**, in the browser, in worker threads. This is what calibration tunes. Server-side work is limited to the paid hosted features (voice cloning, layout preprocessing, hosted rendering).
- **Commerce is WooCommerce plus custom plugins written in this repo** for entitlements and for hosted render credits. There is no separate funnel product to integrate with.

## Commerce and licensing

Billing runs through WooCommerce. The custom WooCommerce plugins needed for entitlement gating, licence keys and hosted render credits are in scope for this repo and must be built here rather than assumed to exist. Hosted render credits are a metered balance consumed by server-side rendering, separate from the plan entitlement.

## UI bar

Everything user-facing (web app, extension popup/overlay/options, purchase and licence flows) must be beautiful, modern and flashy. Plain default styling is not acceptable for a shipped surface.
