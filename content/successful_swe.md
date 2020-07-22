---
title: "Successful SWE Tips"
featured_image: ''
draft: false
---

This is a collection of tips I have curated that I believe anyone wishing to succeed as a SWE in industry should read.


## I don’t know anything!
*“Every great developer you know got there by solving problems they were unqualified to solve until they actually did it.”* 
   -Patrick McKenzie

Becoming a successful software engineer is more about a mindset than technical skills you possess. What matters most is being comfortable in the unknown and being able to learn. No matter what tools/languages you know now, odds are you won’t be using them in a few years. 




## Accept that you won’t understand everything
The software engineering world is a huge machine with tons of moving parts. It is near impossible to understand all of the parts with any level of depth. Sometimes, the best thing to do is to utilize the term “automagically”. You can use this word to explain why some unknown feature/service/etc you depend on works. When you are working on a new feature that relies on features of other developers, you should not be expected to (or try to) understand how the other features are implemented. 

As a general rule, the only questions one really needs to know about an API are:
What are the inputs/outputs?
Does this API make any storage/network calls?
What are the space/time complexities?
Are there any other performance/security considerations one needs to know?

Essentially, you need to understand about about another API/feature to use it, not implement it.



## Jack of all trades, master of none
I’m just gonna quote a [Quora answer](https://www.quora.com/Are-software-engineers-who-are-jack-of-all-trades-really-in-demand) for this one:
  The term «jack of all trades» by extension implies «master of none», but that’s usually unfair.
  The best software engineers are curious, flexible and always looking to pick up new skills. They’re also seniors with years of experience. Someone with that mindset and experience will have mastered a diverse set of skills at a high level. There’s no rule that says you can’t reach a professional level at several loosely related technical areas.

Overall, for this mindset, I would suggest finding the line between depth and breadth. It is good to have a skillset that is diverse, but also, have a few skills that you are proficient in to the point where you can teach others.



## Accept that sometimes projects fail
Projects fail sometimes. Sometimes it's because the business is going another direction, sometimes it’s because new technology came out that made your work obsolete, sometimes you simply messed up. In any event, it is important to understand what causes a project to fail, learn what you can from the failure, and **move on**.



## Don’t rely on your schooling
*“I have never let my schooling interfere with my education”* - Mark Twain

Before you start saying “Alexander says I can skip class”, I said no such thing. It is important to go to class and learn the material you are taught. It is equally (if not more) important to continue learning outside of class. Your classes won’t necessarily teach you software engineering fundamentals such as version control, working with others, working with legacy code. The best way to learn any of that is through simple experience. Whether it’s internships, projects outside of class, hackathons, contributing to open source, do something. 

Side note for anyone looking for jobs, the majority of people applying to that role have a CS degree. Your CS degree won’t make you stand out. **Your work outside of the classroom will make you stand out.**

TL;DR: Go above the minimum requirements. Always.



## You will rarely work alone, get over it
As stated previously, the software engineering world is huge. The days of being a lone programmer working in a basement are over for the majority. To you students, practice working with others now while the stakes are low. **It does not matter how good of a programmer you are if you cannot work with others.**



## Figure out how you learn
Everybody learns differently, the trick is figuring out how you learn. 

Some people learn by reading up on a subject beforehand. Others could read a whole chapter on a subject and forget what the subject is before they are done.
Some people learn best by watching a YouTube video. Others doze off during YouTube videos. 
Some people learn by throwing away the manual and just trying something, learning as they go. Others freeze up in that situation.

It does not matter how you learn. What matters is figuring out how you learn and applying it to what you want to learn. 
**It is better to have failed than to have not even tried.** So just try, experiment while you still can. **I have learned more from my failures than any success.** 

If there is one thing you should have mastered by the time you finish your undergraduate education, it is learning. This is also a skill you will most need to keep sharp. If you can’t continually learn, you will get stuck and be unable to progress.



## Modularity/Generic for the win
*“Humans aren’t very good at handling complexity. We can only think about a handful of things at a time, or less. Programmers are no different. That’s why modularity is so powerful: by hiding away large chunks of code into modules with a clear API, we can simplify our own thought process and take our code to the next level.”*  
-[François Wouts](https://medium.com/@fwouts/the-zenc-master-plan-c693bf3b265e)



## Lines of code (LOC) means nothing
Writing clean code is better than writing less code.

*“Using LOC to measure software progress is like using kg for measuring progress on aircraft manufacturing”* 
-Bill Gates

[Just read this SO post](https://stackoverflow.com/questions/3769716/how-bad-is-sloc-source-lines-of-code-as-a-metric/27047208)

For more reading on clean code check out “Clean Code” by Robert Martin



## Testing
Tests. We hate em. Do you know what is worse than writing tests? Being blamed for broken/untested code. 

Most people think of tests as a way of making sure their code works, which leads them to the thought of “I know my code works, I just wrote it and ran it.” I once heard Leslie Lamport say this, *“You only write tests for the cases you were thinking of when you wrote the code”*. 

At Google, I write tests for two reasons, and neither of them is “to make sure the code works”. Writing code is like writing a math formula. You have your inputs, you have your outputs, and you have to prove it works. When I write tests, their first purpose is to demonstrate to my reviewers that my code works with these cases. 

Secondly, **my tests defend my code**. Sure, once you submit your code to the codebase, it works as intended. But things change, assumptions made in libraries you depend on are removed, a teammate modifies the code you wrote to work in another situation. When that happens, your tests are there to fail and let future developers know “Hey, you forgot about this situation!”. 

Once you start seeing tests as a way to defend yourself and your code, you start really seeing the importance of testing. 
