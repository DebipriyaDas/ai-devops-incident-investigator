# n8n Workflow

## Node 1

Webhook

Receives:

```json
{
  "log":"...",
  "file_name":"error.txt"
}
```

---

## Node 2

Prompt Builder

Builds AI prompt.

---

## Node 3

Gemini 2.5 Flash

Returns:

* incident_summary
* root_cause
* severity
* recommendations
* postmortem

---

## Node 4

JSON Parser

Converts AI response into structured JSON.

---

## Node 5

Supabase Insert

Writes to:

```
investigations
```

---

## Node 6

Respond to Webhook

Response Mode

```
JSON
```

Response Body

```javascript
{{$json}}
```

Important:

Respond node MUST be connected after Supabase Insert.

Otherwise frontend receives empty response.

