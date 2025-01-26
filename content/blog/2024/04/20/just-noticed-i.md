---

microblog: true
guid: http://matti.micro.blog/2024/04/20/just-noticed-i.html
post_id: 4035797
date: 2024-04-20T12:36:40+0200
lastmod: 2024-04-20T12:36:40+0200
type: post
tags:
- "BuildInPublic"
- "mb-sync"
permalink: /2024/04/20/just-noticed-i.html
---
[Just noticed I never sent this…]

#buildinpublic #mbsync

Alright, so the seeder works and I can skip registering all the time when resetting the db.  😅

Instead I only need to run:

```
artisan migrate:fresh
```

and then:

```
artisan db:seed
```

And I'm good to go!

The code needed some trial and error to get right, but looks basically like this:

```php
<?php

namespace Database\Seeders;

use App\Models\Blog;
use App\Models\User;
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Config;
use Illuminate\Support\Facades\Hash;

class AddAdminUserSeeder extends Seeder
{
    public function run(): void
    {
        $user = User::create([
		//...
        ]);
        $user->save();
        $blogs = [
		//...
        ];
        $user->blogs()->saveMany($blogs);
        $user->selected_blog_id = $blogs[0]->id;
        $user->save();
    }
}

```
