## Next.js

### **NOTE: These notes refer to the current stable version 14.2**

---

### Server vs Client Components Overview

#### Server Components

- In Next.js, all components are server components by default.
- Useful for reading files or fetching data from a database.
- They **can't** use hooks or handle user interactions.

#### Client Components

- To create a client component, add `"use-client"` at the top of the component file.
- They can't read files, but can use hooks & manage interactions.

---

Main Topics:

## [Routing](./next-routing.md)
