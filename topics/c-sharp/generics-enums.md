## Generics & Enums

### Generic Class

```cs
public class Pool where T : new()
{
    private Stack _pool = new();

    public T Get()
        => _pool.Count > 0 ? _pool.Pop() : new T();

    public void Return(T item) => _pool.Push(item);
}
```

---

### Generic Constraints

```cs
where T : class        // ref type
where T : struct       // value type
where T : new()        // has default ctor
where T : IDamageable  // implements interface
where T : Entity       // subclass of
```

---

### Enums

```cs
public enum Direction { Up, Down, Left, Right }

public enum StatusEffect
{
    None   = 0,
    Burn   = 1 << 0,  // 1
    Freeze = 1 << 1,  // 2
    Poison = 1 << 2,  // 4
}

var s = StatusEffect.Burn | StatusEffect.Freeze;
bool isBurning = s.HasFlag(StatusEffect.Burn);
```
