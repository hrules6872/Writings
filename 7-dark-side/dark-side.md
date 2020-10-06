# A walk on the dark side
## There has been an Awakening…

![](art/1.jpeg)

## Introduction

This summer [our tech lead](https://twitter.com/jberlana) told us that we were allowed to spend a percentage of our time [at work](https://lolamarket.com/) doing or researching about something we weren’t used to ([a kind of Google’s “20% time policy”](https://www.businessinsider.com/google-20-percent-time-policy-2015-4?IR=T)… but in the good way). There was only one condition: we would have to give a tech talk to the rest of the team on the chosen topic.

**Teaching is the best way to learn.**

## Motivation

Because I often make fun of the programming languages that my teammates use in their daily work (100% trolling just for fun I swear; [I do not want to start any kind of nonsense programming language war](https://www.businessinsider.com/why-coders-get-into-religious-wars-over-programming-languages-2015-6?IR=T)) I thought it would be great to pay them back using a language I haven’t touched for ages: **[PHP](https://eev.ee/blog/2012/04/09/php-a-fractal-of-bad-design/)**.

## Idea

I’m a real fan of automation ([even when we spend more time coding](https://xkcd.com/1205/) the thing than the time it actually saves us afterwards), so based on a function we all use at work almost every day known as “[automatic issue closing via commit messages](https://confluence.atlassian.com/bitbucket/resolve-issues-automatically-when-users-push-code-221451126.html)” (I guess all web-based Git repository managers have a fancy name for that) I started to code **a [Bitbucket](/4-from-github-to-bitbucket/from-github-to-bitbucket.md) Webhook¹.**

## Webho… what?

A **[WebHook](https://en.wikipedia.org/wiki/Webhook) is a `HTTP` callback**: a web application implementing a webhook will `POST` a message (payload) to an user-defined `URL` (web service) when something happens. It’s that simple.

So, in my case, what I coded was a [Githook](/1-git-hooks/git-hooks.md) but [on the other side](https://www.reddit.com/r/ProgrammerHumor/comments/7zhco9/frontend_vs_backend/) (basically it connects Bitbucket+[Trello](https://developers.trello.com/)).

I don’t think it’s worth giving further details about my project itself but I can summarize everything in these points:

* Someone on the team pushes to a [repo](https://confluence.atlassian.com/bitbucket/manage-webhooks-735643732.html)

* Bitbucket sends a [payload](https://confluence.atlassian.com/bitbucket/event-payloads-740262817.html) to our webservice

* It parses that information and then: **do whatever we can imagine.**

## Conclusions

It was very fun to get out of my [comfort zone](http://lmgtfy.com/?q=comfort+zone+where+the+magic+happens) (I can’t tell how many years I’ve been coding exclusively for [Android](https://play.google.com/store/apps/details?id=com.comprea.client) platform) and I can confirm that I’ve taken advantage of the great opportunity we have at work (I wish everyone had it): **I have learned a lot** (and now I am able to troll them [even more](https://twitter.com/Syknapse) 🤷).

**PS: [we’re hiring!](https://lolamarket.com/jobs/)**

## Disclaimer

There are neither slides (I splitted my tech talk into: a code review where my teammates got their revenge pointing up all my mistakes 😃 & a live demo) nor public repository (I don’t dare to make it public because I know it’s not as good as I’d like) but [someone from my team ](https://twitter.com/Jokantaro)(who’s a real Jedi in PHP) thought the idea could be improved (which I think is an amazing proposition because we can still learn about it) so maybe in the future we’ll release something based on this.

**[Stay tuned!](https://twitter.com/LolaMarket_tech)**

[1] Even though it could be a simple script I demanded of myself to meet some requirements: neither use frameworks nor libraries of any kind, follow good practices, patterns and SOLID, and add some tests ([PHPUnit](https://phpunit.de/) is love, my friends).

*****

[External links 👀](https://gist.github.com/hrules6872/25fcd2ab507f2293c8ab8720983afcc4)
