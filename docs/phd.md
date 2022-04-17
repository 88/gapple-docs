# PHD Checker API Routes
**NOTE:** This API is in beta and was just migrated from old code to this new route. It is subject to error.

Minecraft accounts have three states of deletion:
- Deactivation
- Pseudo-hard-deletion
- Hard-deletion

Deactivation is when an account's username and UUID appear taken and all information about the account can be retrieved via the API, you just can't log in to the account anymore.

Pseudo-hard-deletion is when an account's username appears available but isn't, and its UUID appears nonexistent unless you visit certain endpoints in Mojang's API.

Hard-deletion is when an account's username is available and its UUID appears nonexistent on all endpoints of the API.

This API aims to allow users to get information on PHD'd accounts, including their usernames and name history, given a UUID. Usernames are not supported at this time due to limitations in Mojang's own API.

These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.

### `GET /phd/:uuid`

This is currently the only endpoint for this API.

### Possible responses

If the provided UUID is PHD, the API will return HTTP status code `200 OK`. If there is an error connecting to Mojang, the API will return HTTP status code `502 Bad Gateway`, and if the specified UUID does not exist (hard-deleted or never existed) or is not PHD, the API will return HTTP status code `404 Not Found`. If the UUID is invalid, the API will return HTTP status code `400 Bad Request`. If the API is ratelimited, it will return HTTP status code `429 Too Many Requests`. For any of these possible responses, the API will set its `Content-Type` header to `application/json`.

If there is a fatal error with the Worker, the API will return an HTTP status code in the `5xx` range, most probably `500`, and set its `Content-Type` header to `text/html`. The response will contain the string `Worker threw exception` in the HTML.

Here are the different responses that can be returned:

**UUID is PHD / HTTP `200`:**
```json
{"username":"xxemilyy","uuid":"2b4c7e72328d4616b27c070bcfb257ea","name_history":[{"name":"____Luke_____"},{"name":"xxemilyy","changedToAt":1616205193165}],"phd":true}
```

**Invalid UUID / HTTP `400`:**
```json
{"error":"Invalid UUID provided. Please check if it is a valid UUIDv4."}
```

**UUID Belongs to Active Profile / HTTP `404`:**
```json
{"error":"This UUID already belongs to a player. It is not PHD."}
```

**UUID Nonexistent or Belongs to Hard-Deleted Profile / HTTP `404`:**
```json
{"error":"This UUID never existed or belongs to a hard-deleted profile."}
```

**Ratelimited / HTTP `429`:**
```json
{"error":"Currently ratelimited, try again later."}
```

**Fatal Worker Error / HTTP `500`:**

Body too long to include. Should include the string "Ray ID".

**Mojang Connection Error / HTTP `502`**:

```json
{"error":"There was an issue communicating with Mojang. Try again later!"}
```

Copyright [88](https://github.com/88) 2022, all rights reserved.
