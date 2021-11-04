# Account Status API Routes

## NOTE: We have migrated to use UUIDs as a parameter instead of usernames. Please update your projects accordingly.

This is currently the most accurate Minecraft account status API. These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.

**NOTE:** There may be a few extra JSON key/value pairs returned in these responses for debug purposes. Do not check the exact page content for responses! Please decode the JSON and check the individual `status` key or `error` key.

### `GET /status/:uuid`

This is currently the only endpoint for this API.

### Possible responses

The API will almost always return HTTP status code `200 OK`. If you did not input a valid UUIDv4, the API will return HTTP status code `400 Bad Request`. If there is an error connecting to Mojang, the API will return HTTP status code `502 Bad Gateway`, and if the specified user does not exist, the API will return HTTP status code `404 Not Found`. For any of these possible responses, the API will set its `Content-Type` header to `application/json`.

If there is a fatal error with the Worker, the API will return an HTTP status code in the `5xx` range, most probably `500`, and set its `Content-Type` header to `text/html`. The response will contain the string `Worker threw exception` in the HTML.

Here are the different responses that can be returned:

**Status Found / HTTP `200`:**

```json
// NOTE: these responses are placeholders, the information here does not reflect the actual account status for some accounts. please actually use the API to check the statuses if you need to know the status of an account listed here.

// New Microsoft Account (MSA)
{"username":"FunClock1564643","uuid":"aae41b6ff5ce48ba9598f55ed2c81fa3","status":"new_msa"}

// Migrated Microsoft Account (MSA)
{"username":"D__G","uuid":"c7b3d49c580c4af2a824ca07b37ff2f9","status":"migrated_msa"}

// Can't tell what type of MSA it is
{"username":"RyanToysReview","uuid":"416e3d9f71db49ec8c787e8eec740506","status":"msa"}

// Mojang Account
{"username":"Ined","uuid":"bec2968f48ab4504a7b4bde54a789bdb","status":"mojang"}

// Unmigrated Account (Legacy)
{"username":"CREAPER_12","uuid":"1185081a0042432588af257b1ee91bb0","status":"legacy"}
```

**Username Supplied / HTTP `400`**:
```json
{"error":"username_supplied_use_uuid","cause":"we are no longer accepting usernames as a parameter for this endpoint, please switch to UUIDs instead."}
```

**User Not Found / HTTP `404`**:

```json
{"status":"nonexistent"}
```

**Fatal Worker Error / HTTP `500`:**

Body too long to include. Should include the string "Ray ID".

**Mojang Connection Error / HTTP `502`**:

```json
{"error":"There was an issue communicating with Mojang or the provided name was invalid. Try again later!"}
```

Copyright [88](https://github.com/88) 2021, all rights reserved.
