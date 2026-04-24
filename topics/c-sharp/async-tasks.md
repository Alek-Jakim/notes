## Async & Tasks

### async / await Basics

```cs
public async Task LoadSceneAsync(string name)
{
    await Task.Delay(500);        // non-blocking wait
    await ReadFileAsync(name);
}

public async Task FetchScoreAsync()
{
    await Task.Delay(100);
    return 9999;
}
```

---

### Task.WhenAll / WhenAny

```cs
var t1 = LoadMapAsync();
var t2 = LoadAudioAsync();
await Task.WhenAll(t1, t2); // parallel wait

var done = await Task.WhenAny(t1, t2);
// fires when FIRST completes
```

---

### CancellationToken

```cs
var cts   = new CancellationTokenSource();
var token = cts.Token;

StartLoading(token);
cts.Cancel(); // signal cancellation

async Task StartLoading(CancellationToken ct)
{
    ct.ThrowIfCancellationRequested();
    await Task.Delay(1000, ct);
}
```
