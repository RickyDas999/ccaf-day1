# Vision: Athletic Consistency Coach

An app that uses video analysis to help an athlete build a **repeatable base
motion**. It measures how each repetition drifts from the athlete's own
baseline and from best-practice form, then tells them what to fix, without
needing a human trainer.

## Core idea

Repetitive athletic skills reward consistency. The fewer variables that change
from rep to rep, the more predictable the outcome. The app should:

1. **Capture**: the user records many reps of the same motion on video.
2. **Track**: pose estimation and object tracking (body keypoints, ball, club)
   pull out the motion for each rep.
3. **Normalize**: build a baseline "signature" motion from the athlete's own
   reps, and optionally from a best-practice reference model.
4. **Compare**: score each rep against the baseline and reference, and flag
   where and when it deviates (which phase of the motion, which body part, by
   how much).
5. **Coach**: draw overlays on the video (lines, paths, angles) showing exactly
   where the motion needs to change, and give a plain-language correction.
   Real time is the goal; post-session analysis is the first step.

## Example 1: Basketball shooting

- Reference: shooters with a very repeatable form, such as Klay Thompson and
  Jared McCain. Both jump off both feet from a strong base, release at the top
  of the jump, and keep the same mechanics on every shot.
- Things to track per shot: foot placement and stance width, two-foot takeoff,
  knee bend depth, elbow alignment, set point, release timing relative to the
  top of the jump, release height and angle, follow-through, and ball arc.
- Output: a consistency score per shot, the frames where a shot strayed from
  the player's normal shot, and the specific variable that changed (e.g.
  "released on the way down", "base narrower than usual", "elbow flared out").

## Example 2: Golf swing

- Beginners are building habits, so the app should find habits that cause bad
  shots and prescribe changes.
- Things to track: address and posture, takeaway, top of backswing, club and
  hand path, hip and shoulder rotation, impact position, and follow-through.
- Example fault: **coming over the top**. The app detects an out-to-in
  downswing path, draws the actual swing path next to the correct swing plane
  on the video, and shows where the path needs to change.
- Output: the fault, why it causes the result (e.g. a slice or pull), a drill
  or cue to fix it, and a side-by-side comparison with a best-practice swing.

## Generalizing

Sports are plugins on a shared engine:

- **Shared engine**: video ingest, pose and object tracking, splitting a clip
  into reps, segmenting each rep into phases, building the baseline, scoring
  deviation, and rendering overlays.
- **Per-sport module**: phase definitions, key metrics, fault detectors,
  reference models, and the coaching text for each fault.

Other sports that fit: tennis serve, pitching, free throws, sprint starts,
weightlifting form, and so on.

## Open questions

- Platform: mobile app (on-device, real time) vs. web upload (batch) first?
- Single camera angle requirements per sport (e.g. down-the-line vs. face-on
  for golf).
- Where reference "best practice" data comes from, and how to account for
  different body types.
- MVP scope: probably one sport, post-session analysis, own-baseline
  consistency scoring, then add fault detection and real-time feedback.
