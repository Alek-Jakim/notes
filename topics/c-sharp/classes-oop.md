## Classes & OOP

### Class & Constructor

```cs
public class Player
{
    public string Name { get; set; }
    public int    Hp   { get; private set; }

    public Player(string name, int hp = 100)
    {
        Name = name;
        Hp   = hp;
    }
}

var p = new Player("Hero") { Hp = 80 };
```

---

### Properties & Auto-Props

```cs
public int Hp
{
    get => _hp;
    set => _hp = Math.Clamp(value, 0, MaxHp);
}
private int _hp;

// auto-property
public float Speed { get; set; } = 5f;

// computed / read-only
public bool Alive => Hp > 0;
```

---

### Inheritance

```cs
public class Enemy : Entity
{
    public override void Update(float dt)
    {
        base.Update(dt); // call parent
        ChasePlayer();
    }
}

// Sealed = no further subclassing
public sealed class FinalBoss : Enemy { }
```

---

### Abstract & Virtual

```cs
public abstract class Entity
{
    public abstract void Update();       // must override
    public virtual  void Draw(float dt) { }
}

public class Slime : Entity
{
    public override void Update() { ... }
}
```

---

### Interfaces

```cs
public interface IDamageable
{
    int  Hp { get; }
    void TakeDamage(int amount);
}

public class Boss : Entity, IDamageable
{
    public int  Hp { get; private set; }
    public void TakeDamage(int d) => Hp -= d;
}
```

---

### Static Members & Singleton

```cs
public static class GameManager
{
    public static int  Level = 1;
    public static void NextLevel() => Level++;
}

// Singleton pattern
public class AudioManager
{
    public static AudioManager Instance { get; }
        = new AudioManager();
    private AudioManager() { }
}
```

---

### Structs & Records

```cs
// Struct — value type, no heap alloc
public struct Vector2
{
    public float X, Y;
    public float Length => MathF.Sqrt(X*X+Y*Y);
}

// Record — immutable, value equality
public record Tile(int X, int Y, bool Solid);
var t2 = t with { Solid = false }; // copy+modify
```

---

### Operator Overloading

```cs
public static Vector2 operator +
    (Vector2 a, Vector2 b)
    => new(a.X + b.X, a.Y + b.Y);

public static bool operator ==
    (Vector2 a, Vector2 b)
    => a.X == b.X && a.Y == b.Y;
```
