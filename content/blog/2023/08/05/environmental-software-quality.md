---

title: "Environmental software quality"
microblog: false
guid: http://matti.micro.blog/2023/08/05/environmental-software-quality.html
post_id: 3480769
date: 2023-08-05T12:05:26+0200
lastmod: 2023-08-06T21:17:28+0200
type: post
categories:
- "Software Quality"
permalink: /2023/08/05/environmental-software-quality.html
mastodon:
  id: 110836444905047209
  username: matti
  hostname: social.lol
---
*TL;DR: In light of the growing importance of digital services, we ought to consider modern software quality in relation to its environmental impact as well. This is more easily possible thanks to using automated software quality tools and continuous integration.*

Being a programmer means being privileged: You're generally sought after, payed well and enjoy freedoms and perks that other workers could only dream of. I think this still is true even though there have been many tech lay-offs recently. It's not like programmers became obsolete. On average software developers have it pretty good.

In any case, working in software development brings with it also a big responsibility: To at least ponder the consequences of our actions as an industry. Up to and including what that means for the industry in my country (and Europe as a whole in my case), my company, my team and myself.

There are lots of things to consider like privacy issues, accessibility issues and - more and more, although it's not a new thing - environmental issues.

Because of how the world works, even actually pondering those issues at work almost never happens. It's not really part of the discussion - lip service aside - when considering changes to a software system.

I acknowledge the importance of all the ethical issues named und unnamed above, but want to concentrate on environmental issues here: The tech industry as a whole is constantly incentivized to offer and use more resources: It has become standard to expect new computers to be faster and so newer software tends to be more resource hungry than older software. What does that mean, exactly? Well, new hardware needs resources in production to make all the chips, cards, and so on, that's obvious to anyone. But resources are also needed  when using our hardware: A modern laptop generally doesn't require that much power to be used by us, but what about the internet? The data centers that host most of the services we use today and that make up a big part of our modern understanding of what using a computing device should feel like, are insanely resource hungry. Take this example of data centers using fresh water to cool its facilities:

>In The Dalles, Oregon, Google was found to be using a quarter of the city’s water supply to cool its facilities. Tech companies have been facing pushback elsewhere in the United States, but also across the world in places like Uruguay, Chile, the Netherlands, Ireland, and New Zealand. Now opposition is growing in Spain too, where droughts are wiping out crops and people are wondering why they’d give their limited water resources to Meta for a data center.
>— [The ChatGPT revolution is another tech fantasy](https://www.disconnect.blog/p/the-chatgpt-revolution-is-another)

The French think tank "the shift project" [estimated](https://theshiftproject.org/en/article/unsustainable-use-online-video/)  that about 4% of green house gas emissions are the result of the use of digital services and that this figure grows by 9% every year.

### Automation and software quality

A modern software development workflow consists of many pieces, incorporates many different perspectives and hast to take a lot of concerns into account. After all, modern businesses model their processes in software, report, plan and reflect in software and are maybe even selling software products through software market places. Business processes tend to be very complex, simply by virtue of having to deal with historical ballast, future visions, differing politics within the company and a shifting environment in which the software has to function, not to speak of the process itself, which touches many different stake holders that all need different things from a company to do their work.

Because of this, the software development cycle of gathering requirements, implementation, testing and release has started - more than 10 years ago - to accumulate lots of automation tools that are being referred to as continuous integration (ci). For example: When you develop software you often want to make sure that your new feature works as expected before you release a new version of your software. For this, people have developed testing tools. So people would write not only the feature but also a test (or tests) to make sure that the feature does what it should: This basically means you would define inputs and expected outputs and make sure that the new feature returns those expected values, when feeding the defined inputs. When a developer runs their test, they can see that the new feature works. This is great, but it's even greater when used down the road: Because a newer feature could accidentally change the behavior of a system in an unexpected way. With tests you can make sure that deployed code is more resilient against such accidental changes.

An important part of modern development is the code review. So a developer would implement a feature, write tests and send their changes as a merge request (or pull request) to a colleague for review purposes. That colleague would check for any missed requirements, errors in the implementation, code smells and so on. There is a little back and forth between reviewer and programmer and if all is well the code is approved and can be deployed to a test system for a quality assurance colleague to manually test the change, before it then finally finds its way into the "live" software version used by a normal user.

The code review process is especially important in terms of code quality, that is, in terms of aspects of the code that are rarely user facing but nonetheless are a very important part of a resilient application - scalable, easy to test, easy to change, etc. In other words: code review is supposed to help and (often times) ensure a high standard of quality in the codebase.

Back to ci: Continuous integration can automatically find and often times fix a great many problems with new - and old, outdated - code. First of all, it can run all the software tests to ensure backwards compatibility. It can also run a linter, which ensures a consistent style (indentation, order of parts of code, naming scheme, etc.). This improves readability and ensures that a person familiar with one part of the system doesn't need to parse everything about this unknown part of the system: the files look the same and things are generally named as you would expect them to be, and so on.

You can go further. You can let a static analysis tool run, to catch things like giving the wrong inputs to a function (e.g. input is a floating number, but this function expects an integer; in a dynamically typed language like PHP you might catch this error only when the code is actually run - but you want to catch that mistake and fix it before it is encountered in the wild). There are many, many other things where static analysis of a codebase in light of new changes can reveal problems that would otherwise go unnoticed until it's too late.

There's automated testing, linting, static analysis and more tools like "mess detectors" that try to detect valid code but that constitutes generally considered bad programming practices. All of these tools would run before a code reviewer even gets to see the code. Issues with agreed upon standards will be brought up and fixed - in some cases even automatically - before another human even has to see the code. This in the end saves time, improves focus - because humans are not good in spotting standard violations and even prevents some lengthy discussions in some cases - because the machine is dispassionate and just enforces a standard that was agreed upon in the company.

But you can go further. A relatively new idea is to also take software architecture into account when talking about ci. Software architecture is a whole can of worms in itself, but one important concern, as an example, is modularity: You want your code neatly organized so that the whole system stays open to replacement, improvement, extension, change, and so on. You could make sure, for example, that different parts of the system do not talk directly with each other, by defining application layers that separate different parts of the system from another to ensure a sensible organizational structure of the whole. Well, you can test for that in your ci pipeline - the pipeline is what runs all your defined code quality tools, linters and so on - as well, by defining an "architectural fitness function":

>In the 2017 book Building Evolutionary Architectures (O’Reilly), the authors (Neal Ford, Rebecca Parsons, and Patrick Kua) defined the concept of an architectural fitness function: any mechanism that performs an objective integrity assessment of some architecture characteristic or combination of architecture characteristics.
— [Software Architecture: The Hard Parts, "Using Fitness Functions"](https://www.oreilly.com/library/view/software-architecture-the/9781492086888/)

With a function defined you can also write a test in a tool like [phpat](https://github.com/carlosas/phpat). Here's an example from the readme of this project:

```php
<?php

use PHPat\Selector\Selector;
use PHPat\Test\Builder\Rule;
use PHPat\Test\PHPat;
use App\Domain\SuperForbiddenClass;

class MyFirstTest
{
    public function test_domain_does_not_depend_on_other_layers(): Rule
    {
        return PHPat::rule()
            ->classes(Selector::namespace('App\Domain'))
            ->shouldNotDependOn()
            ->classes(
                Selector::namespace('App\Application'),
                Selector::namespace('App\Infrastructure'),
                Selector::classname(SuperForbiddenClass::class),
                Selector::classname('/^SomeVendor\\\.*\\\ForbiddenSubfolder\\\.*/', true)
            );
    }
}
```

And just as with your tests that are supposed to test that the code does what it does, you can test that it does so in an integrity conserving way with an architectural testing tool like this.

### Automating measuring environmental impact

But you can do more: We started this discussion with pondering ethical issues and the impact a software developer's work has. You can now for example measure carbon footprint and energy consumption in a similar fashion in your ci pipeline as all the other things we have mentioned above. An example is [greenframe](https://github.com/marmelab/greenframe-cli) that does this for web apps.

As with all concerns: A measurement is only as good as the idea of what you're trying to measure. Just as with coding standards, testing and architecture, automatic validation and measurement is only good if you measure for a reason - and figuring out that reason will continue being a hard problem. What automation can do, though, is performing consistent measurements of your codebase, which you can then use to gauge the environmental software quality of your project.

* * *

This wraps up this somewhat lengthy blog post. I wish that companies running especially resource hungry applications - like the AIs of today - would incorporate environmental concerns in their assessment of software quality. Because how good is a software really, if it is not built environmentally conscious?
