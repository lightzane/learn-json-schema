# Learning JSON Schema

This is the basic learning for JSON schema.<br>
It is used for creating JSON easier like having an intellisense with guide and validations.

## Getting Started

1. Open [vscode](https://code.visualstudio.com/)
2. Create `schemas` folder
3. Create `your-filename.schema.json` and open it
4. Tell `vscode` about your JSON schemas. [Go here](#settings)
5. Write `{ }`
6. Press `Ctrl + SPACE` and input or select `"$schema"`
7. Press again `Ctrl + SPACE` and choose a specification (i.e. http://json-schema.org/schema)

You can now define your own schema! See examples below...<br>

### Examples

`schemas/profile.schema.json`

```json
{
    "$schema": "http://json-schema.org/schema",
    "$id": "profile.schema.json",
    "required": ["name", "age"],
    "properties": {
        "name": {
            "description": "Give details about your name.",
            "$ref": "./name.schema.json"
        },
        "hobbies": {
            "description": "Things you love to do on your free or \"me\" time.",
            "$ref": "#/definitions/hobbiesdef"
        },
        "age": {
            "description": "How old are you?",
            "$ref": "#/definitions/agedef"
        }
    },
    "definitions": {
        "hobbiesdef": {
            "$comment": "definitions are sub-schemas, and called in $ref, you can also create another schema file rather than having a definition",
            "type": "array",
            "uniqueItems": true,
            "items": {
                "type": "string",
                "examples": [
                    "swimming",
                    "sleeping",
                    "eating",
                    "watching movies",
                    "playing music instruments",
                    "listening to music",
                    "playing outdoor games",
                    "playing video games",
                    "games"
                ]
            },
            "examples": [
                ["swimming", "doing laundry"],
                ["playing games", "while eating"]
            ]
        },
        "agedef": {
            "type": "integer",
            "exclusiveMinimum": 0
        }
    }
}
```

`schemas/name.schema.json`

```json
{
    "$schema": "http://json-schema.org/schema",
    "$id": "name.schema.json",
    "required": ["firstName", "lastName"],
    "additionalProperties": false,
    "properties": {
        "firstName": {
            "description": "Your first name goes here.",
            "type": "string"
        },
        "lastName": {
            "description": "Your surname goes here.",
            "type": "string"
        },
        "nickname": {
            "description": "Enter here what you want your close friends to call you.",
            "type": "string"
        },
        "prefix": {
            "description": "How you are addressed.",
            "type": "string",
            "enum": ["Mr.", "Ms.", "Dr.", "Sir", "Madam"]
        },
        "suffix": {
            "description": "Your suffix (if any).",
            "type": "string",
            "examples": ["Jr", "Sr"]
        }
    }
}
```

### Sample Model

`profile.model.json`

```json
{
    "name": {
        "firstName": "Juan",
        "lastName": "De La Cruz",
        "suffix": "III"
    },
    "hobbies": [
        "playing games",
        "while eating",
        "listening to music",
        "listening to IU music"
    ],
    "age": 3
}
```

## Settings

You need to setup and tell vscode about your schema and where to apply it.<br>
So that the intellisense, validation will display every time you write your JSON object/model.

1. Press `Ctrl + P`
2. Type `>settings`
3. Select `Preferences: Open Workspace Settings (JSON)`
4. Validate that the following is created: `.vscode/settings.json`
5. You can now use its intellisense to construct the following:<br>

`.vscode/settings.json`

```json
{
    "json.schemas": [
        {
            "fileMatch": ["*profile.model.json"],
            "url": "./schemas/profile.schema.json"
        }
    ]
}
```

## References

-   https://json-schema.org/learn/getting-started-step-by-step
