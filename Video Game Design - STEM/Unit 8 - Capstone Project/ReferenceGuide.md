# Vocabulary & Quick Reference

## Project Management Terms

| Term | Definition |
|------|-----------|
| **GDD** | Game Design Document; specification of the game |
| **MVP** | Minimum Viable Product; smallest playable version |
| **Scope** | Amount of work to complete the project |
| **Iteration** | Cycle of build → test → feedback → improve |
| **Vertical Slice** | Complete but small version showing all systems |
| **Prototype** | Working implementation of core mechanic |
| **Playtest** | Real players testing your game |
| **Polish** | Final refinement for quality |
| **Build** | Compiled version for distribution |
| **Reflection** | Analysis of what was learned |

## Build & Export Quick Reference

```csharp
// WebGL Build Checklist
/*
1. File > Build Settings
2. Add all scenes (drag from Hierarchy)
3. Select WebGL platform
4. Configure Player Settings:
   - Company Name
   - Product Name
   - Default Icon
   - Resolution
5. Click "Build"
6. Choose output folder
7. Test in web browser
*/

// Common Build Settings for WebGL
public class BuildSettings
{
    /*
    Quality: Balanced (not ultra to reduce file size)
    Resolution: 1280x720 default
    Vsync: Enabled for smooth gameplay
    WebGL: 2.0 (most compatible)
    Compression: Enabled to reduce size
    */
}
```

## Presentation Outline Template

```
GAME PRESENTATION STRUCTURE:

1. Title Slide (10 seconds)
   - Game name
   - Your name
   - Date

2. Gameplay Demo (5 minutes)
   - Play the game
   - Show core mechanic
   - Demonstrate win condition

3. Design (2 minutes)
   - What makes this game unique?
   - Design pillars
   - Target audience

4. Technical (2 minutes)
   - Key systems
   - Design patterns used
   - Challenges overcome

5. Playtesting (1 minute)
   - Number of testers
   - Average fun rating
   - Key feedback
   - Changes made

6. Reflection (2 minutes)
   - What went well?
   - What was hard?
   - What you learned
   - Future improvements

7. Questions & Discussion
```

## GDD Template Quick Reference

```
GAME DESIGN DOCUMENT

TITLE: [Game Name]

ELEVATOR PITCH:
[One sentence describing the game]

CORE GAMEPLAY LOOP:
1. [Player action 1]
2. [Game response 1]
3. [Player action 2]
4. [Game response 2]
5. [Repeat]

WIN CONDITION:
[How player wins]

LOSE CONDITION:
[How player loses]

MVP FEATURES (Must-Have):
- [Feature 1]
- [Feature 2]
- [Feature 3]

SHOULD-HAVE FEATURES:
- [Feature 4]
- [Feature 5]

NICE-TO-HAVE FEATURES:
- [Feature 6]
- [Feature 7]

TARGET AUDIENCE:
[Description of who plays this game]

TECHNICAL DETAILS:
Platform: [WebGL/Mobile/Desktop]
Art Style: [2D/3D, visual description]
Estimated Scope: [X weeks for MVP]
```
