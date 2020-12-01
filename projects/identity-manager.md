# Identity Manager

The other day I saw an interesting idea, really simple but hard to implement:

> **The right answer to a security question is easy to extract from a person,**
> **however, no one told you that you had to give the right answer.**

Let me make clear: This post is *not* about how to implement security questions,
or whether they are secure.

This post is about how lying on your security questions is actually a good idea,
when you are not careless.

## The Thing About Security Questions

Security questions are about personal details only you and possibly few other people know.
They will usually ask for things like the name of your first pet,
or the place where you first went to school.

However, answers to these questions can be gathered by sweeping your social media,
a determined attacker may be able to discover the answers to your questions and thus gain access to your accounts.
In this case we hit a crossroad, we either never share anything personal online or we can lie when answering these questions.

Nowadays, in our increasingly connected lives, it seems rather extreme that we stop sharing our life,
our friends get their updates on us through social media, and vice-versa.
One may be able to completely avoid social media, but not everyone will want to do so.

All that is left is to lie when answering the questions.

## Why Lie?

To put it simply: Anyone can find out the true right answer, but only you will know the true wrong answer.

For example, my last name is Duarte,
and it is usually the norm (in my country) that the last name comes from the father,
so if the security question asked - "What is your father's last name?" - anyone could easily guess the true answer.

However, if I answer "[Abdulaziz](https://en.wikipedia.org/wiki/Salman_of_Saudi_Arabia)" no one will know except me.
So now, I can be confident that no one but me will be able to answer the question.

But this still leaves us with a problem, if I keep on lying my way through security questions,
I will end up creating several alter-egos and remembering none.

## The Solution

Use an identity manager.
Just like password managers, there should be an identity manager,
some password managers have the concept,
but they only go as far as allowing some usual identity information and some notes.

Ideally they'd be able to identify the selected questions and answers and store them in a key-value fashion.
Until then, I'll make do with secure notes.