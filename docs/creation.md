# Creation date API routes

# WARNING: This API endpoint is now deprecated, thanks to Mojang API issue [WEB-3367](https://bugs.mojang.com/browse/WEB-3367). If/when this issue is fixed, the endpoint will return.

### ADDITIONAL NOTE: These docs serve only as an archive. None of the methods and responses here are to be expected when reaching this endpoint.

This is currently the most accurate Minecraft account creation date API. The origin server is ratelimited after around 4 or 5 requests, proxy support is being worked on.

Credits:

-   [jomo](https://github.com/jomo): main creation date finder using the Babylonian Method
-   [citsuac](https://github.com/citsuac): giftcode logic, fixed a few bugs too
-   [tanpug](https://github.com/tanpug): testing

### `GET /creation/:username`

This is the only endpoint for this API. There really isn't anything else...

### Possible responses

The API will always use `application/json` as its `Content-Type` header. Please view the "Error codes" section for a more detailed explanation of each error code. Here are the different responses that can be returned:

**Success / HTTP `200`:** 
```json
{"username":"tanpug","creation":1485468405,"http_status_code":200}
```

**Error code `1001` / HTTP `404`:** 
```json
{"error":"The username testname2941941 isn't taken on any account.","error_code":1001,"http_status_code":404}
```

**Error code `1002` / HTTP `404`:** 
```json
{"error":"The account Chelsea has had its name taken on more than 1 account or it has a capitalization change.","error_code":1002,"http_status_code":404}
```

**Error code `1003` / HTTP `429`:**
```json
{"error":"The origin server is currently ratelimited from Mojang's API. Try again later, please!","error_code":1003,"http_status_code":429}
```

**Error code `1004` / HTTP `404`:** 
```json
{"error":"Target Notch is <= 1263146630","operation":"less_equal","error_epoch":1263146630,"error_code":1004,"http_status_code":404}
```

**Error code `1005` / HTTP `404`:** 
```json
{"error":"Target Citsuac is > 1599929362","operation":"greater","error_epoch":1599929362,"error_code":1005,"http_status_code":404}
```

**Error code `1006` / HTTP `404`:** 
```json
{"error":"The account izzy_bo_bizzy is unmigrated.","error_code":1006,"http_status_code":404}
```

### HTTP status codes

- 200: Successfully found the creation date.
- 404: Couldn't find creation date.
- 429: Origin server is ratelimited by Mojang. Wait a few minutes, then try again.

### Error codes

- 1001: The provided username isn't taken on any account.
- 1002: The provided account has had its username taken on another account before (or it had a capitalization change), making it impossible to find its creation date.
- 1003: The origin server is currently ratelimited from Mojang's API. Try again later, please!
- 1004: The provided account is most likely too old. It's most likely <= `1263146630`, meaning it was made before 2010.
- 1005: This should never be returned, if it is, the account most likely doesn't exist or there's a server-side error.
- 1006: The provided account is unmigrated, making it impossible to find its creation date.

### Caveats
You're unable to find the creation date of accounts that:

- are unmigrated (e.g `izzy_bo_bizzy`)
- have capitalization changes (e.g `DG` or `pb`)
- have a name that another account has had before (e.g `Chelsea`)
    - an exception to this is giftcode snipes or new accounts (e.g `Brad`)
- have had their name history cleared to appear like a giftcode snipe (e.g `Foxzes`)
    - the creation date that is returned for these types of accounts is always one second after the name was changed off of the old account

You're able to find the creation date of accounts that:

- have a name no one else has had before (this includes accounts with name history)    
    - example: `tanthug`, `Sun`
- giftcode snipes / new accounts
    - example: `Brad`, `Dog`, `Password`
- prename migrated accounts
    - example: `aaa`, `tanpug`, `MCBYT`

Copyright [88](https://github.com/88) 2020, all rights reserved.
