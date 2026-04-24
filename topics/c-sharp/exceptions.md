## Exceptions

### try / catch / finally

```cs
try
{
    LoadLevel(id);
}
catch (FileNotFoundException ex)
{
    Log(ex.Message);
}
catch (Exception ex) when (ex.Data.Count > 0)
{
    throw; // rethrow preserving stack
}
finally { CleanUp(); }
```

---

### throw & Custom Exception

```cs
if (hp < 0)
    throw new ArgumentOutOfRangeException(
        nameof(hp), "HP cannot be negative");

public class GameException : Exception
{
    public GameException(string msg)
        : base(msg) { }
}
```
