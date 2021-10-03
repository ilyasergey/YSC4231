.. -*- mode: rst -*-

FAQ on Learning and Plagiarism
==============================

This page is written by Prof. Ilya Sergey (referred to as "I/me" below) to
outline the learning objectives of his classes, as well as many similar classes
offered by Yale-NUS MCS. It will provide answers to some frequent questions
regarding the homework assessment and and treatment of plagiarism cases

On Learning Objectives
----------------------

Computing classes at Yale-NUS MCS major are designed to provide actionable
knowledge for solving various computational problems by means of writing
computer programs and reasoning about their quality (correctness, performance,
etc). Therefore, most the assessment is done via coding-heavy projects that are
aimed to make the students think about specific problems and come up with
solutions on their own and, less frequently, in small teams.

Whenever a task is told to be completed `individually`, it actually means that
you are expected to find a solution `yourself`. It is absolutely crucial that
you are mindful about the importance of working on solving the problem using
your own understanding and expertise, and without attempting to get parts of the
solution from available sources (your peers, a peer tutor, the internet), as
this defeats the whole point of the carefully designed learning process.

You might feel concerned about the fact that you cannot come up with a solution
for the assignments in what seems to be a reasonable amount of time, and that
the class makes you struggle. In most of the cases, **this is normal**---these
are legitimately difficult disciplines that require your `full engagement` and
pay off in skills that will help you land on highly-paid jobs in industry and
academia, with a great job security in the future.

..
   All the assignments are designed to take approximately 5-7 hours per week to
   complete, requiring you to review the lecture materials, do "paper and pencil"
   design, implement tests and, eventually, write some amount of working code. So
   if you spend considerably more than that, it might be an indication that you
   need to revise your work process. This page provides some advice on how to do
   that.

Indeed, there might be factors that are beyond anyone's control and interfere
with your learning process (e.g., mental of physical illness, or other
comparable hardships). At Yale-NUS College, we are determined to mitigate the
impacts of those events on the quality of your education and are willing to make
reasonable adjustments.

All that said, some of you occasionally find yourself in situations when the set
rules for assessing your knowledge seem unfair and not doing justice to your
efforts, penalising you for no good reason. This FAQ is aimed to clarify the
reasons why those rules are set in this particular way.

On Submission and Resubmission Policies
---------------------------------------

Since all Yale-NUS modules have a relatively low cap on student numbers, it is
possible to organise the learning process in which I (the professor) can provide
detailed feedback for all your submissions, with a quick turn-around. As my goal
is to make sure that everyone learns as much as possible, I have also set a
resubmission policy that allows you to receive an A-high score if 

a. your initial submission has been done by the set deadline,
b. you have attempted to solve all initially provided tasks in a homework and partially succeeded in all of those, and
c. in your resubmission, you have addressed all the comments from my feedback.

**So why do I need to try to solve every task in the initial submission? Can I just do some, and then do the rest in the resubmission?**

The requirement (b) is in place to avoid nearly "empty" submissions made in
time, in an attempt to extend a deadline for a week at a very small penalty.

**I had a really rough week and feel very stressed, having hard time to focus on the homework. May I have an extension?**

You can have an extension in the case if you have a Medical Certificate or an
Assistant Dean's letter. Medical Doctors and ADs are trained to assess the
severity of your situation and, therefore, have an authority to grant
extensions; I am unqualified to do so. I also do not provide ad-hoc extensions
without formal justifications (see above), as those create precedents other
students might appeal to in the future.

**Okay, I didn't realise that the task will take that much time, and I don't have a reason qualifying me for an AD letter. If you don't give me an extension, what should I do?**

I'm afraid, in this case you do your best and possibly take a penalty for a late
submission. Remember that non-attempted sub-tasks will affect your resubmission
score.

**This is rather harsh. Other profs provide extensions more easily and allow for an infinite number of resubmissions.**

Specific submission/resubmission policies are up to each prof; they might vary
depending on the size of the class, nature of the assignments, as well as other
duties that the prof must handle concurrently.

On Approaching the Tasks
------------------------

**I've spent way more than 7 hours on a homework task, and I have no idea how to solve it. What am I supposed to do?**

First, try to reflect on how you've spent those 7+ hours. 

I expect that some fraction of that time has been spent revising the lecture
materials, i.e., slides, lecture notes, and Zoom recordings. Those are designed
to be self-contained, so you're not required to read the textbook (unless you
feel interested in the details). Try to think how the material from the recent
lectures is relevant to solving the task.

It is also not a bad idea to "sketch" some executions of the program you're
asked to implement on a paper---this should help big time to understand its
corner cases. Next, before your start implementing the main program, write some
tests. I usually provide a rudimentary test suite, but please, do not simply
copy/paste code from it, changing the numbers---this is of no help to your
understanding. Instead, try to implement a testing scenario that reflects the
executions you've had in mind.

Now, you've got the tools, the tests, and the understanding of the problem---so
you're nearly there! Most of the programs in my assignments are not that large,
and, if you've done your diligence with the previous parts, you should be able
to write a program that is very close to a correct one. More tests/"paper
debugging" should help to eviscerate the remaining bugs.

**Okay, I've done all of that, but I still don't know how to write that program. Should I ask for help now?**

So, I assume that by now you've gone through the following steps towards the
solution of your homework:

(a) Reviewing the lecture
(b) Thinking about executions of the program in question
(c) Designing and implementing tests
(d) Writing the main program 

If you're stuck on (a)-(c), you should be able to phrase your problem, and it's
absolutely fine to seek help for this issue from your peers, the peer tutor, or
the prof. Let's talk about this next.

On Interaction with Peer Tutor
------------------------------

**So I shouldn't ask the tutor about how to solve the problem?**

If you phrase your question this way, you make it very difficult for the tutor
to help you without jeopardising your submission (see the next section). Peer
tutors are students like yourself who took this class in the past. While they
know solutions to the homework tasks, they are not trained to quickly identify
the source of your confusion and struggle, so, being kind-hearted, they might
feel compelled to reveal parts of the solution to ease your struggle. As
mentioned above, you getting the solution this way renders the exercise useless,
and also puts you at risk of getting penalised for plagiarism.

**Wait, but what may I ask the tutor then?**

Remember, your ultimate goal is to get good understanding of the material, so
you'd be able to solve the problems on your own (and I'm confident you can do
it). So why don't you try asking the peer tutor the following questions that can
help you with (a)-(c):

* Can you explain me how this thing X from the lectures works and give some
  examples of programs that rely on it?
* Can you give an example how the expected program from the homework task should
  work?
* What would be a good scenario to test for this problem? 

**Do you mean there are BAD questions to ask a peer tutor?**

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
happen in virtual Zoom sessions, when one of the participants shares their
screen. For the same reason, if the peer tutor is going to show parts of their
solution/share their screen, remind them not to do so.

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

The penalty for the first detected plagiarism attempt is 0 points for the
assignment, and it's F for the module in the case of the second strike.

**I've just got 0 points for my solution, but I didn't copy my code, so it shouldn't count as plagiarism.**

This is because your submission didn't pass my plagiarism detector (it's not a
particular automated test, but rather a sequence of checks I do). I have a
number of "red flags" I check for, but I'm not going to share them here. Rest
assured, I do not issue this penalty unless I'm 100% sure that the solution is
not original.

The fact that your that code didn't pass my plagiarism check is a symptom, but
it's indicative of the problem: you've taken a shortcut on the most important
part of a class---learning the material and applying your understanding of it to
solve the homework task. Above, I provided some advice on how to address the
problem. The penalty here serves simply as a deterrent against this attitude.

..
   It does not reflect my attitude to you as a student or a person, and will not
   affect my assessment of your future endeavours.

I am not really interested in the provenance of the code that has been
plagiarised. In any event, there are quite a few common scenarios I've heard
about over the years, so let me show how the most popular ones are indicative of
the bigger issue---a student skipping the learning process and trying to get the
solution without taking the class seriously.

* "My solution is similar to the one by the student A, because we've got the
  same recipe from the peer tutor."

We've covered this above: it was not a great idea of ask the tutor to reveal
parts of the solution, but, obviously, I'm not going to penalise them. In any
event, this is qualified as type-(1) plagiarism.

* "My solution is similar to the one by the student A, because we share a lot of
  background and came up with a very similar idea."

While this is, indeed, possible, there is enough inherent diversity in solutions
for the tasks, so I could tell with certainty whether code sharing took place,
when looking at two solutions by two different people.

* "My tests are similar to those of the student A, because we both simply
  modified the tests that you have provided."

We've talked about this above. This is again indicative of a large problem:
should you have tried to write your own tests, this would have never happened.

* "I have accidentally stumbled upon a solution in a different programming
  language on the internet, but I made sure I understood it before translating
  parts of it to the language of this class (OCaml/Scala)".

This is a type-(3) plagiarism. Don't be surprised if the way I detected it is
because some of your peers (to whom you might have even never spoken) did the
same.

**But now, with this penalty, I won't get an A for the class so my GPA will go down.**

If you are serious about a career in computing, this should not be an issue for
the following reasons.

If you're going to apply for an industry job in a software company, it is most
important for you to able to demonstrate your skills on an interview and with
your task project. This is what I'm optimising the outcomes of my classes for.

As for graduate school admissions, it's unlikely that a single B will kill your
application. At the end there will be an interview, at which you can always tell
about how you learned about concept X at my class in a hard way---people will
appreciate your honesty and technical sophistication.

Finally, you can always S/U a class.
