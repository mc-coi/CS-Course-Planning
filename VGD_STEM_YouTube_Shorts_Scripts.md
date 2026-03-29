# Video Game Design — STEM YouTube Shorts Scripts
**34 scripts, one per lesson | Target length: under 60 seconds each**

Days are numbered continuously across units (Days 1–34), matching the STEM semester schedule. Same format as Coding I & II: hook → body → close, ~110–130 words per script.

---

## UNIT 1 — Unity Interface & Game Design Thinking

---

### Day 1: Game Design Vocabulary & Unity Panels

**[HOOK]**
You're about to open Unity for the first time. Before you click anything — here's what you're actually looking at.

**[BODY]**
The Unity editor has five main panels. The **Scene View** is your workspace — you build here. The **Game View** shows what the player will actually see. The **Hierarchy** lists every object in your scene. The **Inspector** shows the details of whatever you've selected. The **Project** panel holds all your files and assets.

Everything you build this semester happens inside these five windows. They work together — click something in the Hierarchy and its details appear in the Inspector.

**[CLOSE]**
You don't need to memorize every button today. Just learn where things live. That's the foundation everything else builds on.

---

### Day 2: Transform Component & Manipulation Tools

**[HOOK]**
Every single object in Unity has one thing in common: a Transform.

**[BODY]**
The **Transform component** controls three things — **position** (where it is), **rotation** (how it's turned), and **scale** (how big it is). These aren't just numbers you type in — you can drag objects directly in the Scene View using Unity's three manipulation tools: Move, Rotate, and Scale.

From code, `transform.position = new Vector3(x, y, z)` moves an object precisely. `transform.Rotate()` spins it. Understanding Transform is non-negotiable because you'll use it in virtually every script you write.

**[CLOSE]**
The Transform is the heartbeat of Unity. Once you're comfortable reading and changing it — in the Inspector and in code — you can place anything exactly where you want it.

---

### Day 3: Materials, Lighting & Scene Building

**[HOOK]**
A scene full of gray boxes isn't a game. Materials and lighting are what make it feel like a world.

**[BODY]**
A **material** defines how a surface looks — its color, shininess, and texture. Create one in the Project panel, set its color in the Inspector, and drag it onto any GameObject. Instant visual identity.

**Lighting** defines the mood. A **Directional Light** acts like the sun — it casts shadows from a consistent angle across the whole scene. Add a warm orange tint for sunset, cold blue for night. Adjust intensity and angle until it feels right.

**[CLOSE]**
Good visuals communicate before the player even touches a button. Color and light aren't decoration — they're design. Spend time here and your scenes will immediately feel more intentional.

---

### Day 4: Creating Scripts & MonoBehaviour Basics

**[HOOK]**
A scene with objects that just sit there isn't a game. Scripts are what give things life.

**[BODY]**
In Unity, behavior comes from **C# scripts**. Create one, attach it to a GameObject, and it runs automatically. Every Unity script starts with two built-in methods: **`Start()`** runs once when the object appears, and **`Update()`** runs every single frame — typically 60 times per second.

`Debug.Log("message")` prints to the Console — your best friend for checking that code is running and that variables have the right values.

**[CLOSE]**
This is the moment the course shifts from clicking to coding. Everything you learned about the Unity interface was setup. Scripts are where the actual game design begins.

---

## UNIT 2 — C# Scripting Fundamentals

---

### Day 5: Variables & Data Types

**[HOOK]**
C# is a strictly typed language. That means before you store anything, you have to declare what type of thing it is.

**[BODY]**
Common types in Unity: **`int`** for whole numbers like score or lives. **`float`** for decimals like speed and jump force — most Unity math uses floats. **`string`** for text. **`bool`** for true/false flags like `isGrounded` or `isDead`.

Here's the key Unity distinction: **`public`** variables show up in the Inspector, where you can tweak them without touching code. **`private`** variables stay hidden. Use public for anything you want to tune during playtesting.

**[CLOSE]**
The ability to adjust public variables in the Inspector while the game runs is one of Unity's most powerful features. Set speed to 5, test it, change it to 8 without recompiling. Design in real time.

---

### Day 6: Methods & Functions

**[HOOK]**
Copy-pasting the same code in ten places is a nightmare to maintain. Methods fix that.

**[BODY]**
A **method** is a named, reusable block of code. Define it once, call it whenever you need it. In C#: `void DoSomething() { }` for methods that don't return a value, or `int CalculateScore() { return score; }` for ones that do.

**Parameters** let you pass information in: `void TakeDamage(int amount)` can be called with any damage value. The method handles the logic — you just pass in the number.

**[CLOSE]**
Well-named methods make your scripts readable. `Jump()`, `TakeDamage()`, `SpawnEnemy()` — you can understand what a script does just by scanning the method names. Write methods that read like descriptions of what they do.

---

### Day 7: Conditionals & Input Detection

**[HOOK]**
Games are all about responding to what the player does. That means detecting input and making decisions.

**[BODY]**
`Input.GetKeyDown(KeyCode.Space)` returns `true` the exact frame the space bar is pressed — perfect for jumps and one-time actions. `Input.GetKey()` returns `true` every frame it's held — better for continuous movement.

Combine with `if/else` to make decisions: if the player presses space *and* they're on the ground, jump. If health drops to zero, trigger the death sequence. Conditional logic is how your game world reacts to everything.

**[CLOSE]**
Input detection plus conditionals is the foundation of player control. Almost every game mechanic you'll ever build starts with: "when the player does X, if condition Y is true, do Z."

---

### Day 8: Transform Manipulation with Vectors & Time.deltaTime

**[HOOK]**
Moving an object looks simple. Making it move *smoothly* at the same speed on every computer requires one extra trick.

**[BODY]**
**`Vector3`** represents a point or direction in 3D space — `new Vector3(x, y, z)`. Add it to `transform.position` to move an object. The problem: `Update()` runs at different speeds on different machines, so movement tied directly to frames runs faster on better hardware.

The fix: multiply by **`Time.deltaTime`** — the time in seconds since the last frame. `speed * Time.deltaTime` means "move this many units per *second*" regardless of frame rate. Every movement calculation in Unity should include it.

**[CLOSE]**
Frame-rate-independent movement is non-negotiable for a game that runs consistently everywhere. One multiplication. Learn it now, apply it everywhere.

---

## UNIT 3 — Physics & Collision

---

### Day 9: Rigidbody & Gravity

**[HOOK]**
What makes objects fall, bounce, and feel like they have weight? The Rigidbody component.

**[BODY]**
Add a **Rigidbody** to any GameObject and Unity's physics engine takes over — gravity pulls it down, forces push it around, and collisions affect its movement realistically. Key settings: **mass** affects how forces change velocity, **drag** slows it down like air resistance.

Physics calculations should happen in **`FixedUpdate()`**, not `Update()`. FixedUpdate runs at a fixed time step (50 times per second by default), keeping physics consistent regardless of frame rate.

**[CLOSE]**
The moment you add a Rigidbody and hit Play, your objects come alive in a way that pure Transform manipulation never achieves. Gravity, momentum, weight — it all just works. Now you control it.

---

### Day 10: Colliders & Collision Detection

**[HOOK]**
Physics without collision detection is just objects falling through each other.

**[BODY]**
**Colliders** define the physical boundary of an object — Box, Sphere, and Capsule colliders cover most cases. When two colliders touch, Unity fires a callback method: **`OnCollisionEnter()`** triggers the moment contact begins, `OnCollisionStay()` fires every frame contact continues, `OnCollisionExit()` fires when they separate.

**Tags** let you identify *what* you collided with. `CompareTag("Enemy")` inside `OnCollisionEnter()` checks if what you hit was an enemy — then you can respond accordingly.

**[CLOSE]**
Collision detection is how your game knows a bullet hit an enemy, a player touched a coin, or a character landed on the ground. Every interactive mechanic you build passes through these callbacks.

---

### Day 11: Triggers & Object Management

**[HOOK]**
Not every area in a game needs to physically block movement. Some just need to detect when something enters.

**[BODY]**
Check **Is Trigger** on a collider and it becomes a zone — objects pass through it, but it still fires `OnTriggerEnter()` when anything enters. Perfect for pickups, damage zones, checkpoints, and portals.

`Instantiate()` creates a new copy of a prefab at runtime — spawn an enemy, create a bullet, drop a pickup. `Destroy()` removes it. `SetActive(false)` hides it without deleting — useful for object pooling, which is far more efficient than constant create/destroy cycles.

**[CLOSE]**
Triggers and object management are the mechanics behind nearly every gameplay system: collectibles, hazards, spawn systems, checkpoints. These two tools show up in every game you'll ever build.

---

### Day 12: Physics-Based Movement & Ground Detection

**[HOOK]**
A jump that works in all situations is harder to build than it sounds.

**[BODY]**
The classic mistake: let the player jump infinitely by pressing space. The fix: **ground detection** using `Physics.Raycast()`, which shoots an invisible line downward from the player and returns true if it hits something. Only allow jumping when that raycast hits the ground.

Apply jump force with `rigidbody.AddForce(Vector3.up * jumpForce, ForceMode.Impulse)` — an instant burst of force upward. Gravity does the rest. Combine grounded detection with force-based jumping and your character's movement feels solid and predictable.

**[CLOSE]**
Reliable jump mechanics make or break a platformer. Get this pattern right once and you'll reuse it in every project. The raycast ground check is the piece most beginners skip — and the reason their character floats.

---

## UNIT 4 — Player Controls & Input

---

### Day 13: Input.GetAxis() & Smooth Input

**[HOOK]**
There's a difference between input that snaps and input that *feels good*. GetAxis is why.

**[BODY]**
`Input.GetAxisRaw("Horizontal")` returns exactly -1, 0, or 1 — instant and digital. `Input.GetAxis("Horizontal")` returns a float that ramps smoothly from 0 to 1 as you hold the key — it accelerates and decelerates. For most movement, the smooth version feels much more natural.

Multiply the axis value by your speed, multiply by `Time.deltaTime`, and you have frame-rate-independent movement in any direction. Four lines of code, polished feel.

**[CLOSE]**
The difference between `GetAxis` and `GetAxisRaw` is subtle but noticeable. Try both in your game and feel it. That tactile responsiveness — the "game feel" — starts right here.

---

### Day 14: Camera Follow & LateUpdate()

**[HOOK]**
A camera that jerks around or clips through walls ruins immersion. Here's how to make it smooth.

**[BODY]**
Camera logic belongs in **`LateUpdate()`** — it runs after all `Update()` methods, so the player has already moved before the camera calculates its new position. This prevents one-frame-off jitter.

**`Vector3.Lerp()`** smoothly interpolates between the camera's current position and the target position each frame — the result is a camera that glides rather than snaps. Maintain an **offset** vector (usually behind and above the player) so the camera never sits inside the character.

**[CLOSE]**
A well-tuned camera follow is invisible — players don't notice it because it just feels right. A bad one is immediately obvious. LateUpdate and Lerp are the two tools that get you there.

---

### Day 15: Game Feel, Juice & Feedback

**[HOOK]**
Two games can have identical mechanics, but one feels incredible and one feels flat. That's "juice."

**[BODY]**
**Juice** is all the visual, audio, and physical feedback that makes actions feel satisfying — screen shake when you take damage, a particle burst when you collect a coin, a punchy sound on impact, a slight squash when you land. None of these change the gameplay. All of them make it feel dramatically better.

**Screen shake**: briefly offset the camera position by a random amount. **Particles**: `Instantiate` an effect prefab at the point of impact. **Audio**: `AudioSource.PlayClipAtPoint()` in one line.

**[CLOSE]**
Juice is often the last thing added and the first thing players notice. A game without feedback feels like clicking on nothing. Add the feedback, and everything feels like it *matters*.

---

### Day 16: State Machines & Code Organization

**[HOOK]**
As your player gets more abilities, if-statements start turning into spaghetti. State machines clean that up.

**[BODY]**
A **state machine** defines a set of states — Idle, Running, Jumping, Falling, Attacking — and rules for transitioning between them. Use a C# **`enum`** to list the states, a variable to track the current one, and a `switch` statement to run the right logic for each state.

The result: clean, readable code where each state handles its own behavior independently. No more nested if-statements checking five conditions at once.

**[CLOSE]**
State machines scale. A simple player might have 4 states. A complex enemy AI might have 10. The structure is the same — and because it's modular, adding a new state doesn't break the ones that already work.

---

## UNIT 5 — Game Design Principles & UI

---

### Day 17: MDA Framework & The Game Loop

**[HOOK]**
Every game ever made follows the same pattern. Once you see it, you can't unsee it.

**[BODY]**
The **MDA framework**: **Mechanics** are the rules and systems — jump, collect, shoot. **Dynamics** are what happens when mechanics interact — increasing difficulty, combo chains, emergent strategy. **Aesthetics** are the emotions those dynamics create — excitement, tension, satisfaction, discovery.

Good game design works backward from the emotion you want players to feel. Want them to feel tense? Design mechanics that create scarcity and time pressure. Want them to feel powerful? Design mechanics that let them grow and dominate.

**[CLOSE]**
MDA is a lens, not a formula. Use it to analyze games you love and reverse-engineer why they work. Then apply it to your own designs before you write a single line of code.

---

### Day 18: Level Design & Grayboxing

**[HOOK]**
The best games teach you to play them without ever showing you a tutorial screen.

**[BODY]**
**Grayboxing** means building your level with simple shapes — gray cubes and ramps — before adding any art. It forces you to focus on *gameplay* instead of visuals, and it's fast to modify. Test whether the platforming works, whether the pacing feels right, whether the player instinctively knows where to go.

**Onboarding through design**: place the first challenge in a safe area where failure has no cost. Introduce each mechanic once in a forgiving context before making it dangerous.

**[CLOSE]**
Polish can't save a level with bad design. Graybox first, feel the gameplay, iterate until it's fun. Then — and only then — add the art. This is how professional level designers work.

---

### Day 19: Canvas & UI Elements

**[HOOK]**
The score counter, health bar, and pause menu — all of that lives on the Canvas.

**[BODY]**
Unity's **Canvas** is a special container for all UI elements. Everything inside uses a **Rect Transform** instead of a regular Transform, with anchors that define how UI scales across different screen sizes. Set anchors to corners and your UI stays in place on any resolution.

**TextMeshPro** renders crisp, scalable text. **Buttons** call C# methods when clicked — hook them up in the Inspector. **Sliders** are perfect for health bars and volume controls. **Layout Groups** automatically arrange lists of UI elements.

**[CLOSE]**
UI is what communicates the game state to the player. A confusing UI breaks immersion even when gameplay is solid. Keep it clean, keep it readable, and make sure it works on every screen size.

---

### Day 20: Menus, Scene Management & Persistence

**[HOOK]**
A complete game isn't just one scene. It's a start menu, a level, a game over screen — all connected.

**[BODY]**
`SceneManager.LoadScene("GameScene")` transitions to a different scene — hook it to a button and you have a functional main menu. `DontDestroyOnLoad()` keeps a GameObject alive across scene transitions — essential for a GameManager or background music that shouldn't restart.

**PlayerPrefs** stores small persistent values — high scores, volume settings, completed levels — that survive between sessions. `PlayerPrefs.SetInt("HighScore", score)` saves it. `PlayerPrefs.GetInt("HighScore")` reads it back.

**[CLOSE]**
These three tools — scene loading, persistence between scenes, and data that survives quitting — are what transform a game mechanic demo into an actual game. They're the connective tissue of your whole project.

---

## UNIT 6 — 2D Game Development

---

### Day 21: Sprite Renderer & Tilemaps

**[HOOK]**
2D games need a completely different toolkit than 3D. Here's where you start.

**[BODY]**
A **Sprite Renderer** displays a 2D image on a GameObject. Import a PNG, set it as a Sprite in the import settings, drag it onto an object — done. **Sorting Order** controls which sprites appear in front: higher numbers render on top.

**Tilemaps** let you paint levels like you're using a stamp — drop tiles from a palette to build platforms, walls, and floors in seconds. No manual placement of hundreds of individual GameObjects. One tilemap, infinite level layouts.

**[CLOSE]**
The Tilemap workflow is genuinely fast once you know it. You can rough out an entire level in minutes. Combined with physics layers and a 2D camera, you've got the foundation for any platformer, top-down game, or puzzle game.

---

### Day 22: 2D Movement with Rigidbody2D

**[HOOK]**
2D movement uses the same physics concepts as 3D — but with a few important differences.

**[BODY]**
**Rigidbody2D** handles gravity and physics for 2D objects. Control horizontal movement by directly setting velocity: `rb.velocity = new Vector2(moveInput * speed, rb.velocity.y)` — this keeps the existing vertical velocity (gravity) while overriding horizontal.

Ground detection in 2D uses `Physics2D.Raycast()` pointed downward. Flip the sprite to face the movement direction by scaling the x-axis to -1: `transform.localScale = new Vector3(-1, 1, 1)`.

**[CLOSE]**
2D platformer movement is one of the most-built things in indie game development. Getting it right — tight controls, reliable grounding, proper sprite flipping — is a milestone. Once you have it working, you have the core of an entire game genre.

---

### Day 23: Animation & the Animator

**[HOOK]**
A character that slides stiffly across the screen looks wrong. Animation is the fix.

**[BODY]**
Unity's **Animator** manages animation states — Idle, Run, Jump, Fall — and the transitions between them. Create **Animation Clips** from sprite sequences, add them to the Animator, then define **Parameters** (booleans, floats, triggers) that control which animation plays.

From code: `animator.SetBool("isRunning", true)` switches to the run animation when movement input is detected. `animator.SetTrigger("Jump")` fires the jump animation once. The Animator handles the transitions smoothly.

**[CLOSE]**
Animation is the layer between logic and feel. Your code makes the character move — the animator makes it look like *running*. Get the transitions right and characters stop feeling like physics objects and start feeling like characters.

---

### Day 24: Prefabs & Complete Systems

**[HOOK]**
What if you need 50 enemies? You don't build 50 enemies. You build one — and prefab it.

**[BODY]**
A **Prefab** is a reusable template. Build your enemy once with all its components — sprite, collider, AI script, health — drag it to the Project panel, and it becomes a prefab asset. Now `Instantiate(enemyPrefab, spawnPoint, Quaternion.identity)` spawns a perfect copy anywhere at runtime.

Change the prefab once and every instance in your game updates automatically. This is how large games manage hundreds of similar objects without losing their minds.

**[CLOSE]**
Prefabs are fundamental to Unity workflow. Bullets, enemies, coins, effects, UI popups — anything that appears more than once belongs in a prefab. Build the system once, spawn it everywhere.

---

## UNIT 7 — Game Systems & Enemies

---

### Day 25: Health Components & Modular Design

**[HOOK]**
Should your player's health system be different from the enemy's? With modular design, it doesn't have to be.

**[BODY]**
A **Health Component** is a script you attach to *any* entity — player, enemy, boss, destructible object — that tracks HP and handles damage. The public method `TakeDamage(int amount)` reduces health; when it hits zero, it fires the death logic.

Because it's a separate, reusable component, the logic lives in one place. Fix a bug in `HealthComponent.cs` and it's fixed for every entity that uses it. Add invulnerability frames once — every entity gets them.

**[CLOSE]**
Modular design is the principle that separates beginner projects from scalable ones. Instead of writing health logic into your player script, your enemy script, and your boss script separately — write it once, attach it everywhere.

---

### Day 26: Enemy AI State Machine

**[HOOK]**
A good enemy doesn't just run at you. It watches, chases, and attacks — based on your position.

**[BODY]**
Enemy AI uses a state machine: **Patrol** — moving back and forth along a path when the player is far away. **Chase** — switching to follow the player when they enter detection range. **Attack** — stopping and striking when the player is within attack range.

`Vector3.Distance(transform.position, player.position)` measures how close the player is. Each frame, check the distance and transition between states accordingly. Add cooldown timers between attacks and the AI feels deliberate instead of spammy.

**[CLOSE]**
This three-state AI pattern — patrol, chase, attack — is the backbone of enemy behavior in countless games. Master it once and you can build increasingly complex AI on top of the same foundation.

---

### Day 27: GameManager Singleton & Scoring

**[HOOK]**
Your score, your lives, your game state — these things need to be accessible from everywhere. That's the Singleton pattern.

**[BODY]**
A **Singleton** means only one instance of a class can exist. In Unity: `public static GameManager Instance;` — set it in `Awake()` and add `DontDestroyOnLoad()` so it persists across scenes. Now any other script can call `GameManager.Instance.AddScore(10)` from anywhere without finding references.

The GameManager centralizes everything global: current score, high score, lives remaining, current game state (Playing, Paused, GameOver). One source of truth for the whole game.

**[CLOSE]**
Without a GameManager, you end up passing references everywhere and data gets out of sync. With one, every system talks to a single source of truth. It's one of the most commonly used design patterns in Unity for good reason.

---

### Day 28: Game State & Complete Systems Integration

**[HOOK]**
A game without a proper win condition, lose condition, and flow isn't a game — it's a tech demo.

**[BODY]**
Use an `enum` to define your **game states**: `Menu`, `Playing`, `Paused`, `Win`, `GameOver`. The GameManager holds the current state and transitions between them. `Time.timeScale = 0` pauses all physics and animations — pause the game without stopping the UI.

**Win and lose conditions** check specific gameplay events: health reached zero, all enemies defeated, timer expired, goal reached. When the condition is met, trigger the state transition. Each state loads the appropriate scene or activates the right UI panel.

**[CLOSE]**
Game state management is the skeleton your entire game hangs on. Every system — enemies, player, scoring, UI — responds to the current state. Get this architecture right and adding new features becomes dramatically easier.

---

## UNIT 8 — Capstone Project

---

### Day 29: Game Design Document & Scope

**[HOOK]**
Before you build your game, you're going to write it down. All of it.

**[BODY]**
A **Game Design Document** defines your game before a single line of code is written: the **elevator pitch** (one sentence), the **core loop** (the repeating cycle of action and reward), the complete **feature list**, and your **MVP** — the minimum viable product that makes the game actually playable.

Scope management is the hardest part. Every feature sounds great in planning. The GDD forces you to decide what stays and what gets cut before you spend time building things that don't fit.

**[CLOSE]**
Game jam veterans have a saying: cut half your features and polish the rest. The GDD is where you learn to be ruthless about scope. A small game that's finished and fun beats a big game that never ships.

---

### Day 30: Prototyping the Core Mechanic

**[HOOK]**
The most important question in game development: is this actually fun?

**[BODY]**
A **prototype** tests the core mechanic with the minimum possible code. Gray boxes for art, placeholder sounds, no menus — just the one mechanic you're betting the whole game on. Build it in a day, play it, and find out if the core idea feels good.

**Fail fast** is the goal. If the mechanic isn't satisfying in its simplest form, adding polish won't save it. If it *is* fun in five minutes of grayboxed play, that's your green light to build.

**[CLOSE]**
Professional studios prototype before committing to full production. You're doing the same thing in miniature. Test the idea before investing the time. If it's fun gray, it'll be great with art.

---

### Day 31: Systems Integration

**[HOOK]**
Individual systems that work in isolation don't always work together. Integration is where you find out.

**[BODY]**
**Integration** means connecting your player, enemies, health system, UI, scoring, and audio so they all communicate properly. The player takes damage → the health component updates → the UI reflects the new health → if zero, the GameManager transitions to GameOver → the GameOver screen appears.

That chain needs to work without any link breaking. Use `GetComponent<>()` to access other scripts on the same object. Pass references through the Inspector or find them with `FindObjectOfType<>()`. Test each connection as you make it.

**[CLOSE]**
Integration is where hidden assumptions get exposed. Two systems that looked compatible on paper will sometimes clash when actually connected. Build the connections one at a time, test each, and fix before moving to the next.

---

### Day 32: Content Creation & Polish

**[HOOK]**
Your game works. Now make it look and sound like it means something.

**[BODY]**
Replace graybox geometry with final sprites or models. Add **particle effects** at key moments — impact, death, collection. Add **sound effects** using `AudioSource.PlayClipAtPoint()`. Tune **animations** so transitions feel snappy and responsive. Adjust **colors and lighting** to establish mood and atmosphere.

Polish isn't cosmetic — it's communication. Every particle, every sound, every animation tells the player something happened. Without them, the game works but nothing feels real.

**[CLOSE]**
Content and polish are where the game goes from something you built to something you'd show someone. Budget real time for this phase. Great polish on a solid foundation is what makes people say "this feels like a real game."

---

### Day 33: Playtesting & Feedback

**[HOOK]**
You've been testing your own game for weeks. That makes you the worst possible tester.

**[BODY]**
**Playtesting** means watching someone else play your game for the first time — without explaining anything. Where do they get stuck? What do they find confusing? What do they enjoy most? What do they try to do that your game won't let them?

You're not defending your design. You're observing. Take notes. Track deaths, confusion points, and moments of delight. Then iterate — make the change, test again, see if it's better.

**[CLOSE]**
Fresh eyes see things you've been blind to for weeks. Every successful game went through dozens of playtesting sessions. One round of honest feedback will improve your game more than a week of solo polishing. Watch people play. Stay quiet. Listen.

---

### Days 34–36: Final Polish, Build & Presentation

**[HOOK]**
This is what everything has been building toward. Time to ship.

**[BODY]**
Final polish: fix the last bugs, balance the difficulty, make sure the win and lose conditions are satisfying. Then **build**: configure Build Settings, add all scenes in the right order, and export — WebGL for the browser, standalone for desktop.

Your **presentation** follows the same structure as any professional demo: what problem does your game solve (what kind of fun does it create?), a live play-through showing the core loop and at least one interesting system, and one thing you'd do differently if you started over.

**[CLOSE]**
You designed, scoped, prototyped, built, integrated, polished, and shipped a game. That's not a school project — that's the same process every professional game developer follows, just compressed. Be proud of what you made. This is a real thing you created from nothing.

---

*End of Scripts — 34 total (covering Days 1–36)*
*Video Game Design STEM | Full Semester*
