# Curl Client

Example using Stakz to create a form to basic curl http client.

<field label="url" description="Url to send the request to">http://localhost:3001/echo</field>
<select label="method" description="Http method" 
options="GET,POST,PUT,PATCH,DELETE,OPTIONS">GET</select>
<yaml label="headers" description="http headers">
Content-Type: application/json
Authorization: Example Token
</yaml>
<json label=body description="Body of the request">
{
    "hello": {
        "world": "hello!"
    }
}
</json>

<script>
return `curl -X ${method} \\
     ${Object.entries(headers).map(([k, v]) => `-H "${k}: ${v}" \\`).join("\n     ")}
     -d '${JSON.stringify(body)}' \\
     ${url}`
</script>

Awesome job!
