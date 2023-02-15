---
title: Stakfile
requirements:
  - command: curl
---

# Http Client

// TODO - 

First we are going to use Stakz to create a form to make a web request client.

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
