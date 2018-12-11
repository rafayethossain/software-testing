# Interacting with Stakeholders

Through much of this book, we have spoken of testing as if in a vacuum.  You write the tests, the software either passes or fails (or you realize you wrote the test incorrectly), you file a defect report, and eventually the problem is fixed.  There is another aspect to testing that you will experience working on projects---the human element.  Managers may disagree with you on what the testing priorities are.  Developers may argue that the "defect" you found is actually expected behavior.  Fellow testers may get into shouting matches with you over subtleties in a requirements specification.

Conflict is inevitable on any team, and in fact, it's probably a positive overall.  If everybody on your team agrees about everything all of the time, beware: You are probably working on a pretty trivial project, and your job is likely to be replaced by a small shell script in the near future.  Resolving conflicts, although it can be difficult, is the key to successfully preparing a product for launch.  Conflicts, as long as they are conducted professionally and productively, are often the fuel that allows a team to perform better as time goes on.

As a software tester, you will have specific challenges when interacting with other members of the development team.  After all, the whole job of a tester is to find problems with software.  They're professional critics, constantly looking for all the weak points of a system in order to make it better.  If this is not done with a gentle touch, it can often be mistaken for being a jerk.  Nobody likes to hear about the problems or shortcomings of the software they wrote, and managers don't like hearing that a product won't be ready.  As a professional fault-finder, it also becomes very easy to sink into a morass of unjustified pessimism about a product.  In this chapter, we'll discuss how to deal with these problems and successfully interact with all the people necessary to bring a project to completion.

## Who and What are Stakeholders?

A __stakeholder__ is any person who has a direct interest in the product.  The specific kind of interest may vary based on the person and their role.  For example, the customer of a product---that is, the person who pays for it---will have a vested interest in paying as little as possible for the product.  Upper management and marketers have the exact opposite goal---they want customers to pay as much for it as possible, within epsilon of the price where people would choose a competitor.  Developers may have an interest in seeing the product written correctly, or using a language or framework that they prefer.  Quality assurance personnel may care about the quality of a product; assessors may care that the product meets all of its legal requirements; the list goes on and on.

Note that stakeholders have a _direct_ interest in the product.  In the philosophical sense, many others will have an interest in the product, or at least will be impacted by it.  For example, the owners of the coffee shop next door will hope that developers start working late and thus start buying more of that sweet, sweet caffeine that comes with their coffee, thus improving their bottom line.  The spouses of the testers may want there to be fewer defects so that the testers can spend more time with their family.  However, these are not direct interests in the product, and it could be argued that any human being is somehow impacted by the project (the Prime Minister of Luxembourg may hope to have your nation's GDP go up in order to improve their position in trade negotiations, and a successful launch of your product will help that goal!)  Although it can be a fuzzy boundary, if a person is not directly familiar with your product, they are in all likelihood not a stakeholder.

As mentioned above, different stakeholders will care about different aspects of the software.  When discussing the product with someone who is in a different stakeholder group than yourself, keep in mind what _they_ are thinking about when they think about the product.  Put yourself in their shoes; does an ordinary user of your system care if the application was written in Haskell, Ruby, or Java?  Does upper management in a Fortune 500 company care about the beautiful symmetry of the icons?  Does a developer care about the latest quarterly earnings report?  Perhaps, in a few cases, or there may be some general curiosity or indirect interest.  After all, if quarterly earnings are negative too many times, there may not be a company to pay the developer's salary, or an ordinary user may also really care about type safety in the programming languages of the applications that they use.  However, in general, people spend enough time worrying about the aspects of the system that they care about that they have very little time for worrying about the rest of it.

The following is a non-exhaustive list of groups of stakeholders and a high-level view of what they are likely to care about.  Depending on the domain in which you are working, there are bound to be additional classifications, or some of these may be combined, but this should give you a general idea.

* _Customers:_ These are the people who will pay for the software.  They will focus on receiving a working system for a low price, and care about cost and the return on investment of purchasing it.
* _Users:_ These are the people who will use the software.  Note that these are sometimes the same as customers, but sometimes not---for example, when a school purchases class registration software, the school is the customer, but students are the users.  They will care about the usability of the system and if it allows them to easily accomplish their goals.
* _Project Management:_ These are the people who manage the specific project, ensuring that it is developed at an appropriate rate and released on time and on budget.  They will care about scheduling (from a resource, time, and scope perspective) and software quality.
* _Upper Management:_ Usually higher up in the management chain, to the point where they will often not be very familiar with a project itself.  They will care about the financials of the project, such as whether or not it is likely to make a profit.
* _Developers:_ The people who write the software. They will care about the tools that they use, how well the program works from a technological standpoint, and how well it solves the problem and meets the requirements.
* _Testers / Quality Assurance:_ The people who test the software and determine the quality of the system.  They will focus on finding defects on the software and care about releasing a quality product.
* _Support Personnel:_ The people who keep the software running, such as field engineers, help desk personnel, and deployment personnel.  They will care about uptime and quality of the system, and its ease of use on behalf of customers.
* _Assessors:_ These people focus on the assessing the legality of a system, ensuring that it meets all the demands made of it by laws for the domain in which it is operating.  They will care about meeting the legal or other documented requirements.

This is only a rough guide to some of the kinds of stakeholders you will interact with as a software tester.  Remember that these are drawn with very broad strokes!  People are individuals, not faceless members of groups, no matter what your friend who has read too many philosophy books has to say.  Although you can use this information to get a general idea of what individual stakeholders are interested in, nothing will take the place of having real interactions, and more importantly, _asking_ what is important to them.

## Reporting and Communicating

When communicating with a stakeholder who has a different focus from you, you should take care to understand the language of that person and what they care about. You should care enough to talk about the things they care about in their language.  Try to put yourself in their shoes before talking to them---first, ask yourself if they care about what you want to talk with them about.  If not, try to think if there is any deeper reason you want to discuss it with them.  In some cases, it is still essential---your manager may not care about a harassment claim, but it's still your duty to report it.  In other cases, though, it won't be necessary, and for someone who has quite a bit on their plate (as most workers do today), it's taking away valuable time that could be used for doing other things.  Second, if they do care about the topic, try to put it in terms that they understand and can conceptualize.  Don't view a conversation as a way to prove your intellect.  Use it as a way to provide valuable information in a form that the other person can use, and receive valuable information that you can likewise use.

One of the key chasms in communication is between technical and non-technical personnel.  If you're reading this book, and I tell you that since you've got a O(n^2) sorting algorithm, you're going to see an exponential increase in RAM usage with larger data sets, you're going to have a pretty good idea of what I mean.  You may even know how to fix it (by quickly searching for "efficient sorting algorithms", of course).  However, this sentence is basically Greek to non-technical personnel (except for fluent speakers of Greek, for whom it is some other language that they don't know).  However, this is the way developers, testers, and other technical personnel talk, because it's how you end up thinking when you deal with it all day, every day.  Remember, though, that other people may spend the majority of their day dealing with accounting, or sales, or marketing, or a million other things, and simply do not have the same frame of reference as you do when it comes to the system you are working on.

If you are communicating with those who are not technical or do not have the domain knowledge of the software under test, remember to explain things as a consequence they care about.  Upper management does not directly care about which sorting algorithm the program uses, but they do care if it means that only small businesses will be able to use the software because it does not handle the data sets of larger businesses.  This has a direct impact that they can understand.  When you are discussing a defect with a developer, you can be more technical and explain the situation in more detail.

When you're in school, the teachers tend to have more knowledge than you on whatever topic you're learning.  That's why they are teachers.  In the real world, though, your managers will often have much less knowledge than you on the specific system or part of the system you are working on.  This can be a shock---isn't the whole point of having bosses to have someone who understands something better than their subordinates?

Not at all.  The point of a manager is to manage.  This means more time spent on estimating, more time dealing with personnel issues, more time dealing with budget issues, etc.  This leaves precious little time for writing code or sometimes even interacting with the system at all.  Even if the manager does remain technical, they are now overseeing a larger part of the system, or even the entire system, and thus will not be able to keep up with as many specifics as you have on the particular part of the system you're working on.  Imagine someone working at the Department of Motor Vehicles, who focuses on renewing driver's licenses---let's call them Redli.  Redli is going to have driver's license renewals down cold.  A person transferring from out-of-state?  Someone has the wrong form of identification?  A new driver who has an old license which was suspended, but a governor's pardon has lifted the felony from their record, thus allowing them to drive again?  Redli knows all of the regulations and laws around all of them, knows exactly how to enter them into the system, and does it quickly and efficiently.

Now let's imagine Guvvy, the governor who gave out that pardon.  Guvvy is, technically speaking, Redli's boss (more like a great-great-great-great-great-grand-boss).  If you put Guvvy in Redli's place tomorrow, all hell will break loose.  Being the executive in charge of the entire state, Guvvy had to have a high-level knowledge of not only the Department of Motor Vehicles, but also environmental regulations, business conditions, the budget of the government, and lots of other things besides.  There is no way Guvvy is going to know the specifics of driver's license renewal and how to take somebody's picture, thus leading to a long line of angry motorists at the local DMV office.

This example was extended _ad absurdum_, but the point remains.  As an individual contributor, you will be focusing on a very small part of a larger project, but you will often have very detailed knowledge of it.  Managers will have a broader view of a project or projects, but will have less knowledge on the specifics of it.  The further up the chain you go, the more this is true; your immediate supervisor will have a good idea of what you do on a day-to-day basis, but the CEO of the company may not even know that you---or your project---exists.

If Redli has a chance to talk to Guvvy about some problems with the driver's license renewal process, a bad idea would be to start with technical details of regulation 437-A, subsection 4, paragraph C, and its definition of "resident".  Redli should talk about it in terms that Guvvy understands---things that annoy voters and would make them more likely to vote for AntiGuvvy (who is, of course, the opponent in the upcoming gubernatorial election).  Guvvy is going to be more receptive to knowing that the law doesn't handle people who own houses in two different states than going into detail about the legalese.  This is impactful for politicians because annoyed voters are less likely to vote for the incumbent (note to political science majors---I am dramatically oversimplifying to make a point, so please do not send me angry letters about gubernatorial election theory).

Similarly, when discussing the system or problems that you are having with your boss, put it into terms that they can understand.  Remember that they often have a broader view of the system than you do, and things that you consider very important may not be as important to them.  In fact, they may not even be aware of problems that you consider obvious.  Providing an open flow of information can be very helpful in both directions, allowing you as a tester to understand the system more holistically and channel your energy and time appropriately.  It can also give your supervisors knowledge of the nitty-gritty of the data, defects, and concerns you are finding in your testing.

## The Red-Yellow-Green Template

One of the best ways I have found to communicate status to managers higher up on the totem pole is the red-yellow-green template.  This is not my invention, or even unique to the software industry, but has been proven useful in many different fields.  It allows you to provide a very high-level overview of status while still providing hooks to go deeper into detail if necessary.  Remember that managers will often not have the same granularity of knowledge of the system that you as a tester will have, and so putting it into simpler terms will allow the system to be intellectually manageable.

If you're familiar with US traffic lights, you know that they consist of three lights: green meaning "go", yellow meaning "slow down", and red meaning "stop".  The standard OS X Windows manager uses a similar convention: green for "maximize", yellow for "minimize", and red for "close".  In each case, green means there is nothing stopping you (drive quickly, maximum window size), yellow means that there are some impediments to progress (the light is about to change to red, the window is minimized), and red means that there are some more serious impediments (traffic is coming from the orthogonal direction, the window is closed).

Using this metaphor, we can divide the system into subsystems or aspects, and mark each one with a red, yellow, or green status.  A green status indicates that there are no issues---that particular subsystem is working fine and/or is on track to being completed on target and on budget.  A yellow status indicates that there a few issues, but they are relatively minor and fixable, although that subsystem may have reduced quality or functionality, or additional resources may be necessary to complete it on time.  A red status indicates a major problem or problems, where that particular subsystem will need substantial help in order to be released on time, if it is even possible to do so.  Putting these into colors allows the eye, which has been trained on these particular colors for years (not to mention "trained" by evolution for millions of years), to quickly ascertain a high-level view of the quality of a system.  Partitioning status into the broad categories of "red-yellow-green" means that you are not going to get a very granular view of the status, but the benefit is that it forces you to put the status into very simple terms.  People tend to deal better with a limited number of options for status.

Dividing the system into subsystems is often already done at this point---for example, you can divide them up based on how you've already developed test plans, or how different work has been assigned to members of the team.  You can adjust it based on what will work best for reporting, however, and whatever makes logical sense.  Remember when interacting with other stakeholders, especially when you are crossing the technical/non-technical divide, that you should take into consideration what they care about, and reduce the focus on what you care about.  Let's assume that your project manager has divided the system up into Subsystems A, B, and C. You have developed your test plans into Subsystems A, B, C, and D, because you feel that D makes more sense as its own subsystem instead of as a part of C.  In most cases, this means that your best course of action when reporting to the project manager is to group your D and C statuses together into Subsystem C.

Along with each subsystem and its status, there should be a short notes section going into detail about _why_ that specific status was chosen.  This section is usually only a few sentences, but provides insight into what possible problems could crop up.  It also allows for knowledgeable questions to be asked, and does not rely solely on the producer of the status for determining it.  Another stakeholder may see what seems like a minor problem to the tester, but actually has major import for delivering the system.

Let's walk through some examples to see how we can use the red-yellow-green template to quickly display status to a manager.  These two examples both involve a system which accepts customer information via an API, stores it in a database, and then emails weekly reports to the marketing department:

```
--------------------------------------------------------------------------------
 Subsystem    Status   Notes
----------- ---------- ---------------------------------------------------------
 Database     Green    Test plan passed with no defects. Performance meets or
                       exceeds all KPIs.

 Input API    Green    Latest version passed all tests, including all edge
                       cases, without any defects.

 Report       Yellow   Several arithmetic errors found on latest test run.
 Generation            May need one additional developer to complete all
                       functionality on schedule, but likely to be on target
                       as-is.

 Email        Green    Two minor design defects found, but due to be fixed by
                       tomorrow.
--------------------------------------------------------------------------------
```

In this first instance, we have a system which is going well.  There are no known major problems, and no worries about major schedule slippage or scope reduction.  At a glance, we can see a sea of green, with only one small island of yellow.  Importantly, it's possible to see why these subsystems have the status they do.  If a stakeholder wanted to know more detail about the design defects in the emails, they can ask more questions, or if they want to know what edge cases were checked in the input API, they can do so.

Now let's look at another version of the system which is perhaps not going as well:

```
--------------------------------------------------------------------------------
 Subsystem    Status   Notes
----------- ---------- ---------------------------------------------------------
 Database     Red      Database cannot store more than one customer's
                       information at a time and randomly deletes data every
                       Thursday.

 Input API    Yellow   System takes several minutes to process each (one
                       kilobyte) request.

 Report       Red      All reports just say "LOL" hundreds of times, and the
 Generation            developer in charge of this seems to have fled to
                       Belarus.

 Email        Red      As far as the testing team can determine, there is no
                       email functionality at this time, and no developers
                       scheduled to work on it.
--------------------------------------------------------------------------------
```

This is not a project that I would like to be managing.  Our nice, green sea has been replaced with a hellish landscape of red.  Even the one yellow subsystem, the Input API, is probably going to require some additional work before it's ready to be released.  Note that this yellow status is very different from the yellow status in the previous example.  These statuses are very broad; having a few known arithmetic errors is an issue which we can probably deal with by making a few simple code changes.  Having a performance issue of the magnitude described here may be very difficult to fix, but the program is still releasable with it, just very slow.  Remember that statuses are subjective and how you categorize subsystems will vary based on the domain of the system you are working on.  For example, a program which crashes once per year of normal use may be acceptable for a video game, but it would be unacceptable for avionics software.

Overall, though, the goal of using this template is to report the status of a system under test to others.  It is not meant for an in-depth review or to stand in for a test report, but merely a way to summarize how a system is operating.  Managers and other stakeholders will appreciate having a way to see the status of the system as a whole before diving down into the technical details.

## Status Reports

Although useful for providing the status of a system, the red-yellow-green template is less useful when describing the status of a tester.  In many places of employment, a daily status report is common.  I found these very useful when dealing with a geographically distributed team, especially if there is little communication during the day (for example, because parts of the team are in different time zones).  Many agile development shops will have daily stand-ups to discuss status, and so an additional email is superfluous.  In workplaces that do not have these or similar meetings, I have found that a quick email at the end of the day will allow managers to understand what all of their employees are doing.  It also allows managers to know if there are any problems, and to provide a check to ensure that their employees are working efficiently and on the correct problems.

### Example: Daily Status Report For A Software Tester

**DAILY STATUS: 7 AUG 2015**

* Finished running Test Plan "Database Subsystem Regression"---recorded as Test Run 471, no new defects
* Wrote script to convert old tab-delimited test data to new comma-delimited format---available in `/scripts` directory on server
* Started writing Test Plan "Graphical Symbology Display"---need to get latest version of symbology standard

BLOCKERS: Need to find latest version of symbology standards before finishing test plan

----

These should not take very long to write; a few sentences should suffice, and bullet points allow for a good overall summary instead of focusing on developing a narrative.  This simple email allows the manager to know what the tester is working on (writing a new test plan), what additional resources are available (a script for reformatting data, which may be helpful for other team members), and where the tester may need additional resources (the latest version of the symbology standard).

Armed with this information, a manager can ask the team members to refocus efforts, or report up to their own manager that there are problems.  They may be able to help with any problems that the tester is experiencing; perhaps they have a copy of the symbology standard the tester can borrow.  Finally, the team can be run more effectively when knowledge is shared in such a manner.  If the entire team can run the script that the tester has developed, they may save hours of time that would have been spent updating the test data files manually.

## A Note on Managing Expectations

As a new member of the team, often there is an urge to promise more than you can deliver.  Although it seems like this is the way to win hearts and minds, it can actually be very problematic.  Software projects almost inevitably run late, and it's fiendishly difficult to accurately estimate how long anything is going to take while developing software.  A project manager is going to be more upset that you promised them something and did not deliver than if you promise a little and deliver quite a bit.  Additionally, the fact that you will have less stress when trying to meet a less ambitious goal may make it easier to actually accomplish more, since you're less likely to make a mistake.

You want to manage expectations.  People will tend to assume that if you don't mention something, then everything is going well with it.  This is a dangerous assumption, but it is also human nature, and going against human nature is a sure-fire way to be disappointed (for examples, see every single project to make a utopian society in the history of Mankind).  Thus, you want to communicate early and communicate often.  If there are problems, don't wait until the last minute to let other stakeholders know, hoping against hope that you'll be able to best them through your heroic efforts.  Software development is not an epic fairy tale, where a noble hero can defeat the evil hordes of defects through sheer willpower and a wise-cracking sidekick.

A professor once said to me, "if you're ever in doubt over whether or not to communicate something, do it."  More information is almost always better than less, especially about problems.  Software development is going to have problems, and testing specifically is always going to uncover defects (if it didn't, I would have been out of a job long ago).  If you have appropriate avenues for communicating these found defects, as well as issues and needs for resources, other stakeholders will appreciate being kept in the loop.

This does not mean that you should spread the news of everything that happens to you far and wide.  Upper management doesn't need to know about every defect you find, and the software developers don't need to know where you went for lunch.  Use the proper channels of communication, which will vary based on the team you are working with.  A daily status report to your immediate manager is usually very useful, because it will provide a secondary view at what might be considered important to other stakeholders.  For example, you may have found what you think is a minor defect, and include it only as a bullet point in your daily status, but your manager realizes that it could have far-reaching ramifications and announces it to the larger team.

## A Note on Meetings

Very few people really enjoy meetings, outside of those who are probably busy taking courses in business school instead of reading a book about software testing.  However, they are often essential to determining the best path forward, and ensuring that the input of all relevant stakeholders is heard.  They often can actually be the most efficient way to get consensus on an issue, as well.

This does not mean that your presence is required at all meetings.  If you find yourself not getting any useful information, or not giving out much information---or at least not enough to justify the time you spend on it---you should consider not going to that meeting any more.  Although it may seem presumptuous to say that you don't think that you belong in a meeting, remember that any time you spend in a meeting is time that you are not spending doing something else.  A good manager will thank you for bringing it to their attention, because it means that you are thinking of your job strategically, and not just doing what is asked of you.

## Clarifying Requirements

One of the most common and important conversations you will have as a tester is clarifying requirements.  Writing down what a software system needs to do is very difficult.  It's almost impossible to do for a non-trivial system without introducing some ambiguity.  Testers will often come across these areas of ambiguity because they are constantly pushing the envelope of what a system is capable of, trying edge cases and corner cases with abandon.  After discovering one of these undefined or under-defined areas, they will need to come to a decision on what is the expected behavior.

If possible, take a moment to step back and think about how the requirement works in tandem with all of the other requirements.  Did you miss something?  Does this requirement make more sense in light of what other requirements are saying?  Is there a logical conclusion that can be made of how the system should act when considered holistically as opposed to focusing on the exact terminology of this particular requirement?

If you still have questions or think you have found some ambiguity, you should discuss the problem with the relevant stakeholders.  These stakeholders will vary based on the domain of the software you're working on and the kind of team you're working with.  In many large companies, systems engineers are in charge of requirements definitions and can help you understand what they were trying to convey.  If it is a design issue, perhaps the UI/UX designers can help you.  If you are working on a startup or a very small team, you may even ask users directly what they think the software should do under those circumstances.

When seeking to clarify requirements, keep in mind that your job as a tester is to objectively test that the system meets the requirements, not to make them!  That means that in general, you should assume that other stakeholders have a better idea of what the expected behavior of a system should be.  This does not mean that you should ignore your thoughts on the matter, or stand idly by while people let you know that "of _course_ the calculator subsystem should crash if anybody enters a number greater than 24."  You should respectfully disagree and tell people your opinions and what you've discovered from a technical perspective.  This is part of being a professional.  However, other stakeholders are also professionals in their particular roles.  Those whose goals focus on _generating_ requirements instead of _testing_ them will often be a more authoritative source for answers.

Finally, if you cannot reason out the best solution, and other stakeholders don't know, you may need to make your own assumption as to the expected behavior.  This is definitely not the preferred solution, but often it is the only possible one.  If nobody has thought about a particular edge case, but you have determined that it needs to be tested, you need to come up with some sort of expected behavior.  Make sure that your assumption is internally and externally consistent with the other requirements of the system, and that it makes sense, at least to you, as reasonable behavior.  When you do this, you should be cognizant of the fact that your assumption may be wrong.  At a bare minimum, mark down what assumptions you made, as part of the test plan or otherwise appropriately documented.  You may want to let other stakeholders know what the assumptions you made were and why you chose them.

Remember that translating from a requirements specification to an actual working system is not an objective, straightforward process.  If it were, we would have no need of technical personnel; we'd merely need to talk about the system that is necessary and a compiler would create it for us.  However, English (or any other natural language) is not nearly specific enough to describe a system in as much detail as a computer needs.  Even if it were, the human mind may not be able to comprehend a listing of the thousands, if not millions, of requirements such a system would entail.  Communicating with others will continue to be an essential part of testing software.

## Ethical Obligations

As a tester of software, you  have obligations to ensure that you are doing your job in an ethical and upright manner.  One may argue that one's job is simply that - a job - and that the benchmark for success is simply to do exactly what is expected of you by your superiors.  However, I would say that the position of tester is a profession.  A profession has obligations outside of the particular company for which the person is doing work.  For example, no (reputable) psychiatrist would violate patient confidentiality in order to make their job easier.  A lawyer should not bill hours that they didn't work, even if it would make their firm more money.

Similarly, a tester should stand up when the situation demands it.  If you have determined that the software is storing personal information in an insecure manner, but your manager has ordered you to ignore it so that the software can be released earlier, what should you do?  If you think that the team is spending too much time adding new features and not enough time fixing defects, is that something that you should bring up to your manager?  Suppose the software itself is doing something underhanded, such as spying on users or sending unsolicited commercial email to millions of email addresses.  Should you continue to work at the company, or on the software?  Should you report it to the media or appropriate law enforcement personnel?  Of course, you may have to pay for toeing the moral line, with additional work, loss of trust from your peers or leaders, or even the loss of your job.  While it's easy to read and discuss ethical dilemmas from a textbook, it's an entirely different matter when your child may not eat unless you do continue doing something morally dubious.

This is a tough line to walk, and there are no easy answers.  If you wait until you have determined that there are absolutely no defects in the software being produced which might cause an issue, then the software will never be released.  If you act solely as a dispassionate observer, drily noting in a footnote that the product could easily cause loss of life, then you are not acting in an ethical manner - even if you followed the letter of the rules.  

What you cannot do is ignore the ethical quandaries which come with being a software tester.  Aside from facing mundane software development ethical issues - such as entering time correctly, not falsifying test reports, etc. - you will, in all likelihood, encounter these less tractable issues.  I recommend you at least think about what your code of ethics is before you encounter such situations in reality.

## Respect

You may have noticed that this subject is full of caveats.  There's a reason for that---dealing with people is hard and full of ambiguity.  In comparison, dealing with software can be a walk in the park.  Part of being a professional is learning to deal with these difficulties and ambiguities with grace and aplomb, and it's very difficult to put together step by step instructions or a template for that.

Much of this chapter can be summarized by the phrase, "be respectful".  Remember that other stakeholders are going to care about different aspects of the system, or they may have a different view of the best path forward.  They may not understand everything that you do, and you may not understand anything that they do.  They may not have the same technical background or domain knowledge as you, leading to very different views of the same data.

It takes more than one kind of stakeholder to see a program to completion, and there are bound to be disagreements.  You are unlikely to change anybody's mind by treating them disrespectfully or condescendingly, and small bits of bad interaction may poison the entire well.  Keep in mind that you are looking at the problem from a very specific point of view, and you don't always have all of the answers.  If you treat people respectfully and listen dispassionately to what stakeholders have to say, you may even change your mind.  Even if you don't, ensuring peaceful dialogue amongst team members---especially those with whom you disagree---will go a long way towards successfully releasing a software product.