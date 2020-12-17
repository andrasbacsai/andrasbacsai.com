## Glued together my favorite libraries

I tried a lot - it not all - frameworks out there for React, Vue, and Svelte. Why? To find my niche framework. I would like to have the most optimal development and deployment experience while coding.  I did not say perfect because there is no such framework. You need to sacrifice something in the name of something else. Or did I just created one, which is perfect for me?

# Most optimal framework (for me)
- Lightning-fast startup of the development environment.
- Instant hot module replacement (HMR).
- API and frontend in the same codebase.
- Superfast backend.
- No SSR.
- Filesystem based routing on the client.
- ES modules.
- Be able to use Tailwind efficiently.
- Based on Svelte. (optional)

There is no such thing in the wild. So I started to glue one together. I do not call it a framework because gluing could be similarly done by my 4 years old son. 

# Ingredients
##  Sapper
I like  [Sapper](https://sapper.svelte.dev/). Most of the requirements are met here (kind of), but I do not like SSR. I tried to work with it, even created a [starter pack](https://github.com/andrasbacsai/sapper-tailwind-starter). It was easy and straightforward most of the time, especially in the beginning. But I recognized it could make things pretty complicated very quickly, and unfortunately, it's tough to use Sapper in SPA only mode.

## SPA mode 
I like  [SPA applications](https://en.wikipedia.org/wiki/Single-page_application). A good product does not need to be over-optimized. If it's simple, works, and easy to be developed, it doesn't matter if it has a good SEO or any other benefits of SSR. SPA is cool!

## Svelte
I like  [Svelte](https://svelte.dev/). Fast, not too complex, and the outcome of my spaghetti code is small. After seeing a video on Twitter about its costs in Co2 emission to transfer unnecessary data over the wire is INSANE! 

%[https://twitter.com/i/status/1337117225405313029]

## Routify
I like  [Routify](https://routify.dev/). Simple (as everything in this list) and has a filesystem-based automated routing for the client.

## Tailwind
I like  [Tailwind](https://tailwindcss.com/). I'm bad at design; I struggle a lot. But I still like to practice and sweat to create horizontally and vertically centered texts in CSS. With Tailwind, I feel I'm not alone. Something is on my side in this hell of a  journey.

## ES Modules
I like technologies that point to the future.  [ES modules](https://flaviocopes.com/es-modules/)  are one of them, in my opinion. I used  [Svite](https://github.com/dominikg/svite) ( [Vite](https://github.com/vitejs/vite)  alternative, just for Svelte), which is awesome! 

(I hope the creator does not abandon it after SvelteKit officially came out someday.)

## Fastify
I like  [Fastify](https://www.fastify.io/). It's super-fast, has a great ecosystem, and despite its speed, it does not lack any features or has some penalty.

## One codebase
I like when the API and the frontend code is in one place. The development is such a relaxing feeling.


So I glued them together, and here is the outcome: 

%[https://github.com/andrasbacsai/svelte-fastify-starter]

This example has a JWT based authentication, guarded endpoints in the backend and frontend, separated environment variables for each layer. 

## +1 

You can try it in Codesandbox (and even develop a full application in it!):
 https://codesandbox.io/s/svelte-fastify-starter-ku9d9

(The initial ES build takes a while, but after that, it's super fast)

# Lesson learned
- It doesn't matter if your application does not follow any overhyped techs. If a plain HTML/javascript file is enough for you to create a cool application, do it! 
- To get the most out of your development performance, use what you like.
- If you don't feel comfortable with a framework, experiment with things you like. You do not need to compromise.

 
---

> If you like these libraries, you can try them and let me know how you feel about it.  Feel free to contact me on Twitter if you have any questions; I'm happy to answer!

---

