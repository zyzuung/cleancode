# To Name


**<ins>Example</ins>**

🔴 Dirty

```dart
int sum() {
  List<int> p = [123, 114, 130];
  int s = 0;
  forEarch(final i in p) {
    s = s + i;
  }

  return s;
}
```	


🟢 Clean

```dart
int sumHeightClass() {
  List<int> heightStudents = [123, 114, 130];
  int sumHeight = 0;
  forEarch(final i in p) {
    sumHeight = sumHeight + i;
  }

  return sumHeight;
}
```


## 1. Naming For Classes

🔴 Dirty

- Common
- MyFunctions
- Info
- etc...

🟢 Clean

- Account
- User
- UserRepository
- GetBuilder
- etc...

☑ Guidelines

1. Noun
2. Be specific
3. Single Responsibility
4. Avoid generic suffixes

<ins>*Note:*</ins> Specific names lead to smaller more cohesive classes


## 2. Naming For Methods

> Lousy Method Names put a very similar burden on your fellow programmers

### Why?

🔹 Poor Method Names require the reader to read the whole Class before understanding what it does.

🔹 Without reading the code you literally have zero idea what logic is inside.

### Example

🔴 Dirty

- Get
- Pending
- Start
- Process
- PageLoad
- etc...

🟢 Clean

- IsValidSubmission
- GetQuestionInfo
- SendEmail
- ImportFile
- etc...

<ins>*Note:*</ins> 

❌ Poorly named Methods because all they do is tell you when they are called not what sits inside. (**Ex**: Get, Start, ...)

✅ Good named Method is select a name so descriptive that the reader doesn't have to read inside the Method to know what it does. You can save yourself a lot of reading when you're hunting down a specific bug.


## 3. Rubber Ducking

![Rubber Ducking](/3.ToName/images/rubber_duck.png)

🔹 Naming should be easy when you honor the Single Responsibility Principle. (If your Class or Method are doing one thing it should be easy to describe what the code is doing).

🔹 If you do not know set name, should ask coworker. But if you have not coworker, **Rubber Ducking** will help you.

🔹 If you're having a hard time naming a Method or a Class **Rubber Ducking** often helps to verbalize. Explain what the Class does out loud for it.

<ins>*Note:*</ins> 

✅ Pay attention to how broad your description. 

✅ Particularly when struggling to name a Method. Ask yourself, am I describing one thing or a set of separate concerns that should potentially reside in separate Classes or separate Methods.


## 4. Warning Signs

⚠️ If you find yourself using the words **And**, **Or**, **If**, within your Method Name it's a sure sign you're trying to do more than one thing.

<ins>*Example:*</ins> `SenEmailAndUploadFile()`, `CopyTextAndShowResult()`, etc...

⚠️ If you name the Method to describe everything inside and need to use these words **And**, **Or**, **If**. 

> A sign you need to create two Methods, not one => **Bad Method**


## 5. Side Effects

✅ A well-structured Name Method shouldn't surprise consumers with unexpected side effects.

<ins>*Example:*</ins> 

❌ a Method called `CheckPassword` shouldn't log the user out.

❌ And `ValidateSubmission` shouldn't save.

<ins>*Summary:*</ins>

✅ Make sure that your Methods don't lie to your readers. Otherwise people have to read through every line and make sure that it does exactly what it says it does. 

✅ We want to be able to trust the contract that you are exposing through the Method Names that you select.


## 6. Abbreviations

❌ The problem with abbreviations is few words have a consistent and unambiguous abbreviation in the first place. Imagine reading a book or article filled with cryptic abbreviations. If the author never expounded on these short terms it would make for a seriously frustrating read.

<ins>*Summary:*</ins>

✅ Abbreviations are just to be avoided

⚠️ Awkwardly abbreviated names hinder discussing the code. Imagine that we have a Class called **Register User**. Well, if instead we call it **RegUsr** or **RegistUser** or **RegisUser** or **RegisterUsr**, none of these flow off the tongue. It makes it more difficult for us to read the code and more difficult for us to have a conversation with our colleagues when issues arise.


## 7. Naming variables: Booleans

✅ Boolean names should sound like true/false questions

✅ Naming a Boolean well helps your code read like spoken word.

🔴 Dirty

- open
- start
- status
- login
- etc...

```dart
if (active) {
  //...
}
```

🟢 Clean

- isOpen
- done
- isActive
- loggedIn
- etc...

```dart
if (isActive) {
  //...
}
```


## 8. Naming variables: Be symmetrical

🔴 Dirty

- on/disable
- quick/slow
- lock/open
- slow/max

🟢 Clean

- on/off
- fast/slow
- lock/unlock
- min/max