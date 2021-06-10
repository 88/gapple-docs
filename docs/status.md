# Account Status API Routes

This is currently the most accurate Minecraft account status API. These docs aim to serve as a guide on how to use this API and what responses can possibly be returned.

**NOTE:** There may be a few extra JSON key/value pairs returned in these responses for debug purposes. Do not check the exact page content for responses! Please decode the JSON and check the individual `status` key or `error` key.

### `GET /status/:username`

This is currently the only endpoint for this API.

### Possible responses

The API will almost always return HTTP status code `200 OK`. If there is an error connecting to Mojang, the API will return HTTP status code `502 Bad Gateway`, and if the specified user does not exist, the API will return HTTP status code `404 Not Found`. For any of these possible responses, the API will set its `Content-Type` header to `application/json`.

If there is a fatal error with the Worker, the API will return an HTTP status code in the `5xx` range, most probably `500`, and set its `Content-Type` header to `text/html`. The response will contain the string `Worker threw exception` in the HTML.

Here are the different responses that can be returned:

**Status Found / HTTP `200`:**

```json
// New Microsoft Account (MSA)
{"username":"mypasswordis0000","uuid":"8ce07be3e365441aaa4301893041c64e","status":"new_msa"}

// Migrated Microsoft Account (MSA)
{"username":"Gr8_Escape", "uuid":"6d752bb0ef41432a825a4d44185de121", "status":"migrated_msa"}

// Can't tell what type of MSA it is
{"username":"testuser","uuid":"9abd218f2b374bfa96d904eb074afdb7","status":"msa"}

// Mojang Account
{"username":"D__G", "uuid":"c7b3d49c580c4af2a824ca07b37ff2f9", "status":"mojang"}

// Unmigrated Account (Legacy)
{"username":"Tremendous", "uuid":"7d96137e15a24f09b79f2366199d822e", "status":"legacy"}
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
