# MidCall — Catches the scam mid-call

Offline Android app (Android 12+). Watches new SMS and answered calls from unknown numbers, scores scam
risk 0-100 live, shows a warning bar at the top of the screen, and explains the danger in plain words.
The app has **no INTERNET permission**.

## Features
- **Protection**: one-tap power control, foreground service, "tap to resume" after restart
- **Live call scanning**: mic -> Vosk speech-to-text -> scoring every ~1.2 s -> top bar with score ring,
  waveform, warning chips, vibration, spoken alert, Hang up / Ignore
- **SMS scanning** (new messages only) with instant warning notification
- **Activity** history with details, **Blocked numbers** with country-code picker (+91 default)
- **Demo mode**: 10 scripted scam calls + 2 genuine calls played live through the real scoring engine
- **On-device AI explanations** (optional model file you download and import in the app)
- **Check a message**, **Learn about scams**, **Report a scam** (helpline 1930), **Diagnostics**
- Apple-style design: glass cards over a soft animated glow, Inter font (closest open match to SF Pro),
  spring animations, iOS push transitions, dark and light themes
- Floating glass tab bar with **Home in the centre**: Activity, Blocked, Home, Learn, Settings
- "Check a message" lives in the search field at the top of Home
- Listening bar styled like Apple's Dynamic Island: springs in from the top, morphs open on a scam

## Design notes
Follows Apple's Human Interface Guidelines as closely as Android allows: iOS system colours, the iOS type scale
(34/28/22/20/17/15/13/12/11), 8-point spacing, large rounded corners, translucent materials, spring motion
and haptic taps. Apple's own SF Pro font cannot be bundled, so the app uses Inter. Android has no true
backdrop blur for cards, so glass is drawn as translucent gradients over blurred colour glows.

## Build and run
1. Open the folder in Android Studio, Sync Gradle, run on a physical phone (Android 12 or newer).
2. **Speech model (needed for live calls)**: download a small Vosk English model from
   https://alphacephei.com/vosk/models (e.g. `vosk-model-small-en-in-0.4`). Put its folders
   (`am`, `conf`, `graph`, `ivector`) in `app/src/main/assets/model/` so that
   `app/src/main/assets/model/am/final.mdl` exists. Rebuild.
3. **AI explanations (optional)**: in the app, Settings > AI explanations > "Open download page", download a
   `.task` model (Gemma 3 1B, or a Llama .task if you have one), then "Choose model file".

## Verify
- `python tools/evaluate.py tools/india_samples.tsv` measures the rules; run `ScamScorerTest` in Android Studio.
- Demo mode needs no permissions or calls: Home > Demo.
- Real call test: call from an unsaved number, answer, speakerphone ON, read a scam script.

## Layout
engine/ scoring | call/ monitor, scanner, Vosk, overlay | ai/ language model | demo/ scripted calls
data/ Room + DataStore | service/ foreground service, SMS, boot | util/ phone numbers, countries
ui/ Compose screens | tools/ Python mirror of the rules + evaluator | docs/ report + demo guide

## Honest limits
- Android blocks silent call recording. Speakerphone is required. The scanner tries several mic modes.
- English speech model only in this build. No automatic call rejection.
- Scores are estimates, and MidCall never clicks links or claims certainty.
- Keep tools/rules.py and engine/ScamRules.kt in sync when you edit rules.
