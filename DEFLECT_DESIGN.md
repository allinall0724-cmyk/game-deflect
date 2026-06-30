# Deflect — Design Doc

**Platform target:** CrazyGames (web/HTML5) — built for fast load, instant play, "one more try" high-score loop.
**Engine:** Godot 4.x — **2D project** (fast web load, simple to build).
**Graphics:** Code-only (primitives — circles, lines, simple shapes, no imported assets), same approach as the wizard project.
**Scope philosophy:** Deliberately small and FINISHABLE. The finish line is defined in this doc up front (see "Definition of Done"). Resist adding features beyond Phase 1 until the core game is shipped and fun.

---

## 1. The Game in One Sentence
A ball bounces around the screen toward your core; you rotate a shield around the core to deflect the ball into enemies, racking up points — miss, and you lose a life.

## 2. Core Mechanic (the ONE thing)
- A **core** sits at the center of the screen.
- A **shield** (a short arc or paddle) orbits the core at a fixed radius. The player rotates it left/right around the core.
- A **ball** moves around the play area. When it comes toward the core, the player must position the shield to deflect it back outward.
- **Enemies** appear around the edges of the screen. Deflecting the ball into an enemy destroys it = points.
- If the ball reaches the core (player failed to deflect it) = lose a life.

That's the whole loop: rotate shield → deflect ball → hit enemies → score → don't let the ball reach the core.

## 3. Controls
- **Left / Right (or A/D, or mouse)**: rotate the shield around the core. (Pick whichever feels best during build — mouse-follow may be most intuitive on web.)
- That's it. One axis of input. Instantly understandable.

## 4. Scoring & Progression
- **Score** = enemies destroyed (each enemy worth points; faster/smaller enemies could be worth more — optional).
- **Difficulty ramps over time**: ball speeds up, more enemies appear, enemies may move. The longer you survive, the higher the score climbs.
- **Lives**: start with 3 (or 1 for pure arcade tension — decide during playtest). Lose one each time the ball hits the core. Game over at 0.
- **High score**: track and display the player's best score this session (persisted locally if easy).

## 5. Visual Style (code-only)
- Core: a circle in the center, maybe pulsing.
- Shield: a colored arc/paddle orbiting the core.
- Ball: a bright circle, maybe with a trail.
- Enemies: simple shapes (circles/triangles) around the edges.
- Background: flat dark color or simple gradient.
- Juice (important for arcade feel): screen shake on deflect, particle burst when an enemy is destroyed, color flash on taking a hit. This "game feel" polish is what makes simple arcade games addictive — worth real attention.

## 6. Definition of Done (Phase 1 — SHIP THIS)
The game is DONE for a first CrazyGames release when:
- [ ] A core, a rotating shield (player-controlled), and a bouncing ball exist on screen.
- [ ] The ball deflects correctly off the shield and reaches/damages the core when missed.
- [ ] Enemies spawn around the edges and are destroyed when the deflected ball hits them.
- [ ] Score increases on enemy kills and is displayed on screen.
- [ ] Lives system works; game ends at 0 lives with a "Game Over" + final score + restart button.
- [ ] Difficulty escalates over time (ball speed and/or enemy count).
- [ ] A start screen and a restart flow exist (click to play / play again).
- [ ] Basic juice: at least a hit particle and a screen-shake-or-flash on deflect/damage.

**When all boxes above are checked, the game is shippable. STOP adding features and ship it.** Everything below is explicitly post-launch.

## 7. Explicitly OUT of Scope for Phase 1 (resist these!)
- Multiple game modes
- Power-ups / upgrades
- Multiplayer / leaderboards beyond a local high score
- Multiple enemy types with complex behavior (start with one)
- Sound/music (nice later, not required to ship — though even simple sound adds a lot of juice)
- Levels/stages (it's an endless arcade game — no levels needed)
- Anything 3D
- Any feature not in the Definition of Done

## 8. CrazyGames Publishing Checklist (for later, once Phase 1 is done)
- Export from Godot as **Web/HTML5**, compressed (Brotli or Gzip — CrazyGames requires compressed builds).
- Integrate the CrazyGames SDK (community Godot 4 addon).
- Confirm it loads fast and plays in a browser.
- Prepare required metadata: title, description, thumbnail, instructions.
- Submit through the CrazyGames developer portal; passes their QA review.
- Must be PEGI 12 / 13+ audience appropriate (this game easily is).

## 9. The One Rule
This project exists to be FINISHED and SHIPPED. The lesson carried over from the wizard project: scope creep is the enemy. When in doubt, cut, don't add. A shipped simple game beats an unshipped ambitious one.
