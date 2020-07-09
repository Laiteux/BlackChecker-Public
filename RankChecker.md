### List of available placeholders
- `<USERNAME>`: Will get replaced with the account username
- `<UUID:N>`: Will get replaced with the account UUID formatted with the chosen specifier (see [this](https://docs.microsoft.com/dotnet/api/system.guid.tostring#System_Guid_ToString_System_String_))

### Notes
- Rank checkers are a JSON array of objects/requests. That means you can perform multiple requests, and play with the `stop` and `continue` properties
- If the rank is empty or only consists of white-space characters, no rank will be assigned to the account
- Cookies aren't shared amongst requests, and there's no way of saving/capturing them (yet)

### Table of available request parameters
| Name | Type | Description | Available | Default | Required |
| :---: | :---: | :---: | :---: | :---: | :---: |
| method | array of string objects | Request method | DELETE, GET, HEAD, OPTIONS, PATCH, POST, PUT, TRACE | GET | |
| address | string | Request address/URL | | | ✓ |
| content | string | Request content/data/payload | | | |
| cookies | array of string objects | Request cookies, names and values | | | |
| headers | array of string objects | Request headers, names and values | | | |
| stop | array of strings | If any of these strings are found in the response, no rank will be assigned to the account | | | |
| continue | array of strings | If the response doesn't contain any of these strings, the requests will be re-sent with a new proxy | | | |
| regex | string | Regular expression to be executed against the response | | | ✓ |
| group | integer | RegEx match group number for the rank | | 1 | |
| ignore | array of strings | If the rank is is any of these strings (case insensitive), no rank will be assigned to the account | | | |

### Example of a (fake) rank checker config using all parameters
```json
[
   {
      "method": "POST",
      "address": "https://checker.black/example",
      "content": "username=<USERNAME>",
      "cookies": {
         "PHPSESSID": "vc02s2cu1nw5dfaamy94pp2bbc"
      },
      "headers": {
         "Content-Type": "application/x-www-form-urlencoded"
      },
      "stop": [
         "Player not found"
      ],
      "continue": [
         "Total playtime"
      ],
      "regex": "<b>Rank:</b> (\\S+)",
      "group": 1,
      "ignore": [
         "None"
      ]
   }
]
```

### Example of a real Hypixel rank checker
```json
[
    {
        "address": "https://plancke.io/hypixel/player/stats/<UUID:N>",
        "stop": [
            "Player not found"
        ],
        "continue": [
            "Player Information"
        ],
        "regex": "<meta name=\"description\" content=\"\\[(.+?)\\]"
    }
]
```

### Example of a real Mineplex rank checker
```json
[
    {
        "address": "https://www.mineplex.com/players/<USERNAME>",
        "stop": [
            "That player cannot be found."
        ],
        "continue": [
            "General Statistics"
        ],
        "regex": "Util.prettyRank\\('(.+?)'\\)",
        "ignore": [
            "player"
        ]
    }
]
```
