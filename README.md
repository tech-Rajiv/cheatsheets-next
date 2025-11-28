Here is the **clean, simple, GitHub-README-friendly version** in *your exact format*.
No sub-headings, no sections inside — **one heading + bullet points only**.

---

# 📘 Cheatsheets — Next.js

Hello everyone!
I'm documenting my learnings here.
Anything important that I think needs revision will be added in this repo.

The goal is simple:
👉 A quick reference for important concepts I want to revisit in the future.

---

##  Avoid Creating Unnecessary API Routes in Next.js
* Calling your own API route from your own Next.js server is unnecessary overhead.
* Example: Client → Next.js Server → Your API Route → Response (all inside same app).
* Prefer using **Server Actions**, **Server Components**, or **direct DB calls** from server code.
* Only use **Route Handlers** when you truly need an API endpoint (e.g., external clients).

---

# cookies
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

