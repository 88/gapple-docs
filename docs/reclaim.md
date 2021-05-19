# Reclaim Detection API docs
Minecraft accounts have a 30-day name change cooldown, meaning they cannot change their names to something else before 30 days have passed. If a username has been changed off of a Minecraft account, it has a 37-day cooldown until the name "drops" to the public. This gives the owner, with their 30-day cooldown, 7 days to change their name back before it "drops". If they choose to change it back, this is known as "reclaiming" the username.

This API's purpose is to estimate if a dropping Minecraft username is a "reclaim". These docs will guide users through how to use this API and what responses can possibly be returned.

### `GET /reclaim/:name_to_check?account=:current_name`
This is the only endpoint for this API.

Parameters are as follows:
- **`name_to_check`** - the username you want to check for reclaims
- **`current_name`** - the current username of the account

### Possible responses

The API will almost always return HTTP status code `200 OK` and set its `Content-Type` header to `application/json`.

If the Mojang API errors out, the API will return HTTP status code `502 Bad Gateway`. The `Content-Type` header will remain `application/json`.

If the user you provide doesn't exist, the API will return HTTP status code `404 Not Found`, and the `Content-Type` header will remain `application/json`.

If there is a fatal error with the Worker, the API will return an HTTP status code in the `5xx` range, most probably `500`, and set its `Content-Type` header to `text/html`. The response will contain the string `Worker threw exception` in the HTML.

Here are the different responses that can be returned:

**Possible Reclaim / HTTP `200`:**
```json
{"reclaim_probability":"possible"}
```

**Low Chance of Reclaim / HTTP `200`:**
```json
{"reclaim_probability":"low"}
```

**Impossible Chance of Reclaim / HTTP `200`:**
```json
{"reclaim_probability":"impossible"}
```

**User Does Not Exist / HTTP `404`:**
```json
{"error":"That user doesn't exist. Are you sure you typed the username correctly?"}
```

**Fatal Worker Error / HTTP `500`:**

Body too long to include. Should include the string "Ray ID".

**Bad Mojang Response: First Stage / HTTP `502`:**
```json
{"error":"Mojang API gave us a bad response on the 1st stage. Try again later!"}
```

**Bad Mojang Response: Second Stage / HTTP `502`:**
```json
{"error":"Mojang API gave us a bad response on the 2nd stage. Try again later!"}
```

Copyright [88](https://github.com/88) 2021, all rights reserved.
