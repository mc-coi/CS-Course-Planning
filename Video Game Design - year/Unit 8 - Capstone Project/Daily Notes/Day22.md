# Day 22: Build & Export

**Session Goal:** Export a standalone build of your game that runs without Unity installed.

---

## Today's Focus

A finished game can be shared. Today you make a build — a standalone executable (Windows, Mac, or WebGL) that anyone can run. This is what you'll demo and submit.

---

## Work Session Agenda

**Minutes 0-10:** Final pre-build checklist (see below). Fix anything missing.

**Minutes 10-30:** Build the game (File → Build Settings → Build).

**Minutes 30-50:** Test the build on a different computer or fresh folder. Does it run?

**Minutes 50-55:** Zip the build folder. Name it: [YourName]_[GameTitle]_Build.zip. Submit or store.

---

## Build Checklist (Complete Before Building)

```
[ ] ALL scenes in File → Build Settings → Scenes In Build (in correct order)
[ ] Game starts on scene 0 (your main menu or first level)
[ ] No errors in Console during final play test in editor
[ ] Resolution Dialog disabled? (Edit → Project Settings → Player → Display Resolution Dialog → Disabled)
[ ] Company/Product name set (Edit → Project Settings → Player)
[ ] Build version set (e.g., 1.0)
[ ] Icons set if desired (Edit → Project Settings → Player → Icon)
```

---

## Build Steps (Windows Standalone)

```
1. File → Build Settings
2. Platform: PC, Mac & Linux Standalone
3. Target Platform: Windows
4. Architecture: x86_64
5. Click "Build" (not "Build and Run")
6. Create a new folder: YourName_GameTitle_Build
7. Wait for build to complete (1–5 minutes)
8. Navigate to the build folder
9. Double-click the .exe to test
10. Zip the ENTIRE folder (not just the .exe — it needs the Data folder!)
```

---

## Build Steps (WebGL — for browser play on itch.io)

```
1. File → Build Settings → WebGL
2. Click "Switch Platform" (may take a minute)
3. Player Settings → Publishing Settings → Compression Format: Disabled
4. Click "Build"
5. Upload the resulting folder to itch.io (free account)
6. Set to HTML game → link becomes shareable!
```

---

## Technical Tips

```csharp
// If your build shows a black screen:
// 1. Make sure scene 0 in Build Settings is your starting scene
// 2. Check for null reference errors that only trigger in build mode

// If build is very large (>100MB for a simple game):
// Edit → Project Settings → Player → Other Settings
// Set Scripting Backend to IL2CPP (smaller builds, but longer compile time)
```

---

## Reflection / Exit Ticket

1. Did your build run successfully? Y / N — if N, what error did you get?
2. How does it feel to run your game outside of the Unity editor?

---

## Progress Checklist

- [ ] Pre-build checklist completed
- [ ] Build created successfully
- [ ] Build tested outside Unity editor — game runs!
- [ ] Build folder zipped and named correctly
- [ ] Submitted to teacher or ready for showcase
