# Openverse API + Real SFX — Recorded Sound Design Pipeline

**Status:** ADDED TO TOOLBELT / RESEARCHED, NOT INSTALLED OR ENABLED
**Purpose:** Search, verify, license, index, and frame-align real sound effects for cinematic website video, photo-booth motion assets, demos, and marketing renders.

## Verified upstream references
- Openverse API: https://api.openverse.org/v1/ (Openverse, open-licensed media search)
- Openverse docs: https://docs.openverse.org/
- Real SFX skill: https://github.com/Clipwing/skills/tree/main/skills/real-sfx
- Real SFX official page: https://clipwing.pro/skills/real-sfx

## Roles
**Openverse API: discovery.** Anonymous API requests can search recordings without credentials under usage/rate limits. Audio endpoint: `GET https://api.openverse.org/v1/audio/?q=whoosh&license=cc0`. Indexed works have individual licenses, attribution and origin metadata. It is a search index, not a guarantee that a file is available, genuine, properly licensed, or suitable.
**Real SFX: sound placement.** Free Clipwing Claude Code skill that selects recordings from an authorized local SFX library, aligns sound to cue lists/timeline or inferred visual moments, and exports a new MP4, an SFX WAV track, and a cue report. It uses real recordings rather than synthesized effects. Upstream reports 78 bundled CC0 UI sounds.

## Proposed workflow
1. Identify cues and desired audio character from the video: transitions, object motion, impacts, ambience, reveal.
2. Search Openverse using narrow queries, primarily `license=cc0` for commercial projects. Present candidates with creator, source, duration, license, and preview before downloading.
3. Independently check source provenance and current license; reject NC/ND or otherwise unsuitable licensing. Do not assume all Openverse audio is CC0. Maintain `audio-provenance.json` and any needed attribution in release artifacts.
4. Curate and normalize approved SFX to a **local authorized library**; avoid downloading large collections or scraping; respect API throttling.
5. Use Real SFX after reviewing the skill scripts and installing into project-scoped `.claude/skills/real-sfx/` only with explicit authorization. Upstream requires Python >=3.9 and FFmpeg in PATH.
6. Supply a cue list and place each effect on the correct frame. Preserve existing music/voice, avoid overpowering effects, verify fades and loudness.
7. Export MP4, separate WAV, cue sheet, source/license manifest; spot-check sync by viewing and listening. Tools' measured analysis does not replace human listening.
8. For website use: weigh autoplay sound accessibility, mute defaults, browser playback restrictions, mobile network cost and performance. **Never assume audible autoplay is appropriate**.

## Best STS uses
- Smash Hero: authentic sizzle, whoosh, motion and UI transition cues for demos/showreels (only when sound is expected).
- The Fun Frame: cinematic event promo video and FotoMaster assets where supported; maintain lightweight codecs/size budgets, required format compatibility, and quiet/muted version.
- STS client sites: optional branded film/video deliveries; audio on web only by explicit user action and accessibility-safe controls.

## Governance
- No installation, scripts executed, media downloads, or transmission of private client assets in this commit.
- No claims that Openverse/Real SFX are installed, tested, or integrated into rendering pipeline.
- Confirm third-party dependencies, file licenses and skill safety before adoption.
- This supplements, never replaces, existing STS copyright, security, performance, and site QA rules.
- Keep provenance even for CC0 when practical; CC BY requires attribution, and non-commercial licenses must not be used for commercial client assets.
- Openverse API has rate limits; do not scrape or circumvent pagination limits.

## Evaluation gate
Pilot on one synthetic 15–30 second demo with 3–5 cues. Grade retrieval relevance, verified licensing, frame sync, sound balance, export integrity, build reproducibility and time spent. Keep disabled until owner approves real adoption.
