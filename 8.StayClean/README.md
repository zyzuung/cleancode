# Stay Clean

## 1. When to Refactor to Clean Code

- We'll review some simple guidelines for when to refactor existing code using Clean Code Principles, as well as techniques for keeping our code clean. Once you've started enjoying the benefits of Clean Code Principles in the code that you write you'll be tempted to use these same techniques to refactor existing code.

- But, I like to remember the principle of if it isn't broke don't fix it. There's nothing wrong with improving your code base, but before you do so remember three simple rules.

### a. You need to work with the code

- If you're refactoring code it should be code you're currently working with. Refactoring for future readers is of questionable values since it means your means investing time now for readers that may not materialize in the future. 

- If code is hard to read, but exists in a system that's been chugging along reliably for years don't risk changing it merely in a desire for cleanliness.

### b. Difficult to comprehend or change

- Refactoring is useful when you find the code difficult to comprehend or change. 

- I emphasize the word you here because this is truly subjective. If you're fixing a simple bug and find the code clear enough, fix the bug and move on. 

- Excessive refactoring of old code is of questionable value when the size of your change is small. Generally, the size of your refactoring should be in line with the size of the code change that you are making. If you need to make a simple one line change, refactoring multiple methods is likely excessive.

### c. Test coverage to protect from regression

- Before making any changes be sure you have sufficient test coverage to assure yourchanges don't introduce regressions in the code.

## 2. Accept No Broken Windows

- How many times have you worked on a poorly written and maintained code base where developers have given up taking pride in their work?

- This depressing situation doesn't happen overnight. It's the byproduct of many small hacks and compromises that were accepted and overlooked over the years.

🔥 Consider a story from the March 1982 issue of theAtlantic. A building with a few broken windows that aren't repaired has the tendency for vandals to break in and break more windows. Eventually, they may even break into the building and if it's unoccupied, perhaps become squatters or light fires inside.

⚠️ Once people can see that a building has been disrespected it's much more likely for others to treat it inthe same manner. 

❌ This toxic mindset affects software projects as well.

✅ To maintain Clean Code bases and avoid costly ground up rewrites we need to maintain pride in our code bases and not allow the mistakes of our past to open the door for accepting evermore technical debt.

## 3. Code Reviews & Pair Programming

- In both commercial and residential construction building inspectors regularly review work to assure that crews are maintaining a high level of quality and following established policies.

✅ This arrangement is equally useful in software development.

- Code Reviews are a highly effective way to avoid the broken windows mentality that we just discussed.Regularly reminding developers that their code will be peer reviewed promotes higher code quality.

- And setting clear guidelines assures that everyone is clear about the expectations and what is on and off limits for a Code Review.

- Code Reviews assure readability since reviewers must be able to read and comprehend the code to understand it and review it. This is a time consuming process, but just like building inspections the time and cost help protect from the risk of costly problems later. (Consider working in pairs)

✅ Pair Programming offers many of the same benefits as Code Reviews, but in real-time. And pairing increases code quality because developers working together are less likely to take costly and confusing shortcuts when writing code.

✅ Pairing also makes naming and refactoring easier as you have someone else to bounce your ideas off of in real time. There's a variety of other benefits to Pair Programming, but the benefits to code quality alone are enough to justify giving it a shot.

## 4. Boy Scout Rule

> The Boy Scouts have a rule that you should leave the campground a little better than you found it. (Robert C. Martin)

- Robert C. Martin reminds us that we should have this same goal when working with existing code.

✅ If we continually leave our code a little better than we found it then code bases won't need big scary rewrites. They will stay clean.

## 5. Summary

- We were reminded not to go wild and start refactoring any code we see that isn't clean. 

### a. Refactor when necessary

- We should only refactor when necessary and this means it should be code that we currently need to work with and the magnitude of our refactoring should be comparable to the size of the necessary code changes.

### b. Set and maintain standards

- Setting and maintainingcoding standards will help keep our code clean.

### c. Do code reviews and watch for broken windows

- Watching for broken windows during these code reviews will help assure that the quality of our application continues to be respected. 

### d. Pair and share your knowledge

- If you haven't already, give Pair Programming a try using these techniques. You'll likely find it's easier to design your application, select good names, and clarify your intent with a partner. And you're both more likely to strive for clarity in your code by spurring each other on.

### e. Leave the code a little better than you found it!

- Remember the Boy Scout Rule, when your editing existing codestrive to leave it a little better than you found it.

- If we consistently do so then we're far less likely to have to rewrite an application later.
