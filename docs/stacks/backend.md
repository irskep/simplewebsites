# Choosing a backend stack

This page isn't done.

## A multi-page app

It's a tradeoff. This site focuses on multi-page apps to counteract the blogosphere idea that single-page apps are always a good default. They are not.

## Python and Flask

At this point, Flask has been used for everything, and [there's a great tutorial for it](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).

I don't recommend using JavaScript for your backend because the landscape changes too quickly. JavaScript web frameworks are not yet old and boring.

### What you give up

It could be faster, which means it could be cheaper. This is why people use Go.

### Good alternatives

Anything that's been around for at least ten years:

- PHP/Laravel
- Python/Django
- Python/Pyramid
- Ruby/Rails
- Ruby/Sinatra
- C#/ASP.NET Core

## SQLite

Most web sites written by hobbyists can probably run on SQLite forever.

In practice, you can deploy SQLite in production by mounting a persistent volume on your web machine and using [Litestream](https://litestream.io/) to replicate it to S3.

Using SQLite isn't even necessarily a scaling tradeoff. It has the unique advantage that roundtrip time to make a query is zero milliseconds, because the database driver is running in your application process.

Using a persistent volume typically costs very little, but also tends to not be available on the free tier of any platform-as-a-service. On Render, you'll be paying at least $7/mo for the Starter tier. On fly.io it's cheaper, more like $3/mo, but fly.io also has much worse reliablity.

### What you give up

Managed database services tend to give you nice admin tools like automatic backups, which you need to figure out for yourself with SQLite. You also need to SSH into your web server in order to run database migrations when you add or remove tables or columns.

You'll probably also give up zero-downtime deploys, because your SQLite volume needs to be detached from the old machine before it can be attached to the new one. In my experience, each deploy to Render involves about 30 seconds of downtime.

### Good alternatives

Supabase.
