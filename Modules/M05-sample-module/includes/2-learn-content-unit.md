# h1
123

## Learn content unit
http://www.microsoft.com/en-us/videoplayer/embed/RWtXMf]
### Video with direct redtiger URL
> [!VIDEO http://www.azure.microsoft.com/en-us/videoplayer/embed/RWtXMf]

### Video with file name and CSV
> [!VIDEO What is a Computer.mp4]

---

### Code
```python
conn = httplib.HTTPSConnection('southcentralus.api.cognitive.microsoft.com')
conn.request("POST", serviceEndpointUrl, body)
response = conn.getresponse()

data = response.read()
```

Making the same API call in C# is simply a change in language-specific syntax:

```csharp
HttpClient client = new HttpClient();
StringContent content = new StringContent(body);
response = await client.PostAsync(serviceEndpointUrl, content);

string data = await response.Content.ReadAsStringAsync();
```

<!-- Custom vision service is GA: https://docs.microsoft.com/en-us/azure/cognitive-services/custom-vision-service/release-notes -->

---
### Lab-Sandbox-task

```yaml
tasks:
- action: exists
  environment: azure
  azure:
    resource:
      type: "Microsoft.DocumentDB/databaseAccounts"
  hint: "Follow the directions to create an Azure Cosmos DB account."
```