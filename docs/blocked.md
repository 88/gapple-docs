# Block Checker + Drop Time API Routes
This is currently the most accurate blocked username checker API. These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.
  
### `GET /blocked/:username`

This is currently the only endpoint for this API.

You can send UUIDs to the endpoint as well, however it will only respond with the "Username Taken" response if the UUID is assigned to a profile. Otherwise it will error out with the "UUID Supplied Instead of Username" response.

### Possible responses

The API will almost always return HTTP status code `200 OK` and set its `Content-Type` header to `application/json`.

If there is a fatal error with the Worker, the API will return an HTTP status code in the `5xx` range, most probably `500`, and set its `Content-Type` header to `text/html`. The response will contain the string `Worker threw exception` in the HTML.

Here are the different responses that can be returned:

**Username Taken / HTTP `200`:**
```json
{"status":"taken"}
```

**Username Available / HTTP `200`:**
```json
{"status":"available"}
```

**Username Dropping Soon / HTTP `200`:**
```json
{"status":"soon","drop_time":"2021-03-03T16:07:17.000Z"}
```

**Username Blocked / HTTP `200`:**
```json
{"status":"blocked"}
```

**Username Invalid / HTTP `200`:**
```json
{"status":"invalid"}
```

**UUID Supplied Instead of Username / HTTP `400`:**
```json
{"error":"uuid_supplied_use_username"}
```

**Fatal Worker Error / HTTP `500`:**

Body too long to include.

**Mojang Connection Error / HTTP `502`:**
```json
{"error":"Mojang connection error. Please try again later!"}
```

Copyright [88](https://github.com/88) 2021, all rights reserved.
