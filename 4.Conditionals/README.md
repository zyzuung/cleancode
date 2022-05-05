# Conditionals

## 1. Introduction

### 4 simple principles to consider when writing conditionals:

✅ 1. <ins>*Clear intent:*</ins>

- Good conditionals clearly convey intent.

- Just as in life, it's not enough to nearly understand that we're going right versus left at a fork. It really helps to understand why we made the decision to go in a given direction in the first place.

- However, if developers made road signs, many would be about as helpful as this. Sure, we can see there's a choice between directions, but it's unclear where each road goes and how I would choose between my options. The wording is cryptic and it's just not helpful. Understanding the original programmer's intent is the most difficult problem.

✅ 2. <ins>*Use the right tool:*</ins>

- Selecting the right tool is foundational to writing clean code.

- With so many ways to send code in a new direction, it's important to think about the reader when selecting an approach.

✅ 3. <ins>*Bite-size logic:*</ins>

- Well-written conditionals offer bite-size logic that our finite minds can easily comprehend at once.

- We'll review methods to tame long, complicated conditionals into clear, simple statements.

✅ 4. <ins>*Sometimes code isn’t the answer:*</ins>

- Sometimes code is not the answer at all.

- A conditional could be completely removed altogether.


## 2. Boolean Comparisons

- Booleans are an obvious choice when there's a true/false decision to handle. However, it's common for programmers to explicitly compare Booleans against true and false. This is totally unnecessary, and it actually just adds noise to the conditional in mostcases.

🔴 Dirty

```dart
if(loggedIn == true) {
  // do something
}
```

🟢 Clean

```dart
if(loggedIn) {
  // do something
}
```

- <ins>*Note:*</ins> How the clean version reads like English. Which would you say in real life? If loggedIn equals true, or if loggedIn?

## 3. Boolean Assignments

- Primary goals when writing clean code is to increase the signal to noise, and to increase the signal to noise => Booleans should be assigned implicitly as well.

🔴 Dirty

```dart
if(cashInWallet > 6.0) {
  goingToSuperMarket = true;
} else {
  goingToSuperMarket = false;
}
```

🟢 Clean

```dart
bool goingToSuperMarket = cashInWallet > 6.0;
```

🔥 Principles for Boolean Assignments

✅ 1. <ins>*Fewer lines*</ins>

- With **Dirty Example** We can see that each Boolean is being explicitly assigned to the value true or false. This is unnecessary.

- With **Clean Example** it's easier to read bite-size pieces of code. And the more signal we can see on the screen at once, the better.

✅ 2. <ins>*No separate initialization*</ins>

- In **Dirty Example** the variable has to be initialized separately from its use within the if and else below, another line on the screen just wasted.

✅ 3. <ins>*No repetition*</ins>

- There's also agreater risk for mistakes since the variable has to be repeated on three separate lines in the dirty example.

✅ 4. <ins>*Reads like speech*</ins>

- The clean version reads a lot like spokenword.

- Let's read each piece of code aloud and see how they compare.

> Clean Example: I am going to super market if the cashInWallet is greater than 6.0$

> Dirty Example:  If the cash in my wallet is greater than 6, I'm going to Super market. Otherwise, I'm not going to Super market.

🔥 If I talked like that in real life, you'd probably look at me funny for being redundant. It's just awkward. Dirty code spoken aloud often sounds overly wordy and strange in real life too.

## 4. Positive Conditionals

🔥 The brain reasons better about positive conditionals than negative ones.

🔥 The negative request creates a lurch in your mind.

✅ So: Use positive conditionals

🔴 Dirty

```dart
if(!isNotLoggedIn) {
  // do something
}
```

🟢 Clean

```dart
if(loggedIn) {
  // do something
}
```

✅ I'm sure you'll agree that this dirty example is confusing and requires careful thought to comprehend the implication and intent. Let's look at the clean example for a contrast.

✅ This reads like the spoken word. It is trivial to understand.

⚠️ Negative conditionals are often a sign of programming by accident. You can imagine the developer was coding along and the code didn't operate as expected. So then he threw an exclamation point in the conditional to negate the Boolean and well, seems to work now. Job is done.

✅ <ins>*Summary:*</ins> If you end up with a negative conditional, strive to refactor the conditional to make a positive rather than a negative test.

## 5. Ternary Elegance

🔴 Dirty

```dart
int feeEnglish = 0;

if(isStudent) {
  feeEnglish = 100;
} else {
  feeEnglish = 0;
}
```

🟢 Clean

```dart
int feeEnglish = isStudent ? 100 : 0;
```

> This approach has many of the same benefits as the implicit "3. Boolean assignment" that we just discussed.

✅ It requires far fewer lines and doesn't require repeating the variable that's being assigned.

✅ Note how the ternary operator only requires a single reference to the `feeEnglish` variable.

❌ The Dirty version makes three separate references, including requiring a dedicated line to initialize the `feeEnglish` variable. That's three different opportunities for a typo and three different references the reader must read.

❌ If the reader isn't interested in what is getting set to the `feeEnglish` variable, then it's trivial to pass by the one liner on the right.

✅ The ternary operator offers a very elegant and terse syntax. It honor the DRY principle. (DRY stands for Don't Repeat Yourself.)

✅ However, clean coders must also remember the term YAGNE. (YAGNE stands for, You Ain't Going To Need It). We should not introduce more complexity in our code just because we think we might need it in the future. Go ahead and add the additional complexity when it's truly necessary.

🔥 <ins>*Note:*</ins> And also, like any tool, the ternary can be abused. You should avoid using multiple ternary operators in a single conditional because it hurts readability.

## 6. Stringly Typed

🔴 Dirty

```dart
if(employeeType == 'manager') {
  // do something
}
```

🟢 Clean

```dart
if(employee.Type == EmployeeType.Manager) {
  // do something
}
```

✅ You can leverage an enum to make a strongly typed check for the employee type.

✅ Benefits to this approach.

### a. <ins>*Strongly typed => No typos:*</ins>

- Strongly typed means that there's no way to make a typo. (If you make a typo the application just will not compile. You cannot run it)

- So, if I typed `manger` here instead of `manager` I'd know immediately, I'd get a squiggly within my IDE. Who knows at what point it would be obvious that that was the line that I had fat-fingered and typed in the wrong information.

### b. <ins>*Intellisense support:*</ins>

- You end up with **Intellisense support** when you, stay strongly typed. **Intellisense** helps us finish our sentences, so the IDE pops down, gives you context, you don't have to type as much to get all this done.

- We will type the em hit `tab keyboard` and then it would fill in `employee type` and then I would have a list of potential options here. So, it's just a more luxurious experience.

### c. <ins>*Documents states:*</ins>

- It also helps document the potential states. So the `employee type` has a certain finite number of options here and `manager` is one of those and I can see those different options and it helps me reason better about the code as I'm learning a new code base.

- You can't do that with these strings (Ex: "manager", 'boss', etc...). I'd have to go hunt around and try to find all the places that `employee type` was referenced, and see whether I could get a feel for all the potential values.

### d. <ins>*Searchable:*</ins>

- It's searchable. Imagine that you have an application that's working with manager data. That's a big problem because if I search for the word manager, I'm going to find this line and I'm going to find it listed all over the place. Potentially in comments and all these, other areas that are completely unrelated to me just trying to figure out how often I'm looking for a given employee type.

- Using an enum, I can easily hunt for all the places that this enum is referenced. My ID will just help me out, and it is definitive when it does so, as opposed to a string search, where, especially if there was some typos in some places, they just wouldn't show up. So, there's a lot of benefits to being strongly typed, if your language does support it.

## 7. Magic Numbers

🔴 Dirty

```dart
if(age > 21) {
  // do something
}

if(status == 2) {
  // do something
}
```

🟢 Clean

```dart
const int legalDrinkingAge = 21;
if(age > legalDrinkingAge) {
  // do something
}

if(status == Status.Active) {
  // do something
}
```

❌ With **Dirty Example** Numbers by themselves without context don't convey any meaning or intent. It doesn't convey much information. The reader is forced to go hunt around for the meaning behind these magic numbers.

✅ Magic numbers are to be avoided. Numbers are typically the wrong tool for the job in conditionals.

- a. Instead, consider setting a `well-named constant` for use in conditionals.

- b. Second option for eliminating magic numbers, that is to use an `enum`. Using these constants and enums, instead of magic numbers, helps avoid typos, since the app won't compile if you make a mistake and you'll get **Intellisense support** from your IDE. Plus, searching for all the usage of a given constant or enum is easy. But the biggest benefit to removing the magic number is it clarifies intent.

## 8. Complex Conditionals

🔴 Dirty

```dart
if(car.Year > 1980
  && (car.Make == "Mazda" || car.Make == "BMW")
  && car.Odometer > 100000
  && car.Vin.StartWith("V2") || car.Vin.StartWith("IA3")) {
  // do Something
}
```

⚠️ Conditionals get out of hand. They tend to grow, over time, until they're hard to work with and unclear.

✅ There are two simple approaches to manage the complexity and clarify intent, so that they don't end up confusing messes like this particular conditional.

- a. Using intermediate variables.

- b. Encapsulation via a function.

### a. <ins>*Using intermediate variables*</ins>

🔴 Dirty

```dart
if(employee.Age > 55
  && employee.YearsEmployed > 10
  && employee.IsRetired == true) {
  // do Something
}
```

🟢 Clean

```dart
bool eligibleForPension = employee.Age > MinRetirementAge
                          && employee.YearsEmployed > MinPensionEmploymentYears
                          && employee.IsRetired;
```

- `Clean version` helps we know that the developer was trying to determine if the employee is eligible for the company pension plan. All through the creation of this simple intermediate variable, we have clarified our intent.


### b. <ins>*Encapsulation via a function*</ins>

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

- With `Dirty version`, you can see that the author recognized that it was getting complex, and he chose to use a comment to help clarify. However, remember, one of the principles of clean code is to favor expressive code over comments. We should only resort to using comments when the code can't adequately explain itself.

✅ We can even use the context of the comment to help us name the method well. The name of the function helps clarify that the intent is to determine if the file request received is valid.

🟢 Clean

```dart
if(ValidFileRequest(fileExtension, isActiveFile, isAdmin)) {
  // do Something
}

bool ValidFileRequest(String fileExtension, bool isActiveFile, bool isAdmin) {
  return (fileExtension == "mp4" ||
     fileExtension == "mpg" ||
     fileExtension == "avi") &&
    (isAdmin || isActiveFile);
}
```

- <ins>*Note:*</ins> That the body of the conditional was simply moved inside the function, we just copied and pasted from above down into here. But there's still room for further improvement to fully clarify our intent within the new method that we've created.

✅ We've created a few intermediate variables to further convey our intent. We've made it clear that `mpg`, `mp4` and `avi` are our list of valid file extensions. It's also now clear that the `isAdmin` or `isActive` check is there to determine if the user should be allowed to view the file at all, that was completely unclear up above.

✅ Notice that the return line now clearly describes our intent and reads like spoken word. It's a `validFileRequest` if it's a `validFileType` and the user is allowed to view the file, very clear. And think about the experience for the reader. If the reader comes across a single line that says, if `validFileRequest`, all the body of the function can be totally ignored from, by the maintenance programmer if they're fixing a bug that's totally unrelated to this piece. It's a single line that they can skip over and move on.

✅ Let's look at another cleaned-up version.

🟢 Clean

 ```dart
 if(ValidFileRequest(fileExtension, isActiveFile, isAdmin)) {
   // do Something
 }

 bool ValidFileRequest(String fileExtension, bool isActiveFile, bool isAdmin) {
   return validFileType && userIsAllowedToViewFile;
 }
 ```

✅ This method is arguably doing two things. It's validating that the requested file extension is within our list of accepted file extensions and it's also checking if the user has the rights to view the file. Those are two separate pieces of logic that could be re-factored to separate methods, so that each method has a clear single responsibility if desired.

## 9. Favor Polymorphism over Enums for Behavior

🔴 Dirty

```dart
void LoginUser(User user) {
  switch(User.status) {
    case Status.active:
        // logic for active users
        break;
    case Status.inActive:
        // logic for user InActive users
        break;
    case Status.locked:
        // logic for user Lock users
        break;            
  }
}
```

🟢 Clean

 ```dart
 void LoginUser(User user) {
   user.Login();
 }

 abstract class User {
   final String name;
   final Status status;
   final int accountBalance;

   abstract void Login();
 }

 class ActiveUser extend User {
   @override
   void Login(){
     // Active User logic here
   }
 }

 class InActiveUser extend User {
   @override
   void Login(){
     // InActive User logic here
   }
 }

 class LockedUser extend User {
   @override
   void Login(){
     // Locked User logic here
   }
 }
 ```

✅ Enums and constants are useful for conditional logic. However, when logic switching is being used to provide notably different behavior, resorting to switch statements and enums can lead to redundant switch statements and hard to read code. Instead, polymorphism can often provide a more scalable solution.

✅ This is particularly true when you notice a switch statement that occurs more than once in your code.

🔥 In this example:

- There's different logic that occurs on log in based on a user's status. Imagine there were multiple points throughout the user's class that contained this same switch statement, checking for the user's status and running complex logic based on that user's status.

- Using polymorphism, we can delegate such details to the user class. With this structure, each class knows how to handle itself, so the switch is no longer necessary in multiple places in our code and the logic for each user type is completely encapsulated within these specific classes. Which really helps you manage complexity within these individual pieces. And it helps eliminate those redundant switches that you could potentially see throughout your code.

## 10. Be declarative if possible

🔴 Dirty

```dart
List<User> matchingUsers = new List<User>();

forEach(var user in users) {
  if(user.AccountBalance < minimumAccountBalance
       && user.Status == Status.Active) {
    matchingUsers.add(user);
  }
}

return matchingUsers;
```

🟢 Clean

```dart
return users
       .Where(u => user.AccountBalance < minimumAccountBalance)
       .Where(u => u.Status == Status.Active);
```

> This code above is simply looping through a list of users to find those that match some specific criteria.

⚠️ The example on top requires five lines and the manual creation of a looping structure to iterate through all the users.

✅ Contrast this with the clean version below. In two lines of very declarative code, we've accomplished the same task.

🔥 If we just read aloud what each snippet is doing, the difference is striking.

### a. Dirty version

- It says, loop through each user in users.

- And If the AccountBalance is less than the minimum and the user's status is active,

- Add the user to the list of matching users.

- Then return the list of matching users

### b. Clean version

- Return users with an AccountBalance less than the minimum who have an active status.

### c. Compare Dirty and Clean

- With Clean version: That is simple and expressive and it reads very much like the spoken word.

- So, if your language happens to have this sort of tooling that allows you to be very declarative, put it to use and you'll save yourself some typing and you'll also save your readers from having to read so much code.

- And then you're also a lot less likely to write a bug, because you're being declarative about what you want rather than writing the code to get you what you want.

- So be declarative, if possible.

## 11. Table Driven Methods

🔴 Dirty

```dart
if(age < 20) {
  return 345.60m;
} else if (age < 30) {
  return 419.50m;
} else if(age < 40) {
  return 476.38m;
} else if(age < 50) {
  return 516.25m;
}
```

- Imagine we're trying to determine insurance rates based on a customer's age. One way to pull this off is to use a long if statement and place all the rates directly within the code. This is called hard coding.

- Hardcoding isn't so bad when it's a small amount of data that won't change. But in this case, you can imagine insurance rates will regularly change and thus require changes to our code. You could imagine also how quickly this could spiral into a very complex and dynamic set of logic for a real insurance application. In these instances, the logic typically doesn't belong in the code at all. Instead, it belongs in the database.

- So here's the data base table that can replace the complex, hard coded if statement on the drity version.

🟢 Clean

> InsuranceRate table

| InsuranceRateId | MaximumAge  | Rate     |
| :--------------:| :---------: | :-------:|
| 1               | 20          | 346.60   |
| 2               | 30          | 420.50   |
| 3               | 40          | 476.38   |
| 4               | 50          | 516.25   |

```dart
return Repository.GetInsuranceRate(age);
```

- Once the table is populated with the correct data, it's simply a matter of querying the table in your code.

- So not only is our code much cleaner, but any time the data changes, we don't have to release a new version of the application. We simply update a row in the database.

✅ Clean code abstracts away things that change and avoids hard coding dynamic values.

✅ There's a variety of places that the table-driven approach makes sense,including pricing structures and complex dynamic business rules. This technique can make your applications ultra flexible without requiring much code. And sometimes, it's helpful to think about your logic as nothing more than a complex set of look up data.

✅ So, in summary, the table-driven method approach is great for dynamic logic and helps to avoid hardcoding data into our application. It also helps us avoid writing and maintaining complex data structures. And finally, it's easily changeable without a coat change or application deployment.

🔥 Examples:

• Insurance rates

• Pricing structures

• Complex and dynamic business
