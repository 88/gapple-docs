# CORS proxy routes
### `GET /cors/profile/:uuid`
- What is returned: Raw response from `api.mojang.com/user/profile/`, including any status codes or error messages. The only thing added is the `Access-Control-Allow-Origin` header.

### `GET /cors/username/:username`
- What is returned: Raw response from `api.mojang.com/users/profiles/minecraft/`, including any status codes or error messages. The only thing added is the `Access-Control-Allow-Origin` header.

### `GET /cors/names/:uuid`
- What is returned: Raw response from `api.mojang.com/user/profiles/:uuid/names`, including any status codes or error messages. The only thing added is the `Access-Control-Allow-Origin` header.

### `GET /cors/sessionserver/:uuid`
- What is returned: Raw response from `sessionserver.mojang.com/session/minecraft/profile/:uuid`, including any status codes or error messages. The only thing added is the `Access-Control-Allow-Origin` header.

### `GET /cors/optifine/:username`
- What is returned: An `image/png` object of the user's OptiFine cape
- On error: An `application/json` response similar to this:
```json
{"error": "No OptiFine cape was found for the account :username."}
```
- Status code: `200` on success, `404` on error.

### `GET /cors/labymod/cape/:uuid`
- What is returned: An `image/png` object of the user's LabyMod cape
- On error: An `application/json` response similar to this:
```json
{"error": "No LabyMod cape was found for the account with UUID :uuid."}
```
- Status code: `200` on success, `404` on error.

### `GET /cors/labymod/bandana/:uuid`
- What is returned: An `image/png` object of the user's LabyMod bandana
- On error: An `application/json` response similar to this:
```json
{"error": "No LabyMod bandana was found for the account with UUID :uuid."}
```
- Status code: `200` on success, `404` on error.

### `GET /cors/textures/:identifier`
- `:identifier` is the texture identifier normally passed to `https://textures.minecraft.net/texture/`.
- What is returned: An `image/png` object of the specified texture, fetched from Minecraft's texture servers.
- On error: An `application/json` response similar to this:
```json
{"error": "No Minecraft texture exists under the identifier :identifier."}
```
- Status code: `200` on success, `404` on error.

Copyright [88](https://github.com/88) 2021, all rights reserved.
