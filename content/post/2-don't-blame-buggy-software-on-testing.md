---
title: "2: Don't Blame Buggy Software On Testing"
date: 2020-03-01T16:33:37-06:00
draft: false
---

Every so often, someone on social media will point out a bug in a product and go on to blame the testing - or lack thereof - of that product.

I literally saw this happen the other day on Twitter, and I'd link it here, but I don't want to signal-boost a behavior I find toxic.

Things get especially bad when a person that identifies as a tester finds bug in a product from a company that has recently disbanded a separate Test Team or disbanded a dedicated Tester Role altogether.

Said tester will quickly point out that it is the lack of good testing - due to the lack of dedicated testers, obviously, - that has caused the issue.

But there's a problem with that thinking. Testing doesn't fix bugs. And neither do Dedicated Testers.

Dedicated Testers do not have agency when it comes to fixing a bug. In a traditional enterprise environment, testers have agency to do something along these four things when they see a bug:

1. Block acceptance of a work item
2. Write a defect in some ever-growing bug backlog
3. Fail a test case
4. Complain to another co-worker in person

None of these actually fix the issue. In traditional environments, testers are not empowered to make a pull request to fix a bug. That's a developer's job - and they're testers. They test stuff and they inform the team of any issues that they find. Their role stops there. The rest of the feedback cycle is out of their hands.

But in order for product to change, the feedback cycle must be completed. And testers don't control the completion of the feedback cycle.

On top of that, as soon as a customer complains about bug on social media, the tester is cut out of the feedback loop. A company doesn't need a tester to *also* tell them that the product is misbehaving when a customer is *already* doing that publicly.

The bug may have gotten out because of shoddy testing practices, but it may also have gotten out despite world-class testing taking place.

And with the customer reporting a bug via Twitter, the company already knows its broken. At that point, the problem is not lack of testing or lack of knowledge about the product. The problem is how quickly a company can respond to new knowledge about their product.

The problem is the feedback cycle.

But back to testers and testing... As a customer, you don't know what kind of testing has taken place. You don't know whether someone has already reported that bug internally and a decision was made to ship with it. Or someone reported it, but it was ignored because it was lost in the backlog. Or it was reported, but was closed with "wont-fix" and "a customer is never going to do that" message. Or maybe it was reported and a developer already fixed it, but it was pushed to the next release, so it's sitting and waiting to be shipped.

As an outsider, you don't know what part of the feedback cycle is broken.

So next time you see a bug in someone else's product, don't blame the tester. Report the bug via appropriate channels and move on. Don't use someone else's failure to jeer, or to promote your favorite flavor of a process. Instead take a page out of #HugOps playbook and send them some hugs.

With that said, I'll go and scrub my post history of mean tweets.
