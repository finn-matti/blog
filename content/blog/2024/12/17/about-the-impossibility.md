---

title: "About The Impossibility Of Steph Ango's \"self-guaranteeing promises\""
microblog: false
guid: http://matti.micro.blog/2024/12/17/about-the-impossibility.html
post_id: 4521890
date: 2024-12-17T14:34:13+0200
lastmod: 2024-12-27T12:46:43+0200
type: post
permalink: /2024/12/17/about-the-impossibility.html
mastodon:
  id: 113668186240028616
  username: matti
  hostname: social.lol
bluesky:
  id: bafyreifz6vq7um4246fqtaw6q6fan5v3xbujxv7zaw4w7gbdv55j5ixeye
  url: 'at://did:plc:ivue7yhu4vdejz7tu3jejpok/app.bsky.feed.post/3ldiu4mxmkf2m'
  link: 'https://bsky.app/profile/did:plc:ivue7yhu4vdejz7tu3jejpok/post/3ldiu4mxmkf2m'
  handle: finn-matti.bsky.social
  hostname: bsky.social
  did: 'did:plc:ivue7yhu4vdejz7tu3jejpok'
---
## Changelog

- 2024-12-27
	- Added links to quoted mastodon posts
- 2024-12-17
	- Title case for post title
	- Fixed a typo in the changelog...
	- Added another post script about another perspective on guarantee: One that looks at a product before its acquisition by the user.

## Blog Post

The CEO of [Obsidian](/2022/02/27/good-apps-obsidian.html) recently wrote:

>Companies break promises all the time. A self-guaranteeing promise does not require you to trust anyone. You can verify a self-guaranteeing promise yourself.
>
>File over app is a self-guaranteeing promise.
— [Steph Ango: Self-guaranteeing promises](https://stephango.com/self-guarantee)

I asked him on Mastodon about this:

>[@kepano](https://micro.blog/kepano) What are other self-guaranteeing promises besides File over app? What makes "File over app" different than, say, relicensing? Couldn't a "File over app" company just pivot to use another storage format in the same way they could relicense their code going forward?
— [Me](https://social.lol/@matti/113589939317209395)

He answered:

>[@matti](https://micro.blog/matti) Sure the company could pivot, but what makes the promise self-guaranteeing is that you have control over the files so you can switch apps at any time.
>
>I will be adding an appendix with a list of self-guaranteeing promises people send in. One example someone shared was Volvo putting the patent of the three-point safety belt into the public domain.
>
>Lots of examples are straightforward e.g. "stainless steel" is self-guaranteeing because you can see/test the material yourself.
— [@kepano/Steph Ango](https://social.lol/@kepano@mastodon.social/113590149197890968)

I was still confused, so I asked a follow up question:

>[@kepano](https://micro.blog/kepano) So the promise is not a company’s promise, because otherwise the open source relicensing example would work, too: You can for example keep using elastic/redis/sourcegraph/whathaveyou before they relicensed as well and continue using the product as it is up to that point. Same with stainless steel. If the company changes what their knives are made of, the knives they produced up to that point will still be stainless steel.
>
>Not trying to be difficult, but to understand! 😅
— [Me](https://social.lol/@matti/113593528159962723)

Sadly, he didn't answer to my question, but he did update has post. However, I am still not really satisfied. So I tried to read the post a little closer, to figure out where the problem lies:

>“Stainless steel” is a self-guaranteeing promise. You can test it yourself on any tool that makes this promise, and the stainlessness of the steel cannot be withdrawn.

Even though we start the blog post with "companies", self-guaranteeing promises can only be made "by" or about products of a certain version. A knife may or may not be stainless steel. That can be tested. And a company may have _so far_ produced stainless steel knives but nothing about this promise actually _guarantees_ that the company will also produce stainless steel knives in the future.

>Terms and policies are not self-guaranteeing. A company may promise the privacy of your data, but those policies can change at any time.

This is true for stainless steel knives also. A knife bought last year was stainless steel, but their new batch is not anymore. Terms and policies are easier to change and changes to them can be much less noticeable, but there is no categorical impossibility that the  "same" knives couldn't be non-stainless steel if I purchase a new set tomorrow.

>A self-guaranteeing promise about privacy gives you proof that the tool cannot access your data in the first place.

Again, this can only be said about a software product, pertaining to a particular version range that may or may not include future versions as well. If it includes future version only time can tell. You can verify that the software product _so far_ has been respecting your privacy by not accessing your data, but that does not actually say anything about future versions of an app.

>Open source alone is not self-guaranteeing. Even open source apps can rely on data that is stuck in databases or in proprietary formats that are difficult to switch away from.

This is maybe the first time in this post that we see mention of difficulty to change, which is, I suspect, what this is - or in any case should be - about: Some promises are harder to take back than others. Making knives all of a sudden out of non-stainless (stainful?) steel will be very hard, whereas changing the terms of use is relatively easy. If you safe data in plaintext files instead of a proprietary data structure makes it harder to move away from the former, because a change like this will be super obvious and will incur at this point - if we talk about a mature product like Obsidian - an enormous development cost.

HOWEVER: Cost of change for a company is no guarantee that this company is not altering its behavior in the future. It makes it more probable, but an alternative future is still possible. What we can say without running into these problems is that this knife is made of stainless steel or that Obsidian Version v1.7.7 is using a "file over app" philosophy to save data. I can use this version for as long as it will run and can rest assured it will save my notes as plaintext files. Will Obsidian v23.42.0 still be "file over app"? Probably, but it is not guaranteed.

P.S.: Just to make clear that I understand that one interpretation of the "guarantee" term here could be that as soon as Obsidian is not doing file over app anymore, they broke their promise and therefore the guarantee is void. But then there is no useful distinction between any promise and self-guaranteeing ones. If instead the point was therefore that I as the user can easily verify that the promise is still upheld by checking if Obsidian is actually saving my data as plaintext files, then "user-verifiable promise" would have been a _much_ better term. Because my verification does not make it self-guaranteeing at all. My ability to do so does not interact with the promise part in a way that extends the validity of it into the future.

P.P.S.: In order to have a real guarantee, you need a third party - society - that has power over the company and disallows certain behaviors. For the scope of the user and the company we can now speak of a guarantee. However even this guarantee is only "load-bearing" for as long as society doesn't change its rules - which is highly unlikely, but again, not impossible. It seems the concept of "guarantee" is problematic, eh?

EDIT: P.P.P.S: I just realized that there could be another interpretation. It could be meant as a promise that is said before acquisition and easily verified after. But even then "user-verifiable promise" would haven the better term, as said in the first post script: "If you buy this, you'll get a knife that is made of stainless steel" is a promise that can be falsified pretty quickly, sure. But it is not telling us anything about the future after acquisition happened - meaning here for future knife sets/future versions of a software. We're still stuck with only being able to verify this knife, or this version of this app. For the knife that is maybe not so important, because knife updates aren't a thing as much as software updates are, but for apps we are interested in long-term reliability throughout future versions of the app and not only in the short time in between before acquisition and thereafter.
