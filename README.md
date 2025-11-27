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



