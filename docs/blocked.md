# Block Checker + Drop Time API Routes
This is currently the most accurate blocked username checker API. These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.
  
### `GET /blocked/:username`

This is currently the only endpoint for this API.

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

**Fatal Worker Error / HTTP `500`:**

Body too long to include.

Copyright [88](https://github.com/88) 2021, all rights reserved.
