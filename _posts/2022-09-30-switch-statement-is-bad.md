---
title: Switch statement is bad
date: 2022-09-30 14:57:00 +0800
categories: [blog, programming]
tags: [switch-statement]
---

## **Switch Statements**
While reading to an [article](https://betterprogramming.pub/the-art-of-refactoring-5-tips-to-write-better-code-3bc1f6f7689) by Estefania Garcia Gallardo that explains about the ways of refactoring code, I learnt that **the switch statements** is not a good things to have when it comes to a clean code. 

Below shows a quote that been taken from the article that explains why the **switch statement** is bad:

> It has been stated that, switch statements are very verbose (expressed in more words than are needed), hard to maintain and hard to debug.
{: .prompt-info }


Based on the reason expressed by the author above, it clearly shows that the switch statements is not suitable for a larger codebase. Try imagining a switch statements with many case clauses in code snippet below, it can be quite frightening to maintain right? Whenever we want to add a new case we have to manually add each case and break statement which prone to human error and also violates the SOLID principles. 

```js
	function getHeroes(position) {
		let hero;
		
		switch(position) {
			case '2':
				hero = 'Juggernaut';
				break;
			case '1':
				hero = 'Outworld Devourer';
				break;
			case '3':
				hero = 'Timbersaw';
				break;
			case '4':
				hero = 'Lion';
				break;
			case '5':
				hero = 'Oracle';
				break;
			// more cases ... 
			default: 
				hero = 'roshan'
		}
		return hero;
	}
```

## **Switch Alternatives** 
Thriving for a clean code is a must have goals for every developer, thus, instead of using switch statements why not try using **Object Literal** and **Polymorphism** instead to boost maintainability of the codebase.

### Object Literal 
By implementing Object literal instead of switch statement it can enable modification process much easier and easy to maintain. 

Below shows the snippet of object literal:
```js
	const heroes = {
		'1': 'Juggernaut',
		'2': 'Outworld Devourer',
		'3': 'Timbersaw',
		'4': 'Lion',
		'5': 'Oracle'
	};

	function getHeroes(position){
		return heroes[position] || 'roshan';
	}

	Console.log(getHeroes('1')); // Result: Juggernaut (option)
	Console.log(getheroes('tra')); // Result: roshan (default)
	
```

**Explanation:**

| Element            | Details                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------- |
| Heroes Object      | Outside of the function, holds a values for user option, it can be easily maintain and or added a new values.  |
| getHeroes() method | Replace the switch statement, by handling user request, the OR symbols represent default value similar to switch statements                                                                                                                            |

### Polymorphism
By implementing Polymorphism instead of switch statement it can enable modification process much easier and easy to maintain. 

Below shows the snippet of Polymorphism:

```js

	class Heroes {
		position();
		name();
	}
	
	class Heroes1 extends Heroes {
		position() {
			Console.log('1');
		}
		name() {
			Console.log('Juggernaut')
		}
	}

	class Heroes2 extends Heroes {
		position() {
			(Console.log)('2');
		}
		name() {
			Console.log('Outworld Devourer')
		}
	}

	class Heroes3 extends Heroes {
		position() {
			Console.log('3');
		}
		name() {
			Console.log('Timebersaw')
		}
	}
	// more heroes ...

	var heroes1 = new Heroes1();
	var heroes2 = new Heroes2();
	var heroes3 = new Heroes3();
	
	heroes1.name();      // Result: Juggernaut
	heroes1.position();  // Result: 1
```

**Explanation:**

| Element            | Details                                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------------------- |
| Heroes Class       | Acting as a default value                                                                                      |
| Heroes1 ... Class  | Acting as an option that user can use (case-break statement)                                                                                                                            |


---
# Sources:
1. [The art of refactoring](https://betterprogramming.pub/the-art-of-refactoring-5-tips-to-write-better-code-3bc1f6f7689)
2. [Why switch statement are bad?](https://www.linkedin.com/pulse/why-switch-statements-bad-th%C3%A9o-farnole-/)