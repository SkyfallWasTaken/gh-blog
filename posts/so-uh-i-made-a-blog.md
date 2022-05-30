# So, uh, I made a blog
<summary>I made a cool blog using GitHub and CF Workers. In fact, you're looking at it right now!</summary>

Personally, I wanted something _better_ than WordPress, Ghost or Jekyll.

Something that looks hot and is easy to use, but isn't a slow mess.

Recently I found [utteranc.es](https://utteranc.es/), a cool little platform that lets you use GitHub Issues for blog post comments! One day, I had an idea:

💡 **What if we used GitHub for _blog posts?_**

It's not a bad idea, I thought. Obviously, (a) it's been done before (with Jekyll), and (b) it's not the _best_ editing experience. Assets, for instance, need to be uploaded to a special `assets` folder to be used. But it's not _awful_, so I thought to myself: Hey, let's give it a shot!

## How do we do this?
With GitHub Actions!

Basically:
- I write a blog post and push it to the posts repository,
- GitHub Actions:
  - converts it to HTML
  - optimizes assets and pushes these to the `assets_optimized` folder
  - changes asset URLs to point to the optimized ones
  - lets my CF Worker know about the new blog post as well as the BlurHash for the photos,
- The Worker does preprocessing and stuff and saves the template as well as the metadata to Workers KV.

Whenever someone (like you!) visits the site, the Worker injects some JS (for the BlurHashed images, which isn't necessary, so you don't actually need it!) into the result and serves it to the user.

Nice and fast! 
