# A simple, reliable frontend stack

"Use things that are ten years old" unfortunately doesn't work in the frontend world because browsers have evolved much more than HTTP has. In this guide, I present two alternatives: a trendy one with a great framework design but more tooling than I'd like, and an obscure one with almost no tooling at all.

## Option 1: Vue, Pinia, and Vite

[Vue 3](https://vuejs.org/guide/introduction.html) (with the "composition API") is sort of like "what if the React community didn't go nuts," and [Pinia](https://pinia.vuejs.org/) is like "what if JS state management was actually really obvious."

(Still working on this.)

## Option 2: esbuild, sass, and Arrow

I can't remember the last time I opened up a complex project I hadn't touched in months or years and didn't need to immediately deal with a bunch of broken build or framework dependencies. It doesn't seem to matter whether the tools are maintained by one person or an army of maintainers, whether the tools are recommended by authors of the framework it supports not, or whether a library is a few months or a few years old. They all break. It's infuriating.

To route around all these issues, I'm trying out a simplified frontend stack that completely removes transitive dependencies (meaning tool X relies on library Y which relies on library Z, etc.).

1. [esbuild](https://esbuild.github.io) for bundling JavaScript and TypeScript
2. [sass](https://sass-lang.com/install) for bundling CSS
3. [Arrow](https://www.arrow-js.com/) or [React](https://react.dev/) for interactivity

Arrow is plain JavaScript, and React requires JSX, both of which are supported by esbuild.

### What you give up

In the interest of simplicity, this stack does _not_ include server-side rendering of JavaScript-provided HTML, or hot module reloading. Both of these features can be nice, but also add significant complexity to the stack. Server-side rendering requires writing your server in JavaScript and having templates that act differently in different contexts, and hot module reloading involves proxies and websockets and splitting your JS bundle into multiple parts.

### Developer experience

The way you develop an app with this stack is to run 3 processes simultaneously:

1. Python web server
2. esbuild
3. sass

With these tools, you can write a web app like we used to do it in 2012, but much better, because the standards have evolved.

## Alternatives

There was a time when I would have recommended [Parcel](https://parceljs.org/), but they broke their plugin API on a major upgrade. [Webpack](https://webpack.js.org/) is relatively stable, but is famously difficult to configure, and does too much to be easy.

I try to steer people away from React because the maintainers and apparently the entire community assume that you want to do "server-side rendering" or make a "single-page app," both of which go against the grain of making an ordinary web site that you can understand.
