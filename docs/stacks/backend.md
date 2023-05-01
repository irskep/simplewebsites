# Choosing a backend stack

Humanity has been making web sites for over 30 years. Somehow, we keep inventing new and strange ways to write web servers, when the old ways work fine.

## Make a multi-page app

Single-page apps are a complexity trap that require you to use fragile dependencies.

In a multi-page app, your server sends different HTML pages back in response to different URLs, but probably the same CSS and JavaScript. When you run your JS, you can look for elements on the page and add behaviors to them, up to and including replacing the whole page with JavaScript-defined UI.

In a single-page app, your server sends the same HTML, JavaScript, and CSS no matter what URL is requested, and the JavaScript decides what to render on the page based on the browser's URL. In some ways this can feel "simpler," but there are hidden costs:

1. You need to use a "routing" library on the client. [More APIs](https://reactrouter.com/en/main/upgrading/v5) to [break over time](https://router.vuejs.org/guide/migration/).
2. Your page will probably take longer to load because you'll need to request additional data via an API after the page loads.
3. Your single-page-app JS code might not be appropriate to run on your landing page without cookies, so you'll have multiple pages anyway.

If you're confident you can make a robust SPA that works the way you want to, go for it! But in my experience, beginners seem extremely prone to getting totally lost when something goes wrong in their SPA.

### "Server-side rendering" is also a complexity trap

Lots of mainstream teaching material, including the primary React docs, steer you toward writing your web server in JavaScript and using "SSR" to generate HTML so that when your JS first runs, the DOM is already in the right state. Doing this adds significant complexity, and again, fragile dependencies. It also cuts you off from using languages that are better suited to writing web servers.

## Use Python and Flask, or something similar

At this point, Flask has been used for everything, and [there's a great tutorial for it](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).

I don't recommend using JavaScript for your backend because the landscape changes too quickly. JavaScript web frameworks are not yet old and boring.

#### What you give up

It could be faster, which means it could be cheaper. If you want fast and cheap, use Go.

#### Good alternatives

Anything that's been around for at least ten years:

| Framework                                                      | Language |
| -------------------------------------------------------------- | -------- |
| [Laravel](https://laravel.com/)                                | PHP      |
| [Django](https://www.djangoproject.com/)                       | Python   |
| [Pyramid](https://trypyramid.com/)                             | Python   |
| [Rails](https://rubyonrails.org/)                              | Ruby     |
| [Sinatra](https://sinatrarb.com/)                              | Ruby     |
| [ASP.NET Core](https://dotnet.microsoft.com/en-us/apps/aspnet) | C#       |

## Use SQLite

Most web sites written by hobbyists can probably run on [SQLite](https://sqlite.org/index.html) forever.

In practice, you can deploy SQLite in production by mounting a persistent volume on your web machine and using [Litestream](https://litestream.io/) to replicate it to S3.

Using SQLite isn't even necessarily a scaling tradeoff. It has the unique advantage that roundtrip time to make a query is zero milliseconds, because the database driver is running in your application process.

Using a persistent volume typically costs very little, but also tends to not be available on the free tier of any platform-as-a-service. On [Render](https://render.com), you'll be paying at least $7/mo for the Starter tier. On [fly.io](https://fly.io) it's cheaper, more like $3/mo, but fly.io also has much worse reliablity.

### What you give up

Managed database services tend to give you nice admin tools like automatic backups, which you need to figure out for yourself with SQLite. You also need to SSH into your web server in order to run database migrations when you add or remove tables or columns. (Despite these inconveniences, once you get things set up, they will keep working with no effort.)

You'll probably also give up zero-downtime deploys, because your SQLite volume needs to be detached from the old machine before it can be attached to the new one. In my experience, each deploy to Render involves about 30 seconds of downtime.

### Good alternatives

[Supabase](https://supabase.com/) does appear to have a Postgres free tier. For now.
