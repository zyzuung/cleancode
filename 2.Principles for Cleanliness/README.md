# Principles for Cleanliness


## Three Principles for Clean Code

> 1. Right tool for the job

> 2. High signal to noise ratio

> 3. Self-documenting


### 1. <ins>Right tool for the job </ins>

*Know about “boundaries” between technologies*

**Advantages:**

- Cached 
- Code colored 
- Syntax checked
- Separation of concerns
- Reusable Avoids string parsing
- Can minify & obfuscate

⚠️ Avoid using one language to write another language/format via strings.
ex: Using strings in Dart, C#, Java, etc... to create

- HTML
- XML
- JSON
- CSS
- JavaScript

🔥 <ins>*Note:*</ins> One language per file


### 2. <ins>High signal to noise ratio</ins>

⚪ **Signal**

 🔺 Logic that follows the **TED** rule:
 
 - **T**erse
 - **E**xpressive
 - **D**o one thing

⚪ **Noise**

- High cyclomatic complexity
- Excessive indentation
- Zombie code
- Unnecessary comments
- Poorly named structures
- Huge classes
- Long methods
- Repetition
- No whitespace
- Overly verbose

✅ **Signal to noise ratio so important**

*Because*

> 1. Our brain is the compiler
> 2. The mess builds quietly

🚩 **DRY Principle**

> Don’t repeat yourself
> Many of same principles as relational DB normalization
> Copy and paste is often a design problem

🔥 **Refer**: [DRY Principle Link](https://topdev.vn/blog/yagni-dry-la-gi-nguyen-tac-yagni-dry-trong-java/)


### 3. <ins>Self-documenting Code</ins>

✅ *Understanding the original programmer’s intent is the most difficult problem.*
> **Fjelstad & Hamlen**

✅ **Well written code is self-documenting.**

- Clear intent
- Format for readability
- Layers of abstractions
- Favor code over comments

