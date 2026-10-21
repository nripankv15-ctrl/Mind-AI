# ManyMind AI Windows wrapper

This Electron shell opens the current HTTPS ManyMind AI website and uses a hardened renderer configuration (`nodeIntegration: false`, `contextIsolation: true`, `sandbox: true`). It does not bundle model weights or work offline.

Build on Windows with Node.js 22:

```powershell
npm install
npm run build:win
```

The NSIS installer is written to `dist/ManyMind-AI-Setup-1.0.0.exe`. For wider distribution, obtain a code-signing certificate and configure signing in CI; this project does not include private signing keys.
