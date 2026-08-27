# LSS Updater - Netlify Deployment

## Quick Start

## Your Netlify URL

**https://lss-oman.netlify.app**

The endpoint URLs are already configured:
- Student: `https://lss-oman.netlify.app/student/latest.json`
- Tutor: `https://lss-oman.netlify.app/tutor/latest.json`

## How to publish an update

1. Build the app with signing:
   ```powershell
   $env:TAURI_SIGNING_PRIVATE_KEY = "C:\Users\<you>\.tauri\lss-updater.key"
   $env:TAURI_SIGNING_PRIVATE_KEY_PASSWORD = "mypassword"
   cd packages/tutor && cargo tauri build
   ```

2. Find the built files:
   - `packages/tutor/src-tauri/target/release/bundle/nsis/LSS_Tutor_<VERSION>_x64-setup.exe`
   - `packages/tutor/src-tauri/target/release/bundle/nsis/LSS_Tutor_<VERSION>_x64-setup.exe.sig`

3. Read the `.sig` file content

4. Update `updater/tutor/latest.json`:
   - Set `version` to the new version
   - Set `notes` to the changelog
   - Set `signature` to the `.sig` file contents
   - Set `url` to the download URL

5. Copy the `.exe` file to `updater/releases/`

6. Drag & drop the updated `updater/` folder to Netlify again

## File Structure

```
updater/
├── README.md              ← This file
├── tutor/
│   └── latest.json        ← Tutor update endpoint
├── student/
│   └── latest.json        ← Student update endpoint
└── releases/
    ├── LSS_Tutor_x.x.x_x64-setup.exe
    ├── LSS_Tutor_x.x.x_x64-setup.exe.sig
    ├── LSS_Student_x.x.x_x64-setup.exe
    └── LSS_Student_x.x.x_x64-setup.exe.sig
```
