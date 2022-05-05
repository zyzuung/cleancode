# Functions

## 1. Introduce

- a. Create Functions that have a high signal to noise ratio for easy readability

- b. Creating a Function makes sense.

- c. Techniques to maintain simplicity in code

- d. Code smells to avoid and refactoring techniques for eliminating these issues all together

- e. Wrap up by discussing error handling techniques.

### Method vs Function

- Both are simply pieces of code that are called by name.

- The core difference is Methods are associated with an object.

- The two terms are interchangeable.

- The principles apply equally to Methods and Functions.

## 2. When to Create A Function

- Functions help us organize our code into small targeted pieces of logic. This has many of the same benefits as paragraphs when writing. And much like paragraphs it's much easier to understand what the writer is talking about when the paragraph has a clear purpose and doesn't ramble on about seemingly unrelated topics.

- There are 4 common reasons to create a function

### a. To avoid Duplication

- Clean Code honors the DRY Principle and doesn't repeat itself.

### b. Indentation is a sign of complexity

- Some developers think this is the only reason to create a function. But, as we're about to see there are a variety of other reasons that functions are useful, even if the code is only called once. Indentation is a sign of complexity. As code gets to deeplyIndented it becomes hard to understand and maintain. So, this is another great reason to create a Function.

### c. Understanding the programmer's intent

- Understanding the programmer's intent is the hard part. So, we can use well-chosen function names to provide high level summaries of our logic just as headings in a book aid comprehension and navigation.

- Comments can also serve this purpose, but if you're about to write a comment you can instead create a well-named method that helps convey intent.

### d. To help maintain a single responsibility methods

- To help maintain a single responsibility methods should do one thing and one thing well. A method that does one thing shouldn't get very long. Remember long paragraphs become tedious too.

## 3. Avoid Duplication

- The importance of creating functions when I needed to call the same logic multiple times.

- Copying and pasting code made maintenance harder, especially bug fixes, where I'd have to make sure that I'd changed more than one place.

- `DRY (Don't repeat yourself)` is one of the most important principles in software development since it helps assure that we minimize the lines of code that we have to maintain.

- <ins>*Duplicated code*</ins> means two places to maintain, fix, and two redundant places to read.

## 4. Excessive Indentation Overview

- The second reason to create a function is **Excessive Indentation**.

- As our logic grows more complex it's common to see an arrow shape form. **Arrow Code** is defined by its arrow shape, which is a reference to the deep levels of Indentation.

![Arrow Code](/5.Functions/images/arrow_code.png)

- **Arrow Code** is a sign that a method has high cyclomatic complexity. High cyclomatic complexity hurts readability, hinders testing, and increases the likelihood of bugs in a given method.

- This arrow shape also hurts comprehension by reducing signal to noise. The reader has to maintain all the layers in his or her head simultaneously. And the negative impact of deep levels of nesting has been documented in studies as well.

- A 1986 study by Noam Chomsky and Gerald Weinberg found that comprehension decreases beyond three levels of nested 'if' blocks. This excessively nested code is commonly called Arrow Code.

- There are three simple methods to eliminate this toxic Arrow Code: `Extract a Method`, `Fail Fast`, and `Return Early`.

## 5. Extract Method

- When refactoring to a method we simply move related pieces of logic to well-named methods that better convey intent and help us eliminate excessively deep indentation.

- When refactoring Arrow Code its often simplest to start with the most deeply nested code and work your way out.

![Extract Method](/5.Functions/images/extract_method.png)

- Moving this while loop to a method. As you can see, the level of indentation is reduced and the arrow shape is less pronounced.

✅ Refactoring to a method has benefits beyond just removing Arrow Code and reducing cyclomatic complexity of the method. It also enhances readability since readers of this method can now skip over a one liner if they're not interested in the details of how this complex section that we just moved works.

✅ The method remains available for reference by those interested, but it doesn't add noise when one is simply seeking to understand the big picture.

✅ When a class is refactored to many small methods that do one thing well the reader can choose to read at the level of abstraction that is most useful to their purpose.

✅ If the reader is looking for a high level overview of the algorithm thetop level method signatures provide that and if they want details the child methods are there and their names provide clarity of intent.

🔥 <ins>*Summary:*</ins> Ultimately refactoring to a method offers the same benefits as the footnotes that we see here in this article.

## 6. Return Early

- Returning Early is another helpful approach for eliminating deep indentation in our code.

- The big idea with Returning Early is if you have nothing more to do return.

- Let's look at an example. As you can see it's deeply indented

![Return Early](/5.Functions/images/return_early.png)

- As you can see it's deeply indented. This method is validating a user name. There is a variety of reasons that a user name might be invalid.

- <ins>*Note:*</ins> that a local variable is valid is used to store the state of whether the user name is valid and it's defaulted to false at the top of the method.

- Only if all four of the if statements are evaluated to true is the user name found to be valid.

❌ This method has four levels of indentation, which hurts readability.

🔥 Let's review a version that Returns Early.

![Return Early New](/5.Functions/images/return_early_new.png)

🔥 <ins>*Note:*</ins> That in this version there's no indentation at all. There's also no need for the temporary `isValid` variable that was created in the other version. Instead, with each evaluation we check for an attribute that would make the user name invalid and we return as soon as the user name is found to be invalid.

✅ This creates a method with multiple return values, which some might find undesirable.

✅ Years ago it was popular logic to only allow one return statement per function. However, Returning Early can really help tame deeply indented code and thus enhancereadability and maintainability.

> Use a return when it enhances readability…In certain routines, once you know the answer…not returning immediately means that you have to write more code.
(Steve McConnell, Code Complete book)

✅ Returning Early is also helpful because it mimics real life decision making. Once we know there is no reason to move on we stop.

## 7. Fail Fast

- Failing Fast is really simple to comprehend. When there is nothing more that you can do in a method just Fail.

![Fail Fast Dirty](/5.Functions/images/fail_fast_dirty.png)

- Failing in this case means that you throw an exception as soon as an unexpected situation that can't be handled occurs, as you can see here.

![Fail Fast Success](/5.Functions/images/fail_fast_clean.png)

- `Guard Clauses` assure that the inputs to a method are valid before continuing processing.

- Running all `Guard Clauses` and `Retuning Early` simplifies a method byreducing indentation and thus cyclomatic complexity.

- `Guard Clauses` are useful for creating a contract at the top of your method that clarifies the expected state for parameters.

🔥 In this example the user name and password fields are expected to not be null or empty. So, rather than adding levels of nesting that mask the core intent of the method we can place the safety checks at the top of the method and then throw exceptions immediately if an exceptional state is found.

🔥 If a large number of checks are necessary before performing the body of the method it can even be useful to refactor these checks at the top to a named method.

- Failing Fast is also useful when working with switch statements. Every switch should have a default value so you're aware when the switch falls into an unexpected state.

- <ins>*Example:*</ins> What would happen in this example if there wasn't a default.

![Fail Fast Switch](/5.Functions/images/fail_fast_switch.png)

- If someone attempted to login as a user in an unexpected status the system wouldn't log the user in. But, it also wouldn't have thrown an exception. So, we'd likely get a ticket later from a user complaining about their inability to log in and it would be really difficult to figure out why since the system wouldn't have thrown an error in this spot and it may or may not have failed elsewhere depending on how the related code was structured.

🔥 This is `Failing Slow` and it masks root causes and makes debugging a difficult investigative chore. Be sure that you `Fail Fast`.

## 8. Convey Intent

- To Convey Intent, the third reason to create a function.

🔴 Dirty

```dart
// Check for valid file extensions. Confirm admin or active
if(fileExtension == "mp4" ||
   fileExtension == "mpg" ||
   fileExtension == "avi") &&
  (isAdmin || isActiveFile) {
  // do Something
}
```

- With this Conditional you can see the author recognized it was getting complex and chose to use a comment to help clarify.

✅ However, we can completely clarify our intent in code by refactoring this Conditional to a well-named method with good variable names inside.

🟢 Clean

 ```dart
 if(ValidFileRequest(fileExtension, isActiveFile, isAdmin)) {
   // do Something
 }

 bool ValidFileRequest(String fileExtension, bool isActiveFile, bool isAdmin) {
   bool validFileExtensions = new List<String>() {"mp4", "mpg", "avi"};

   bool validFileType = validFileExtensions.contains(fileExtension);
   bool userIsAllowedToViewFile = isActiveFile || isAdmin;

   return validFileType && userIsAllowedToViewFile;
 }
 ```

✅ Again we could refactor since this method is really doing two things.

> 1. It's validating the requested file extension and checking if the user has the rights to view the file.

> 2. Those separate pieces of logic could each be refactored to separate methods so that each method has a clear single responsibility.

## 9. Do One Thing

- `Do one thing` is The fourth and final reason to create a function.

- To keep the signal to noise ratio high our function should do one thing.

- There is a number of advantages to keeping a single responsibility.

🔹 **It aids the reader**: A well-chosen function name summarizes the functionally inside.

🔹 **It promotes reuse**: It also promotes reuse because small focused functions are easier to reuse than larger functions that do many things.

🔹 **It eases naming and testing**: functions that do one thing are much easier to name and if a function is hard to name or has a name that's too broad that's a sign that there's an opportunity to split it up.

🔹 **It helps us avoid side-effects**: The reader should know what the function does by reading the name. If there's other potentially surprising things going on inside consider refactoring to a separate function.

## 10. Mayfly Variables

🔥 Can you imagine reading a chapter in a book where a dozen characters were listed upfront. Traditional books introduce readers to new characters when it's time for them to truly interact with the story. Introductions occur just in time. Introductions occur just in time. This avoid taxing the reader with a lot of information upfront that's not yet value added and totally out of context.

🔥 Initializing all of my variables together at the top. The problem with this approach is, it runs directly contrary to the Rule of Seven.

> Rule of Seven: The reader has to keep track of all these variables throughout their reading and can't remove them from their finite memory until they go out of scope at theend of the function. Plus, anyone considering refactoring this code now has to consider the implications on the variables above.

❌ This adds unnecessary mental weight since any variable in scope must be considered.

❌ Developers run the code in their heads as they read. And having an excessive number of variables in scope is like asking our reader to spin multiple plates at once.

✅ Instead, well-structured functions should contain only `Mayfly`

### What's a Mayfly Variable?

- The Mayfly has one of the shortest lifespans of any creature on earth. Many only live for 30 minutes and the oldest only live for about 24 hours.

![Mayfly](/5.Functions/images/mayfly.png)

✅ We should strive to give our variables Mayfly style lifetimes.

✅ There's two simple ways to do this:

🔥 1. We should Initialize Variables just-in-time:

When the variable is needed bring it to life. And the moment that it is no longer necessary get it out of scope so that the mental weight is lifted.

🔥 2. if you're creating targeted functions that do one thing you're going to end up with Mayfly variables automatically.

Short functions mean variables go in and out of scope in a flash, which makes the readers job less taxing.

## 11. How many parameters?

- A high number of parameters makes a function hard to follow and it's a strong sign that the function is doing too much.

✅ So, we should strive for 0-2 parameters.

- As you focus on writing small focused functions, hitting this goal will get easier and quite natural. This will make your code easier to read, understand, and test. And it also helps assure that the function is doing one thing.

🔴 Dirty

```dart
void SaveUser(User user, bool sendEmail, int emailFormat, bool printReport, bool sendBill) {
  // do something
}
```

🟢 Clean

 ```dart
void SaveUser(User user) {
  // do something
}
 ```

❌ The parameters tell the story quite clear. This function is called SaveUser, but it obviously handles more than that.

- This function accepts parameters that determine whether it should send an email and what format that email should be in. It lets the caller specify whether it should print. And finally specify whether the user should be send to bill.

- Emails, printing, and billing are all separate concerns from saving a new user and they souled be handled, therefore, in separate functions.

🔥 Another Example:

🔴 Dirty

```dart
void SaveUser(User user, bool emailUser) {
  // save user

  if(emailUser) {
    // email User
  }
}
```

🟢 Clean

 ```dart
void SaveUser(User user) {
  // save user
}

void EmailUser(User user) {
  // email user
}
 ```

- These Boolean parameters area also called Flag Arguments. Flag Arguments are a very strong sign that the function is doing two things since by definition, when a Boolean is true one thing happens, and when a boolean is false a fundamentally different thing happens.

❌ Here you can see from the function signature that it both saves and optionally emails a user.

✅ These methods can be easily split up so that they have a single targeted responsibility.

## 11. What's Too Long?

- Too long is a highly arbitrary measurement, but I'm sure you can agree that at some point a function is too long and needs to be split up.

- Here's a few signs that your function may be getting too long.

### a. Using blank lines and comments too much

- When functions get long developers often resort to using blank lines and comments to separate their lines of thought, much in the same way that authors use paragraphs.

- However, these blank lines and comments are often a sign that the function is doing too much and could benefit from being split into separate well-named function.

- Whitespace and Comments are both useful tools for sure. But, nonetheless they're a smell that a function is getting too long. If it doesn't fit on the screen it might be time to split it up.

✅ Keeping functions this short also assures that the reader doesn't have to keep too many variables or pieces of logic in his or her head at once.

### b. A function should be easy to name if it has a single clear defined task.

- So, if you're having a hard time coming up with a name that totally describes what the function does it's likely too long.

✅ Refactor it into separate functions.

### c. Multiple Conditionals exist in a function

✅ When Multiple Conditionals exist in a function consider calling a separate function to extract out the Conditional.

- This provides a clear description of the intent given the state of the Conditional.

### d. Methods that are hard to digest often work with more than one layer of abstraction at a time

✅ A function should work with a single layer of abstraction.

- This makes it both easier to read and easier to debug.

- Also, remember the Rule of Seven again. A function is very hard to digest with seven parameters or more than seven variables in scope at a given time. So, keep an eye out for high numbers of either of these.

🔥 In his book **Clean Code, Bob Martin** draws some clear guidelines for functions. He suggests that functions should:

- Rarely be over 20 lines and hardly ever over 100 lines.

- Functions shouldn't have more than 3 parameters.

✅ Writing small, targeted, well-named methods makes my code easier to write and work with later.

🔥 In Linux's style guide, They say that the maximum length is inversely proportional to the complexity and indentation level of that function.

- So, if you have a conceptually simple function that is just one long, but simple case statement it's okay to have a longer function.

- If you have a complex function adhere to the limits all the more closely.

✅ <ins>*Summary:*</ins>

- Simple functions can be longer.

- Complex functions should be short.

- Yes, this is arbitrary, but use your best judgement.

## 12. Exceptions

- In functions things go wrong. And Exceptions are useful for halting the system when it's in a perilous and unexpected state.

- The three types of exceptions we're going to discuss are: `Unrecoverable`, `Recoverable`, and `Ignorable`.

| Unrecoverable   | Recoverable        | Ignorable      |
| :--------------:| :----------------: | :-------------:|
| Null reference  | Retry connection   | Logging click  |
| File not found  | Try different file |                |
| Access denied   | Wait and try again |                |

a. <ins>*Unrecoverable:*</ins>

- Unrecoverable exceptions are by far the most common.

- Examples include null reference exceptions and file not found exceptions when the missing file makes it impossible for the application to move forward in a useful and predictable state.

b. <ins>*Recoverable:*</ins>

- When Recoverable exceptions occur all isn't necessarily lost. It's worth giving things a second try.

- Examples of these exceptions are attempting to reestablish a database connection, trying a different file or just waiting for a moment for some third party API to come back up so that you can try again.

- With Recoverable exceptions it's important to consider ultimately giving up on retries at some point so your application isn't stuck in some infinite loop. But, there's nothing wrong with swallowing an exception in these instances so that you can give it one more try.

c. <ins>*Ignorable:*</ins>

- There's a rare class of exceptions that's indeed truly `Ignorable`.

- Wrote a click logging system for use on websites. If the click logging failed I chose to swallow the exception and allow the system to continue normally since it had no impact on the user.

- We were willing to accept not collecting some data in order to assure the user wasn't impacted when our click logging system failed.

- There is nothing wrong with logging and ultimately swallowing an exception if you're completely clear on the implications. But remember, these instances are rare and its key to think through the downstream impacts on this system.

### Note:

- You should never catch an exception you can't handle intelligently, let it bubble up.

- If you have an error that you can't swallow, that you can't deal with on the spot, and that you can't deal with higher up in the application then your application is broken.

- The correct behavior for a broken application is to crash immediately.

❌ A broken application that tries to limp along in an inconsistent state is a danger to itself, its data, and ultimately its users.

✅ The best way to make sure this happens is to throw an unchecked exception. If someone knows how to deal with the error they'll catch it eventually. Otherwise, it'll cause your application, or at least the current use case, to die without causing any further damage or corruption.

✅ When considering exceptions keep in mind that logging an error alone isn't enough.

- In this example, we're registering a speaker in a try block and if it fails we're logging the error.

🔴 Dirty

```dart
try {

  RegisterSpeaker();

} catch (Exception ex) {

  LogError(ex);

}

 EmailSpeaker();
```

🟢 Clean

```dart

RegisterSpeaker();

EmailSpeaker();

```

- However, after logging the error the system simply moves on to email the speaker.

❌ That's a problem. This code block shouldn't allow the application to continue since emailing the speaker a confirmation after a registration failure means that the speaker will be informed that they're registered when they're actually not.

✅ Think very carefully about the implications of catching an exception and allowing the system to continue. If the system can't reliably and logically move on, stop processing.

✅ To keep try/catch blocks easily readable it's helpful to place the body of the try within a function.

🟢 Clean

```dart

 void RegisterSpeaker() {
   try {
     // do something
   } catch(Exception ex) {
     LogError(ex);
   }
 }

```

- Imagine trying to read this version if the commented section were long. It can become hard to see where the try starts and ends.

- And more importantly, using a function like this clear version provides a clean name for the section of code. This makes it clear to the reader exactly what is being attempted in the try block.

🔴 Dirty

```dart
try {

  // Many
  // lines
  // of
  // complicated
  // And
  // verbose
  // logic
  // here

} catch (ArgumentOutOfRangeException) {

  // do Somthing here

}
```

🟢 Clean

```dart

try {

    SaveThePlanet();

} catch (ArgumentOutOfRangeException) {

    // do Somthing here

}

void SaveThePlanet() {
  // Many
  // lines
  // of
  // complicated
  // And
  // verbose
  // logic
  // here
}

```
