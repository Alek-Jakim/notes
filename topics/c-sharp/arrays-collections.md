## Arrays & Collections

### Arrays

```cs
int[] hp = { 100, 80, 60 };
int[] grid = new int[8];

// 2D
int[,] map = new int[10, 10];
map[2, 3] = 1;

int len = hp.Length;
```

---

### List\<T\>

```cs
var bullets = new List();
bullets.Add(new Bullet());
bullets.Remove(b);
bullets.RemoveAt(0);
bullets.Clear();
int  count = bullets.Count;
bool has   = bullets.Contains(b);
```

---

### Dictionary\<K, V\>

```cs
var items = new Dictionary
{
    { "sword", 1 }, { "shield", 2 }
};
items["potion"] = 5;
bool has = items.ContainsKey("sword");
items.TryGetValue("axe", out int val);
```

---

### HashSet, Stack, Queue

```cs
var visited = new HashSet();
visited.Add(pos); // no duplicates

var undo = new Stack();
undo.Push(act); undo.Pop();

var events = new Queue();
events.Enqueue(e); events.Dequeue();
```
