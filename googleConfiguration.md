# Google Configuration

**Step 01:** Go to https://console.developers.google.com/apis/credentials

**Step 02:** credentials -> create credentials -> OAuth client ID

**Step 03:** Application type, Name, Authorised JavaScript origins(root url->devlopment or production), Authorised redirect URIs

```javascript
For production: https://{YOUR_DOMAIN}/api/auth/callback/google
For development: http://localhost:3000/api/auth/callback/google
```
