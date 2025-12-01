
# 📘 Cheatsheets — Next.js

Hello everyone!
I'm documenting my learnings here.
Anything important points about ***Nextjs*** that I think needs revision will be added in this repo.

The goal is simple:
✅ A quick reference for important concepts I want to revisit in the future.



# 👉 Next wants to know your components
* Every coomponents has to have type example 'use client' or 'use server', by default if you donot provide anything it is considered as 'use server' server-components
* In Reactjs we cannot do async components, but next can do , so we can call db and make async component take that data and generate html css js in server and serve that response
```
async function getUser() {
  return user;    // db call
}

// 2) Async Server Component
export default async function Page() {
  const user = await getUser();  // call server function

  return (
    <main>render here</main>
  );
}
```
* In React we can do waterfall effect, using useEffect but not this async function.

# 👉 Avoid Creating Unnecessary API Routes in Next.js
* Calling your own API route from your own Next.js server is unnecessary overhead.
* Example: Client → Next.js Server → Your API Route → Response (all inside same app).
* Prefer using **Server Actions**, **Server Components**, or **direct DB calls** from server code.
* Only use **Route Handlers** when you truly need an API endpoint (e.g., external clients).

# 👉 Rendering key points
Next.js does NOT automatically make your route a static site (SSG) or build-time HTML just because you didn’t use "use client".
### **The default is: “Server Component with Static Rendering (unless data decides otherwise)”**
Meaning:
- If your page has **no dynamic data**, yes → it becomes **SSG**. Server Component + no dynamic fetch = SSG
- If your page imports `fetch()` with default caching → it also becomes **SSG**. Server Component + fetch() with default caching = SSG
- If your page uses **`fetch(..., { cache: 'no-store' })`** → it becomes **SSR**.  Fetch with cache: "no-store" = SSR
- Fetch with { next: { revalidate: X } } = ISR
- If your page uses **cookies, headers, dynamic route params**, etc. → it becomes **SSR**.
- `"use client"` only makes the component run on browser — it does **not** affect SSG/SSR.
If your component uses:
- `cookies()`
- `headers()`
- `searchParams`
- dynamic `params`
- database queries inside the component
- `unstable_noStore()`
**5. Using dynamic things like above makes the route SSR**
  
# 👉 cookies
* In browser-initiated first requests, we cannot add custom headers (like tokens) because the browser sends them automatically.
* CSR apps (React) work fine because user-specific authenticated requests happen *after* JS loads and can read `localStorage`.
* SSR apps (Next.js) must know the user **before rendering HTML**, so they cannot rely on `localStorage`.
* Cookies are automatically sent on every request, including the very first, making them perfect for SSR auth.
* Because cookies auto-send, they introduce CSRF risk — a malicious site can trigger requests using your cookies.
* Use **SameSite=Lax** for safe defaults: cookies allowed on normal navigation but blocked on cross-site POST requests (prevents CSRF).
* Use **SameSite=Strict** is most secure but breaks login when arriving from external sites. banks ussualy use this.
* Use **HttpOnly** cookies to prevent frontend JS from reading or modifying the cookie (protects against XSS).
* `expiry: <seconds>` sets how long the cookie is valid.
* Your browser stores cookies from every website you visit, but… Each website gets its own private cookie storage.
*  facebook.com -	fb_session, google.com - g_session, yourapp.com	token - refresh-token. They cannot read each other's cookies.
*  When you open example.com, the browser looks at:
*  domain matches	cookie domain must match request domain
*  path matches	/api cookie won’t be sent to /auth
*  secure=true	only sent on HTTPS
*  sameSite=Lax/Strict	controls cross-site sending
*  If rules match → browser autosends only those cookies with the request.

---

