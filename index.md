---
title: Stakfile
requirements:
  - command: curl
---

# Http Client

// TODO -

First we are going to use Stakz to create a form to make a web request client.

<field label="url" description="Url to send the request to">url</field>
<field label="method" description="Http method">GET</field>
<json label=body description="Body of the request">
{
"hello": {
"world": "hello!"
}
}
</json>

```Stakz.yaml
schema:
  type: object
  properties:
    url:
      type: string
      default: http://postman-echo.com
    method:
      enum: ["GET", "POST", "PUT", "PATCH", "DELETE"]
      description: The http verb
    headers:
      type: object
      description: Http headers
    body:
      type: object
      description: Http body.
script: |
  return `curl -X ${method} \\
  ${Object.entries(headers)
            .map(([k, v]) => `     -H "${k}: ${v}"`)
            .join(' \\\n')} \\
     -d '${JSON.stringify(body)}' \\
     ${url}/${method}`
```

Awesome job!
