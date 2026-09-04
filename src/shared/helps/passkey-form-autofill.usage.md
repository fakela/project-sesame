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

## Passkey form autofill

Passkey form autofill, also called conditional UI, allows a single sign-in form
to handle both passkeys and passwords. This page demonstrates that flow, along
with how the WebAuthn
[Signal API](https://developer.chrome.com/docs/identity/webauthn-signal-api)
cleans up invalid or orphaned passkeys.

### How to test it

1. Click or tap the username field to trigger the browser's autofill
   suggestions.
2. If you have credentials saved in your password manager for this site:
   - **Select a saved password**: The username fills in automatically. Click
     **Continue** to move to the password step.
   - **Select a saved passkey**: A browser verification prompt appears.
     Complete the verification to sign in.
3. If you don't have a passkey or an account yet, enter any username and click
   **Continue**. On the next page, enter any password to register. The password
   is ignored, but the step simulates a traditional sign-up flow.

### WebAuthn Signal API demo

If the server rejects a passkey sign-in because it cannot find the matching
public key, for example because you deleted the credential from your account
settings while the passkey remains in your password manager, the server uses the
WebAuthn Signal API to notify the browser. Your password manager then deletes
the invalid passkey, so it no longer appears as an option.
