extends: default.liquid

title: New Site, Who Dis? 
date: 28 September 2016 22:00:00 -0700
path: /:year/:month/:day/new-site-who-dis
---

My old blog was built on [Ghost](https://ghost.org).
While I liked it for the most part, I recently noticed that I had
an old version of Ghost and needed to update.

Ghost is still pretty new so the update process is very manual.
You basically need to check out the current version and replace the
core files by hand.

While that in itself is not too bad, Ghost is built on node, required module
updates, and needed an sqlite3 db. And I just don&rsquo;t think that&rsquo;s
necessary for my needs. It&rsquo;s actually quite the opposite. I want
as little friction to blogging as possible. I&rsquo;m already shit at it so
fighting to even get it up and running is not ideal.

#### Say howdy to yet another blog site

I&rsquo;ve recently fallen in <span class="heart">❤</span> 
with [Rust](https://www.rust-lang.org)
so this blog is powered by a static site generator written in Rust called
[Cobalt](https://github.com/cobalt-org/cobalt.rs).

It&rsquo;s all I really need, and with my posts being markdown and layouts in
HTML, it shouldn&rsquo;t be too hard to move to another if needed. With Ghost,
this isn&rsquo;t as easy.

Luckily, I only had a handful of posts on the old one so putting those back up
shouldn&rsquo;t be tough.
