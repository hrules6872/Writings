# How good are Git Hooks?
## I’ve tried them and [the answer will shock you](https://venngage.com/blog/7-reasons-why-clicking-this-title-will-prove-why-you-clicked-this-title/)

As developers we use Git (or at least we should) an uncountable number of times
a day¹ so, because [not all of us are machines yet](https://media.giphy.com/media/TgHosMP8OADYO6onsC/giphy.gif), we can sometimes make a mistake as the result of the rush (i.e pushing a commit to master when it should go to dev). To try to cut down these kinds of slips we have **Git Hooks’** help.

### What are Git Hooks?

Git Hooks are **extensionless executable scripts²** you can place in your repository’s hooks folder ([by default](https://git-scm.com/docs/git-config#git-config-corehooksPath) *.git/hooks*)³ to trigger actions at certain points in Git’s execution. In other words: we can **automate** what we always want to happen before/after using a `git` command.

![](art/1.jpeg)

There is a huge [list of hook types](https://github.com/git/git/blob/master/Documentation/githooks.txt#L42)⁴ you can attach⁵ scripts to but here we will see just a few.

https://gist.github.com/hrules6872/6816a97f27c75eb19a33a205a7d6dc27

> Tip: they can always be bypassed adding the`--no-verify` param

I hope the code snippets attached below are self-explanatory.

#### Pre-commit

https://gist.github.com/hrules6872/8077d6799ba53499be361b931059eda2

#### Commit-msg

https://gist.github.com/hrules6872/6ce15e97f83b34d4e63af983df153340

#### Pre-push

https://gist.github.com/hrules6872/d52b3730de8251d99782fa9e327846b7

> As a good practice we could run our tests at this point as well 😉

![](art/2.jpeg)

### Sharing hooks with our lovely team

As the default hooks folder belongs to `.git` folder which isn’t versioned we can use one of these strategies depending on our Git version⁶ to share hooks among our team members:

* **version 2.9 or greater:**

https://gist.github.com/hrules6872/50edf1956d0794e900b3883159e67f0e

> Tip: you can apply this configuration to all current (and future) repositories adding the `--global` param

* **earlier version than 2.9:**

https://gist.github.com/hrules6872/f01187a6ff4459f4e3cb20ff7b66b705

Said that, you can use this script I’ve created for lazy people like me:

https://gist.github.com/hrules6872/90b0b9111d74c0eb057068099e9ceff1

> Another additional benefit of using a different folder than the default one is that we can keep them updated

![](art/3.jpeg)

### Introducing Git Hooks⁷ repository

In order to be able to run multiple hooks within each type avoiding the creation of a huge and cumbersome single script loaded of comments, I have created a [public repository](https://github.com/hrules6872/GitHooks) which offers a new structure to store our hooks: each type of hook (i.e. `pre-commit`) launches the scripts we have stored in its corresponding subfolder (i.e `/pre-commit-hooks`).

> To disable or enable a hook you can use the `git-hooks-state.sh` script (which basically is a `chmod` alias that changes their executable permission depending on the new state indicated)

**I wish I didn’t have to say it but PRs are very welcome.**

![](art/4.jpeg)

PS: you will have a lot more spare time to configure your hooks if you start using [LolaMarket](https://lolamarket.com/) to shop for groceries 😄

*****

[1] Remember, commit early and often.<br> [2] Use `chmod +x script.sh` from terminal to make a script executable<br> [3] Every Git repository has a hooks folder which contains some disabled sample hook files but IMHO they are pretty useless 🔥. You can checkout the latest version [here](https://github.com/git/git/tree/master/templates)<br> [4] They are usually categorized into two main types: client side and server side<br> [5] It supports any scripting language that [your system knows how to execute](https://github.com/hrules6872/GitHook/issues/1)<br> [6] Use `git --version` to find out your current version of Git<br> [7] Great naming, isn’t it? 😞

*****

[External links 👀](https://gist.github.com/hrules6872/d2710acff24e29ba7164d4db48674a79)