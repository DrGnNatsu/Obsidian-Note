---
tags:
  - ppl
---
# Abstraction
- Abstraction for memory is **variables**.
- Sometimes, abstraction is very close to the characteristics of cells.
    - *Example*: An Integer is represented directly in one or more bytes of memory.
- **Variable attributes**: Name, Address, Type, etc.
# Names

## Why Names?
Variables, subprograms, labels, user-defined types, and formal parameters all have names.
## Design Issues for Names
- What is the maximum length of a name?
- Are names case-sensitive or not?
- Are special words reserved words or keywords?
## What is a Good Name?
> "A good speech should be like a woman's skirt; long enough to cover the subject and short enough to create interest." — Winston S. Churchill
## Names - Length
- If too short, it cannot imply any meaning.
- **Language examples**:
    - Earliest languages: Single character.
    - **FORTRAN 95**: Maximum of 31 characters.
    - **C99**: No limit, but only the first 63 characters are significant; external names are limited to 31 characters.
    - **C#, Ada, and Java**: No limit, and all characters are significant.
    - **C++**: No limit, but implementers often impose one.
## Names - Form
- Names in most PLs have the same form: A letter followed by a string consisting of letters, digits, and underscore characters.
- In some languages, special characters are used before a variable's name (e.g., `$`, `@`).
- **Note**: In early versions of Fortran, embedded spaces were ignored (e.g., `Sum Of Salaries` and `SumOfSalaries` are equivalent).
## Names - Special Characters/Words
- **PHP**: All variable names must begin with dollar signs (`$`).
- **Ruby**:
    - Variable names beginning with `@` are instance variables.
    - Variable names beginning with `@@` are class variables.
- **Keyword**: A word that is special only in certain contexts.
    - *Example in Fortran*: `Real VarName` (`Real` is a data type, thus a keyword), `Real = 3.14` (`Real` is a variable).
# Variable Attributes
## Address (L-value)
- **Address**: The memory address with which the variable is associated.
- A variable may have:
    - Different addresses at different times of execution.
    - Different addresses at various locations within a program.
- **L-value**: The Address of a variable is sometimes called an l-value because the address is required when a variable appears on the left side of an assignment.
- **Aliases**: If two variable names can be used to access the same memory location, they are called aliases.

**Example of Aliasing:**
```python
list1 = [1, 2, 3]
list2 = list1       # create alias!
list2.append(4)     # Address of list1 and list2 is the same!
```
## Type
- **Type determines**:
    - The range of values the variable can take.
    - The set of operators defined for values of this type.
    - For floating-point, the type also determines precision.
- **Example**: int type in Java specifies a range of -2,147,483,648 to 2,147,483,647.
## Value (R-value)
- **Value**: The contents of the location with which the variable is associated.
- **Example**: l_value ← r_value (l_value refers to address, r_value refers to value).
---
# Binding
- A **binding** is an association between:
    - Entity ↔ Attribute (e.g., variable and its type or value).
    - Operation ↔ Symbol.
- **Binding Time**: The time at which a binding takes place (Thời điểm diễn ra ràng buộc).
## Possible Binding Times
- **Language design time**: Bind operator symbols to operations (e.g., * for multiplication).
- **Language implementation time**: Bind floating-point type to a representation; bind int in C to a range of values.
- **Compile time**: Bind a variable to a type in C or Java.
- **Execution time**: The program is actually running on the machine.
## Binding Example
Code: count = count + 5 (count is a local variable)
- Type of count: Bound at **compile time**.
- Set of possible values of count: Bound at **language implementation time**.
- Meaning of +: Bound at **language design time**.
- Internal representation of 5: Bound at **compile time**.
- Value of count: Bound at **execution time** with this statement.
## Static vs. Dynamic Binding
- **Static Binding**: The method to be called is determined at **compile time**.
    - C++: Non-virtual methods.
    - Python: Direct method calls on instances.
- **Dynamic Binding**: The method to be called is determined at **runtime**.
    - C++: Virtual methods.
    - Python: Method overriding and dynamic type system.
**C++ Example (Static vs. Dynamic):**
**Static**
``` C++
#include <iostream>
class Animal {
public:
	void makeSound() {
		std::count << “Animal Sound”;
	}
};

int main() {
	Animal animal;
	animal.makeSound();
	return 0;
}
```
**Dynamic**
``` C++

#include <iostream>
class Animal {
public:
	void makeSound() {
		std::count << “Animal Sound”;
	}
};

class Dog: public Animal {
public:
	void makeSoung() overide {
		std::cout << “Bark”;
	}
}

int main() {
	Animal* animal = new Dog();;
	animal->makeSound();
	delete animal;
	return 0;
}
```

# Scope
- The **scope** of a variable is the **range of statements** in which the **variable is visible**.
> [!note] 
> A variable is available when it is declared 
> A variable is visible when it is declared and already referenced (used)
- A variable is **visible** in a statement *if it can be referenced* in that statement.
- **Block**: A textual region which can contain declarations within that region. (Example: procedure foo() { var x: integer; ... }).
### Static vs. Dynamic Scope
- **Static Scope (Lexical Scoping)**: Scope is *determined by the program's structure* (code layout).
    - Rule: Search in the local function, then the enclosing static parent.
- **Dynamic Scope**: Scope is based on the calling **sequence of subprograms**, determined at run-time.
    - Rule: Search in the local function, then the dynamic parent (caller).
## Static Scope Example
- main is the static parent of p2 and p1.
- p2 is the static parent of p1.
- Static parent defines where a variable or function can access surrounding variables.
## Dynamic Scope Example
**Languages**: APL, SNOBOL4, early LISP dialects. Common LISP and Perl allow both.  
**Scenario**:
- big() calls sub1().
- sub1() refers to variable x.
- Under **Static Scoping**: x in sub1 refers to global x (or immediate static parent).
- Under **Dynamic Scoping**: Since big calls sub1, sub1 looks for x in big (the caller) if not found locally.