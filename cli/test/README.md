# Test
## Exec
When ran in a directory of a microservice (a directory containing a `microservice.guide` and `Dockerfile`) this command will build
the microservice and execute a given command.
### Usage
```
exec [-e] [command] [args...]
```

#### command
Command is a required argument. The microservice will be executed with the given command.

#### args...
If a command required arguments they can be passed as follows: `key:val`. If required arguments are not given `exec` will fail.

#### Environment variables
If the microservice has any required environment variables they must be passed in with the `exec` command. Much like Docker,
environment variables can be passed as follows: `-e FOO='bar'`. If a required environment variable is not supplied `exec` will fail.

### Example `exec` call
```sh
omg exec -e BOT_TOKEN='xoxb-****' send message:'Hello, World!' to:CAFAF9C
```
```sh
✔ Built Docker image with name: 067a8912-a1fe-4e00-ba4b-ffcc363ca0ab
✔ Stared Docker container with id: a941268edae7
✔ Ran command: send with output: {
  "ok": true,
  "reply_to": 1,
  "ts": "1528904352.000735",
  "text": "Hello, World!"
}
✔ Stopped Docker container: a941268edae7
```
