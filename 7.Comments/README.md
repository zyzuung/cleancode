# Comments

## 1. Introduce

- And if this is all you can say about the topic of Clean Code that's not a great sign.

- And Comments indeed have their place. But, heres the thing. Over reliance on Comments is a Code Smell.

- Comments should only be chosen as a solution after a consideration of the alternatives.

- Like any other data structure there should be a clear reason to justify their existence.

- Comments are either Signal or Noise.

- Comments are sometimes not kept up to date and they can be used to explain confusing code that could simply be refactored in a cleaner manner.

- Many developers think their code is clean enough that it doesn't need comments, but as we've seen, clearly conveying intent is not easy.

- You're probably looking for a definitive answer to the bottom line question. Are comments great, or a code smell?

## 2. A Necessity and a Crutch

- Comments are both a Necessity and a Crutch.

- Let's review a couple rules that will help guide our conversation.

### a. Prefer expressive code over comments

- Comments are useful, but when code could do the same job with equal clarity we should choose to make our intent clear in code instead of comments.

- **Why?** So, code is more likely to be kept updated by maintenance programmers and is, of course, the definitive reference for what the code is doing.

### b. Use comments when code alone can’t be sufficient

- We should use comments when the code alone can't be sufficient for providing the necessary documentation.

- Here's a list of comments that we should try to avoid:

| Header     | Header          |
| ---------- | --------------- |
| Redundant  | Divider         |
| Intent     | Brace Tracker   |
| Apology    | Bloated Header  |
| Warning    | Defect Log      |
| Zombie Code|                 |

🔥 Let's go ahead and walk through these one by one.

## 3. Redundant Comments

- Redundant Comments repeat exactly what the code says right next door. So, there's really no value added here

🔥 Look at some examples:

🔴 Dirty

```dart
int i = 1; // set i = 1

var copy = new User(); // Instantiate a new user

/// <summary>
/// Default Contructor
/// </summary>
class User() {
  //
}

/// <summary>
/// Calculates Total Charges
/// </summary>
class CalculatesTotalCharges() {
  // Total charges calculated here
}
```

- Here I am setting `i` to `1`. That is completely clear in the code on the left. I am instantiating a new `user`. Or I am marking my `Default Constructor`, which is obviously clear if the name of the method matches the name of the class for instance.

- Finally, I'm calculating total charges. Here I've repeated the exact name of my method up in my comment.

- Now, the problem with Redundant Comments is they break the DRY Principle. You are repeating yourself.

- You've now created two different points that you have to maintain and you've really added no value. This is also lowering the signal to noise ratio.

- This is extra text that the reader is typically going to read, but they're not getting any value from it as there is no new content here.

❌ So, you'll often see these when people require comments on every single method and especially down here, this `CalculateTotalCharges` for instance, it's not really necessary to add a comment on every single method if your methods are named well and in this case it is so there's no additional fidelity that comes from this particular comment so you might as well just remove it and free up a few lines on your screen. So, in summary here's two rules to avoid `Redundant Comments`.

### a. Assume your reader can read

- Assume that your reader can read code in the language that you have written.

### b. DRY (Don't repeat yourself)

- The code itself conveys all the information that you need for these simple examples. No comments are necessary.

## 4. Intent Comments

🔴 Dirty

```dart
// Assure user's account is deactivated
if(user.Status == 2)
```

🟢 Clean

```dart
if(user.Status == Status.InActive) {
  //
}
```

- In this example, the developer is using a comment to clarify what the magic number 2 stands for.

- This is easily refactored out via a well-named constant, or in this case, an enumeration. Now, the code clearly conveys intent. No comment necessary.

- There's a number of ways to avoid needing:

✅ a. To create an Intent Comment including creating an `improved function name`

✅ b. Declaring an `intermediate variable`

✅ c. Creating a `constant or an enumeration` as we saw above or finally

✅ d. `Refactoring a conditional into a well-named function`.

## 5. Apology Comments

- Apology Comments. These are the comments that make maintenance programmers want to cry.

🔴 Dirty

```dart
// Sorry, this crashed a lot so I'm just swallowing the exception.
```

- You finally navigated to the point where the bug was reported and just to find a comment like this. Comments like this are a sign that the original developer just didn't bother finishing the job. It's malpractice because it leaves a mess for someone else to have to clean up later. Here's another example.

🔴 Dirty

```dart
// I was too tired to refactor is pile.
// of Spaghetti code when I was done...
```

- This developer was so exhausted after merely getting it to work that the left a mess that no one else has hopes of easily understanding.

✅ Keep in mind no one likes apologizing so why not just avoid it. Instead, fix the issue before you `commit` or `merge your code`. Or if for some reason that's not possible add a `TODO` marker comment if you must.

## 6. Warning Comments

🔴 Dirty

```dart
// Here be dragon - See Bob

// Great Sins against code
// begin here...
```

- Warning Comments are closely related to the Apology Comments we just discussed. But, they are arguably even worse.

- **Why?** So, they are also warning that lousy code is ahead, but with Warning Comments the developer isn't bothering to apologize.

- Warming Comments are often characterized by a warning that a section of code can only be touched by a certain developer.

- Sometimes warning are indeed necessary, but in many cases they are simply a sign of an area that needs to be refactored.

## 7. Zombie Code

![Zombie Code](/7.Comments/images/zombie_code.png)

- With Example, We don't except half-baked features so why should we do so in the code that we support. So, **what does this odd behavior look like in code?** Well, it looks like this.

- Well, it looks like this. Imagine, your reading through code trying to fix a bug or add a feature. What do you do when you come to sections of commented out code? It totally disrupts your flow. These sections of commented out code are Zombie Code.

- **Why Zombie Code?** Well, zombies aren't really dead. As horror movies have taught us those zombies appear to be dead. They're still alive enough to haunt us.

- In the same way Zombie Code straddles this line between alive and dead just waiting for a chance to ruin our day. Commented out code is alive because it's in the current code base. Programmers stumble across it in a keyword search and interact with it during maintenance and refactoring.

- But, the code is also dead because it's not executed in production. Thus, it's a Zombie that should be buried pronto.

- Today's code never really dies. As long as you have source control there's always a historical reference that will get you back to previous versions. (Git, SVN, etc...)

- There are 2 root causes for the ongoing problem of Zombie Code

### a. Risk Aversion

- Some developers view deleting code as inherently risky. They lack the strength of conviction and sense of purpose that's required to delete unnecessary code so they hoard it in comments where it can live to haunt another day.

- Sure, it's easier to not even think about whether code should remain in the code base, but code must be deleted regularly because great developers know that code is a liability. Less is more.

- Keep in mind commented out code is still code, but its code that's not solving any problems. It's just getting in the way.

### b. Hoarding mentality

- Developers may argue that they comment out code just in case it might be useful to someone later. This is Hoarding and does us all a disservice. Code that is no longer useful for production remains in source control history. Remember with source control, deleted code doesn't die it's merely buried alive.

- Commenting out code just creates noise for the reader and saddles our application with technical debit. Commented out code is just as useless to the application as this old trash is to this kitchen. The old wrappers and labels tell a story of what we used to do in the kitchen, but at the expense of us getting anything new done efficiently.

✅ We must strive to keep our Signal to Noise Ratio as high as possible. This aids in comprehension, speeds reading, and helps protect us from creating buggy code due to misunderstanding.

❌ Zombie Code is directly opposed to comprehension. It slows reading and maintenance because less actual production code is on the screen at any given time. It's visual noise because it's unclear if one should read it at all.

- For some reason we often accept this compromise as developers, but we'd never accept such sloppiness in the real world. Imagine if the New York Times looked like this. Imagine if the New York Times looked like this.

![New York Time](/7.Comments/images/new_york_time.png)

❌ We would not stand for this. Notice how reading the text doesn't flow? The increased noise hurts comprehension. And it's difficult to ignore the commented section even though it's likely irrelevant or worse, misleading and incorrect.

- Zombie Code makes the story unclear. Should a programmer spend time reading the commented out code or not? Commented out code also creates Ambiguity about whether the code should have been commented out at all.

- Imaging you're a maintenance programmer who stumbles across a swath of Zombie Code around an area where a bug has been reported. The programmer's job is now much harder. The commented code must be read and comprehended to determine its potential impact. Was the code accidentally commented out for testing and never averted? Perhaps the person who commented out can help. So, who was that? An investigation ensues.

- This additional `Ambiguity` takes time to resolve and adds mental weight to what could otherwise be a simple debugging process. This Ambiguity also hinders refactoring. Remember that we should regularly be leaving the code a little better than we found it.

- But, when a class or a method contains a chunk of Zombie Code things get tricky. If I refactor this section do I need to consider this commented out code? Will it be turned back on again soon? How will it interact with my new implementation? These are questions maintenance programmers shouldn't have to ask. Furthermore, integrated refactoring tools won't make corresponding changes to commented out code.

- Thus, as methods, variables, and classes are renamed and signature are changed the commented out code falls behind. When commented out code is resurrected it's highly likely the app won't even compile.

✅ Summary Zombie Code is a problem because it reduces thereadability of our code. It creates ambiguity because we need to wonder whether the commented out code should have ever been commented out in the first place.

- This also hinders refactoring because we have to consider whether the commented out code needs to be refactored when we're changing other code around it. It also adds noise to searches. When we're doing keyword searches Zombie Code shows up and it really should no longer be in scope.

### Notes: code isn't "lost" anyway

| Header                   |
| ------------------------ |
| Reduces readability      |
| Creates ambiguity        |
| Hinders refactoring      |
| Add noise to searches    |
| Code isn’t “lost” anyway |

- Remember, with source control we can always get back in time to see previous versions of the code.

- Here's a mental checklist.

- So, here's a mental checklist. If you're about to comment out code ask yourself: When if ever, would this code be uncommented? If there's not a definitive impending date then it's likely it never will be uncommented. Can I delete this and simply get it from source control later if necessary? Is this incomplete work that should be rolled back and worked via a branch instead?

- This avoids adding noise and confusion for others. Is this a feature that should be enabled or disabled via configuration? If you're commenting out code to temporarily disable a feature perhaps a configuration setting would be more appropriate. Finally, did I refactor out the need for this code all together? If it's no longer necessary just delete it.

✅ Summary:

🔥 About to comment out code? Ask yourself:
- When, if ever, would this be uncommented?
- Can I just get it from source control later?
- Is this incomplete work that should be worked via a branch?
- Is this a feature that should be enabled/disabled via configuration?  Did I refactor out the need for this code?

## 8. Dividers and Brace Trackers

- If you've ever maintained a code base burdened with extremely long functions then you've likely seen this trick. When functions get too long developers often resort to using comments to break up sections as you can see here.

🔴 Dirty

```dart
void MyLongFunction() {
  lots
  of
  code

  // Start Search for available concert tickets

  lots
  of
  concert
  search
  code

  // End of concert ticket search

  lots
  more
  code
}
```
- If your function has gotten so long that it's getting hard to navigate consider refactoring to a few separate functions to enhance readability and remove the need for the Divider Comment all together.

- Much like the Divider Comments we just discussed Brace Tracker Comments are used to help developer navigate really long stretches of code.

🔥 Here's the idea behind Brace Tracker Comments:

- When the body of a conditional grows long enough that we can't fit it all on the screen then when you see a closing curly brace it can be really unclear what it's closing. So, these Brace Tracker Comments sit here at the end of the conditional and tell us what it's closing.

- There's a better alternative, Just like Divider Comments it's easily avoidable by refactoring to a function. This separate function will enhance readability and it also reduces the cyclomatic complexity of the function.

![Brace Tracker](/7.Comments/images/brace_tracker.png)

## 9. Bloated Header

- Check out my flashy Bloated Header

![Bloated Header](/7.Comments/images/bloated_header.png)

- Back when I was working regularly in the Unix Shell we required a similar boiler plate template at the top of every file. The idea was to enforce consistency and make sure we had all the info we needed if a bug popped up.

🔥 There is a number of issues with this particular example.

a. Avoid line endings on comments like this. Keeping those asterisks at the right place is really a hassle. Enough so that some developers may decide not to update the header at all to avoid it.

b. DRY (don't repeat yourself). The file name is completely obvious by viewing the file itself and the author and the created date should be accessible via source control instead.

c. Rather than creating your own ad hock style for comments follow your languages style Conventions.

## 10. Defect Log

![Defect Log](/7.Comments/images/defect_log.png)

- You can avoid using comments like this for logging defect fixes in your code.

- Change metadata belongs in source control, not code. Adding comments like this to code can quickly make reading a really noisy chore.

- Imagine how annoying it would be to read a book filled with all the author's notes about where they fixed logical fallacies and typos. It would make following their story much more difficult.

✅ Summary: Defect Log comments cause these same issues.

## 11. Clean Comments

- Let's walk through some examples of Clean Comments.

### a. To Do Comments

- To Do Comments are handy because they allow the developer to easily get back to a specific section of code that needs more attention later.

- I hesitate to call To Do Comments clean since they can certainly be abused. But, they're useful enough that IDE even provides a dedicated task list window where you can see any comments that begin with To Do, Hack or Undone.

✅ Here's a few tips for assuring To Do style comments remain useful.

- If your IDE Of choice doesn't offer this support make sure you Standardize as a team so that everyone understands the intent of these comments.

- Watch out for many To Do's that are actually an apology or a warning in disguise. If there is time to do it right now finish it, because the fact is these are very often just ignored.

- I've seen many code bases littered with To Do's from well-meaning programmers who have never gotten around to working through their task list. But, when used judiciously To Do Comments can be a handy way to keep track of open items that need attention in the short term.

### b. Summary Comments

- Summary Comments offer much the same benefit to readers as an introduction at the beginning of a book. They prepare the reader for what to expect.

- Good Summary Comments describe the code at a high level that's not necessarily apparent by simply reviewing the class or the functions name. They're often particularly useful for providing a high level overview of classes since a class name alone isn't typically sufficient to fully convey the scope and interactions of the methods inside.

- However, be sure you're not using Summary Comments to augment poorly named classes or functions. Small well-named functions are often so self-documenting that a Summary Comment would simply be redundant.

- So, seek to convey your intent in code. But, be sure to add Summary Comments to give your readers the high level context that they need. Sometimes we have important data to track that just isn't possible to convey in code. In these cases comments can help us provide documentationdirectly within the code where it's most likely to be useful.

🟢 Clean

```dart
// Encapsulates logic for calculating retiree benefits

// Generates custom newsletter emails
```

### c. Document Comments

- Documentation comments such as these are often helpful when interacting with third parties.

🟢 Clean

```dart
// See www.facebook.om/api for documentation
```
