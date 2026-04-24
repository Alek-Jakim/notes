## Variables & Types

### Value Types

```cs
int    hp = 100;
float  speed = 3.5f;
double dist = 1.414;
bool   alive = true;
char   grade = 'A';
byte   flags = 0xFF;
long   score = 9_999_999L;
```

---

### Reference Types

```cs
string  name = "Player";
int[]   arr  = new int[4];
List<int> list = new();
object  obj  = null;
```

---

### VAR, CONST, READONLY

```cs
var pos = new Vector2(0, 0); // inferred
const int MAX_HP = 100;      // compile-time
readonly float spawnX = 5f; // set in ctor
```

---

### Nullable Types

```cs
int?    maybeHp = null;
string? maybeName = null;

int hp = maybeHp ?? 0;    // null-coalesce
int val = maybeHp!.Value; // null-forgiving
```

---

### Type Conversion

```cs
int    i = (int) 3.9f;        // explicit → 3
float  f = 5;               // implicit
string s = i.ToString();
int    n = int.Parse("42");
bool   ok = int.TryParse(s, out n);
```

---

### Type Conversion

```cs
string s = $"HP: {hp}/{MAX_HP}";
string r = @"C:assetsmap"; // verbatim
bool eq = string.Equals(a, b,
    StringComparison.OrdinalIgnoreCase);
string up = s.ToUpper();
string tr = s.Trim();
```
