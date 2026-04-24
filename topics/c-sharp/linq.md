## LINQ

### Filtering & Projection

```cs
var alive = enemies
    .Where(e => e.Hp > 0)
    .Select(e => e.Name)
    .ToList();

// query syntax
var q = from e in enemies
        where e.Hp > 0
        select e.Name;
```

---

### Ordering & Grouping

```cs
var sorted = enemies
    .OrderByDescending(e => e.Hp)
    .ThenBy(e => e.Name)
    .ToList();

var groups = enemies.GroupBy(e => e.Type);
foreach (var g in groups)
    Console.WriteLine($"{g.Key}: {g.Count()}");
```

---

### Aggregates

```cs
int   total = enemies.Sum(e => e.Hp);
int   max   = enemies.Max(e => e.Hp);
float avg   = enemies.Average(e => e.Hp);
int   count = enemies.Count(e => e.Alive);
bool  any   = enemies.Any(e => e.IsBoss);
bool  all   = enemies.All(e => e.Hp > 0);
```

---

### First, Single, Take, Skip

```cs
var first = enemies.FirstOrDefault(e => e.IsBoss);
var one   = enemies.SingleOrDefault(e => e.Id == id);

var page = enemies
    .Skip(20)
    .Take(10)
    .ToList();
```

---

### Joins & Flattening

```cs
var loot = enemies
    .Where(e => !e.Alive)
    .SelectMany(e => e.Drops)  // flatten
    .Distinct()
    .ToList();

var joined = items.Join(drops,
    i => i.Id, d => d.ItemId,
    (i, d) => (i.Name, d.Qty));
```
