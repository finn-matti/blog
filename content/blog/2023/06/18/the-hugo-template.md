---

title: "The (Hu)go template syntax is bad."
microblog: false
guid: http://matti.micro.blog/2023/06/18/the-hugo-template.html
post_id: 3260183
date: 2023-06-18T20:14:05+0200
lastmod: 2023-06-29T00:43:23+0200
type: post
tags:
- "Blog"
- "Dev Notes"
images:
- https://cdn.uploads.micro.blog/44388/2023/2023-06-19-hugo-templating-sucks-2.jpeg
photos:
- https://cdn.uploads.micro.blog/44388/2023/2023-06-19-hugo-templating-sucks-2.jpeg
photos_with_metadata:
- url: https://cdn.uploads.micro.blog/44388/2023/2023-06-19-hugo-templating-sucks-2.jpeg
permalink: /2023/06/18/the-hugo-template.html
mastodon:
  id: 110566599231965182
  username: matti
  hostname: social.lol
---
There is no two ways about it. It's just bad and often counterintuitive. It's hard to read, hard to write, hard to debug, hard to fill in blanks. Easy things should be easy and hard things should be possible. I feel like everything is just hard with it - not impossible per se, but often harder then it should be.

I mean just look at this one line:

{% raw %}
```go-html-template
{{ $paginator := .Paginate (where .Site.Pages.ByDate.Reverse "Type" "post") (index .Site.Params "archive-paginate" | default 25) }}
```
{% endraw %}

This does/means the following:

- `$paginator` - that's a custom variable, it needs to be prefixed with a `$`
- `:=` - you need to use this operator to declare a variable and assign a value. But later it's fine to just use `=` to reassign it.
- `.`  - "the dot". It holds the context, which is basically a kind of scope. Why the scope is not implied? I don't know. I guess if you'd have a `this` keyword, you'd end up writing `this.whatever…` and you would still need to differentiate globals and in-scope vars, so I guess that's better?
- `.Paginate` - Inside "the dot" there exists a `Paginate` function which has to be upper case because that is the way to make a function visible outside of its "package" in go. If you look at [the list of available functions in hugo](https://gohugo.io/functions/), you will know that a function was exported, but not why. Also a lot of functions were not exported, but you also do not know why. I assume that the lower case functions are all part of hugo's templating standard lib. But it's not explained what is going on in the docs explicitly.
- ` ` - A space (yup). Functions and parameters are separated by spaces, so this space indicates the start of the Paginate function call (And not the parentheses in front of the `where`, as one might think when coming from other languages).
- `(` - The start of the parentheses denotes a nested expression.
- `where` - that's the `where` function which takes an array and compares a value at a given key using an operator (equals is implied and can be omitted like has been done here) to a value and only keeps the elements that pass the test.
- `.Site.Pages.ByDate.Reverse` - The `.Site.Pages` part is an array of all pages of the blog. The `ByDate.Reverse` part is used (and available only) on [list pages](https://gohugo.io/templates/lists/#what-is-a-list-page-template) - another detail you'll have to know - that is pages that have other pages under them in the file hierarchy. AND that the homepage is a special kind of list page. This is a snippet from the home page, so you can use it here to change the order of the retrieved array. Why you can't retrieve pages in similar manner on non list pages is unclear to me.
- `"Type"` - This is the key parameter of the `where` function. The key is "Type" here. Why is `Type` capitalized? Maybe it has to because of exports? Maybe it's some other reason that I don't know. In any case it is part of the keys of the element that is kept (or discarded). For the pages array an element includes things like a `Permalink`, a published `Date` and a also a `Type`. How do you know what an element includes? Well, it's hard to say, because the [proposed solution](https://gohugo.io/templates/template-debugging/#what-variables-are-available-in-this-context) to use something like `&#123;&#123; printf "%#v" . }}` within a range function call that references the pages from the `Paginator` above only prints garbage. An actual solution is to use `<pre>&#123;&#123; . | jsonify (dict "indent" " ") }}</pre>` which gives a pretty printed JSON representation of all the available properties within a given context. But you'll not find this solution in the docs, you have to get lucky and find it in the forum or [Stack Overflow](https://stackoverflow.com/questions/64163573/how-to-inspect-variables-in-the-current-scope-in-hugo).
- `"post"` - this is the match parameter of the `where` function. In other words the value found for the key "Type" must match this value in order to be included in the filtered array.
- `) (` - we finish one nested expression - which is parameter one of our `.Paginate` call (the array to paginate) and start another nested expression - parameter two (the page size) of `.Paginate`
- `index .Site.Params "archive-paginate"` - this returns the value at index or key n of a given array. So in this case the value at .SiteParams.archive-paginate
- ` | default 25)` if `index` does not return a value the default function can take over and return a default value. I don't know why this has to be a function. I also find the whole part `index .Site.Params "archive-paginate" | default 25` difficult to parse: Is the pipe still part of the index function call? You'll have to know what pipes are.

Finally, we have parsed the whole thing:

```
instantiate customVar =
functionCallThatReturnsAPaginator(
    functionCallThatReturnsAFilteredArray,
    (
        functionCallThatReturnsANumber ||
        functionCallThatReturnsaAdefaultValue
    )
)
```

And `.Paginator` itself is just an object that makes it easier to refer to and implement a paged navigation for an array of given elements (posts).

Apart from the unusual syntax I find (Hu)go templates hard to parse, even if I grok them somewhat. (Hu)go's way to write function expressions, namely using spaces instead of parentheses and commas make the whole line harder to read than it needs to be. Compare:

{% raw %}
```go-html-template
{{ $paginator := .Paginate (where .Site.Pages.ByDate.Reverse "Type" "post") (index .Site.Params "archive-paginate" | default 25) }}
```
{% endraw %}

vs.

{% raw %}
```
{{$paginator := .Paginate(where(.Site.Pages.ByDate.Reverse,"Type","post"),(index(.Site.Params,"archive-paginate") | default(25)))}}
```
{% endraw %}


Granted, this is still hard to read, because a lot is happening in this one line of code, but still: I'd argue it's much easier to parse, because opening and closing parentheses and commas carry much more information than a simple space could. Spaces are also commonly used to align or balance things as has happened around the pipe char. Does this carry semantic meaning? Nope, not in this case!


<img src="uploads/2023/2023-06-19-hugo-templating-sucks-2.jpeg" alt="A visualization of what different symbols of the templating syntax mean in our example. It turns out that the space char carries three differnt meanings: an aesthtic space, a start of a parameter list, a delimiter between parameters." title="2023-06-19-hugo-templating-sucks-2.jpeg" border="0" width="600" height="424" />

The space is doing an enormous amount of overtime here and I have yet to see a good justification of muddling the waters like this. The only reason I could see is that you have to balance parentheses, meaning you're ending up with the line ending in `)))`. The best part is that you still need parens in any case, you just have to put them around the whole function expression! The real template version safes you two parentheses for the price of a parsing headache. I feel like that's not worth it.

Let's move on: It should be super easy to limit the list of pages to only include a certain category of posts, right? Would this have been what you'd come up with on the first try?

{% raw %}
```go-html-template
{{ $allPosts := where .Site.Pages.ByDate.Reverse "Type" "post" }}
{{ $allDailyDogos := where .Site.Pages "Params.categories" "intersect" (slice "DailyDogo") }}
{{ $onlyDogos := intersect $allPosts $allDailyDogos }}
{{ $paginator := .Paginate ($onlyDogos) (index .Site.Params "archive-paginate" | default 25) }}
```
{% endraw %}

So far so good. How about the inverse? You'll find that there is no way to tell the line `$allDailyDogos` to simply do the inverse. There is no `"not intersect"` or whatever. You have to use another function called `symdiff`:

{% raw %}
```go-html-template
{{ $allPosts := where .Site.Pages.ByDate.Reverse "Type" "post" }}
{{ $allDailyDogos := where .Site.Pages "Params.categories" "intersect" (slice "DailyDogo") }}
{{ $noDogos := symdiff $allDailyDogos $allPosts }}
{{ $paginator := .Paginate ($noDogos) (index .Site.Params "archive-paginate" | default 25) }}
```
{% endraw %}


Symdiff is short for [symmetric difference](https://en.wikipedia.org/wiki/Symmetric_difference) and means here that we want all elements from the `$allPosts` array that are not part of the `$allDailyDogos` array. Meaning we are keeping only those posts, which is like filtering for the inverse of the `$onlyDogos` array from before.

We could have mashed this all into one line to make it totally unreadable, but I think this is instructive and it would have not been anymore readable in other template languages (if they even would've been able to deal with this as a one liner). Still:

- Why do I need to make a slice/array out of "DailyDogo"?
- Why is there no `NOT` operator? - it would've been nice in two instances: 1. inside the `where` function to save an extra call to `symdiff` or 2. as a better (I'd say) alternative to using `symdiff`, because people think more along the lines of "all but not these kinds of things" instead of "symmetrical difference of these two sets".
- Why is it so hard to chain conditions to the `where` function to the point where you'd rather create two arrays instead of filtering the array down in one step?

Ugh. There is so much in just this one line - and the subsequent slight changes I have done - that I find weird and unergonomic. I hope I could also show that it's not complete and utter failure to understand what's going on, either. Sometimes things are just badly designed for the most obvious use cases in order to accommodate fancier goals. I'd rahter have a templating syntax/language that makes things easier. If that makes it more boring: Good. I'm here to improve my blog first and foremost.
