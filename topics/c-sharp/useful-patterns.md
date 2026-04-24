## Useful Patterns

### Object Pooling

```cs
var pool = new Pool();
Bullet b = pool.Get();
b.Fire(direction);
// on collision / out of screen:
b.Reset(); pool.Return(b);
```

---

### Observer / Event Bus

```cs
static class EventBus
{
    static Dictionary>> _subs = new();

    public static void Subscribe(Action cb)
        => GetList(typeof(T)).Add(e => cb((T)e));

    public static void Emit(T e)
        => _subs.GetValueOrDefault(typeof(T))
                ?.ForEach(cb => cb(e));
}
```

---

### State Machine

```cs
enum State { Idle, Running, Jumping, Dead }
State _state = State.Idle;

void Update()
{
    switch (_state)
    {
        case State.Running: UpdateRun();  break;
        case State.Jumping: UpdateJump(); break;
    }
}

void TransitionTo(State next) => _state = next;
```

---

### Extension Methods

```cs
public static class VectorExtensions
{
    public static float Angle(this Vector2 v)
        => MathF.Atan2(v.Y, v.X);

    public static Vector2 Normalized(this Vector2 v)
        => v / v.Length();
}

pos.Angle(); // works on any Vector2
```

---

### using / IDisposable

```cs
using var stream = File.OpenRead("save.dat");
// auto-disposed at end of scope

public class RenderTarget : IDisposable
{
    public void Dispose() => _texture?.Dispose();
}
```

---

### Deconstruction & Tuples

```cs
(int x, int y) = GetSpawnPoint();
var (hp, mp)   = player.GetStats();

// return multiple values
(int Hp, int Mp) GetStats() => (100, 50);

// named tuple
var stats = (Hp: 100, Mp: 50);
int h = stats.Hp;
```
