AssemblyScript Native Messaging host

# Install dependencies

```
git clone https://github.com/guest271314/native-messaging-assemblyscript
cd native-messaging-assemblyscript
bun install assemblyscript assemblyscript/wasi-shim
```

# Compile to WASM

```
./node_modules/.bin/asc -Ospeed --config ./node_modules/@assemblyscript/wasi-shim/asconfig.json nm_assemblyscript.ts -o nm_assemblyscript.wasm
```

Adjust `nm_assemblyscript.sh` accordingly to execute the compiled WASM with a WebAssembly runtime other than `wasmtime`, e.g., `bun`, `wasmer`, et al.

# Installation and usage on Chrome and Chromium

1. Navigate to `chrome://extensions`.
2. Toggle `Developer mode`.
3. Click `Load unpacked`.
4. Select `native-messaging-assemblyscript` folder.
5. Note the generated extension ID.
6. Open `nm_assemblyscript.json` in a text editor, set `"path"` to absolute path of `nm_assemblyscript.sh` and `chrome-extension://<ID>/` using ID from 5 in `"allowed_origins"` array. 
7. Copy the file to Chrome or Chromium configuration folder, e.g., Chromium on \*nix `~/.config/chromium/NativeMessagingHosts`; Chrome dev channel on \*nix `~/.config/google-chrome-unstable/NativeMessagingHosts`.
8. To test click `service worker` link in panel of unpacked extension which is DevTools for `background.js` in MV3 `ServiceWorker`, observe echo'ed message from Bun Native Messaging host. To disconnect run `port.disconnect()`.

The Native Messaging host echoes back the message passed. 

For differences between OS and browser implementations see [Chrome incompatibilities](https://developer.mozilla.org/en-US/docs/Mozilla/Add-ons/WebExtensions/Chrome_incompatibilities#native_messaging).

# License
Do What the Fuck You Want to Public License [WTFPLv2](http://www.wtfpl.net/about/)
