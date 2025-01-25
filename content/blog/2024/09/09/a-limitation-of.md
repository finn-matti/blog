---

title: "A Limitation Of Laravel's Seeders - And Why It is There"
microblog: false
guid: http://matti.micro.blog/2024/09/09/a-limitation-of.html
post_id: 4341822
date: 2024-09-09T17:23:23+0200
lastmod: 2024-09-09T17:23:23+0200
type: post
categories:
- "Dev Notes"
images:
- https://cdn.uploads.micro.blog/44388/2024/cleanshot-2024-09-09-at-14.35.532x.png
photos:
photos_with_metadata:
permalink: /2024/09/09/a-limitation-of.html
mastodon:
  id: 113108284287698926
  username: matti
  hostname: social.lol
---
Laravel has pretty cool tools to work with databases and fill them with seeded data. This is useful in many contexts, but mostly if you want to test things.

[Seeders](https://laravel.com/docs/11.x/seeding) are cool, because they can make use of model [factories](https://laravel.com/docs/11.x/eloquent-factories) - or factories for short - to create some test data the conforms to what we consider valid data.

However, the combination of seeders and model factories has a limitation and that is, that seeders are not meant to know of each others' results. So if you have three tables - users, blogs, posts for example -  that have some kind of relationship to each other _and_ would like to have individual seeders for those tables, then you can't use factories in those seeders without some extra work currently.

Note that factories do not have this limitation. You can use `recycle` on a model factory and use the resulting model in a subsequent factory call. This even works with indirect relationships, like a post that belongs to a blog and a blog also belonging to a user (and therefore the post belonging to a user). This short youtube video explains what I'm talking about:

<iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/8sNkNOTkEXY?si=8u0a5xnhxd-ozP_B" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

So that's pretty cool and all but if you want dedicated seeders for different parts of your database you're still out of luck. Why would you want different seeders? Because you may want to separate the generation of seed data by entity. Sure, you could create a user which in turn also creates a blog with a handful of posts in it, but maybe you'd rather create a user, a blog and some posts and bind them to each other afterwards.

Separating the seeding procedure in this way will help you later, too, you might think, because if I ask you where posts are seeded, the answer could be "in the PostSeeder, duh", if we could use that convention.

We would need to make it possible to receive the results of a seeder, but there is a problem: A seeder is supposed to create more than one row - or at least it should be possible work that way. So in other words: If we want to create a handful of posts per blog and we create one or two of those per user and we also create three test users (let's say), how are we supposed to relate all of these disparate entities to each other even if we could take the results from one seeder with us to the next? How do we disambiguate the instances of the created entities? Which one of our 2 blogs should be connected to the 10 posts? Should it be five and five? Two and eight? How do we communicate that?

We would need to explicitly set specific entities created by the factory in the other seeder on the factory in the current, but it will become confusing rather quickly, because factories might also have states - like a user who is deactivated and so forth. And as I said, if we create more than one, how do we pick an entity?

Since it's not easily possible to tell the next seeder what the previous seeder has created, having lots of seeders - e.g. one for each table - doesn't make sense. We have to take the route, where we handle creating related but different entities in the same seeder.

Another practical problem comes from the fact that a database seeder doesn't return its creates models, only the seeder classes it itself called. In order to still go the route of keep entities in their own seeders, we would need to enhance the basic database seeder classes Laravel provides. So from that perspective it seems that the framework itself doesn't intend you to separate the creation of different entities using factories out into different seeders.

P.S.: It is kind of weird then, that when you create a model that you are also given the option to create a database seeder:

<img src="uploads/2024/cleanshot-2024-09-09-at-14.35.532x.png" alt="A screenshot of the artisan make:model cli command, showing that it allows to create a database seeder when creating a model." title="CleanShot 2024-09-09 at 14.35.53@2x.png" border="0" width="598" height="269" />

This seems to suggest that maybe there is an intent to create seeders for every model (or entity), but as I tried to show, this is not practical and the seeder classes themselves do not really follow that logic and do not afford you the functionality to communicate between different seeders out of the box.

P.P.S.: What you can do is communicate through the database, I guess. Meaning that if you create entities in one seeder - using a factory (or not) - you can of course read those rows from the database and relate different entities to each other by retrieving them from the database. But you'll lose the elegance of expressing these relationships through the ORM and the recycle method.
