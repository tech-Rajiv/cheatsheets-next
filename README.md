# 📘 Cheatsheets — Next.js

Hello everyone!  
I'm documenting my learnings here.  
Anything important that I think needs revision will be added in this repo.

The goal is simple:  
👉 A quick reference for important concepts I want to revisit in the future.

---

## 🚫 Avoid Creating Unnecessary API Routes in Next.js

When you do this:

**Client → Next.js Server → Your Own API Route → Response to Client**

…you’re basically calling yourself unnecessarily.

### ✔️ Instead Use:
- **Server Actions**
- **Server Components**
- **Direct DB Calls in Server Functions**
- **Route Handlers only when truly needed**

---

# cookies

Here are **clean, short, accurate bullet points** you can paste directly into your notes 👇

---

# 🔑 **Important Notes — Auth in CSR vs SSR & Why Cookies Are Needed**

### **Client-side Rendered Apps (React)**

* First request loads HTML, CSS, JS — **same for everyone**, no auth needed.
* You **cannot** send tokens in headers on this first request.
* After JS loads, React can read `localStorage` and send authenticated requests manually.
* Auth works because the **user-specific fetch happens later**, not during initial page load.

---

### **Server-side Rendered Apps (Next.js)**

* Server must know the user **before rendering HTML** for the first request.
* SSR code **cannot access localStorage**, sessionStorage, or browser memory.
* Therefore, no user token is available unless it comes from the request headers.
* Only **cookies are automatically sent by the browser** on every request, including the first.
* So SSR apps must use **cookies for authentication**, not localStorage.

---

# 🍪 **Why Cookies Solve the Problem**

* Cookies are automatically included in every request made to your domain.
* Server receives the cookie → validates user → renders personalized HTML immediately.
* Works perfectly with SSR, API routes, middleware, and server components.

---

# 🛡 **CSRF Risk (Cross-Site Request Forgery)**

* Because cookies are auto-sent, a malicious website can trigger requests on the user’s behalf.
* Browser will attach your cookies → server thinks it’s you → dangerous.

---

# 🧷 **Cookie Security Attributes**

### **1. HttpOnly**

* Prevents JS from reading or modifying cookies.
* Protects against XSS attacks stealing your token.

### **2. SameSite**

* Controls when cookies are sent in cross-site requests.

**Options:**

* **SameSite=None** → Cookies sent to all domains; required for third-party usage; must use `Secure`.
* **SameSite=Strict** → Most secure but breaks login when arriving from external links.
* **SameSite=Lax** (Recommended/Default) →

  * Cookies allowed when navigating normally (clicking links).
  * Cookies blocked for cross-site POST → prevents CSRF attacks.
 
### **2. expiry**

* **expiry: 60**  → Cookie has expiry in secods
---



  

