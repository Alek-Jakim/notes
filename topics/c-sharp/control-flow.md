## Control Flow

### IF / ELSE IF / ELSE

```cs
if (hp <= 0)
{
    Die();
}
else if (hp < 20)
{
    PlayLowHpSound();
}
else
{
    Heal();
}
```

---

### SWITCH EXPRESSION

```cs
string tier = score switch
{
    >= 1000 => "S",
    >= 800  => "A",
    >= 600  => "B",
    _       => "C"   // default
};
```

---

### SWITCH STATEMENT

```cs
switch (state)
{
    case GameState.Menu:
        ShowMenu(); break;
    case GameState.Playing:
        RunGame(); break;
    default:
        Reset(); break;
}
```

---

### Ternary & NULL Operators

```cs
string alive = hp > 0 ? "alive" : "dead";

string n = player?.Name;        // null-cond.
int    x = player?.Hp ?? 0;     // null-coal.
player?.bullets.Clear();         // safe call
```

---

### Pattern Matching

```cs
if (obj is Enemy e && e.Hp > 0)
    e.Attack();

if (shape is Circle { Radius: > 5 } c)
    Draw(c);

bool isHurt = entity is
    Player { Hp: < 20 } or
    Ally   { Hp: < 10 };
```
