# NextJs-Authentication-Docomentation

**Step 01:** Install NextAuth

```javascript
npm install next-auth
```

**Step 02:** Create route.ts file in /app/api/auth/[...nextauth]/route.ts

```javascript
// /app/api/auth/[...nextauth]/route.ts
import NextAuth from "next-auth"

const handler = NextAuth({
  ...
})

export { handler as GET, handler as POST }

```

**Step 03:** Create authOptions.ts file inside the /src/uitls/authOptions.ts and add auth options

```javascript
import NextAuth from "next-auth";
import { NextOptions } from "next-auth";
export const authOptions: NextAuthOptions = {
  // Configure one or more authentication providers
  providers: [],
};

export default NextAuth(authOptions);
```

### Github Authentication

**Step 01:** Set Github provider option inside the provider array in /app/api/auth/[...nextauth]/route.ts

```javascript
import NextAuth from "next-auth";
import { NextOptions } from "next-auth";
import GitHubProvider from "next-auth/providers/github";
export const authOptions:NextAuthOptions = {
  // Configure one or more authentication providers
  providers: [
    GitHubProvider({
      clientId: process.env.GITHUB_ID as string,
      clientSecret: process.env.GITHUB_SECRET as string,
    }),
  ],
};

export default NextAuth(authOptions);
```

**Step 02:** Go to https://github.com/settings/developers docs and Create oAtuh app

**Step 03:** Generate clientId and client secret

**Step-04:** Setup onClick handler into button and setup callbackurl to redirect dashboard after authentitcation

```javascript
 onClick={() =>
                signIn("github", {
                  callbackUrl: "http://localhost:3000/dashboard",
                })
              }
```

### Session in Server Components

Firstly, add AuthSecret inside the auth options

```javascript
import NextAuth from "next-auth";
import GitHubProvider from "next-auth/providers/github";
import { NextOptions } from "next-auth";

export const authOptions:NextAuthOptions = {
  // Configure one or more authentication providers
  providers: [
    GitHubProvider({
      clientId: process.env.GITHUB_ID,
      clientSecret: process.env.GITHUB_SECRET,
    }),
    secret:process.env.NEXTAUTH_SECRET
  ],
};
```

It is also similar in all server components. Use the same function as mentioned above.

```javascript
await getServerSession(authOptions);
```

### signOut functionality in next Auth

Call signOut method in onClick event,

```javascript
import { signOut } from "next-auth/react";
<button onClick={() => signOut()}>sign out</button>;
```

### Google Authentication

**Step 01:** Set Google provider option inside the provider array in /app/api/auth/[...nextauth]/route.ts

```javascript
import NextAuth from "next-auth";
import GoogleProvider from "next-auth/providers/google";
import { NextOptions } from "next-auth";
export const authOptions = {
  // Configure one or more authentication providers
  providers: [
    GoogleProvider({
      clientId: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
    }),
  ],
};

export default NextAuth(authOptions);
```

**Step 02:** Go to https://console.cloud.google.com/apis/credentials?project=nextjs-authentication-450913 docs and Create oAtuh app

**Step 03:** Generate clientId and client secret

**Step-04:** Setup onClick handler into button and setup callbackurl to redirect dashboard after authentitcation

```javascript
 onClick={() =>
                signIn("google", {
                  callbackUrl: "http://localhost:3000/dashboard",
                })
              }
```

### Private route using NextJs middleware

The most simple usage is when you want to require authentication for your entire site. You can add a middleware.js file in src directory with the following:

```javascript
export { default } from "next-auth/middleware";
```

That's it! Your application is now secured. 🎉

If you only want to secure certain pages, export a config object with a matcher:

```javascript
export { default } from "next-auth/middleware";

export const config = { matcher: ["/dashboard"] };
```

Now you will still be able to visit every page, but only /dashboard will require authentication.

If a user is not logged in, the default behavior is to redirect them to the sign-in page.

If you want to ommit the default behaviour then add the bellow object in the auth options

```javascript
pages: {
    signIn: "/login",
  }
```
