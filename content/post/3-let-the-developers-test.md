---
title: "3: Let the Developers Test"
date: 2020-03-08T17:50:48-06:00
draft: false
---

There's a bit of a false dilemma going on when people talk about "Tester" vs "Developer" mindset. There's an assumption that only one or the other can be embodied in a person, but not both.

But I don't think that separating these into two distinct mindsets is useful.

Let me explain.

Here's what people usually mean by **"Tester Mindset"** - A person who **thinks about how stuff might break** when they're working on that stuff.

Here's what people usually mean by **"Developer Mindset"** - A person who writes happy-path code and **thinks about how to make stuff work.**

And here's why this distinction of builder vs. breaker makes no sense: **A developer who writes code that is not resilient to how stuff might break not writing good code. A developer must *necessarily* think with a "Tester Mindset" in order to write good code.**

## Developers with "Tester Mindset"

A developer that is creating an input field on a web app, must *necessarily* think about input sanitation, including SQL injection, sting length, and a host of other naughty strings.

A developer that is interacting with a REST API, must *necessarily* think about how the API may malfunction and write code that handles the API being unresponsive, or returning an unexpected response.

A developer that is writing a class that interacts with a filesystem must *necessarily* think about how to handle missing files, already existing files, locked files, missing directories, permissions and a host of other I/O issues specific to the filesystem.

If a developer wants to write good code, they, while using whatever Developer mindset they have, must also think about how stuff might break and thereby also have a Tester mindset.

## Developers without "Tester Mindset"

But for far too long we've let developers write crappy code, rewarding them for marking things "Done" instead of doing the right thing and encouraging crappy code instead better code. This resulted in hiring an army of testers to come after developers and write a bunch of bugs in a bug tracking software, so that the developers can then go back and re-write the code to be less crappy.

We've gotten complacent with the crappy output some developers create.

And not only that, We've encouraged crappy output from developers. We made "quality" to be a QA Team's responsibility and gave a free pass to developers to just write stuff without thinking about quality. After all, there's a whole team *over there* whose job title and role is to think about quality. They'll take care of it. Why would developers overstep their bounds and think about quality?

## Dev and Test are two halves of a Feedback Loop

Lets take a flashcard as an example.

Say you're learning Russian and you see the word "мяч" on the flashcard. The creative "developer" side of you will go through your recently learned letters and sounds and come up with a plausible solution.

For the sake of this illustration, lets say you've decided that "мяч" means "mine".

You're effectively done "Developing" and you can mark this flashcard "Done" in your Jira. Git commit --all, git push --force. Job done!

But not so fast. The next thing you do is flip over the card and read what it says and assess or "Test" your work. You then learn that "мяч" means "ball" and not "mine." So close, yet so far. Shouldn't have pushed the repo before running unit tests.😉

## Applying the Feedback Loop

Now, lets imagine that the flashcard is a User Story.

A developer spent some time working on it, came up with the best word for "мяч", and passed passed it on to the Test team. The test team picked it up once it bubbled up to the top of their backlog, flipped the flashcard over, assessed the developers work, and tossed it back to the developer to be redone. Lets say that process took three days.

Will the developer remember what they did three days later? I mean sure, they'll remember the *what*, since that's literally what's in source control. But will they remember the *why?*

"Action" followed by "Assessment" are two inseparable parts of a feedback loop. The sooner the feedback is provided, the sooner learning can take place.

Moving the "Assessment" or the Testing half of the feedback loop into a separate "Mindset", and by extension a separate role - or worse - a completely different team, is an excellent way to make sure that quality of the output suffers.

Let the developers test. You'll get better code faster.
