# Validate
When ran in a directory of a microservice (a directory containing a `microservice.guide`), validation will be ran against that file.
```sh
omg utils
```
#### Example output
##### Valid `microservice.yml`
```json
{
  "valid": true,
  "microsericeYaml": {
    "commands": {
      "boolean": {
        "output": "boolean",
        "help": "Generates a random boolean"
      },
      "string": {
        "help": "Generates a random string",
        "format": "{{length}}",
        "output": "string",
        "arguments": {
          "length": {
            "type": "int",
            "required": true,
            "help": "Length of string"
          }
        }
      }
    }
  },
  "errors": null
}
```
##### Invalid `microservice.yml`
```json
{
  "valid": false,
  "microsericeYaml": {
    "commands": {
      "boolean": {
        "output": "boolean",
        "help": "Generates a random boolean"
      },
      "string": {
        "help": "Generates a random string",
        "format": "{{length}}",
        "arguments": {
          "length": {
            "required": true,
            "help": "Length of string"
          }
        }
      }
    }
  },
  "errors": [
    {
      "keyword": "required",
      "dataPath": ".commands['string']",
      "schemaPath": "#/properties/commands/patternProperties/%5E%5BA-Za-z%7C_%5D%2B%24/required",
      "params": {
        "missingProperty": "output"
      },
      "message": "should have required property 'output'"
    },
    {
      "keyword": "required",
      "dataPath": ".commands['string'].arguments['length']",
      "schemaPath": "#/properties/commands/patternProperties/%5E%5BA-Za-z%7C_%5D%2B%24/properties/arguments/patternProperties/%5E%5Cw%2B%24/required",
      "params": {
        "missingProperty": "type"
      },
      "message": "should have required property 'type'"
    }
  ]
}
```
