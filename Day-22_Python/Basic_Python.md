# Python Fundamentals – Detailed Descriptions

## 1. Variables and Data Types
Python uses dynamic typing, meaning variables do not require explicit type declarations.  
A variable is created when a value is assigned to it.  

<img width="538" height="160" alt="image" src="https://github.com/user-attachments/assets/e74945ed-4e0f-4389-8714-5b20d41bf281" />
<img width="386" height="86" alt="image" src="https://github.com/user-attachments/assets/9564927c-04d8-4dcc-ae4f-cc6d4af5dd48" />
<img width="512" height="66" alt="image" src="https://github.com/user-attachments/assets/a661b5da-010d-4e84-846a-bf3a4c83c25b" />

Data Types:- Core data types include integers, floats, strings, booleans, lists, tuples, dictionaries, and sets.  
Understanding these types is essential because DevOps automation often involves handling configuration data, logs, command outputs, and structured information.

<img width="440" height="480" alt="image" src="https://github.com/user-attachments/assets/a08ba369-2ccd-46b9-bd21-d58abdd8e5d5" />
<img width="505" height="187" alt="image" src="https://github.com/user-attachments/assets/3d4db9da-244f-4824-9fec-656c02fdbd20" />

---

# Python Data Types and Operators

## 1. What Are Data Types?
Data types define the kind of value a variable can store.  
They determine how data is stored in memory and what operations can be performed on it.  
In Python, data types are dynamic, meaning you do not need to declare them explicitly.

---

## 2. Python Data Types

### Integer (int)
Represents whole numbers used in calculations, counters, and system metrics.

### Float (float)
Represents decimal numbers used for precise measurements or percentages.

### String (str)
Represents text data used for filenames, logs, messages, and configuration content.

### Boolean (bool)
Represents True or False values used in conditional logic and decision-making.

### List (list)
Ordered, mutable collection used for storing multiple items such as server lists, records, or IPs.

<img width="353" height="117" alt="image" src="https://github.com/user-attachments/assets/2751c63b-2598-47b7-b9a6-dff967796789" />

### Tuple (tuple)
Ordered, immutable collection used for storing fixed sets of data that should not change.

### Dictionary (dict)
Key-value based structure used for configurations, metadata, JSON data, and API responses.

### Set (set)
Unordered collection of unique items used for removing duplicates or comparing items.

---

## 3. Python Operators

### Arithmetic Operators
Used for mathematical operations.  
Includes addition, subtraction, multiplication, division, modulus, exponent, and floor division.

### Comparison Operators
Used to compare two values.  
Includes equal, not equal, greater than, less than, greater or equal, and less or equal.

### Logical Operators
Used to combine conditional statements.  
Includes and, or, and not.

### Assignment Operators
Used to assign values to variables.  
Includes simple assignment and compound assignments like add-equal, subtract-equal, multiply-equal, etc.

### Membership Operators
Used to check if a value is part of a sequence.  
Includes in and not in.

### Identity Operators
Used to compare memory locations of objects.  
Includes is and is not.

---

## 7. Conditional Statements
Conditional statements (if, elif, else) allow scripts to make decisions based on specific conditions.  
They are essential for writing automation logic such as checking system health, validating input, or branching deployment workflows.

<img width="989" height="649" alt="image" src="https://github.com/user-attachments/assets/12721b9f-8207-4a83-82b2-3a535f8952f8" />

```
# ===============================
# DATATYPES & STRING
# ===============================
# input() always returns data as STRING datatype.
# day_of_week is a STRING.
day_of_week = input("Enter the day of week: ").lower()  # converting user input (string) to lowercase

print(day_of_week)  # printing the string value

# ===============================
# OPERATORS
# ===============================
# "==" is a comparison operator (checks equality)
# "or" is a logical operator (checks if any one condition is true)

# ===============================
# CONDITIONS (if / else)
# ===============================
# if condition checks whether the day is Saturday or Sunday.
# If condition is TRUE, it will print "I will learn python".
# Else block runs when condition is FALSE.

if day_of_week == "saturday" or day_of_week == "sunday":  # checking conditions using operators
    print("I will learn python")

else:  # condition is false
    print("I will learn AWS")
```

<img width="1264" height="946" alt="image" src="https://github.com/user-attachments/assets/b467a727-92ff-4937-89ac-a30578d0f662" />


---

### append()
- Adds an item to the **end** of the list.
- Modifies the existing list.
- Commonly used to grow a list dynamically.

### insert()
Inserts an item at a specific index.
Shifts existing elements to the right.
Useful when you want the new item at a specific position.

---
## 8. Loops
Loops allow repeated execution of code blocks.  
They are widely used in DevOps to iterate through servers, log files, configuration entries, cloud resources, and API results.

---

## 9. Functions
Functions group reusable blocks of logic.  
In DevOps, functions help structure automation scripts, reduce duplication, and improve maintainability.  
They are essential for building modular scripts for tasks like monitoring, deployments, validations, and system checks.

---

## 10. Modules and Packages
Modules allow code organization into separate files, and packages group multiple modules.  
This structure is important for building larger automation projects, CI/CD utilities, cloud automation tools, and system helpers.

---

## 11. File Handling
File handling enables reading, writing, and modifying files.  
It is heavily used for managing logs, configuration files, inventory files, and templated deployments.  
Understanding file operations is essential for DevOps engineers working with Linux systems and automation pipelines.

---

## 12. Error Handling
Error handling using try, except, and finally ensures scripts run smoothly even when unexpected issues occur.  
It is critical in production automation to prevent script crashes, handle timeouts, manage failed commands, and capture useful error messages.

---

## 13. Virtual Environments
Virtual environments isolate Python dependencies for projects.  
This prevents version conflicts between tools and ensures repeatable builds, especially in CI/CD pipelines.

---

## 14. Input and Output
Understanding input handling and output formatting helps build interactive scripts and CLI utilities.  
It is also useful for structuring output logs for automation and debugging.

---

