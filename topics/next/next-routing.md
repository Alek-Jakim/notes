## Routing in Next.js (ver. 14.2)

- All routes are placed in the **app** folder (located in the **src** folder).

- Files that correspond to a route are named _page.js_ or _page.tsx_.

- Every folder corresponds to a path segment in the URL.

Examples:

- http://localhost:3000/users = "./projectRoot/src/app/users/page.tsx"

- http://localhost:3000/users/posts = "./projectRoot/src/app/users/posts/page.tsx"

---

### Dynamic Routes

- Don't know the exact segment names ahead of time? Want to create routes from dynamic data? Then look no further! Use Dynamic Segments; created by wrapping a folder's name in square brackets: [folderName].

Example:

- localhost:3000/users/1 = "./projectRoot/src/app/users/[userId]/page.tsx

```javascript
interface IUserParams {
  params: {
    // This will be whatever name you chose for the folder.
    userId: string,
  };
}

const UserPage = ({ params }: IUserParams) => {
  return <div>User {params.userId}</div>;
  // http://localhost:3000/users/3 --> User 3
};

export default UserPage;
```

---

### Nested Dynamic Routes

- Ok hotshot, you think you understand dynamic routes? Then how would you handle nested dynamic routes? We're talking crazy shit. For example:
  http://localhost:3000/users/1/posts/3.

- Well that's easy, you just go further down the rabbit whole: http://localhost:3000/users/[userId]/posts/[postId]

So the folder structure would look like this:

```
└── 📁app
    └── 📁users
        └── 📁[userId]
            └── 📁posts
                └── 📁[postId]
                    └── page.tsx
                └── page.tsx
            └── page.tsx
        └── page.tsx
    └── globals.css
    └── layout.tsx
    └── page.tsx
```

---

### Catch-all Segments

- Dynamic Segments can be extended to catch-all subsequent segments by adding an ellipsis inside the brackets [...folderName]. Now, you're probably thinking "What the f\*\*\* does that even mean?"

- Well, instead of creating a new file for every possible URL, you create one file that can handle many different URL variations. This is helpful if you don't know exactly how many parts a URL might have or if it changes.

- Here's an example. Let's say you are building a documentation page for multiple features & concepts. The url would be something like `http://localhost:3000/docs/feature1/concept3`

- If you created 20 different `page.tsx` files for every feature & concept, that would equal to **400** files, which is nuts.

- 20 Features X 20 Concepts = 400 files
- 20 Features X 1 [conceptId] = 20 files
- 1 [featureId] X 1 [conceptId] = 1 file

- That last one seems kinda cool, no? Well, keep in mind that each new segment would require additional nesting. So `http://localhost:3000/docs/feature1/concept3/example5` would be: 1 [featureId] X 1 [conceptId] X 1[exampleId]. Grab my binary hand and let me show you a better way to do this shit.

- In the `docs` folder, just add a new folder called `[...slug]` (slug is a standard naming convention), and inside the `[...slug]` folder add a `page.tsx` file. It should look like this.

```javascript
const DocsPage = ({
  params,
}: {
  params: {
    // http://localhost:3000/docs/feature1/concept3 --> ["feature1", "concept3"]
    slug: string[],
  },
}) => {
  if (params.slug?.length === 2) {
    return (
      <h1>
        Viewing docs for {params.slug[0]} and {params.slug[1]}
      </h1>
    );
  } else if (params.slug?.length === 1) {
    return <h1>Viewing docs for {params.slug[0]}</h1>;
  }
  return <div>DocsPage</div>;
};

export default DocsPage;
```

- If you go to `http://localhost:3000/docs` (presuming there's no "./app/docs/page.tsx" file.), you'll get a big, fat 404 - Page Not Found. To prevent that shit, just rename the `[...slug]` folder to [[...slug]]. This is called **Optional Catch-all Segment**, if you wanna get all fancy. It just means that `/docs` is also matched.
