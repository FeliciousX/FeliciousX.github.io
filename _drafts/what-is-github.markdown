---
layout: "post"
title: "What is Github?"
description: "Confused what's Github and what's Git? What's the difference?"
category: "Blog"
tags: [blog, git, github, version control]
---

I feel the need to write about this topic because many people who have never experienced any form of `version control` will be super confused when they are told "_Just clone my repo from Github_" or "_fork my repo and check it out, it's on Github"._

I remember being so confused when I first heard all these terms. The term was so alien to me. I couldn't even distinguish between _Github_ and _git_ . I know. Maybe it's just me. This was years ago.

Before I go on, I just need to make 1 thing clear. I will assume you don't even know what `version control` means. Maybe this is a good article for new developers or even non-developers.

Anyways, lets get started.

## Disclaimer
There's probably a few good articles explaining the distinction of Git and Github and the likes. A link to this article is easier to find and show to my fellow friends in the future when they ask me the same question.

## Knowledge Gap

I will put out some terminologies out here that's frequently used by developers and will explain along the way. This is just to let you know if you encounter these words and you don't understand it, it's probably not your fault.

1. __Version Control / Revision Control__
2. __Repository (Repo)__
3. __Git (commands in git e.g. _push, pull, clone, commit, merge, rebase_)__

## Github

So you [googled what is Github?][1]. You scratch your head. Then you [googled what is Git?][2]. Google says `git` is ___an unpleasant or contemptible person.___

At this point you probably have given up if you're not a tech guy.

So what is it? Well, the quick version is that Git is an open-source software and was created by [Linus Torvalds][3]. Github make use of Git, build tools on top of Git and provide services to users.

You got me? Mmhm? Ok.

## Git

Ahh.. Git.. the software almost every modern developer uses to `version` their code. THERE IT IS AGAIN. THAT WORD. Okay. Story time!

Imagine coding a software. If you're not a software developer then maybe you can't. Okay let's change the analogy a little.

Imagine writing a long essay on your computer. It will take days, maybe months to complete. That kind of essay. Yes?

Imagine you wrote your 1st paragraph. Save it. Call it version 1. Write your 2nd paragraph, save it. Call it version 2. Edit the 1st paragraph again, save it. Call it version 3.

Now if you want to go back to the version where your 1st paragraph was unedited, you can just open version 2. All these processes are made easy with `Git`.

So in `git` this is what would have happened.

1. Open Story.txt
2. Write 1st paragraph. Save.
3. `git add Story.txt`
4. `git commit -m "My first paragraph"` (Your 1st commit)
5. Write 2nd paragraph. Save.
6. `git add Story.txt`
7. `git commit -m "My second paragraph"` (Your 2nd commit)
8. Edit 1st paragraph. Save.
9. `git add Story.txt`
10. `git commit -m "Edited 1st paragraph"` (Your 3rd commit)

Now when you want to go back to your previous commit where 1st paragraph was unedited, you can just run `git checkout HEAD~1` and now your file `Story.txt` will look exactly like how it was on the second commit.

Imagine everytime you `commit` in `git`, git takes a `snapshot` of your files at that instance.

## References

- [HTG Explains What is Github][4]

[1]: https://www.google.com/search?hl=en&q=what%20is%20github "What is Github?"
[2]: https://www.google.com/search?h1=en&q=what%20is%20git "What is Git?"
[3]: https://en.wikipedia.org/wiki/Linus_Torvalds "Linus Torvalds"
[4]: http://www.howtogeek.com/180167/htg-explains-what-is-github-and-what-do-geeks-use-it-for/ "HTG Explains What is Github"
