# Test-Driven Development

Although we have covered how to write unit tests from a broad perspective, the question remains---how do we integrate test writing into the software development process?  In the old days, software testing was often an entirely separate process from writing the code, but today, software quality is the job of developers, as well.  Conversely, software testing has acquired many aspects of development; it is the rare tester who never has to write any code.  Even testers who mostly do manual testing will often write integration scripts or other tools.

Test-Driven Development (TDD) is one methodology for writing quality software  with a well-thought-out testing suite.  By following the tenets of TDD, developers will know what to test, in what order, and a way of balancing unit testing and coding the application under test.  It's not a panacea, of course.  In the software world, as Frederick Brooks reminds us, there is no silver bullet.  However, by using TDD properly, the werewolf of software development can be tamed a little bit.

## What is TDD?

Test-Driven Development is a software development methodology that comprises several key points:

1. _Writing tests first, before code:_ Before you even start thinking of _how_ to do something, this forces you to think of _what_ is to be done.  Since your code has not been written, you can check that the test initially fails (in order to avoid tautological tests which always pass), and have a specific goal that you are reaching toward (getting the test you just wrote to pass).

2. _Writing only code that makes the test pass:_ This ensures that you focus on writing relevant code, instead of spending time working on possibly superfluous frameworking or other code.  One of the key benefits of TDD is that it allows you to focus, by training you to keep your eye on the one goal of the cycle instead of thinking of all the other possible bits of code that you could be writing.

3. _Writing only tests that test the code:_ It's tempting to write tests for the sake of writing them; this will help to keep tests only being written for the functionality being written.

4. _A short turnaround cycle:_ TDD emphasizes quick cycles, which work to keep the developer on track and focused on a short, specific goal.

5. _Refactoring early and often:_ __Refactoring__ is the process of changing code without changing its external functionality.  This may include actions as simple as changing a variable name or adding a comment, all the way to modifying key architectures or algorithms.  What differentiates from refactoring from just "writing code" is that refactoring improves the internal quality of the codebase without having a direct effect on the external quality.  While refactoring does not have an immediate effect on the external quality of the system under test, however, it will often have an indirect effect.  This is because refactoring can make the code easier to read, understand, maintain, and modify.  As the process of development continues, refactoring will make it easier for developers to continue to do their work.

Here is an example of a poorly-written program.  We will refactor it to be easier to read, without modifying any of its actual functionality.

```java
public class Hours {

    public static void main(String[] args) {
        double chikChirik = 792.34;
        try {
            chikChirik = Double.parseDouble(args[40 / 3 - 13]);
        } catch (Exception ex) {
            System.exit(1 * 1 * 1);
        }
        int kukurigu = 160 % 100;
        int gruhGruh = (2 * 2 * 2 * 2 * 2 * 2) - 4;
        System.out.println((chikChirik * kukurigu * gruhGruh) + " seconds");
    }
}
```

The first thing that we notice is that there are absolutely no comments.  This will make it difficult to read.  Also, the use of Bulgarian animal noise onomatopoeias for variable names, while perhaps interesting from a linguistic standpoint, does not give you much information on what those variables are supposed to represent (_chik-chirik_ is the noise that Bulgarian birds make, _kukurigu_ what Bulgarian roosters make, and _gruh-gruh_ what Bulgarian pigs make).  There is also unnecessary variable setting and complication.  For example, both `kukurigu` and `gruhGruh` variables are set to 60 after the computations take place.  Variable `chikChirik` will never actually be used with its default value of 792.34; why is it set to this very particular value?  All exceptions are caught from the line where  `chikChirik` is set; we should check for very discrete possible failure modes.  Several of our variables are never modified - these should be constants (in Java, `final` variables).  Finally, there is most likely the opportunity to partition some of this computation into separate methods instead of doing everything in the main method.

All of these are problems that can be fixed without modifying how the program actually behaves.  This is what makes this process _refactoring_ instead of fixing defects.  The code itself works as advertised, it just does not do it in a way which will make further development easy.  Let's fix some of these problems and see how the refactored code looks.  Software development is a very complicated process, one which often stretches the minds of even the best programmers, testers, and managers.  Whatever we can do to reduce the cognitive burden on ourselves and future team members will certainly be appreciated!


```java
public class Hours {

    final static int MINUTES_PER_HOUR = 60;
    final static int SECONDS_PER_MINUTE = 60;

    /**
     * Given a number of hours, return the number of seconds that
     * would be equivalent to that number of hours.
     */
    
    public static double calculateSeconds(double hours) {
        return hours * MINUTES_PER_HOUR * SECONDS_PER_MINUTE;
    }

    /**
     * Given a double representing the number of hours as the first
     * argument on the command line, this will print out the number
     * of seconds in that number of hours.  
     * For example, 1 hour = 3600.0 seconds.
     * Additional arguments from the command line are ignored.
     */
    
    public static void main(String[] args) {
        double numHours = -1;
        try {
            numHours = Double.parseDouble(args[0]);
        } catch (NumberFormatException nfex) {
            // The argument passed in could not be parsed
            System.exit(1);
        } catch (ArrayIndexOutOfBoundsException oobex) {
            // No argument was passed in
            System.exit(1);
        }
        System.out.println(calculateSeconds(numHours) + " seconds");
        
    }
    
}
```

This is much easier to read and understand, even though its behavior is exactly the same as the original, unrefactored code.  This will also allow us to more easily make modifications.  Let's say that we wanted to display an error message instead of silently exiting if an argument could not be read or parsed.  With the refactored code, we can see the various failure modes and easily add appropriate error messages based on the problem (e.g., "Argument could not be parsed as a double." or "At least one argument must be passed in.").  Perhaps we want to modify our program to calculate French Revolutionary Time, which had 100 seconds per minute and 100 minutes per hour (and 10 hours in a day).  It is very simple for me to see the constants indicating values for `SECONDS_PER_MINUTE` and `MINUTES_PER_HOUR` and modify them to the appropriate values.  It would have been much more difficult with the original code.

Sadly, refactoring is often held off until later in the development process, when it is much more difficult to do.  This is especially the case if there has not been much time spent on refactoring earlier, or if the development team has little experience in refactoring code.  The difficulties encountered in refactoring then becomes an excuse to continue to avoid doing it.  It becomes a self-fulfilling prophecy; avoiding refactoring of code makes it even more difficult to refactor!  By refactoring often, it becomes a part of the development process and a habit, instead of something that will be done "if there's enough time" (note: there is never enough time).

## The Red-Green-Refactor Loop

We work within these constraints by using the "red-green-refactor" loop.  A single cycle in TDD involves the following three steps:

1. _Red:_ TDD is a form of __test-first development__ (TFD), so the first thing to do is write a test.  The developer writes a failing test for a new piece of functionality or an edge case that should be checked.  The newly written test---and only that test---should fail.  If the newly written test does not fail, that means that the code has already been written for that functionality.  If other tests fail, this means that there is a problem with the test suite---perhaps an intermittent or non-deterministic failure of a test---that should be fixed before moving on.  This phase is called "red" because many unit testing frameworks will display failing tests in red.  Since red-green colorblindness affects a good portion of the human population, and humans are by far the most likely animal to program, this may not be the best color selection.  Regardless, we will follow this standardized naming convention.

2. _Green:_ The developer now writes code to make this test pass. This work will focus only on making this test pass, while not causing any other tests to fail.  At this point, some "ugly" code is to be expected; the focus is on making it work as opposed to making it pretty.  If other tests fail, then the developer has inadvertently caused a regression and should work on fixing that.  At the end of this phase, all tests should be passing ("green").

3. _Refactor:_ Once all the tests pass, the developer should examine the code that was just written and refactor it.  There may be small problems like magic numbers (i.e. "naked" values in a program that are not described or represented by a constant such as `if (mph > 65) { ... }` instead of `if (mph > SPEED_LIMIT) { ... }`) or large problems such as a poorly-chosen algorithm.  These can be fixed during this phase, since in the previous phase the focus was simply on getting the results correct.  An easy way to remember this is the mnemonic "first make it green, then make it clean".  Since there is always a fall-back position of properly functioning (if poorly written) code, the developer can try multiple approaches without worrying about getting to a point where the code doesn't work at all.  In the worst case scenario, the code can be reverted back to where it was at the end of the "green" phase and a different path can be chosen for rewriting.

After each red-green-refactor cycle, the developer should think of the next piece of functionality to add, and then loop back.  This cycling will continue until the software is done. This is a path of testing, coding, and refactoring that will eventually culminate in a complete product.  As a side effect, it will also include a solid test suite that is directly relevant to all the functionality of the program.

This could all be re-written as a very simple algorithm.  By doing so, we can see how this helps focus the attention of the person writing the software; there is always a well-defined next step:

1. Write a test for functionality which has not been written yet.
2. Run test suite---only the newly written test should fail.  If not, first figure out why other tests are failing and fix that problem.
3. Write enough code to make that test pass, without causing other tests to fail
4. Run test suite---if any test fails, go back to step 3.  If all tests pass, continue.
5. Refactor code that you have written, and/or any associated code.
6. Run test suite---if any tests fail, go back to step 5.  If all tests pass, continue.
7. If there is any more functionality to add, go to step 1.  If there is no more functionality to add, the application is complete!

## Principles of Test-Driven Development

There are several principles to keep in mind when writing in a TDD manner.

* _YAGNI (You Ain't Gonna Need It):_ Don't write any code that you don't need in order to make the tests pass!  It's always tempting to make a nice abstract system which can handle all sorts of different future variations on whatever it is you're doing now, but you will also make the code more complex.  What's worse, you will be making it more complex in ways that may not ever help the system's future development.  Avoid complexity until it's absolutely necessary.  If there are more edge cases or equivalence classes that need to be dealt with, add more tests first.

* _KISS (Keep It Simple, Stupid):_ One of the goals of TDD is to ensure that the codebase is flexible and extensible, and one of the greatest enemies of those two goals is complexity.  Complex systems are difficult to understand and thus modify; complex systems tend to be overfit to the specific problem they were developed for, and it's difficult to add new features or functionality.  Keep your code simple and your design simple, and consciously avoid adding additional complexity.

* _Fake It 'Til You Make It:_ It's okay to use fake methods and objects in your tests, or just use a placeholder such as `return 0;` as the entire body of a method.  You can come back later with additional tests and code once they are necessary.

* _Avoid Slow Running Tests:_ If you are working with TDD, you are running at least three full test runs each iteration through the red-green-refactor loop.  That's a minimum and assuming that your code never causes problems in other tests or has any defects of its own.  If running your test suite takes two or three seconds, this is a minor price to pay for the extra quality that TDD provides; if it takes several hours, how long before developers are going to start ignoring the process in order to actually get some work done?

* _Remember That These Are Principles, Not Laws:_ It would be counterproductive to entirely ignore what else the software needs to do in the next few iterations of the red-green-refactor loop.  Occasionally, a test may be slow but necessary, or actually making a method would be just as simple as adding a fake version of it.  Although you should endeavor to follow the principles of TDD, I know of nobody who has never violated one of the principles (although perhaps that speaks more to the type of people with whom I spend time).

## Example: Building FizzBuzz via TDD

In order to understand how TDD works, let's write a simple `FizzBuzz` program using it.  Recall that `FizzBuzz` consists of:

1. Printing every number from 1 to 100, with the following exceptions.
2. If the number is evenly divisible by both three and five, then the word "FizzBuzz" should be printed instead of the number.
2. If the number is evenly divisible by three, then the word "Fizz" should be printed instead of the number.
3. If the number is evenly divisible by five, then the word "Buzz" should be printed instead of the number.

First, let's build a "walking skeleton" of the application.  Assuming we already have JUnit or a similar testing framework installed, and we aren't deploying it anywhere, all we have to do is generate our initial `FizzBuzz` class.  Since we're iterating through a range of values, each of which is entirely decidable based on its value, let's create a class that has a main method and a `fizzbuzzify` method, which will return the correct string for a given value.

Thinking a little ahead, we know that we're going to have to iterate through the numbers 1 through 100.  Therefore, there are four cases that we'd like to test for:

1. The number itself should be returned, if the number is not evenly divisible by 3 or 5
2. The string "Fizz" should be returned, if the number is evenly divisible by 3 but not evenly divisible by 5
3. The string "Buzz" should be returned, if the number is evenly divisible by 5, but not evenly divisible by 3
4. The string "FizzBuzz" should be returned, if the number is evenly divisible by both 5 and 3

Our testing is helped by the fact that this is a pure function---its return value is entirely determined by the input parameter.  It has no dependence on global values and has no side effects like output, and no other external dependencies.  Sending in 2 will always return "2" and do nothing else, sending in 3 will always return "Buzz" and do nothing else, and so on.

```java
public class FizzBuzz {

    private static String fizzbuzzify(int num) {
        return "";
    }

    public static void main(String args[]) {

    }

}
```

Now let's add our first test, using the first case.  The first number that is not evenly divisible by 3 or 5 is 1, so let's use 1 as the first value to test for our `fizzbuzzify()` method:

```java
public class FizzBuzzTest {

    @Test
    public void test1Returns1() {
        String returnedVal = FizzBuzz.fizzbuzzify(1);
        assertEquals("1", returnedVal);
    }

}
```

If we run this, it will fail---`fizzbuzzify` returns an empty string, which is not equal to 1, and thus the assertion fails.  Well, there's a simple fix for that!

```java
public class FizzBuzz {

    private static String fizzbuzzify(int num) {
        return "1";
    }

    public static void main(String args[]) {

    }

}
```

When we run the test again, it passes!  Let's move on to the next phase and look for refactoring opportunities.  In this case, I don't think there are any; sure, there's a magic number (well, technically a magic string consisting of a number), but what can you do, replace it with a constant `NUMBER_ONE`?  That's not any more understandable.

Let's add another test, for 2, which should return a non-fizzy, non-buzzy string, "2":

```java
public class FizzBuzzTest {

    @Test
    public void test1Returns1() {
        String returnedVal = FizzBuzz.fizzbuzzify(1);
        assertEquals("1", returnedVal);
    }

    public void test2Returns2() {
        String returnedVal = FizzBuzz.fizzbuzzify(2);
        assertEquals("2", returnedVal);
    }

}
```

When we run this, as expected, we get one failure; since our `fizzbuzzify()` method will only ever return 1, it's never going to return 2.  We also note that we didn't cause the initial test to fail by adding this test---the only test that fails is the new one, `test2Returns2()`.  Fixing up the code should be pretty simple, right?

```java
public class FizzBuzz {

    private static String fizzbuzzify(int num) {
        if (num == 1) {
            return "1";
        } else {
            return "2";
        }
    }

    public static void main(String args[]) {

    }

}
```

Now all of our tests pass!  We are coding geniuses!  Go ahead and give yourself a pat on the back!

Of course, this pattern is not going to work going forwards.  Let's refactor the code a bit so that it will work with all integers, instead of having to add a new `else if` for each individual value:

```java
public class FizzBuzz {

    private static String fizzbuzzify(int num) {
        return String.valueOf(num);
    }

    public static void main(String args[]) {

    }

}
```

Much better!  Tests are still passing, so we can move on to the next cycle in the loop.  Let's add a test for `fizzbuzzify(3)`, which should return "Fizz":

```java
    @Test
    public void test3ReturnsFizz() {
        String returnedVal = FizzBuzz.fizzbuzzify(3);
        assertEquals("Fizz", returnedVal);
    }
```

`fizzbuzzify(3)` will actually return "3", of course, causing our test to fail.  However, that can be fixed quickly!

```java
    private static String fizzbuzzify(int num) {
        if (num == 3) {
            return "Fizz";
        } else {
            return String.valueOf(num);
        }
    }
```

Huzzah, our tests pass!  This isn't an ideal solution, though---it will only work with 3, and we know that it should be any number that's evenly divisible by 3.  A bit of refactoring and we should be able to handle any number divisible by 3:

```java
    private static String fizzbuzzify(int num) {
        if (num % 3 == 0) {
            return "Fizz";
        } else {
            return String.valueOf(num);
        }
    }
```

This also might give us more ideas for additional unit tests later---perhaps we want to check if 6, 9, or 3000 work.  For now, though, let's just move on to add "Buzz":

```java
    @Test
    public void test5ReturnsBuzz() {
        String returnedVal = FizzBuzz.fizzbuzzify(5);
        assertEquals("Buzz", returnedVal);
    }
```

Once again, the test will fail, so we add an additional else to our conditional:

```java
    private static String fizzbuzzify(int num) {
        if (num % 3 == 0) {
            return "Fizz";
        } else if (num % 5 == 0) {
            return "Buzz";
        } else {
            return String.valueOf(num);
        }
    }
```

Tests pass now, and there doesn't seem to be any refactoring to do.  Let's try one final test for the "FizzBuzz" return value:

```java
    @Test
    public void test15ReturnsFizzBuzz() {
        String returnedVal = FizzBuzz.fizzbuzzify(15);
        assertEquals("FizzBuzz", returnedVal);
    }
```

This test fails, since the current method will return "Fizz":

```java
    private static String fizzbuzzify(int num) {
        if ((num % 3 == 0) && (num % 5 == 0)) {
            return "FizzBuzz";
        } else if (num % 3 == 0) {
            return "Fizz";
        } else if (num % 5 == 0) {
            return "Buzz";
        } else {
            return String.valueOf(num);
        }
    }
```

Tests are now passing!  We might go further with refactoring---for example, moving `num % 3 == 0` and `num % 5 == 0` to their own methods---but this shows a simple outline of the TDD process.  Oftentimes, steps are bigger in actual development, but a key tenet to keep in mind is to keep the tests relatively specific and targeted at particular output values.  Grouping the input and output values into equivalence classes, as discussed earlier, can help you to decide what needs to be tested and what order to test things in.

## Benefits of TDD

One of the biggest benefits of TDD is that it automatically creates a test suite during development.  Instead of having to worry about fitting in time to develop a testing framework and writing tests, the mere act of development will create one for you.  Testing is, sadly, often relegated to the end of the project (which means that it will be given short shrift or even avoided entirely).  Using TDD ensures that you will at least have some sort of test suite even if other testing is curtailed.

When tests are part of the workflow, people remember to do them.  You probably don't think "ugh, I need to remember to brush my teeth today" every morning when you wake up; it's just a habit that you do as part of your morning routine.  You're more likely to write tests when it's something that you just do all the time and have created a habit around doing.  Since more tests are correlated with higher quality code, this is definitely a good thing!  When things are done more often, they are also easier to do.  Any problems with the test suite will be found quickly, and parts which are problematic and code which is difficult to test will be dealt with sooner.

Yet another benefit is that the tests that you write with TDD are relevant, since new tests must fail first (ensuring that the test is not redundant) and must pass before the cycle of writing a piece of code is considered "complete".  You are less likely in this case to write tests which are unnecessary or tautological, or over-test one area and under-test another.

If you are writing tests after the fact, it's easy to fall into the trap of assuming that what the program does is what the program should do.  However, remember that tests are supposed to check expected behavior against the observed behavior.  If you are "expecting" something that you already "observed", your tests run the risk of being tautological!

TDD forces you to work in small steps.  This helps to ensure that you don't go too far off the path working on something.  If you wrote four lines of code and introduced a defect, it's much easier to find out where you went wrong than if you find the defect after writing a thousand lines of code.  I like to think of writing code as crossing Antarctica with vicious penguins all around, and tests are fortresses against the penguins.  You can easily cross the entire continent if you only go a mile or two before setting up another fortress, as there is always a place close by to retreat to if the penguins get that mad gleam in their eye.  You can then choose another path, perhaps with fewer penguins, and build a fort there.  Crossing the Antarctic without building anti-penguin forts would be a foolhardy maneuver, because any penguin attack might mean re-tracing your steps all the way to your landing craft.  Writing large pieces of code without tests similarly prevents you from making solid progress as any defects may cause you to have to scrap much of the code that you have already written.

When you are testing code from the beginning, the code is much more likely to be testable.  Not only will you learn how to test the code in this particular application because you are doing it all the time, you are not likely to write code that you can't test.  Why would you?  Your code needs to pass the test that you've already written, so you are going to make it in a way that will make it testable.  Since you are also constantly adding on to the codebase, as opposed to seeing it as one large "version" to be committed as a giant block, your code will also be extensible.  You're extending it with each cycle of the red-green-refactor loop!

Using TDD provides 100% test coverage, or at least close to it.  Although code coverage is not a perfect metric---there are plenty of defects that can be hidden in code that is entirely covered by tests---it assures you that you are at least checking each line of code once.  This is much better than many software projects.

Test-Driven Development provides a structured framework to write software with.  Although there are certainly many drawbacks (some of which will be enumerated below) and situations for which it is a suboptimal methodology, it does provide you with a way to move forward.  The strict but flexible steps of the red-green-refactor loop provide developers with a list of things to do next.  You are constantly adding tests, writing code to make them pass, and refactoring.  When you don't have a framework to follow, you may spend lots of time refactoring existing code, or not nearly enough time writing tests, or too much energy writing tests and not writing code.  At a bare minimum, you've got to consider how much time and resources you'd like to spend on each section.  With TDD, you have ready-made answers, so you don't have to think about it, and your mind is clear to work on other things.  There is an excellent book, _The Checklist Manifesto_ by Atul Gawande, which explains how having a checklist (even one as simple as red-green-refactor) can help you in a variety of endeavors.  Software engineering is no exception.

Finally, and most importantly, developing software using TDD can give you confidence in your codebase.  You are walking the tightrope of development with a net; you know that the software you are writing can at least do the things that you ask of it.  You have guard rails that let you know when you've caused problems in other parts of the application.  You have a seasoned team of developers letting you know what the next steps are.  You are not alone.

## Drawbacks of TDD

As mentioned above, there is no silver bullet in software development.  Developing software using TDD has many benefits, but it's not always the correct methodology to use.  Be aware of the following drawbacks before deciding to use TDD.

Developing in TDD means writing many unit tests.  If your team needs to be coerced into testing software in the first place, this focus may drive out other kinds of tests, such as performance testing and systems testing.  You need to keep in mind that just because you have written many unit tests for a method which utilizes some functionality, this does not mean that you have thoroughly tested that functionality.

There is no doubt about it---in the short run, writing tests will mean more time spent to get the same amount of features.  There are benefits, to be sure, such as improved code quality.  However, if one had waited until the night before a project is due for a software class (ahem), TDD would probably not be the way to go.  In this case, a bulletproof program which doesn't meet half the requirements for the homework assignment is much worse than a program which does everything it's supposed to do, as long as you don't pass any invalid parameters to it or hit Control-C or breathe too heavily around it.  However, for larger projects or projects without such a small deadline, using TDD or a similar methodology will often be faster in the long run.  A good analogy is that writing software without tests is like riding a go-kart; it seems really fast, but is actually slow.  Writing software with tests is like riding a jet plane; it seems really slow, but is actually very fast.

Traditionally, TDD provides less time up-front for architecture decisions.  Due to the short cycle time of the red-green-refactor loop, less time may be spent on design and architecture as opposed to writing code which implements user stories.  In many cases, such as simple web applications, this is perfectly valid.  Default architectures may be fine and spending too much time thinking about them may be counterproductive.  In other cases, especially with new kinds or domains of software, architectural choices may be difficult and consequential, and it makes sense to spend more time at the beginning of the project thinking about them.

Furthermore, architectural design changes made later in development may be difficult to implement.  Although the methodology is meant to be flexible, some design decisions would require numerous modifications once code is written.  It may be easier to spend more time earlier in the software development life cycle thinking about what is to be done, instead of assuming that you will be able to make changes later.

Certainly for some application domains, test-driven development is the wrong approach.  If you are building a prototype of something, and are not sure what the expected behavior should be, but you know that it's going to change rapidly and not be used in production, then TDD is overkill.  The ever-growing test suite, which usually acts as a safety net, would become an albatross around your code's neck.  If you are trying to figure out the expected behavior as you go along, it makes little sense to use a methodology which presupposes that you know what the expected behavior is.  In a different vein, extremely safety-critical applications, such as power systems or avionics controls, will require much more design and forethought than TDD can provide.  In this case, TDD may be a little _too_ flexible.

Remember that when you write automated tests, you are actually writing code.  Sure, the code looks a little different, but you're still adding more and more overhead to your codebase.  This is another place for things to go wrong, another place for refactoring, another place to update any time a change is made to the requirements or direction of the project.  Although this overhead is often compensated for with an increase in the quality of the application, in some cases it may not be.  On especially small projects and scripts, it may be much faster to simply do some manual testing to ensure that it does what it's supposed to do, instead of spending the time on developing an entire framework around the application.

Finally, as an engineer, you often do not start with a greenfield (that is, an entirely new) project.  Often, you are modifying or adding features to already-existing software, much of which has been written using different methodologies or paradigms.  If you start working on a project which uses a very rigid Waterfall methodology, or code which is not easily testable, trying to use TDD may be more trouble than it's worth.  It may also alienate you from team members, or force you to spend too much time to develop your features.

