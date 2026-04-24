## Delegates & Events

### Delegates / Func / Action

```cs
// Func returns a value
Func ease = t => t * t;

// Action returns void
Action onHit = dmg => PlayHitFX(dmg);

// custom delegate
public delegate void OnDeath(Entity who);
```

---

### Events

```cs
public event Action OnDamaged;

// subscribe
player.OnDamaged += ShowDamageNumber;
player.OnDamaged += dmg => hp -= dmg;

// raise
OnDamaged?.Invoke(30);

// unsubscribe
player.OnDamaged -= ShowDamageNumber;
```

---

### Closures

```cs
int count = 0;
Action increment = () => count++;  // captures count
increment();
increment();
// count == 2
```
