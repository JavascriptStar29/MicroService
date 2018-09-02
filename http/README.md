# HTTP Server

## Query Arguments

```yaml
commands:
  concat:
    arguments:
      left:
        type: string
      right:
        type: string
    output: string
    http:
      method: get
      endpoint: /concat

lifecycle:
  run:
    command: ["FLASK_APP=example.py", "flask", "run", "--host=0.0.0.0"]
    port: 5000
```

```python
# example.py
from flask import Flask
from flask import request
app = Flask(__name__)

@app.route('/concat')
def concat():
    left = request.args.get('left', '')
    left = request.args.get('right', '')
    return f'{left}{right}'
```

```javascript
// Request
{
  "left": "a",
  "right": "b"
}
```

```bash
# Platform Translation
$ curl -X GET http://service:5000/concat?left=a&right=b

# Response
ab
```

## Post Body

Using [PostGraphile](https://github.com/graphile/postgraphile) as the GraphQL service.

```yaml
commands:
  query:
    arguments:
      query:
        type: string
    http:
      method: post
      endpoint: /graphql

lifecycle:
  startup:
    command: ["postgraphile", \
              "-n", "0.0.0.0", \
              "-c", "$DATABASE_URL"]
    port: 5000

environment:
  database_url:
    type: string
    help: The PostgreSQL url to connect to.
```

```javascript
// Request
{
  "query": "{allUsers{...}}"
}
```

```bash
# Platform Translation
$ curl -X POST -d '{"query":"{allUsers{...}}"}' http://service:5000/query

# Response
{
  "data": {...}
}
```
