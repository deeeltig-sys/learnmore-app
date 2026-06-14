# LearnMore — Pɛ Adesua: Seek Knowledge (Capacitor Project)

GitHub repo: `learnmore-app`
Backend repo: `peadesua-backend`

Fully online AI learning hub by ProjectX Web Development. The old "offline
AI" version is dead — this version talks to your Flask + Groq backend
(`peadesua-backend`) over the internet.

## Folder structure

```
learnmore-project/
├── capacitor.config.json
├── package.json
├── package-lock.json
└── www/                  ← Capacitor webDir (this is what ships in the APK)
    ├── index.html        ← the app (frontend)
    └── assets/
        ├── usted-logo.png      ← ADD THIS
        └── projectx-logo.png   ← ADD THIS
```

## What's done

- `www/index.html` — onboarding (Name, Age, Topic), bright electric blue +
  silver onboarding screen, dark chat UI, loader screen wired for the
  USTED + ProjectX logos.
- Capacitor config already points `webDir` at `www`.

## What YOU need to do next

### 1. Add the two logo files
Drop these into `www/assets/`:
- `usted-logo.png` — USTED logo (PNG, ideally with transparent or white bg)
- `projectx-logo.png` — ProjectX logo (PNG)

The loader screen already references these paths — no code changes needed
once the files are there.

### 2. Set your backend URL
In `www/index.html`, find this line near the top of the `<script type="module">`:

```javascript
const BACKEND_URL = "https://YOUR_DEPLOYED_BACKEND_URL/ask";
```

Replace with your deployed Render URL, e.g.:

```javascript
const BACKEND_URL = "https://peadesua-backend.onrender.com/ask";
```

### 3. Install dependencies (first time only)
```bash
npm install
```

### 4. Add Android platform (first time only)
```bash
npx cap add android
```

### 5. Sync web assets into the native project
Run this every time you change `www/index.html` or add assets:
```bash
npx cap sync android
```

### 6. Build the APK
Open in Android Studio:
```bash
npx cap open android
```
Then Build → Build Bundle(s)/APK(s) → Build APK(s).

Or build from command line (requires Android SDK set up):
```bash
cd android
./gradlew assembleDebug
```
APK lands in `android/app/build/outputs/apk/debug/app-debug.apk`.

## Reminder

Test the backend URL in a browser first (`https://YOUR_URL.onrender.com/`)
— it should return `{"status": "ok", ...}`. If it returns an error or
times out, fix that before building the APK, or the app will just show
"Could not reach the AI" on every message.

## Push to GitHub

Create an empty repo named `learnmore-app` on github.com first (no README,
no .gitignore — just the bare repo), then:

```bash
cd learnmore-project
git init
git add .
git commit -m "LearnMore - Pe Adesua: Seek Knowledge - online v1"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/learnmore-app.git
git push -u origin main
```

