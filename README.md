![tailwind-nextjs-banner](/public/static/images/twitter-card.png)

# Tailwind Nextjs Starter Blog

[![GitHub Repo stars](https://img.shields.io/github/stars/timlrx/tailwind-nextjs-starter-blog?style=social)](https://GitHub.com/timlrx/tailwind-nextjs-starter-blog/stargazers/)
[![GitHub forks](https://img.shields.io/github/forks/timlrx/tailwind-nextjs-starter-blog?style=social)](https://GitHub.com/timlrx/tailwind-nextjs-starter-blog/network/)
[![Twitter URL](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Ftwitter.com%2Ftimlrxx)](https://twitter.com/timlrxx)
[![Sponsor](https://img.shields.io/static/v1?label=Sponsor&message=%E2%9D%A4&logo=GitHub&link=https://github.com/sponsors/timlrx)](https://github.com/sponsors/timlrx)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/git/external?repository-url=https://github.com/timlrx/tailwind-nextjs-starter-blog)

This is a [Next.js](https://nextjs.org/), [Tailwind CSS](https://tailwindcss.com/) blogging starter template. Probably the most feature-rich Next.js markdown blogging template out there. Comes out of the box configured with the latest technologies to make technical writing a breeze. Easily configurable and customizable. Perfect as a replacement to existing Jekyll and Hugo individual blogs.

Check out the documentation below to get started.

Facing issues? Check the [FAQ page](https://github.com/timlrx/tailwind-nextjs-starter-blog/wiki) and do a search on past issues. Feel free to open a new issue if none has been posted previously.

Feature request? Check the past discussions to see if it has been brought up previously. Otherwise, feel free to start a new discussion thread. All ideas are welcomed!

## Sample posts

- [A markdown guide](https://tailwind-nextjs-starter-blog.vercel.app/blog/github-markdown-guide)
- [Learn more about images in Next.js](https://tailwind-nextjs-starter-blog.vercel.app/blog/guide-to-using-images-in-nextjs)
- [A tour of math typesetting](https://tailwind-nextjs-starter-blog.vercel.app/blog/deriving-ols-estimator)
- [Simple MDX image grid](https://tailwind-nextjs-starter-blog.vercel.app/blog/pictures-of-canada)
- [Example of long prose](https://tailwind-nextjs-starter-blog.vercel.app/blog/the-time-machine)
- [Example of Nested Route Post](https://tailwind-nextjs-starter-blog.vercel.app/blog/nested-route/introducing-multi-part-posts-with-nested-routing)

```bash
npx degit 'timlrx/tailwind-nextjs-starter-blog#contentlayer'
```

or JS (official support)

```bash
npx degit https://github.com/timlrx/tailwind-nextjs-starter-blog.git
```

2. Personalize `siteMetadata.js` (site related information)
3. Modify the content security policy in `next.config.js` if you want to use
   any analytics provider or a commenting solution other than giscus.
4. Personalize `authors/default.md` (main author)
5. Modify `projectsData.js`
6. Modify `headerNavLinks.js` to customize navigation links
7. Add blog posts
8. Deploy on Vercel

## Development

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

### Compose

Run `node ./scripts/compose.js` to bootstrap a new post.

Follow the interactive prompt to generate a post with pre-filled front matter.

## Deploy

**Netlify / GitHub Pages / Firebase etc.**  
As the template uses `next/image` for image optimization, additional configurations have to be made to deploy on other popular static hosting websites like [Netlify](https://www.netlify.com/) or [GitHub Pages](https://pages.github.com/). An alternative image optimization provider such as Imgix, Cloudinary or Akamai has to be used. Alternatively, replace the `next/image` component with a standard `<img>` tag. See [`next/image` documentation](https://nextjs.org/docs/basic-features/image-optimization) for more details.

The API routes used in the newsletter component cannot be used in a static site export. You will need to use a form API endpoint provider and substitute the route in the newsletter component accordingly. Other hosting platforms such as Netlify also offer alternative solutions - please refer to their docs for more information.

## Licence

[MIT](https://github.com/timlrx/tailwind-nextjs-starter-blog/blob/master/LICENSE) © [Timothy Lin](https://www.timlrx.com)
