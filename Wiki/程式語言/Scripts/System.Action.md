Action 是一個將「方法」作為「參數」進行傳遞的功能  

```csharp
private void Start()
    {
        RunJob(x => {
            Debug.Log("你抽到的號碼是" + x);
            Debug.Log("恭喜你囉！");
        });
    }
 
    public void RunJob(System.Action<int> onComplete)
    {
        Debug.Log("開始隨機取號...");
        onComplete(Random.Range(0, 1000));
    }
```

原文出處 : <https://tedliou.com/archives/unity-chsarp-action/>
