# lazy-load-bg-video

Lazy loading background videos in Webflow with vanilla-lazyload

Clone an example site from Made in Webflow:

https://webflow.com/made-in-webflow/website/background-vid-test

## vanilla-lazyload

[vanilla-lazyload](https://github.com/verlok/vanilla-lazyload) is a super lightweight JavaScript library to help lazy load videos using the Intersection Observer API (which isn't compatible with [older browsers](https://caniuse.com/?search=intersectionObserver)).

If you need to support older browsers, you can look into [yall.js](https://github.com/malchata/yall.js) (Yet Another Lazy Loader).

For a good overview on why you may want to lazy load videos and the strategy do so, please review:

https://web.dev/lazy-loading-video/

The tldr; lazy loading videos will help with site performance for background video elements below the fold, especially on mobile devices.

## How it's done

### The HTML

First, you're going to want [a page in your style guide](https://webflow.com/blog/how-to-build-a-living-style-guide-in-webflow) dedicated to components where the native Webflow element can permanently live.

Add in your background video element here and style it however you like. Once complete, publish the page and then open the live site where the element lives.

Right click to inspect it and once you have it selected in dev tools. Right click and copy the element.

Now we need to modify the code a little bit so paste this into an IDE, a Webflow embed block, or a plain text editor.

On the video element we'll add a `class="lazy` and `preload="none"`. Then on the sources inside it, we'll change the `src` of the video to `data-src` and add `type="video/mp4"`. Of course you'll want the type to match, so set `webm` for WebM videos or `ogg` for OGG files.

You can see the diff between what we copied and what was changed here:

https://github.com/Webflow-Examples/lazy-load-bg-video/commit/e2fc3fe889ffd7b80b4697f353ba330bfac97124

Once you have that copy the code and go to the page in Webflow where you want the background video element to live and add a `Embed` block to your canvas. Now paste in the code.

### The JavaScript

Now you'll want to download the library and upload it somewhere and include it in the `before` body section of your page. You can [get a CDN link from the GitHub repo](https://github.com/verlok/vanilla-lazyload#-getting-started---script).

When adding to your project, you can use async:

```html
<script
  async
  src="https://cdn.jsdelivr.net/npm/vanilla-lazyload@17.8.3/dist/lazyload.min.js"
></script>
```

Above that, you'll want to add a script and configure vanilla-lazyload to your liking, but in our example we used:

```js
window.lazyLoadOptions = {
  elements_selector: ".lazy",
  threshold: 1,
};
```

Here's a link to see the full list of options:

https://github.com/verlok/vanilla-lazyload#options

Now, publish your page and watch your site performance take off!! 🚀
