<!--
 Copyright 2026 Google Inc. All rights reserved.

 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at

     https://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License
-->

## Integrating automatic passkey creation

Automatic passkey creation uses the WebAuthn **conditional create** API. Your
site calls `navigator.credentials.create()` with `mediation: "conditional"`, and
the password manager silently creates a passkey if its conditions are met. This
drives passkey adoption by creating a passkey at the moment the user
authenticates, without sending them to a settings page.

Make the call immediately after the user successfully authenticates with a
traditional password. The password manager checks that a saved password was used
recently, so the sooner you call it, the better the chance the conditions are
met. If your sign-in flow includes a second step, make the call once that step is
complete.

### Key integration conditions

- **Saved password:** A password for the site must be saved in the browser's
  password manager.
- **Recent password use:** The user must have recently signed in using that
  saved password.
- **No existing passkey:** There must be no existing passkey for this account in
  the password manager.
- **Immediate invocation:** Call `navigator.credentials.create()` immediately
  after password authentication completes. The available window varies by
  browser.
- **Silent error handling:** Gracefully ignore `InvalidStateError`,
  `NotAllowedError`, and `AbortError` from a conditional create call. The browser
  handles these cases silently, so surfacing them only confuses the user.
- **Skip flag verification:** The registration response returns both `UP` (user
  presence) and `UV` (user verified) as `false`. Skip both checks when you verify
  the credential on your server.

### Learning resources

- [Automatically create passkeys for your users using Conditional Create](https://developer.chrome.com/docs/identity/webauthn-conditional-create)
