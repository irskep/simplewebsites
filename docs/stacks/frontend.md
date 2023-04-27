# Choosing a frontend stack

"Use things that are ten years old" unfortunately doesn't work in the frontend world because browsers have evolved much more than HTTP has. So if you want to minimize the likelihood that one of your tools will become "obsolete," your best bet is to use things that are easy to replace, or have few dependencies.

## Custom syntax adds risk

The things most "modern" UI frameworks have in common are declarative updates and custom syntax. The most common syntax is JSX, which lets you write `<div>Hello</div>` instead of `h('div', {}, 'Hello')`. Other frameworks like Svelte and Vue have more all-consuming custom file formats which let the build tool do fancy things to your code like wrap them in hidden function calls or generate completely different code.

The convenience of these custom syntaxes and file formats is nice, but they introduce hard dependencies on a _transpilation_ step, where a complex program needs to run in order to turn your `.vue`, `.svelte`, or `.jsx` file into a `.js` file. And this step is almost always implemented as a plugin to another build tool such as Vite or Webpack, which means there are two dependencies that can break, and you're locked into the design decisions of the build tool you choose.

## Vanilla JS syntax is viable

There are frameworks which don't require special syntax, but still provide declarative updates. The biggest one is [Lit](https://lit.dev/), with lots of established SaaS users. There's also the newcomer [Arrow](https://www.arrow-js.com/), which is a minimalist library that is very unopinionated and flexible, at the cost of making you figure out how to organize your own stuff.

Some of the custom-syntax frameworks also support ways of calling them without custom syntax. Vue calls its plain JS form ["render functions."](https://vuejs.org/guide/extras/render-function.html) [Preact](https://preactjs.com/guide/v10/getting-started/) and [Solid](https://www.solidjs.com/guides/getting-started#buildless-options) give you a couple different options for writing plain JS.

You do give up a bit of convenience, but remember, you're not only giving up convenience, you're also gaining simplicity and removing complexity from your build.

### JavaScript template strings are pretty nice for writing HTML these days

The arrival of [tagged templates](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates) has enabled people to bring some of the benefits of JSX back to ordinary JavaScript syntax. If you use a framework that supports something like [HTM](https://github.com/developit/htm) or [lit-html](https://lit.dev/docs/libraries/standalone-templates/), you can have a JSX-like experience without leaving the ES6 standard behind.

## Just use esbuild and nothing else

esbuild turns a bunch of JavaScript, TypeScript, JSX, and/or TSX files into one big JavaScript file and optionally one big CSS file. It's really nice that esbuild supports JSX, because it means you can use a little bit of that syntactic magic.

If you want to use a custom syntax, go off and learn Webpack or Vite. You're too smart for this web site. Shoo!

## Viable web frameworks

While writing all that, I did some light research into which mainstream JS frameworks can be effectively used with esbuild alone with no plugins. Here's a best-effort summary of what I found.

| Name                             | Plain JS by default? | Slower execution when using plain JS | JSX in esbuild? | Docs for plain JS use                                                                 |
| -------------------------------- | -------------------- | ------------------------------------ | --------------- | ------------------------------------------------------------------------------------- |
| [Lit](https://lit.dev/)          | **Yes**              | No                                   | No              | n/a                                                                                   |
| [Arrow](https://arrow-js.com/)   | **Yes**              | No                                   | No              | n/a                                                                                   |
| [React](https://arrow-js.com/)   | No                   | ?                                    | **Yes**         | [React Without JSX](https://legacy.reactjs.org/docs/react-without-jsx.html)           |
| [Vue](https://vuejs.org/)        | No                   | Yes                                  | ?               | [Render Functions](https://vuejs.org/guide/extras/render-function.html)               |
| [Preact](https://preactjs.com/)  | **Yes**              | ?                                    | **Yes**         | [Getting Started](https://preactjs.com/guide/v10/getting-started/)                    |
| [SolidJS](https://preactjs.com/) | **Yes**              | Yes                                  | No              | [Buildless options](https://www.solidjs.com/guides/getting-started#buildless-options) |

## A note on Sass

[Sass](https://sass-lang.com/) makes it _slightly_ more convenient to write CSS. It's not really necessary these days, but I tend to use it because it's familiar and easy to add to my workflow. The `sass` command line tool is as simple as esbuild.
