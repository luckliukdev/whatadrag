# Leaderboard Submission Documentation

## How to Submit Scores to Leaderboard
To submit scores to the leaderboard, you'll need to make a POST request to the following endpoint:

```
POST /api/submit-score
```

### Request Body Format
```json
{
  "playerId": "string",
  "score": "integer"
}
```

### Example Request (JavaScript)
```javascript
fetch('https://yourapi.com/api/submit-score', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_API_TOKEN'
  },
  body: JSON.stringify({
    playerId: 'player123',
    score: 100
  })
});
```

## GitHub API Integration Guide
1. **Generate a Personal Access Token** from your GitHub account settings.
2. **Authenticate API requests** using the token in the Authorization header.

### Example Request to GitHub API (Get User Repositories)
```javascript
fetch('https://api.github.com/user/repos', {
  headers: {
    'Authorization': 'token YOUR_GITHUB_TOKEN'
  }
}).then(response => response.json()).then(data => console.log(data));
```

## Security Information
### Token Usage
- Keep your tokens confidential and do not share them in public repositories.
- Rotate tokens periodically and use environment variables to manage them securely in your applications.

## Examples for Different Platforms
### Unity Example
```csharp
using UnityEngine;
using System.Collections;
using UnityEngine.Networking;

public class ScoreSubmitter : MonoBehaviour {
    void SubmitScore(string playerId, int score) {
        StartCoroutine(PostScore(playerId, score));
    }

    IEnumerator PostScore(string playerId, int score) {
        WWWForm form = new WWWForm();
        form.AddField("playerId", playerId);
        form.AddField("score", score);

        using (UnityWebRequest www = UnityWebRequest.Post("https://yourapi.com/api/submit-score", form)) {
            yield return www.SendWebRequest();

            if (www.result == UnityWebRequest.Result.ConnectionError || www.result == UnityWebRequest.Result.ProtocolError) {
                Debug.Log(www.error);
            } else {
                Debug.Log("Score submitted successfully!");
            }
        }
    }
}
```

### Other Platforms
- Always refer to their official documentation for API request guidance.
- Adapt the example requests used above to the language and libraries of your choice.