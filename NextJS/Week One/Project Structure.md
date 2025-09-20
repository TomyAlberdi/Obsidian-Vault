Created: 2025-09-20 19:31
## Family Tree:
1. NextJS
2. [[Week One]]
-- -
This page provides an overview of **all** the directory and file conventions in Next.js, and recommendations for organizing your project.
## Directory and File conventions
### Top-Level Directories
These are used to organize your application's code and static assets.
- `app`: App Router
- `pages`: Pages Router
- `public`: Static assets
- `src`: Optional app and pages source directory.
#### `App` directory
Next.js uses file-system routing, which means the routes in your application are determined by how you structure your files.
Inside `app` there's a `layout.tsx` file. This file is the root layout. It's required and must contain the `<html>` and `<body>` tags.
```tsx
export default function RootLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  )
}
```
There's also a home page `app/page.tsx` with some initial content:
```tsx
export default function Page() {
  return <h1>Hello, Next.js!</h1>
}
```
Both `layout.tsx` and `page.tsx` will be rendered when the user visits the root of your application (`/`).
#### `Public` directory
Create a `public` folder at the root of your project to store static assets such as images, fonts, etc. Files inside `public` can then be referenced by your code starting from the base URL (`/`).
You can then reference these assets using the root path (`/`). For example, `public/profile.png` can be referenced as `/profile.png`.

### Top-Level Files
Top-level files are used to configure your application, manage dependencies, run middleware, integrate monitoring tools, and define environment variables.
- `next.config.js`: Configuration file for Next.js.
- `package.json`: Project dependencies and scripts.
- `instrumentation.ts`: OpenTelemetry and Instrumentation file.
- `middleware.ts`: Next.js request middleware.
- `.env`: Environment variables.
- `.env.local`: Local environment variables.
- `.env.production`: Production environment variables.
- `.env.development`: Development environment variables.
- `.eslintrc.json`: Configuration file for ESLint.
- `.gitignore`: Git files and directories to ignore.
- `next-env.d.ts`: TypeScript declaration file for Next.js.
- `tsconfig.json`: Configuration file for TypeScript.
- `jsconfig.json`: Configuration file for JavaScript.
### Routing Files
- `layout`
- `page`
- `loading`
- `not-found`
- `error`
- `global-error`
- `route`: API endpoint.
- `template`: Re-rendered layout.
- `default`: Parallel route fallback page.
### Nested Routes
Directories define URL segments. Nesting directories nests segments. Layouts at any level wrap their child segments. A route becomes public when a `page` or `route` file exists. Examples:
- `app/layout.tsx`: Route layout wraps all routes.
- `app/blog/layout.tsx`: Wraps `/blog` and descendants.
- `app/page.tsx`: Public route `/`.
- `app/blog/page.tsx`: Public route `/blog`.
- `app/blog/authors/page.tsx`: Public route `/blog/authors`.
### Dynamic Routes
Parameterize segments with square brackets. Use `[segment]` for a single param, `[...segment]` for catch-all, and `[[...segment]]` for optional catch-all. Access values via the `params` prop. For example:
- `app/blog/[post]/page.tsx`: `/blog/my-first-post`
- `app/shop/[...article]/page.tsx`: `/shop/clothing/shoes`, `/shop/clothing/shirts`.
- `app/docs/[[...article]]/page.tsx`: `/docs`, `/docs/layouts-and-pages`, `/docs/api-references/use-routes`.
### Route Groups and private directories
Organize code without changing URLs with route groups `(group)`, and colocate non-routable files with private directories `_directory`.
- `app/(marketing)/page.tsx`: Group omitted from URL.
- `app/(shop)/cart/page.tsx`: URL `/cart`, share layouts within `(shop)`
- `app/blog/_components/Post.tsx`: Not routable, safe place for UI utilities.
- `app/blog/_lib/data.ts`: Not routable, safe palce for utils.
### Parallel and Intercepted Routes
These features fit specific UI patterns, such as slot-based layouts or modal routing.
Use `@slot` for named slots rendered by a parent layout. Use intercept patterns to render another route inside the current layout without changing the URL, for example, to show a details view as a modal over a list.

| **Pattern (docs)**  | **Meaning**          | **Typical use case**                 |
| ------------------- | -------------------- | ------------------------------------ |
| `@directory`        | Named slot           | Sidebar + main content               |
| `(.)directory`      | Intercept same level | Preview sibling route in a model     |
| `(..)directory`     | Intercept parent     | Open parent child as overlay         |
| `(..)(..)directory` | Intercept two levels | Deeply nested overlay                |
| `(...)directory`    | Intercept from root  | Show arbitrary route in current view |
## Organizing your project
Next.js is **unopinionated** about how you organize and colocate your project files. But it does provide several features to help you organize your project.
### Component Hierarchy
The components defined in special files are rendered in a specific hierarchy:
- `layout.js`
- `template.js`
- `error.js` (React error boundary)
- `loading.js` (React suspense boundary)
- `not-found.js` (React error boundary)
- `page.js` or nested `layout.js`
![[file-conventions-component-hierarchy.avif]]
The components are rendered recursively in nested routes, meaning the components of a route segment will be nested **inside** the components of its parent segment.
![[nested-file-conventions-component-hierarchy.avif]]
### Colocation
In the `app` directory, nested folders define route structure. Each folder represents a route segment that is mapped to a corresponding segment in a URL path.
However, even though route structure is defined through folders, a route is **not publicly accessible** until a `page.js` or `route.js` file is added to a route segment.
![[project-organization-not-routable.avif]]
And, even when a route is made publicly accessible, only the **content returned** by `page.js` or `route.js` is sent to the client.
This means that **project files** can be **safely colocated** inside route segments in the `app` directory without accidentally being routable.
![[project-organization-colocation.avif]]
While you **can** colocate your project files in `app` you don't **have** to. If you prefer, you can keep them outside the `app` directory.
### Private folders
Private folders can be created by prefixing a folder with an underscore: `_folderName`
This indicates the folder is a private implementation detail and should not be considered by the routing system, thereby **opting the folder and all its subfolders** out of routing.
![[project-organization-private-folders.avif]]
Since files in the `app` directory can be safely colocated by default, private folders are not required for colocation. However, they can be useful for:
- Separating UI logic from routing logic.
- Consistently organizing internal files across a project and the Next.js ecosystem.
- Sorting and grouping files in code editors.
- Avoiding potential naming conflicts with future Next.js file conventions.
### Route groups
Route groups can be created by wrapping a folder in parenthesis: `(folderName)`
This indicates the folder is for organizational purposes and should **not be included** in the route's URL path.
![[project-organization-route-groups.avif]]
Route groups are useful for:
- Organizing routes by site section, intent, or team. e.g. marketing pages, admin pages, etc.
- Enabling nested layouts in the same route segment level.
