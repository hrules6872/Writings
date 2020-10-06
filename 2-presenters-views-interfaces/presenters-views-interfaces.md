# Presenters and Views meet The Interface Segregation Principle
## also known as “the 4th letter in the SOLID acronym”

![](art/1.jpeg)<span class="figcaption_hack">[Superman vs. Muhammad Ali Comic Book](https://en.wikipedia.org/wiki/Superman_vs._Muhammad_Ali)</span>

There are several posts about the **MVP**¹ pattern (or whatever fancy name some authors use to call it `:wink:`) and even more of them explaining what **SOLID**² stands for, so we will focus on:

1.  The contract between presenter and view
1.  Code reuse

> Speaking of MVP and contracts, some developers should read [this](http://blog.karumi.com/interfaces-for-presenters-in-mvp-are-a-waste-of-time/) for goodness sake!

#### DRY³

Time and again we are told that we must **avoid repetition and redundancy** because “the less code to maintain the better” but then we find ourselves typing almost the same interfaces over and over again an indefinite number of times.

https://gist.github.com/hrules6872/143bed9e18aeed2195cd478106420c3e

> It’s almost pseudo-code, but I’m sure it’s not the first time you’ve seen something like that `:shrug:`

#### KISS⁴

What can we do to follow the DRY principle mentioned above? **Applying the Interface Segregation Principle.** That’s it.

https://gist.github.com/hrules6872/2db9d7cd1243cfb07792c7e7dfcb41b8

**What do you think?** From my point of view, among other benefits, it looks much cleaner, more refactor-friendly and certainly a better way to avoid monolithic interfaces with hundreds of methods.

#### BONUS: Kotlin developers

Kotlin offers [Sealed classes](https://kotlinlang.org/docs/reference/sealed-classes.html) whose best description is: [Enums with super-powers](https://antonioleiva.com/sealed-classes-kotlin/). Using this kind of class we may be able to go [a little further](https://imgflip.com/i/29qsz7).

https://gist.github.com/hrules6872/af1561469b7f13f51e19c55584bdcc6c

> Further information about these **Sealed Classes** is available [here](/5-sealed-class/sealed-class.md) `:trophy:`

#### Conclusion

It’s true that we haven’t gone into the details but I think the code fragments shown above are worth more than a thousand words `:sunglasses:`

We here at [Lolamarket](https://lolamarket.com/tienda) believe that our code looks way better using this so I encourage everyone to try it and leave a comment below or [tweet](https://twitter.com/hector6872) me with any questions/suggestions!

*****

[1] [Model-View-Presenter](https://en.wikipedia.org/wiki/Modelâviewâpresenter) (btw it’s impressive to know this architectural pattern is over 20 years old `:wow:`)<br> [2] [SOLID](http://butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod) (the acronym is not used in its original paper so look for the reference to “the first five principles of *class design*” or even better go for a [easier explanation](http://lmgtfy.com/?q=solid+design+principles))<br> [3] [Don’t Repeat Yourself](https://en.wikipedia.org/wiki/Don't_repeat_yourself) <br> [4] [Keep It Short and Simple](https://en.wikipedia.org/wiki/KISS_principle) (politically correct variation)

*****

[External links 👀](https://gist.github.com/hrules6872/00362163fe92e0d92e1e2d1d1fcacd84)
