GetRequest
***
```csharp
using System.Collections;
using System;
using UnityEngine;
using UnityEngine.Networking;
using Newtonsoft.Json;
 
    public MyData loadedData;
 
    private void Start()
    {
        ParsingJS("http://192.168.50.43/datatest/1");
    }
 
    IEnumerator GetRequest(string endpoint, Action<UnityWebRequest> callback)
    {
        using (UnityWebRequest request = UnityWebRequest.Get(endpoint))
        {
            // Send the request and wait for a response
            yield return request.SendWebRequest();
            callback(request);
        }
    }
 
    public void ParsingJS(string url)
    {
        StartCoroutine(GetRequest(url, (UnityWebRequest req) =>
        {
            if (req.result != UnityWebRequest.Result.Success)
            {
                Debug.Log($"{req.error}: {req.downloadHandler.text}");
            }
            else
            {
                Debug.Log(req.downloadHandler.text);
                loadedData = JsonConvert.DeserializeObject<MyData>(req.downloadHandler.text);
            }
        }));
    }
```
***
創立對應Json變數的Class類(Sript:MyData)
```csharp

    [System.Serializable]
    public class MyData
    {
        public classify[] info;
        public classify[] lv;
        public Data[] data;
    }
 
    [System.Serializable]
    public class classify
    {
        public string sn, lv, label, remark;
    }
    [System.Serializable]
    public class Data
    {
        public int t;
        public string sn, k, v, u, r;
    }
```
