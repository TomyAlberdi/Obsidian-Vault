Created: 2025-09-24 15:16
## Family Tree:
1. NextJS
2. [[Week One]]
-- -
Next.js uses **file-system based routing**, meaning you can use folders and files to define routes. This page will guide you through how to create layouts and pages, and link between them.
## Creating a Page
A **page** is UI that is rendered on a specific route. To create a page, add a `page` file inside the app directory and default export a React component. For example, to create an index page (`/`):
![[page-special-file.avif]]
```tsx
export default function Page() {
  return <h1>Hello Next.js!</h1>
}
```
## Creating a Layout
A layout is UI that is **shared** between multiple pages. On navigation, layouts preserve state, remain interactive, and do not rerender.
You can define a layout by default exporting a React component from a `layout` file. The component should accept a `children` prop which can be a page or another layout.
For example, to create a layout that accepts your index page as child, add a `layout` file inside the `app` directory:
![[layout-special-file.avif]]
```tsx
export default function DashboardLayout({
  children,
}: {
  children: React.ReactNode
}) {
  return (
    <html lang="en">
      <body>
        {/* Layout UI */}
        {/* Place children where you want to render a page or nested layout */}
        <main>{children}</main>
      </body>
    </html>
  )
}
```
The layout above is called a root layout because it's defined at the root of the `app` directory. The root layout is **required** and must contain `html` and `body` tags.
