# Notes

## Client-Side Navigation

You create routes as files under pages and use the built-in Link component. No routing libraries are required.

The Link component enables client-side navigation between two pages in the same Next.js app.<br>
Client-side navigation means that the page transition happens using JavaScript, which is faster than the default navigation done by the browser. Browser does not load the full page and client-side navigation is working.

## Code Splitting and Prefetching

Next.js does code splitting automatically, so each page only loads what’s necessary for that page. That means when the homepage is rendered, the code for other pages is not served initially.

Furthermore, in a production build of Next.js, whenever Link components appear in the browser’s viewport, Next.js automatically prefetches the code for the linked page in the background.

If you need to add attributes like, for example, className, add it to the a tag, not to the Link tag.
```
<Link href="/">
  <a className="foo" target="_blank" rel="noopener noreferrer">
    Hello World
  </a>
</Link>
```

## Assets, Metadata, and CSS

If you want to customize the &lt;html&gt; tag, for example to add the lang attribute, you can do so by creating a pages/_document.js file.

CSS Modules, automatically generates unique class names. For using it, you have to open CSS file under component that name is like blabla.module.css. And the style can be used after importing in component and defined inside className.

```
import styles from './layout.module.css';

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>;
}
```

In Next.js, you can add global CSS files by importing them from pages/_app.js. You cannot import global CSS anywhere else.

## Styling Tips

https://nextjs.org/learn/basics/assets-metadata-css/styling-tips

## Pre-rendering and Data Fetching

Next.js pre-renders every page. This means that Next.js generates HTML for each page in advance, instead of having it all done by client-side JavaScript. Pre-rendering can result in better performance and SEO.

Next.js pre-renders the app into static HTML, allowing you to see the app UI without running JavaScript. Therefore, you would see the same page when disabled JS on browser.

## Two Forms of Pre-rendering

- Static Generation is the pre-rendering method that generates the HTML at build time. The pre-rendered HTML is then reused on each request.
- Server-side Rendering is the pre-rendering method that generates the HTML on each request.

```
Note: In development mode, getStaticProps runs on each request instead.
```

```
You might have noticed that each markdown file has a metadata section at the top containing title and date. This is called YAML Front Matter, which can be parsed using a library called gray-matter.
```

In Next.js, the lib folder does not have an assigned name like the pages folder, so you can name it anything. It's usually convention to use lib or utils.

## Using Static Generation (getStaticProps())

https://nextjs.org/learn/basics/data-fetching/getstaticprops-details

To use Server-side Rendering, you need to export getServerSideProps instead of getStaticProps from your page.

## Client-side Rendering

If you do not need to pre-render the data, you can also use the following strategy (called Client-side Rendering):

- Statically generate (pre-render) parts of the page that do not require external data.
- When the page loads, fetch external data from the client using JavaScript and populate the remaining parts.

This approach works well for user dashboard pages, for example.

## SWR

Next.js has created a React hook for data fetching called SWR. We highly recommend it if you’re fetching data on the client side. It handles caching, revalidation, focus tracking, refetching on interval, etc.


## Dynamic Routes

In pages/posts/[id].js, we’ll write code that will render a post page

```
import Layout from '../../components/layout';

export default function Post() {
  return <Layout>...</Layout>;
}

export async function getStaticPaths() {
  // Return a list of possible value for id
}

export async function getStaticProps({ params }) {
  // Fetch necessary data for the blog post using params.id
}
```
getAllPostIds function must return an array of objects. Each object must have the params key and contain an object with the id key. Returns an array that looks like this:

```
[
  {
    params: {
      id: 'ssg-ssr'
    }
  },
  {
    params: {
      id: 'pre-rendering'
    }
  }
]
```

https://nextjs.org/learn/basics/dynamic-routes/dynamic-routes-details

## API Routes




# HANDLE posts.js LATER AND tsconfig.json (include part) TURN IT TO TS. 
Layout home olayı da biraz muallak boolean ama neye göre

# Libraries

- gray-matter
- remark, remark-html
- date-fns


# Default

This is a [Next.js](https://nextjs.org/) project bootstrapped with [`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.tsx`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.ts`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
