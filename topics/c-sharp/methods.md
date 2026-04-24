## Methods

### Method Signatures

```cs
// return type  name   params
int  Add(int a, int b) => a + b;

void TakeDamage(int dmg, bool critical = false)
{
    hp -= critical ? dmg * 2 : dmg;
}
```

---

### ref / out / in Params

```cs
void Swap(ref int a, ref int b)
    => (a, b) = (b, a);

bool TryFire(out Bullet b)
{
    b = ammo > 0 ? new Bullet() : null;
    return b != null;
}

void Read(in int val) { }  // readonly ref
```

---

### Optional & Named Args

```cs
Spawn(x: 10, y: 20, pooled: true);

void Spawn(float x=0, float y=0,
           bool pooled=false) { ... }
```

---

### Params & Overloads

```cs
void Log(params object[] args) { ... }
Log("hp", hp, "alive", alive); // any count

// overloads — same name, different signature
void Attack(Enemy e) { ... }
void Attack(Enemy e, int dmg) { ... }
```

---

### Local Functions & Lambdas

```cs
int Distance(Vector2 a, Vector2 b)
{
    float Sq(float v) => v * v; // local fn
    return MathF.Sqrt(Sq(b.X-a.X) +
                      Sq(b.Y-a.Y));
}

Func alive = hp => hp > 0;
Action    hurt  = dmg => hp -= dmg;
```
