# Block Checker + Drop Time API Routes
This API's purpose is to check if Minecraft usernames are blocked, taken, available, or dropping soon. These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.

**NOTE:** There may be a few extra JSON key/value pairs returned in these responses for debug purposes. Do not check the exact page content for responses! Please decode the JSON and check the individual `status` key or `error` key.

**NOTE:** This API is not to be trusted for droptimes. Its main purpose was to check for blocked usernames and its functionality was changed to scrape NameMC for droptimes later in its lifetime. Now that NameMC has better scraping protection, this endpoint is **not** reliable for droptimes anymore. Please do **NOT** use this API for reliable droptimes!
  
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

**Username Blocked OR Dropping / HTTP `200`:**
```json
{"status":"blocked_or_dropping","error":"Error while checking if the name is dropping. Please try again later!"}
```

**UUID Supplied Instead of Username / HTTP `400`:**
```json
{"error":"uuid_supplied_use_username"}
```

**Droptime Fetch Ratelimit / HTTP `429`:**
```json
{"status":"blocked_or_dropping","error":"Ratelimit while checking if the name is dropping. Please try again later!"}
```

**Fatal Worker Error / HTTP `500`:**

Body too long to include. Should include the string "Ray ID".

**Mojang Connection Error / HTTP `502`:**
```json
{"error":"Mojang connection error. Please try again later!"}
```

Copyright [88](https://github.com/88) 2022, all rights reserved.
