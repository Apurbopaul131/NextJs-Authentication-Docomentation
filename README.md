# NextJs-Authentication-Docomentation

### Step 01: Install NextAuth

```javascript
npm install next-auth
```

### Step 02: Create route.ts file in /app/api/auth/[...nextauth]/route.ts

```javascript
// /app/api/auth/[...nextauth]/route.ts
import NextAuth from "next-auth"

const handler = NextAuth({
  ...
})

export { handler as GET, handler as POST }

```

### Step 03: Create authOptions.ts file inside the /src/uitls/authOptions.ts and add auth options

```javascript
import NextAuth from "next-auth";

export const authOptions = {
  // Configure one or more authentication providers
  providers: [],
};

export default NextAuth(authOptions);
```

### Github Authentication

### Step 01: Set Github provider option inside the provider array in /app/api/auth/[...nextauth]/route.ts

```javascript
import NextAuth from "next-auth";
import GitHubProvider from "next-auth/providers/github";
export const authOptions = {
  // Configure one or more authentication providers
  providers: [
    GitHubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
  ],
};

export default NextAuth(authOptions);
```

### Step 02: Go to https://github.com/settings/developers docs and Create oAtuh app

### Step 03: Generate clientId and client secret

### Step-04: Setup onClick handler into button and setup callbackurl to redirect dashboard after authentitcation

```javascript
 onClick={() =>
                signIn("github", {
                  callbackUrl: "http://localhost:3000/dashboard",
                })
              }
```
