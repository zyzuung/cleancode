# Classes

## 1. Introduce

- When to Create a Class

- Cohesion

- Organization

- Primitive Obsession

- Outline Rule

🔥 SOLID Principles

🔥 Design Pattern

## 2. When to Create a class

✅ Classes are like headings in a book:

- A heading in a book provides a high level summary of the content inside. When a reader searches for a specific concept later these heading provide a road map.

- Headings make a book more scannable and help the reader comprehend the paragraphs inside more easily by providing a high level summary of the topic being discussed.

- A well-written heading should contain a number of related paragraphs underneath that stick closely to the topic outlined in the heading.

- Well-named and targeted Classes provide a strong queue to the high level intent of what's inside and thereby aid the reader.

- Just like a heading with related paragraphs a Class should contain multiple methods that relate closely to a single clear responsibility.

- There's a number of logical reasons to create a Class or extract a Class from an existing Class.

a. <ins>*To model an object:*</ins>

- These objects can model either Concrete or Abstract concepts. Classes are especially helpful with abstract concepts because they assign concrete names and behaviors to these concepts and thereby make them more approachable.

-  If the methods in your Class have little to do with one another it's a sign the Class has `Low Cohesion`.

b. <ins>*Low Cohesion:*</ins>

- Classes with Low Cohesion should be split up into separate Classes with more targeted responsibilities.

c. <ins>*To Promote Reuse:*</ins>

- Even if a piece of code could be part of a larger Class put it in its own Class if it is useful for another program and thereby easier to work with. It's also useful to create a Class to reduce complexity.

- Creating a new Class means that the reader doesn't have to consider the mental weight of a solved problem.

- The Class hides away the complexity and groups related operations behind the scenes, out of sight, out of mind, and allows somebody to just trust that, that piece will work.

d. <ins>*To clarify parameters:*</ins>

- Classes can greatly simplify information passing when complex data structures are involved.

- Classes can convert a loose bag of related variables into something more concrete, easier to reason about, and more tangible.

- If you end up passing the same variables to several functions then quite likely those variables and functions should be a Class.

## 3. Cohesion

- We often run in to the problems in our Classes when we assign responsibilities to the wrong Class or expect a single Class to do too much.

- Cohesion is a measure of how strongly the responsibilities of a Class are related.

- Highly Cohesive Classes have closely related functionality. This makes them easier to read since a Class name serves much the same purpose as a heading in a book.

- It's easier to understand what a Class is doing when the heading truly summarizes its focus clearly at a high level.

- Highly Cohesive Classes are more likely to be reused because the logic inside is more likely to be discovered in the first place.

- When Classes contain large groups of unrelated methods it's far less likely for other developers to even find the code. They are thus more likely to reinvent to wheel and break and `DRY Principle` by repeating the same logic in their own way in some new Class.

- Classes with Low Cohesion often have poor names as well since it's difficult to name a Class with many desperate responsibilities. These Classes are often given overly generic names that attract lazy developers who don't want to think about where their logic truly belongs.

✅ To avoid attracting lazy developers it's important to keep Class names descriptive. This helps keeps Cohesion high.

- This principle is closely related to **Bob Martins Single Responsibility Principle**, which states that each module should do one thing and one thing well and it should have only one reason to change.

🔥 To avoid creating Low Cohesion Classes keep an eye out for a few things here:

a. <ins>*Watch for methods that don't interact with the rest of the Class:*</ins>

- In Highly Cohesive Classes the methods and properties work together to accomplish the task. This regular interaction is a sign the Class is Cohesive.

- Low Cohesion Classes feel more like a random set of functionality, which makes them hard to understand and maintain and less likely to be reused by others.

- In a similar way watch out for fields that are only used by one method. Fields should be used by many methods in the Class and if they're not consider if the field or set of fields is a sign that the related functionality should be extracted to a separate Class.

- Source control can also help tell the tale of Classes that are doing too much. If you see a Class that receives many more commits than average it's likely a candidate for refactoring to separate Classes with Higher Cohesion.

🔥 Let's consider an example of a Class with Low Cohesion:

- This Vehicle Class allows you to edit vehicle options, update pricing, schedule maintenance, send maintenance reminders, select financing, and calculate monthly payments.

- Now, these items are all generally related to vehicles. A Class handling these rather desperate responsibilities though is likely to have Low Cohesion because the methods that deal with maintenance will utilize a very different set a fields than the vehicle options and financing and payments will require complex math and business logic that is totally unrelated to the simple tasks of editing vehicle options.

🔥 Let's look a potential refactoring

![Vehice](/6.Classes/images/vehice.png)

- This refactoring of the Vehicle Class breaks it into three separate Classes. These Classes are more Cohesive since they perform a closely related set of functions. The Vehicle Class now handles the responsibilities that are very specific to the core vehicle data like editing vehicle options and pricing.

- The Vehicle Maintenance Class handles scheduling maintenance for vehicles and sends maintenance related reminders.

- The Vehicle Finance Class handles presenting financing options and calculating monthly payments based on the selected financing options.

- Imagine I need to add a new feature for financing a vehicle. By placing the financing logic in a separate Class I now have an obvious and more approachable Class to review and modify.

- I've also reduced the risk because my change to the Vehicle Finance Class should be highly unlikely to impact any functionality in the Vehicle Maintenance or Vehicle Classes.

- Also, keep in mind that the Cohesion becomes increasingly important as a Class grows larger and logic within the application becomes more complex.

- In a very small simple system mixing these concerns together in a single Class wouldn't necessarily feel burdensome.

- But, imagine if each of these Highly Cohesive Classes on the right contained a thousand lines of code. Then, the idea of being placed together would sound extremely painful.

- Classes with overly general and undescriptive names lead to Magnet Classes and as we know magnets attract items.

- In the same way Classes with poor names, like these, attract lazy developers. Classes with names like Common and Utility often grow quickly to thousands of lines of unrelated code.

- When you instantiate a Class you should have a clear idea of what it is and what it does just from the name. This is why Classes should typically have noun names. The more concise the name the smaller the Class.

- So, start with naming well and strive for Class Cohesion. You can roughly measure Class Cohesion by reviewing how many methods use the Classes instance variables. Instance variables used by only one or two methods are an indication that those methods could be refactored out to another Class.

## 4. When is A Class too Small?

- Developers nearly always error on the side of creating Classes with too many desperate pieces of functionality. That said, here's a few signs that a Class is too small.

- If two Classes rely heavily on one another and call a large portion of each other's methods, then they might be a candidate for joining into a single Class.

- If you see one Class that relies heavily on another Class then this feature envy might be a sign that the two Classes belong together.

- Overly small Classes can make it difficult to understand how the system hangs together. There's just too many small moving parts. This can lead to other issues like Classes that are tightly bound to one another.

- These issues are all nearly unicorns in the real world. Developers rarely make this mistake of overly small Classes and very often make the mistake of creating monolithic Classes with way too many responsibilities.

## 5. Primitive Obsession

- Object oriented programmers can easily slip into passing around loose pieces of related data that should really be encapsulated within a Class.

- This Dirty example breaks the Rule of Seven by having more than seven parameters. These parameters are all clearly properties of a user so a user object should be passed into this method instead.

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

- Now, there's a tradeoff to be made here. If the method used only one or two parameters from a user then passing the specific necessary properties can help clarify the precise data dependencies and the methods intent by showcasing what is required without viewing the method body.

- The Clean version lumps related data items into a Class. There are multiple benefits to thisapproach:

**a.** It **helps the reader conceptualize** the code and intent by assigning a well understood name to the group of parameters.

**b.** It takes something **implicit**, in this case a long list of parameters, and makes it **explicit** by assigning the group a name that can be reasoned about.

**c.** Properties can **encapsulate** business logic and rules for their values to avoid putting in ad hock code wherever these primitives are utilized.

**d.** If another property is later added to the user object that needs to be leveraged by this method, the method signature itself isn't impacted. (**Aids maintenance**)

e. You can easily **find all references** to the user object in code. When you pass around a loose set of primitives finding all the references to those primitives in the related user data can become a daunting task.

✅ So remember, if you're passing around a set of related data items it's a sign that it's time to create a Class.

## 6. Principle of Proximity

✅ Readers naturally read from the top down. Thus, it's really helpful to keep related actions together.

- It's very natural to be reading a method and see it call another method.

- So, if the callee is the next method below the reader's job is very easy. It's harder to read and work with a Class when you have to scroll up and down or use a keyboard shortcut to jump back and forth while reading function calls.

- <ins>*Example*<ins>: This Class snippet is laid out top down

![Principle of Proximity](/6.Classes/images/proximity.png)

- Notice how when you read the call to validate data you can glance down and see that it's the next method in the Class.

- The next call within `ValidateRegistration` is `SpeakerMeetsOurRequirements`. You'll notice again that it's placed right below `ValidateData`. So, it's still conveniently close.

❌ This is of course a loose rule since methods are often called multiple times from different places and you can only place a function in one spot.

✅ But, when possible it's helpful to the reader to keep methods that interact or that are closely related to one another close to each other in the Class.

## 7. Outline Rule

- A well-written outline has multiple layers. It defines high level concepts and drills down to specific points made under each concept.

- Or think about a well-written book. If you're thumbing through an unfamiliar chapter looking for a specific high level idea it's helpful to have section headings. Then you can easily scan for a particular high level concept. Classes that utilize the Outline Rule offer the reader the same benefit.

- The Outline Rule increases the signal to noise of our code by providing the reader with multiple layers of abstraction. These layers are provided by creating well-named methods that describe the high level steps involved in a process. Each of these high level methods delegate to lower level methods that ultimately do the work.

![Outline Rule](/6.Classes/images/outline_rule.png)

- With this style you may have some methods that are literally nothing but a list of related method calls and that is okay. It converts something implicit and potentially confusing into a well-named structure that's easier to understand and better conveys intent.

- By doing so you build an Outline into your code allowing the readers to reason about your code at the layer of abstraction that's most helpful to their purpose.

- Often, Classes contain one or two high level methods that drill down into Child Methods. With a structure like this a high level overview of the algorithm involved isn't clearly provided.

🔥 This cleaner example instead:

![Outline Rule Example](/6.Classes/images/outline_rule_example.png)

- You can see a high level overview of the three methods involved. If you want an overview of what Method `1` is doing you can review the names of its three Child Methods. If the functionality outlined in Method `1a` is of interest you can even see that at a high level it involves the steps outlined in `1ai` and `1aii`.

- When a Class is designed to honor the Outline Rule it's easy to review its functionality and the layer of abstraction that is most useful to your purposes and dig down to the right level of detail as needed.
