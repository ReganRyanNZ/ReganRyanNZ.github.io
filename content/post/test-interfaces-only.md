+++
Categories = ["ruby"]
Description = ""
Tags = ["testing"]
date = "2016-08-08T17:11:45+12:00"
menu = "main"
title = "Test Interfaces Only"
+++

Learning code, I never liked tests. Why? Because the process went like this:

1. Write code that works (by manually looking at the results).
2. Write tests to satisfy professors/people that wanted to see tests.

My initial naive thought was: "Why write more code? These tests aren't useful, I've already written the code I need, and it works." Those were dark days, my friend. Then a highly recommended book came my way, Practical Object-oriented Design In Ruby, that showed me code *changes* a lot. Like, a lot. Without tests, you'll need to manually look at *everything* whenever you make a change, to ensure nothing got broken. My process then became this:

1. Write code that works (by manually looking at the results).
2. Write tests on everything, to prove that it works without needing manual inspection.
3. Change the code a little bit.
4. Flip the table because half the tests are now broken (but the code is correct).

After reading the aforementioned textbook a bit more, I realised why I was having such an awful time. I wasn't just testing for the expected output, I was also testing the implementation. I demanded the specific "what", and I demanded the specific "how" as well.

If you, reader, have a sinking feeling that this is you too, then listen closely. Every object should have a public interface (how others talk to it), and a private implementation (how it figures out how to give others what they want). The public methods are the menu at a restaurant. The private methods are the kitchen out back.

With this in mind, consider the following question: If you ask for an item from the menu, does it matter *how* that item is prepared? Did they use a spatula or a spoon? Was the stove on medium heat or high? As long as you get your food, it doesn't matter what specific method they used. With this break through my process is now this:

1. Write code that works (by manually looking at the results).
2. Write tests for the interfaces between objects (checking the output of public methods).
3. Change the code a little bit (different setup in the kitchen).
4. Run tests to ensure the right food is still being served.

Now I can make a change to the inner workings of my code, run my test suite, and know that the program still works. My tests don't trip me up, because I'm not enforcing the "how", only the resulting "what".
