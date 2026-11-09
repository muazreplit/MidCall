# MidCall — Catches the scam mid-call

**MidCall** is an Android scam-call protection app designed to identify suspicious conversational patterns **while a call is happening** and warn the user before they are manipulated into sharing sensitive information or sending money.

MidCall focuses on **what the caller is trying to make you do**, not just who is calling.

> **A scammer doesn't need to hack your phone if they can convince you to hand them the keys yourself.**

---

## 🔐 Privacy & Architecture

MidCall is designed as a **local-first, privacy-focused Android application**.

- **No `INTERNET` permission**
- Core scam detection runs locally on the device
- No cloud server required for the core protection flow
- No cloud-based call recording or transcription
- Scam scoring and rules are processed locally
- SMS analysis happens locally
- Call history and app data are stored locally
- Users remain in control of optional AI explanation models imported into the app

MidCall is intentionally designed so that sensitive call-related information does not need to be sent to a remote server for its core detection.

---

# 🚨 Core Features

### Live Scam Call Detection

When an unknown caller is answered, MidCall can analyze available microphone audio locally using an on-device speech recognition pipeline.

The flow is:

**Audio → Vosk Speech-to-Text → Scam Rules → Risk Score → Warning**

The scam risk score is calculated continuously on a **0–100 scale**.

MidCall looks for combinations of suspicious conversational signals such as:

- Bank or government impersonation
- Fake KYC/account warnings
- OTP or PIN requests
- UPI/payment manipulation
- Urgency and threats
- Requests to install remote-access applications
- Suspicious links
- Financial requests
- Secrecy or pressure tactics
- Emotional manipulation

The goal is not to declare that a caller is definitely a scammer.

Instead, MidCall provides a **risk estimate and understandable warning** so the user can make a safer decision.

---

## ⚠️ Real-Time Warning System

When suspicious activity is detected, MidCall can display a prominent warning interface containing:

- Live risk score
- Warning category
- Suspicious-pattern chips
- Plain-language explanation
- Vibration feedback
- Spoken warning
- Ignore option
- Hang-up option

Example:

> **⚠️ Possible Scam**  
> Caller is requesting an OTP and creating urgency.  
> **Do not share your OTP or transfer money.**

The warning interface is designed to remain understandable even when the user is stressed or distracted during a call.

---

# 🎙️ Call Audio & Android Limitations

Android places strict restrictions on third-party applications accessing cellular call audio.

Because of these platform restrictions, **MidCall does not claim to secretly record or directly capture both sides of every cellular call**.

For supported testing scenarios, MidCall uses the device microphone and recommends **speakerphone mode** so that the conversation can be picked up by the microphone.

The scanner attempts supported microphone/audio configurations available to the application.

This is an important platform limitation rather than something MidCall attempts to bypass.

> **Speakerphone is required for the current real-call testing flow.**

---

# 🧠 Detection Engine

MidCall's core detection engine is **local and rule-based**.

The scoring engine evaluates multiple signals instead of triggering an alert from a single keyword.

For example:

```text
OTP request
      +
KYC threat
      +
Urgency
      +
Bank impersonation
      ↓
Higher scam risk
```

This reduces the chance of treating ordinary conversations containing isolated words such as "bank", "OTP", or "payment" as scams.

### Important

The scoring system provides an **estimate**, not certainty.

MidCall does not claim that every detected conversation is fraudulent.

---

# 📱 SMS Protection

MidCall can monitor newly received SMS messages and locally evaluate them for suspicious patterns.

Potential warning categories include:

- Fake bank messages
- KYC scams
- OTP-related scams
- Prize/reward scams
- Suspicious links
- Payment requests
- Account suspension threats
- Impersonation

When a suspicious message is detected, MidCall can show an immediate warning notification.

---

# 🧪 Demo Mode

MidCall includes a built-in demo environment for presentations and testing.

It contains:

- **10 scripted scam scenarios**
- **2 genuine conversations**
- Live scoring using the actual detection engine
- No phone call required
- No permissions required

Demo scenarios can simulate situations such as:

- Bank impersonation
- Fake KYC expiration
- OTP theft
- Police/digital-arrest threats
- UPI payment manipulation
- Remote-access scams
- Urgent account suspension

This allows the complete detection and warning flow to be demonstrated safely without making real scam calls.

---

# 🤖 Optional On-Device AI Explanations

MidCall can optionally use a locally imported language model to generate clearer explanations of detected scam patterns.

The AI explanation feature is **optional** and separate from the core detection engine.

The core protection does not depend on a cloud AI service.

Users can import a supported `.task` model through:

**Settings → AI Explanations → Choose Model File**

Supported models depend on the model format and device capabilities.

---

# 🛡️ Protection

MidCall provides a central protection control for enabling or disabling monitoring.

Features include:

- One-tap protection control
- Foreground protection service
- Protection state persistence
- Tap-to-resume after restart
- SMS monitoring
- Call monitoring

---

# 📊 Activity

MidCall maintains a local activity history containing previous detections and their details.

Users can review:

- Risk score
- Detection categories
- Warning details
- Call/message context
- Detection time

The application does not require a cloud account for this history.

---

# 🚫 Blocked Numbers

Users can maintain a local list of blocked numbers.

Features include:

- Add/remove numbers
- Country-code picker
- `+91` default
- Number normalization
- Local storage

MidCall does **not** automatically reject calls in the current version.

---

# 🔎 Check a Message

The Home screen includes a **Check a Message** search field.

Users can paste suspicious text and receive a local scam-risk assessment without requiring a cloud API.

---

# 📚 Learn About Scams

MidCall includes educational content covering common scam techniques, including:

- OTP scams
- KYC scams
- Bank impersonation
- UPI fraud
- Remote-access scams
- Digital arrest scams
- Phishing
- Social engineering
- Urgency and emotional manipulation

The goal is not only to detect scams, but also to help users understand **why the conversation or message is dangerous**.

---

# 📞 Report a Scam

MidCall provides access to India's cybercrime reporting resources, including the **1930 cybercrime helpline**.

---

# 🩺 Diagnostics

A dedicated Diagnostics section helps test:

- Protection service
- Microphone availability
- Speech recognition model
- Required permissions
- Audio configuration
- Detection engine
- App state

This is particularly useful because Android device manufacturers can implement different restrictions around call audio and background services.

---

# 🎨 Design

MidCall follows an **Apple-inspired visual language adapted for Android**.

Design principles include:

- Glass-style cards
- Soft animated glow backgrounds
- Large rounded corners
- Inter typography
- iOS-inspired type scale
- 8-point spacing system
- Spring animations
- Haptic interactions
- Light and dark themes
- Translucent surfaces
- Dynamic Island-inspired listening interface

The actual Apple **SF Pro** font is not bundled. MidCall uses **Inter** as the closest open alternative.

Android does not provide a universal true backdrop-blur system for application cards, so the glass effect is implemented using translucent surfaces, gradients and blurred background glows.

---

# 🧭 Navigation

MidCall uses a floating glass navigation bar with:

**Activity · Blocked · Home · Learn · Settings**

Home is positioned in the centre for quick access to the main protection interface.

The **Check a Message** feature is accessible directly from the Home search field.

---

# 🏗️ Project Architecture

```text
MidCall/
│
├── engine/
│   └── Scam scoring and detection rules
│
├── call/
│   ├── Call monitoring
│   ├── Audio scanner
│   ├── Vosk speech recognition
│   └── Call overlay
│
├── ai/
│   └── Optional on-device language model
│
├── demo/
│   └── Scripted scam/genuine conversations
│
├── data/
│   ├── Room database
│   └── DataStore
│
├── service/
│   ├── Foreground protection service
│   ├── SMS receiver
│   └── Boot handling
│
├── ui/
│   └── Jetpack Compose screens
│
├── util/
│   ├── Phone number utilities
│   └── Country information
│
├── tools/
│   ├── Python scoring mirror
│   └── Evaluation tools
│
└── docs/
    ├── Research report
    └── Demo guide
```

---

# 🛠️ Technology Stack

- **Kotlin**
- **Android**
- **Jetpack Compose**
- **Room**
- **DataStore**
- **Foreground Services**
- **Vosk**
- **On-device speech recognition**
- **Optional on-device language model**
- **Python evaluation tools**

---

# 🚀 Build & Run

### 1. Open the project

Open the project in **Android Studio**.

Sync Gradle and run the application on a physical Android device.

**Supported:** Android 12+

---

### 2. Install the Vosk speech model

Download a small English Vosk model from:

https://alphacephei.com/vosk/models

For example:

`vosk-model-small-en-in-0.4`

Place the model contents inside:

```text
app/src/main/assets/model/
```

The final structure should contain:

```text
app/src/main/assets/model/am/final.mdl
```

Rebuild the application.

---

### 3. Optional AI explanation model

Inside the application:

**Settings → AI Explanations → Open Download Page**

Download a compatible `.task` model and import it using:

**Choose Model File**

AI explanations are optional and are not required for the core scam detection engine.

---

# 🧪 Testing

### Automated rule evaluation

Run:

```bash
python tools/evaluate.py tools/india_samples.tsv
```

### Android tests

Run:

```text
ScamScorerTest
```

from Android Studio.

### Demo testing

Navigate to:

**Home → Demo**

Demo mode does not require permissions or real calls.

### Real-call testing

For the current supported testing flow:

1. Use an unsaved/unknown number.
2. Answer the call.
3. Turn **speakerphone ON**.
4. Read a test scam script.
5. Observe the live detection and warning interface.

---

# ⚠️ Current Limitations

MidCall is a prototype and has important technical limitations.

### Android call audio

Android restricts third-party access to cellular call audio.

Therefore:

- Speakerphone is required for the current real-call testing flow.
- MidCall does not secretly record cellular calls.
- MidCall does not claim unrestricted access to both sides of a cellular call.
- Device manufacturers may apply additional restrictions.

### Speech recognition

The current build primarily supports:

- English speech
- Vosk-based local speech recognition

### Detection

- Risk scores are estimates.
- Detection is not guaranteed to identify every scam.
- New scam techniques may not be covered by existing rules.
- The current system does not automatically reject calls.

### AI explanations

- Optional
- Device-dependent
- Requires a compatible imported model
- Not required for the core detection engine

---

# 🔒 Security & Privacy Principles

MidCall follows several core principles:

**Local first.**

**No cloud dependency for core detection.**

**No unnecessary call recording.**

**No `INTERNET` permission.**

**Explain the danger instead of simply showing a score.**

**Warn without claiming certainty.**

---

# 🎯 Why MidCall?

Traditional caller protection often focuses on:

> **“Who is calling?”**

MidCall focuses on:

> **“What is this caller trying to make you do?”**

A scammer can use a new phone number, impersonate a trusted organization, or manipulate a victim through urgency and fear.

MidCall is designed to identify those **conversational warning signs** and intervene at the moment they matter.

---

# 📌 Project Status

**MidCall is an active prototype under development.**

The project currently includes:

- Local scam-risk scoring
- Live detection pipeline
- Vosk speech recognition
- SMS scanning
- Real-time warning UI
- Demo scenarios
- Local activity history
- Number management
- Optional on-device AI explanations
- Diagnostics
- Scam education
- Reporting resources

The next stage of development focuses on improving detection accuracy, audio integration within Android's supported capabilities, warning UX, multilingual support, and real-world validation.

---

## ⚖️ Disclaimer

MidCall is a safety-assistance tool and **not a guarantee against fraud**.

Users should never share OTPs, PINs, passwords, card credentials or remote-access permissions with an unknown caller, even when MidCall does not display a warning.

**Stay alert. Stop. Verify.**
