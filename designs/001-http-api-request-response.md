# 001 · HTTP API Requests and Responses

## The problem

A task app needs to create a task and load it later. Its frontend must tell the difference between a saved task, invalid input, and a server failure. Design the HTTP contract that lets the frontend handle each outcome.

## Prerequisites

- **Client and server.** The client sends a request. The server handles it and returns a response.
- **URL and path.** A URL identifies where to send the request. A path such as `/tasks/42` identifies a resource on that server.
- **JSON.** A text format for sending structured data such as `{"title":"Review API notes"}`.
- **Headers and body.** Headers describe the message. The body carries data when the message has one. `Content-Type: application/json` describes a JSON body.
- **Status code.** The three-digit code in the response tells the client the outcome at the HTTP level.

## Predict first

1. The server saves a new task before replying. Which status should it return, and how can the client find the new task?
2. The client looks up a task ID that does not exist. What should the response contain?
3. The server accepts an export request but is still building the file. What should the client show?

<details>
<summary>Hint</summary>

Distinguish a resource that exists now from work that the server has accepted for later. Then decide how the client will get the next update.

</details>

## The API contract

| Request | Outcome | Response |
| --- | --- | --- |
| `POST /tasks` with a valid title | Task saved | `201 Created`, `Location: /tasks/42`, and the saved task as JSON |
| `GET /tasks/42` | Task found | `200 OK` and the task as JSON |
| `POST /tasks` with a blank title | Input rejected under this API's validation policy | `400 Bad Request` and a JSON error identifying the title field |
| `GET /tasks/99` | Task missing | `404 Not Found` and a JSON error with a stable code |
| `POST /exports` | Export accepted and still pending | `202 Accepted` with a status URL in the body |
| Any request with an unexpected server failure | Request failed | `500 Internal Server Error` and a generic JSON error with a request ID for support |

### Create a task

Illustrative HTTP/1.1 request and response.

```http
POST /tasks HTTP/1.1
Host: api.example.test
Content-Type: application/json
Content-Length: 28

{"title":"Review API notes"}
```

```http
HTTP/1.1 201 Created
Location: /tasks/42
Content-Type: application/json
Content-Length: 36

{"id":42,"title":"Review API notes"}
```

The method and path tell the server what the client is asking for. The status code tells the client that creation succeeded. The `Location` header identifies the new resource, and the body supplies the data the UI can render immediately.

### Return a validation error

For a blank title, this API returns `400` with the following body.

```json
{
  "code": "INVALID_TITLE",
  "message": "Enter a title.",
  "field": "title"
}
```

The UI can use the stable `code` and `field` to highlight the input. Keep stack traces and database details in server logs.

### Return a status for background work

`POST /exports` can return `202` and `{"id":"e42","status":"queued","statusUrl":"/exports/e42"}`. The client can then call `GET /exports/e42`. That lookup can return `200` with `status: "failed"` if the lookup succeeded and the export itself failed. The HTTP status describes the current request. The JSON field describes the export.

## When should the server respond?

For a quick task insert, wait for the save and return `201`. For a long-running export, accept the work and return `202` once it has been recorded for processing. The second approach keeps the initial response short but requires a status endpoint and a UI that handles pending and failed jobs.

## 35-minute practice

| Time | Activity |
| --- | --- |
| 5 min | Recall the difference between a method, a status code, a header, and a body. |
| 10 min | Sketch the requests and responses for saving and loading a task. |
| 10 min | Write expected status, headers, and JSON for a valid title, a blank title, and a missing ID. Use these as test cases. |
| 5 min | Debug a UI that displays “Export complete” immediately after receiving `202`. Identify which response field should drive that message. |
| 5 min | Explain aloud why `GET /exports/e42` can return `200` when the export failed. |

After two or three days, redraw the create-task exchange from memory and explain when you would choose `201` or `202`.

[HTTP status code definitions in RFC 9110](https://www.rfc-editor.org/rfc/rfc9110.html#section-15)
