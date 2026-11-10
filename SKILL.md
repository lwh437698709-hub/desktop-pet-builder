---
name: desktop-pet-builder
description: Create or update desktop pets by planning actions, preparing character-consistent animation prompts and assets, integrating interaction states, and packaging for macOS or Windows.
metadata:
  short-description: Build desktop-pet actions, assets, interactions, and packages
---

# Desktop Pet Builder

Use this skill when the user wants to create or improve an animated desktop pet, its action assets, input behavior, or installable app. For the detailed production and QA checklist, read [the reusable workflow](references/desktop-pet-production-workflow.md).

## Required user confirmation points

### 1. Choose actions, then collect matching images

- If the requested actions are not clear, ask which actions the user wants before requesting images. Offer relevant choices such as mouse gaze, held/drag sway/release, walking, sleeping, kneading, and stretching. Reuse actions already specified; do not ask the user to repeat them.
- After the action choice is clear, request the pet’s identity reference and images that show the selected poses/actions. If suitable images are already attached or named in context, use them instead of asking again.
- Once the images are available, write prompts that preserve the identity reference and describe only the selected action, framing, background, camera stability, continuity, and desired start/end poses. Keep separate prompts for actions with different motion semantics.
- If the user asks only for prompts or material preparation, stop at that scope; do not integrate the pet into an app or package it without being asked.

### 2. Choose the packaging platform

- Before platform-specific app integration or packaging, confirm whether the deliverable targets macOS, Windows, or both, unless the user has already stated the target in the current request or established context.
- Do not infer Windows just because packaging is happening on a Mac, or infer Mac because the development machine is a Mac.
- For material-only work, do not block progress on a platform choice. Ask when the workflow reaches integration/package planning.

## Production workflow

1. Define the identity bible, selected actions, state transitions, canvas, anchors, display size, and target platform.
2. Inspect source images/videos and metadata. Preserve originals. Produce one pilot and a numbered contact sheet before processing a full sequence.
3. Extract and key/cut out frames. Review the entire animation at native display scale, not only a small contact sheet. Track defective frame numbers and repair only the affected frames with consistent masks/curves.
4. Normalize each frame to one transparent canvas with isotropic scaling and named head/body/ground anchors. Never distort aspect ratio. Retain margin for ears, whiskers, paws, props, and tail.
5. Show the processed sequence and transition preview to the user for approval before replacing existing app assets.
6. Implement a state machine: a single visible state at a time; define event triggers, loop/one-shot behavior, cancellation, and the exact return state. Use program logic for input timing and AI/video assets for semantic body motion.
7. Package only for the chosen platform. Verify application/installer icons, startup behavior, upgrade-in-place rules, install path, and version identity.
8. Validate every transition, long holds, rapid input, frame boundaries, monitor/display scaling, clean install, upgrade, and uninstall on the target operating system.

## Quality invariants

- Preserve the user's identity reference; action references define pose, not a new character.
- Never stretch or squash frames to force alignment. Align by head size and anchors using uniform scale and translation.
- Check every flagged frame in context with its neighbors; a repair must not create edge flicker, holes, missing body parts, or clipped tails.
- Do not claim that interpolated samples are genuinely captured viewpoints. Inspect loop seams and discard malformed frames rather than keeping them to satisfy a frame count.
- Keep keyboard monitoring limited to the minimum events needed to animate. Do not read, log, or store typed characters.
- Separate confirmed requirements from assumptions. Ask only at the two decision gates above when information is missing; otherwise proceed and keep the user updated.
