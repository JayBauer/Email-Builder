# Emails don't have to suck now
What up my glipglops, I told you I'd put this on a repo and then forgot all weekend. But now it's here, no more shit-tier email development for you.

## How to use
- Clone this repo with `git clone`
- Run `npm install` in the folder to get everything ready to go
- `npm start` will get you going with development, with live reload and SASS sourcemaps
- Run `npm run build` when you're ready to compile for production

## Inky
Inky is a templating language for emails. It uses Foundation as it's grid system, but compiles everything to email-friendly HTML tables and such. The syntax is real straightforward.

I put a bunch of example code in the `examples.html` file, but none of it looks nice. Maybe later. Here's some stuff to know:
- Use the `<spacer>` element to create vertical spacing instead of padding or margins, it will be way more consistent
- Wrapping things in `<center>` will center your stuff real nice
- `<menu>` and `<item>` are better to use than `<ul>` and `<li>` apparently, I would use it since it basically just builds your lists out as tables

For our purposes, everything you'll need is likely in the `examples` file.

## Panini
This setup also uses Panini, which you might have used before. It lets you add variables to the top of your page, and that data is then passed to either the page itself or the template you're using at compile time. This is also how you tell the email what template it should be using, which are created in the 'layouts' folder. There's one in there already that you'll probably never really need to touch.

Add something like this to the top of your page template:
```
---
layout: default
subject: This is the email subject, dingus
description: This is a description or something probably
---
```

And it would get added to this in the layout you selected:
```
<head>
<title>{{ subject }}</title>
</head>
<h1>{{ description }}</h1>
```

## Some things to keep in mind
All your CSS will be inlined at production, which means a couple of things:
- Do not use `!important` on anything other than media queries. That being said, make sure EVERY rule in your media queries are important, since they can't be inlined and will instead be shoved into a `<style>` tag in the header
- Once your stuff is compiled for production, ALL your CSS will be inlined (minus queries). If you have any weird styling problems after compiling, this is the first place you should look, as it may behave slightly differently than if you were relying on inheritance and all that fancy stuff normal CSS usually does.
