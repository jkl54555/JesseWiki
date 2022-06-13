##graphQL-client-unity

部分說明可參考Git網站(設定等部分)  
url:https://github.com/Gazuntype/graphQL-client-unity  
若沒有Json.dll可加入JsonDotNet  
(MRTK、Nuget自帶)  
url:https://assetstore.unity.com/packages/tools/input-management/json-net-for-unity-11347  
  
  
###scripts

using:
```csharp
using GraphQlClient.Core;
using UnityEngine.Networking;
```
設定Api
```csharp
public GraphApi graphApi;
private void Start()
    {
        graphApi.url="http";
        graphApi.SetAuthToken("token");
    }
```
```csharp
    //PostOne 透過Api設定進行輸入
    public async void PostOne()
    {
        GraphApi.Query createUser = graphApi.GetQueryByName("QueryName", GraphApi.Query.Type.Query);
        UnityWebRequest request = await graphApi.Post(createUser);
        string data = request.downloadHandler.text;
    }
 
    //PostTwo透過createUser.query更改Api設定
    public async void PostTwo()
    {
        GraphApi.Query createUser = test1.GetQueryByName("testttt", GraphApi.Query.Type.Query);
        createUser.query = "inputString";
        UnityWebRequest request = await test1.Post(createUser);
    }
    /*
    Ex. inputString:
            query {
          listProjects (listObjects(id: 15)){
            data {
              listObjects(id: 72) {
                data {
                  id
                  enabled
                  target
                  name
                }
              }
            }
          }
        }
    */
```
