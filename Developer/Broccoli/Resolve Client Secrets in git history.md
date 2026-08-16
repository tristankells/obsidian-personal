- Current setup triggers the following warning, need to address this instead of ignoring.

---
Push blocked because a secret was detected

[Secret scanning](https://docs.github.com/code-security/secret-scanning/protecting-pushes-with-secret-scanning) found a **Google OAuth Client ID** secret in your attempted push. 

Allowing this secret risks exposure. Instead, consider [removing the secret from your commit and commit history](https://docs.github.com/code-security/secret-scanning/working-with-secret-scanning-and-push-protection/working-with-push-protection-from-the-command-line#resolving-a-blocked-push).

Exposing this secret can allow someone to:

- Verify the identity of this **Google OAuth Client ID** secret
- Know which resources this secret can access
- Act on behalf of the secret's owner
- Push this secret to this repository without being blocked