.. -*- mode: rst -*-

FAQ on Learning and Plagiarism
==============================

This page is written by Prof. Ilya Sergey (referred to just "I/me" below) as an
attempt to outline the learning objectives of his classes (as well as many
similar classes offered by Yale-NUS MCS), and explain the reasons for the rules
for the homework assessment and treatment of plagiarism cases. It will also try
to answer some specific questions you might have with regard to approaching
homework assignments.

On Learning Objectives
----------------------

Computing classes at Yale-NUS MCS major are designed to provide actionable
knowledge for solving various computational problems by means of writing
computer programs and being able to reason about their quality (correctness,
performance, etc). Therefore, all the assessment is (mostly) done via
coding-heavy projects that are aimed to make you think about specific problems
and come up with optimal (or good enough) solutions, mostly on your own and,
less frequently, in small teams.

Whenever a task is told to be completed `individually`, it actually means that
you are expected to find a solution `yourself`. It is absolutely crucial that
you are mindful about the importance of working on solving the problem using
your own understanding and expertise, and without attempting to get parts of the
solution from available sources (your peers, a peer tutor, the internet), as
this defeats the whole point of this learning process.

You might feel stressed about the fact that you cannot find a solution for the
assignments in what seems to be a reasonable amount of time, and are concerned
that the class makes you struggle too much. In most of the cases, **this is
normal**---these are legitimately difficult disciplines that require your `full
engagement` and pay off in skills that will help you land on highly-paid jobs in
industry and academia, with a great job security in the future. All the
assignments are designed to take approximately 5-7 hours per week to complete,
requiring you to review the lecture materials, do "paper and pencil" design,
implement tests and, eventually, write some amount of working code. So if you
spend considerably more than that, it might be an indication that you need to
revise your work process. This page provides some advice on how to do that.

Indeed, there might be factors that are beyond anyone's control and interfere
with your learning process (e.g., mental of physical illness, or an announcement
that your university will close soon). At Yale-NUS, we are determined to
mitigate the impacts of those events on the quality of your education and are
willing to make reasonable adjustments.

All that said, some of you occasionally find yourself in situations when the set
rules for assessing your knowledge unfair and do not do justice to your efforts,
penalising you for no good reason. This FAQ is aimed to clarify the reasons why
those rules are set in this particular way, and what are my expectations about
your work.

On Submission and Resubmission Policies
---------------------------------------

Since all Yale-NUS modules have a relatively low cap on student numbers, it is
possible to organise the learning process in which I (the professor) can provide
detailed feedback for all your submissions, with a quick turn-around. As my goal
is to make sure that everyone learns as much as possible, I have also set a
resubmission policy that allows you to receive an A-high score if (a) your
initial submission was done on time, (b) you have attempted to solve all
initially provided tasks and partially succeeded in some of those, and (c) you
addressed all the comments provided in the initial feedback in your
resubmission.

**So why do I need to try to solve every task in the initial submission? Can I
  just do some, and then do the rest in the resubmission?**

The requirement (b) is in place to avoid nearly "empty" submissions made in
time, in an attempt to extend a deadline for a week at a very small penalty. I
don't enjoy such attempts of gaming the system, and this is why this rule is at
place.

**I had a really rough week and feel very stressed, having hard time to focus on
  the homework. May I have an extension?**

You can have an extension in the case if you have a Medical Certificate or an
Assistant Dean's letter. Medical Doctors and ADs are trained to assess the
severity of your situation and, therefore, have an authority to grant
extensions. Regular profs (like myself) do not have such training and,
therefore, are unqualified to do so. I also do not provide ad-hoc extensions
without formal justifications (see above), as those create precedents other
students might appeal to in the future.

**Okay, I didn't realise that the task will take that much time, and I don't
  have a reason qualifying me for an AD letter. If you don't give me an
  extension, what should I do?**

I'm afraid, in this case you do your best and possibly take a penalty for a late
submission. Remember that non-attempted sub-tasks will affect your resubmission
score.

**This is rather harsh. Other profs provide extensions more easily and allow for
  an infinite number of resubmissions.**

Specific submission/resubmission policies are up to each prof; they might vary
depending on the size of the class, nature of the assignments, as well as other
duties that the prof must handle concurrently (research, admin, serving on
committees, accounting, organising events, supervising capstones, managing the
lab, etc).

On Approaching the Tasks
------------------------

**I've spent way more than 7 hours on a homework task, and I have no idea how to
  solve it. What am I supposed to do?**

First, try to reflect on how you've spent those 7+ hours. I expect that some
fraction of those is spent revising the lecture materials (slides/lectures).
Those are designed to be self-contained, so you're not expected to read the
textbook (unless you feel interested in the details). Next, try to think how the
material from the recent lectures is relevant to solving the task.

It is also not a bad idea to "sketch" some executions of the program you're
asked to implement on a paper---this should help big time to understand its
corner cases. Next, before your start implementing the main program, write some
tests. I usually provide a rudimentary test suite, but please, do not simply
copy/paste code from it, changing the numbers---this is of no help to your
understanding. Instead, try to implement a testing scenario that reflects the
executions you've had in mind.

Now you've got the tools, the tests, and the understanding---it shouldn't take
too long to implement your program. Most of the programs in my assignments are
not that large, and, if you've done your diligence with the previous parts, you
should be able to write a program that is very close to a correct one. More
tests/"paper debugging" should help to eviscerate the remaining bugs.

**Okay, I've done all of that, but I still don't know how to write that program.
  Should I ask for help now?**

So, I assume that by now you've gone through the following steps towards the
solution of your homework:

(a) Reviewing the lecture
(b) Thinking about executions of the program in question
(c) Designing and implementing tests
(d) Writing the main program 

It is very unlikely that you'll get dead-stuck in (d) if you've completed the
parts (a)-(c). Furthermore, at this point, if you're stuck on (a)-(c), you
should be able to phrase your problem, and it's absolutely fine to seek help for
this issue from your peers, the peer tutor, or the prof. Let's talk about this
next.

On Interaction with Peer Tutor
------------------------------

**So I shouldn't ask the tutor about how to solve the problem?**

If you phrase your question this way, you make it very difficult for the tutor
to help you without jeopardising your submission (see the next section). Peer
tutors are students like yourself who took this class in the past. While they
know solutions to the tasks, they are not trained to quickly identify the source
of your problem (neither am I, but I'm doing my best), so, being kind-hearted,
they might feel compelled to reveal parts of the solution to ease your struggle.
As mentioned above, you getting the solution this way renders useless the
exercise, and also puts you at risk of getting penalised for plagiarism.

**Wait, but what can I ask the tutor then?**

Remember, your ultimate goal is to get good understanding of the material, so
you'd be able to solve the problems on your own (and I'm confident you can do
it). So why don't you try the following questions that can help you with (a)-(c)
with the peer tutor:

* Can you explain me how this thing X from the lectures works and give some
  examples of programs that rely on it?
* Can you give an example how the expected program from the homework task should
  work?
* What would be a good scenario to test for this problem? 

**Do you mean that there are BAD questions to a peer tutor?**

Oh, plenty! Here are some examples.

* Can you hint the structure of the solution?

This is the same as asking for a part of the solution. The tutor might not have
a good intuition of what is an `essential` part of the task, so by revealing the
structure, as asked, they might ruin the assignment for your and give me a fair
ground to penalise you for plagiarism.

* My code doesn't work, and I don't know why. Can you take a look?

It is beyond the peer tutor's capacity to work as your personal debugger. It is
also a well-known fact that if you start talking out loud about your failing
tests and what your implementation does, you will most likely find a bug very
soon (this is so-called "rubber duck debugging"). 

For the same reason it's not a good idea to as the prof this question. In a
limited number of cases, I might know what causes a certain problem (as I've
seen my share of those issues), but I don't have an immediate fix for every
possible bug (and, just like a tutor, I'm not your personal debugging
assistant). Furthermore, by asking this you deprive yourself of the precious
"aha" moment when you find the bug.

* Can I show you my code and you tell me if it's okay?

This is not a great question for a number of reasons. First, you ask the tutor
to provide an assessment that you should be able to do yourself (by writing
tests and benchmarks). Second, it increases the chance of some of your peer
students seeing your code and adopting some parts of it for yourself (this
counts as plagiarism for all involved parties). This is even more likely to
happen in the Zoom sessions, when one of the participants shares their screen.
For the same reason, if the PT is going to show parts of their solution/share
their screen, remind them not to do so.

To conclude, your interactions with the peer tutor should aim at filling the
holes in your understanding of the lecture material and the assignment tasks,
but not at "fishing" for implementation strategies. It's okay to ask them about
tests, but only at the level of "paper-and-pencil" discussion, not sharing the
tests implementation.

On Plagiarism and Penalties
---------------------------

As of now, I define plagiarism at my class as follows:

(1) Obtaining the answer directly from anyone or anything else in any form
(2) Adapting a solution from a similar one found on the internet
(3) "Copying with understanding" from other resources

**I've just got 0 points for my solution, but I didn't copy my code, so it
  shouldn't count as plagiarism.**

This is because your submission didn't pass my plagiarism detector (it's not a
particular automated test, it's just what I do). I have a number of "red flags"
I check for, but I'm not going to share them here. Rest assured, I do not issue
this penalty unless I'm 100% sure that the solution is not original.

The fact that your that code didn't pass my plagiarism check is a symptom, but
it's indicative of the problem: you've taken a shortcut on the most important
part of this class---learning the material and applying your understanding of it
to solve the homework task. Above, I provide some advice on how to address the
problem. The penalty here serves simply as a deterrent against this attitude. It
does not reflect my attitude to you as a student or a person, and will not
affect my assessment of your future endeavours.

I am not that interested in the provenance of the code. In any event, there are
quite a few common explanations I've heard over the years, so let me explain how
the most popular ones are indicative of the bigger issue---a student skipping
the learning process and trying to get the solution without taking the class
seriously.

* "My solution is similar to the one by the student A, because we've got the
  same recipe from the peer tutor."

We've covered this above: it was not a great idea of ask the tutor to reveal
parts of the solution, but, obviously, I'm not going to penalise them. In any
event, this is qualified as type (1) of plagiarism.

* "My solution is similar to the one by the student A, because we share a lot of
  background and came up with a very similar idea"

While this is, indeed, possible, there is enough diversity in most of the tasks,
so I could tell with certainty whether there was more than just common
background, when looking at two solutions by two different people.

* "My tests are similar to those of the student A because we both simply
  modified those you have provided."

We've talked about this above. This is again indicative of a large problem:
should you tried to write your own tests, this would have never happened.

* "I have accidentally stumbled upon a solution in a different programming
  language on the internet, but I made sure I understood it before translating
  parts of it to the language of this class (OCaml/Scala)".

Seriously? :) In any event, this is a type-(3) plagiarism. Don't be surprised if
the way I detected it is because some of your peers (to whom I might have never
even spoken) did the same.

I think, this should provide enough explanation on the real reasons why I care
about originality of solutions.

**But now, with this penalty, I won't get an A for the class so my GPA will go
 down.**

If you are serious about a career in computing, this should not be an issue for
the following reasons.

If you're going apply for an industry job in a software company, you should know
that very few of those companies care about grades. What is important is you
being able to demonstrate your skills on an interview and with your task
project. This is what I'm optimising my class for. And if someone raises their
eyebrow about you having a B+ in a computing class, you can always tell them a
story about how you learned about concept X in a gard way---people will
appreciate your honesty and technical sophistication.

The same goes for academic admissions. It's unlikely that a single B+ for an
will kill your application, and at the end there will be an interview at which
you can always tell a story, as suggested above. Finally, you can always S/U a
class.
