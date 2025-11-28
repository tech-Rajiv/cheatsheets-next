
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



# 👉 cookies
* In browser-initiated first requests, we cannot add custom headers (like tokens) because the browser sends them automatically.
* CSR apps (React) work fine because user-specific authenticated requests happen *after* JS loads and can read `localStorage`.
* SSR apps (Next.js) must know the user **before rendering HTML**, so they cannot rely on `localStorage`.
* Cookies are automatically sent on every request, including the very first, making them perfect for SSR auth.
* Cookies allow the server to authenticate instantly and send personalized HTML on first load.
* Because cookies auto-send, they introduce CSRF risk — a malicious site can trigger requests using your cookies.
* Use **HttpOnly** cookies to prevent frontend JS from reading or modifying the cookie (protects against XSS).
* Use **SameSite=Lax** for safe defaults: cookies allowed on normal navigation but blocked on cross-site POST requests (prevents CSRF).
* **SameSite=Strict** is most secure but breaks login when arriving from external sites.
* **SameSite=None** sends cookies to all domains (must use Secure), used for 3rd-party integrations.
* `expiry: <seconds>` sets how long the cookie is valid.

---

