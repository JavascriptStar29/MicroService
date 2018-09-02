# Logs

Services **MUST** write logs to a specific location in a specific format.

```
service: [<level>] <message>
```

> Syslog Example

```python
#!/usr/bin/env python

import logging
import logging.handlers
import os

syslog_host = os.environ['OMG_LOG_HOST']
syslog_port = os.environ['OMG_LOG_PORT']

# define the logger and set the logging level
logger = logging.getLogger('root')
logger.setLevel(logging.INFO)

# add handler
handler = logging.handlers.SysLogHandler(address=(syslog_host, int(syslog_port)))

# add formatter
record_layout = '%(name)s: created=%(created)f [%(levelname)s] %(message)s'
formatter = logging.Formatter(record_layout)

handler.formatter = formatter
logger.addHandler(handler)

# log the message
logger.info("Logging some cool data")
```

> Log file Example

```shell
#!/usr/bin/env bash

LOGGER_NAME="foot"
LOGGER_LEVEL="INFO"
LOG_FILE="/var/log/microservice.log"

logMsg() {
  LOGGER_LEVEL="$1"
  LOGGER_MESSAGE="$2"
  TIMESTAMP=$(date +'%b %e %R:%S')
  echo "$TIMESTAMP $HOSTNAME $LOGGER_NAME: created=$(date +%s) source_file=$0 [$LOGGER_LEVEL] $LOGGER_MESSAGE" >> $LOG_FILE
}

logMsg "INFO" "Logging some data"
```

Write logs to `syslog` or to `/var/log/microservice.log`

Containers are passed the following environment variables to be used in logging:

- `OMG_APP_ID`
- `OMG_STORY_ID`
- `OMG_LOG_HASH`

Syslog environment variables:

- `OMG_LOG_HOST`
- `OMG_LOG_PORT`


### Logging Levels

Levels **SHOULD** be one of the following.

| Level    |
|----------|
| CRITICAL |
| ERROR    |
| WARNING  |
| INFO     |
| DEBUG    |
| NOTSET   |
