## Loops

### FOR Loop

```cs
for (int i = 0; i < 10; i++)
    Console.WriteLine(i);

// reverse
for (int i = arr.Length - 1; i >= 0; i--)
    Process(arr[i]);
```

---

### FOREACH Loop

```cs
foreach (var enemy in enemies)
{
    enemy.Update(delta);
    if (enemy.Hp <= 0) enemy.Die();
}
```

---

### WHILE / DO-WHILE Loop

```cs
while (!gameOver)
    Update();

do
{
    attempt = RollDice();
} while (attempt < 3);
```

---

### BREAK / CONTINUE / RETURN

```cs
foreach (var e in enemies)
{
    if (e == null) continue; // skip
    if (e.IsBoss)   break;    // stop loop
    e.Update();
}
```
