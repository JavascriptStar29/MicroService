# Lifecycle

A service **MAY** define custom lifecycle commands for each state of your microservice.

*If the service interfaces with HTTP or RPC, the lifecycle **MUST** define a run command.*

```yaml
lifecycle:
  initialize:
    command: ./initialize.sh
    timeout: 300
  startup:
    command: ./startup.sh
    timeout: 300
  run:
    command: ["/bin/server", "-p", "5000"]
    port: 8080
  shutdown:
    command: ./shutdown.sh
    timeout: 300
  terminate:
    command: ./terminate.sh
    timeout: 300
```
## State Transistions

`initialize` => `startup` => `run` => `shutdown` => `terminate`

- `initialization`
  - Execute a command before *all instantiations* of your microservice are started

- `startup`
  - Execute a command before an *individual instantiation* of your microservice is started

- `run`
  - Run command for your microservice

- `shutdown`
  - Execute a command after an *individual instantiation* of your microservice is shutdown

- `terminate`
  - Execute a command after *all instantiations* of your microservice are shutdown

## Run
The `command` **MAY** start a service which is blocking (e.g., HTTP or RPC server). Exclude the `timeout` and include the `port` in which to bind to.

```yaml{3,4}
lifecycle:
  run:
    command: ["/bin/server", "-p", "5000"]
    port: 5000
```

Based on the configuration above, the Docker run command would be the following:

```bash
$ docker run -d -p 81433:5000 \
           --entrypoint /bin/server \
           foobar -p 5000
```
