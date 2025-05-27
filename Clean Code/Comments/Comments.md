Created: 2025-05-27 16:20
## Family Tree:
1. [[Clean Code]]
-- -
Comments are, at best, a necessary evil. Their proper use is to compensate for our failure to express ourself in code.
The older a comment is, and the farther away it is from the code it describes, the more likely it is to be just plain wrong. The reason is simple: programmers can't realistically maintain them. Inaccurate comments are far worse than no comments at all.
### Comments Do Not Make for Bad Code
One of the more common motivations for writing comments is bad code. Clear and expressive code with few comments is far superior to cluttered and complex code with lots of them. Rather than spend your time writing the comments that explain the mess you've made, spend it cleaning that mess.
### Explain Yourself in Code
There are certainly times when code makes a poor vehicle for explanation, but this doesn't mean that code is seldom, if ever, a good mean for explanation. Examples:
```java
// Check to see if the employee is eligible for full benefits
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```
And:
```java
if (employee.isEligibleForFullBenefits())
```
It takes only a few seconds of thought to explain most of your intent in code. In many cases it's simply a matter of creating a function that says the same thing as the comment you want to write.