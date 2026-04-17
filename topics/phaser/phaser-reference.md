# Phaser + TypeScript Reference Guide

A practical cheat sheet covering everything you need to get started building games with Phaser and TypeScript.

---

## Table of Contents

1. [Project Setup](#1-project-setup)
2. [Game Structure](#2-game-structure)
3. [The Game Loop](#3-the-game-loop)
4. [Animated Sprites](#4-animated-sprites)
5. [Keyboard Input](#5-keyboard-input)
6. [Physics & Collision Detection](#6-physics--collision-detection)
7. [Camera](#7-camera)
8. [Sound](#8-sound)
9. [Essentials Every Beginner Should Know](#9-essentials-every-beginner-should-know)

---

## 1. Project Setup

```bash
mkdir my-game && cd my-game
npm init -y
npm install phaser
npm install --save-dev typescript vite
```

**`tsconfig.json`**
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "ES6",
    "moduleResolution": "bundler",
    "strict": true,
    "noEmit": true
  },
  "include": ["src"]
}
```

**`index.html`**
```html
<!DOCTYPE html>
<html>
  <head><meta charset="utf-8" /><title>My Game</title></head>
  <body>
    <script type="module" src="/src/main.ts"></script>
  </body>
</html>
```

**`package.json` scripts**
```json
"scripts": {
  "dev": "vite",
  "build": "vite build"
}
```

> ⚠️ **Import gotcha:** Use `import * as Phaser from "phaser"` — not `import Phaser from "phaser"`. Vite cannot resolve Phaser's default export and will throw a runtime error.

---

## 2. Game Structure

### Config & Bootstrap

```typescript
import * as Phaser from "phaser";

const config: Phaser.Types.Core.GameConfig = {
  type: Phaser.AUTO,        // WebGL if available, else Canvas
  width: 800,
  height: 600,
  backgroundColor: "#1a1a2e",
  physics: {
    default: "arcade",
    arcade: { gravity: { y: 300 }, debug: false }
  },
  scene: [BootScene, GameScene, UIScene]  // loaded in order
};

new Phaser.Game(config);
```

### Scene Skeleton

Every scene has three lifecycle methods:

```typescript
class GameScene extends Phaser.Scene {
  constructor() {
    super("GameScene");  // string key used to reference this scene
  }

  preload() {
    // Runs once — load all assets here before anything renders
    this.load.image("bg", "assets/bg.png");
    this.load.spritesheet("player", "assets/player.png", {
      frameWidth: 48,
      frameHeight: 48
    });
    this.load.audio("jump", "assets/jump.mp3");
  }

  create() {
    // Runs once after preload — build the scene: add sprites, set up physics, etc.
    this.add.image(400, 300, "bg");
  }

  update(time: number, delta: number) {
    // Runs every frame (~60fps) — all game logic goes here
  }
}
```

> **Scenes are the core unit.** You can run multiple scenes simultaneously — useful for layering a HUD on top of your game world (`this.scene.launch("UIScene")`).

---

## 3. The Game Loop

`update()` is called every frame by Phaser automatically. You never call it yourself.

```typescript
update(time: number, delta: number) {
  // time  — total ms elapsed since the game started
  // delta — ms elapsed since the last frame (~16ms at 60fps)

  // Always scale movement by delta so speed is frame-rate independent
  this.player.x += 200 * (delta / 1000);  // moves 200px per second regardless of FPS
}
```

### Scheduling Events

Never use `setTimeout` or `setInterval` — use Phaser's built-in time events so they pause correctly with the scene.

```typescript
// Run once after a delay
this.time.delayedCall(2000, () => {
  console.log("2 seconds later");
});

// Repeat on an interval
this.time.addEvent({
  delay: 1000,
  callback: this.spawnEnemy,
  callbackScope: this,
  loop: true
});

// Cancel an event
const event = this.time.addEvent({ ... });
event.remove();
```

---

## 4. Animated Sprites

### Step 1 — Load a spritesheet in `preload()`

```typescript
this.load.spritesheet("player", "assets/player.png", {
  frameWidth: 48,
  frameHeight: 48
});
```

### Step 2 — Define animations in `create()`

Animations are **global** — define them once and any sprite using the same key can play them.

```typescript
this.anims.create({
  key: "walk",
  frames: this.anims.generateFrameNumbers("player", { start: 0, end: 7 }),
  frameRate: 10,
  repeat: -1       // -1 = loop forever
});

this.anims.create({
  key: "idle",
  frames: this.anims.generateFrameNumbers("player", { start: 8, end: 9 }),
  frameRate: 4,
  repeat: -1
});

this.anims.create({
  key: "attack",
  frames: this.anims.generateFrameNumbers("player", { start: 10, end: 14 }),
  frameRate: 12,
  repeat: 0        // 0 = play once
});
```

### Step 3 — Create a sprite and play animations

```typescript
// Static sprite (no physics)
const sprite = this.add.sprite(100, 100, "player");

// Physics sprite (can collide, has velocity)
const player = this.physics.add.sprite(100, 100, "player");

// Play animations
player.play("walk");
player.play("idle");

// Play once then stop
player.play({ key: "attack", repeat: 0 });

// Listen for animation completion
player.on("animationcomplete", (anim: Phaser.Animations.Animation) => {
  if (anim.key === "attack") {
    player.play("idle");
  }
});

// Flip sprite horizontally (e.g. for left/right movement)
player.setFlipX(true);
```

---

## 5. Keyboard Input

### Arrow Keys (quickest option)

```typescript
// Declare in your class
private cursors!: Phaser.Types.Input.Keyboard.CursorKeys;

// In create():
this.cursors = this.input.keyboard!.createCursorKeys();

// In update():
if (this.cursors.left.isDown) {
  this.player.setVelocityX(-200);
  this.player.setFlipX(true);
  this.player.play("walk", true);  // true = don't restart if already playing
} else if (this.cursors.right.isDown) {
  this.player.setVelocityX(200);
  this.player.setFlipX(false);
  this.player.play("walk", true);
} else {
  this.player.setVelocityX(0);
  this.player.play("idle", true);
}

// Jump — check body.blocked.down to prevent double-jumping
if (this.cursors.up.isDown && this.player.body!.blocked.down) {
  this.player.setVelocityY(-400);
}
```

### WASD or Custom Keys

```typescript
// Declare in your class
private wasd!: {
  up: Phaser.Input.Keyboard.Key;
  left: Phaser.Input.Keyboard.Key;
  down: Phaser.Input.Keyboard.Key;
  right: Phaser.Input.Keyboard.Key;
};

// In create():
const kb = this.input.keyboard!;
this.wasd = {
  up:    kb.addKey(Phaser.Input.Keyboard.KeyCodes.W),
  left:  kb.addKey(Phaser.Input.Keyboard.KeyCodes.A),
  down:  kb.addKey(Phaser.Input.Keyboard.KeyCodes.S),
  right: kb.addKey(Phaser.Input.Keyboard.KeyCodes.D),
};

// In update():
if (this.wasd.left.isDown) { ... }
```

### One-Shot Key Events (fires once per press, not every frame)

```typescript
this.input.keyboard!.on("keydown-SPACE", () => {
  this.player.play("attack");
});

this.input.keyboard!.on("keydown-ESC", () => {
  this.scene.pause();
});
```

---

## 6. Physics & Collision Detection

Phaser has three physics systems. **Arcade** is the right choice to start with — it's fast and simple. Matter.js is available for complex simulations.

### Setting Up Arcade Physics

```typescript
// In game config:
physics: {
  default: "arcade",
  arcade: {
    gravity: { y: 300 },  // global downward gravity
    debug: false           // set true to see hitboxes during development
  }
}
```

### Physics Bodies

```typescript
// Physics sprite
const player = this.physics.add.sprite(100, 100, "player");

// Physics properties
player.setVelocity(100, 0);          // set x and y velocity at once
player.setVelocityX(200);            // horizontal only
player.setVelocityY(-400);           // vertical only (negative = up)
player.setGravityY(200);             // extra gravity on this specific sprite
player.setCollideWorldBounds(true);  // stop at the edges of the world
player.setBounce(0.3);               // bounciness (0 = none, 1 = full)
player.setDragX(500);                // horizontal friction / deceleration

// Resize the hitbox (useful when sprite art has padding)
player.setBodySize(32, 40);          // width, height
player.setOffset(8, 8);             // offset from sprite origin
```

### Static Groups (immovable platforms, walls, floors)

```typescript
// Create a static group
const platforms = this.physics.add.staticGroup();

// Add sprites to it
platforms.create(400, 568, "platform");
platforms.create(200, 400, "platform");

// Or create a simple rectangle platform without an image
const floor = this.add.rectangle(400, 580, 800, 32, 0x666666);
this.physics.add.existing(floor, true);  // true = static body
```

### Colliders (objects bounce off each other)

```typescript
// Player stands on platforms
this.physics.add.collider(player, platforms);

// Two dynamic objects collide
this.physics.add.collider(player, enemies);

// Collider with a callback (fires when they collide)
this.physics.add.collider(
  player,
  enemies,
  this.handleEnemyHit,   // callback
  undefined,             // process callback (optional filter)
  this                   // callback context
);

private handleEnemyHit(
  player: Phaser.Types.Physics.Arcade.GameObjectWithBody,
  enemy: Phaser.Types.Physics.Arcade.GameObjectWithBody
) {
  // handle damage, death, etc.
}
```

### Overlaps (detect contact without physics response)

```typescript
// Collect coins on touch — no bounce, just a callback
this.physics.add.overlap(
  player,
  coins,
  this.collectCoin,
  undefined,
  this
);

private collectCoin(
  player: Phaser.Types.Physics.Arcade.GameObjectWithBody,
  coin: Phaser.Types.Physics.Arcade.GameObjectWithBody
) {
  (coin as Phaser.Physics.Arcade.Sprite).destroy();
  this.score += 10;
}
```

### Groups (manage many objects of the same type)

```typescript
// Dynamic group (e.g. enemies, bullets)
const bullets = this.physics.add.group();

// Spawn a new bullet
const bullet = bullets.create(x, y, "bullet") as Phaser.Physics.Arcade.Sprite;
bullet.setVelocityX(400);

// Destroy bullets that leave the screen
bullets.getChildren().forEach((b) => {
  const bullet = b as Phaser.Physics.Arcade.Sprite;
  if (bullet.x > 900) bullet.destroy();
});

// Collide entire group with platforms in one line
this.physics.add.collider(bullets, platforms, (bullet) => {
  (bullet as Phaser.Physics.Arcade.Sprite).destroy();
});
```

---

## 7. Camera

```typescript
// Follow the player smoothly
this.cameras.main.startFollow(player);

// Follow with lerp (0 = instant, 1 = no lag, 0.1 = very smooth)
this.cameras.main.startFollow(player, true, 0.1, 0.1);

// Set world bounds larger than the screen (for scrolling levels)
this.physics.world.setBounds(0, 0, 3200, 600);
this.cameras.main.setBounds(0, 0, 3200, 600);

// Zoom in or out
this.cameras.main.setZoom(1.5);   // 1.5x zoom in
this.cameras.main.setZoom(0.75);  // zoom out

// Shake (great for hit feedback)
this.cameras.main.shake(200, 0.01);  // duration ms, intensity

// Fade in/out (useful for scene transitions)
this.cameras.main.fadeIn(500);
this.cameras.main.fadeOut(500, 0, 0, 0);  // duration, r, g, b

// Flash (great for taking damage)
this.cameras.main.flash(300, 255, 0, 0);  // duration, r, g, b

// Pan to a point
this.cameras.main.pan(500, 300, 1000, "Linear");

// Stop following
this.cameras.main.stopFollow();
```

> **Tip:** Always set both `this.physics.world.setBounds()` and `this.cameras.main.setBounds()` when building a scrolling level — one controls physics, the other controls what the camera can see.

---

## 8. Sound

### Loading Audio

```typescript
// In preload():
this.load.audio("jump", "assets/jump.mp3");
this.load.audio("music", ["assets/music.ogg", "assets/music.mp3"]);  // fallback formats
```

### Playing Sound Effects

```typescript
// Play once
this.sound.play("jump");

// Play with options
this.sound.play("jump", {
  volume: 0.5,    // 0 to 1
  rate: 1.2,      // playback speed (1 = normal)
  detune: 100,    // pitch in cents
  delay: 0.3,     // delay before playing (seconds)
});
```

### Background Music

```typescript
// In create():
const music = this.sound.add("music", {
  loop: true,
  volume: 0.3
});
music.play();

// Control playback
music.pause();
music.resume();
music.stop();

// Fade volume
this.tweens.add({
  targets: music,
  volume: 0,
  duration: 2000,
  onComplete: () => music.stop()
});
```

### Global Sound Control

```typescript
// Mute/unmute everything
this.sound.mute = true;
this.sound.mute = false;

// Set global volume
this.sound.volume = 0.5;
```

> **Browser autoplay policy:** Browsers block audio until the user interacts with the page. Always trigger your first sound or music after a click/keypress — for example on a "Press any key to start" screen.

---

## 9. Essentials Every Beginner Should Know

### Adding Things to the Scene

```typescript
this.add.image(x, y, "key");                          // static image, no physics
this.add.sprite(x, y, "key");                         // animatable sprite, no physics
this.add.text(x, y, "Hello!", { fontSize: "16px", color: "#ffffff" });
this.add.rectangle(x, y, width, height, 0xff0000);    // solid color rectangle
this.add.circle(x, y, radius, 0x00ff00);              // solid color circle
```

### Coordinates

Phaser uses **top-left origin**: `(0, 0)` is the top-left corner. X increases right, Y increases **down**.

By default, sprites are positioned by their **center**. Images are positioned by their **top-left corner** unless you change the origin:

```typescript
sprite.setOrigin(0.5, 0.5);  // center (default for sprites)
sprite.setOrigin(0, 0);      // top-left
```

### Depth / Z-ordering

Objects render in the order they were created. Use `setDepth()` to control layering:

```typescript
background.setDepth(0);
player.setDepth(1);
uiText.setDepth(10);
```

### Switching Scenes

```typescript
this.scene.start("GameScene");          // stop current, start new
this.scene.start("GameScene", { level: 2 });  // pass data to the next scene
this.scene.launch("UIScene");           // run another scene on top (parallel)
this.scene.pause("GameScene");          // pause without stopping
this.scene.resume("GameScene");
this.scene.stop("UIScene");             // stop and destroy

// Receive data passed from another scene
create(data: { level: number }) {
  console.log(data.level);
}
```

### Game Object Properties

```typescript
sprite.setPosition(x, y);
sprite.setScale(2);            // 2x size
sprite.setScale(1.5, 2);       // different x/y scale
sprite.setAlpha(0.5);          // transparency (0 = invisible, 1 = opaque)
sprite.setAngle(45);           // rotation in degrees
sprite.setRotation(Math.PI);   // rotation in radians
sprite.setVisible(false);      // hide without destroying
sprite.destroy();              // remove from scene entirely
```

### Tweens (Animations Without Physics)

```typescript
// Move, fade, scale anything over time
this.tweens.add({
  targets: sprite,
  x: 400,
  alpha: 0,
  duration: 1000,           // ms
  ease: "Power2",           // easing function
  yoyo: true,               // reverse back after completing
  repeat: -1,               // -1 = loop forever
  onComplete: () => {
    sprite.destroy();
  }
});
```

### Debug Tips

```typescript
// Show physics hitboxes (in arcade physics config)
arcade: { debug: true }

// Log to console without cluttering update()
// Use a counter to only log every N frames:
if (this.frameCount % 60 === 0) {
  console.log(this.player.body!.velocity);
}
```

---

## Quick Reference Card

| Task | Code |
|---|---|
| Add physics sprite | `this.physics.add.sprite(x, y, "key")` |
| Set velocity | `sprite.setVelocity(vx, vy)` |
| Collide two objects | `this.physics.add.collider(a, b)` |
| Detect overlap | `this.physics.add.overlap(a, b, callback)` |
| Play animation | `sprite.play("key")` |
| Check key held | `key.isDown` |
| One-shot key event | `this.input.keyboard!.on("keydown-X", fn)` |
| Camera follow | `this.cameras.main.startFollow(sprite)` |
| Camera shake | `this.cameras.main.shake(200, 0.01)` |
| Play sound | `this.sound.play("key")` |
| Loop music | `this.sound.add("key", { loop: true }).play()` |
| Switch scene | `this.scene.start("SceneName")` |
| Destroy object | `sprite.destroy()` |
| Hide object | `sprite.setVisible(false)` |
| Tween an object | `this.tweens.add({ targets, x, duration })` |
