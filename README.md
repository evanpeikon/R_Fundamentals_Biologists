# 🧬 R Fundamentals for Biologists 
I previously created a guide called [Bash Fundamentals for Bioinformatics](https://github.com/evanpeikon/bash_fundamentals), which provided a crash course on essential Bash commands, including how to navigate a file system and move, copy, edit files, and more. After publishing that guide I received a number of messages from students and wet lab biologists who want to break into bioinformatics, but are daunted because they lack a programming background.

In response to that, I created a guide called [Python Fundamentals For Biologists](https://github.com/evanpeikon/Python_Fundamentals_Biology/tree/main), which was intended for those who are interested in learning bioinformatics but are overwhelmed by the sheer volume of coding instructionals available. This guide highlighted key concepts without overwhelming beginners with minutiae or glossing over critical concepts. Now, as a follow up to Python Fundamentals For Biologists, I've created this complimentary guide to R. 

Importantly, this guide assumes you are familiar with basic R syntax. With that foundation, you'll be ready to learn key programming concepts that will appear time and time again. From understanding the logic behind loops and conditionals, to deciphering the power of functions, and creating clean data visualizations, this guide is your short go-to resource, equipping you with the tools to decipher and compose code that unlocks the mysteries hidden in biological data.

## 🔴 Storing Data In Lists and Dictionaries 
Lists and named lists are fundamental in managing and manipulating biological data in R. A list in R is similar to a Python list in that it can store an ordered collection of objects, while a named list is akin to a Python dictionary because it associates values with specific labels or names (keys). These structures are particularly useful for bioinformatics tasks such as sequence analysis, where efficiently navigating and organizing data is essential.

### Working With Lists in R
In R, a list is a versatile data structure that can store elements of different types, including vectors, strings, numbers, or even other lists. Lists are defined using the list() function, and their content can be modified dynamically. Below are examples of how to create and manipulate lists in R:

```R
# Create lists
list_1 = list(1, 2, 3, 4, 5)  # List of integers
print("List of Integers:")
print(list_1)

list_2 = list("A", "T", "G", "C")  # List of strings
print("List of Strings:")
print(list_2)

list_3 = list(list(1, 2, 3), list("A", "T", "G", "C"))  # List of lists
print("List of Lists:")
print(list_3)
```
In R, lists can also be combined using the c() function, as shown below:

```R
# Combine lists
new_list <- c(list_1, list_2)
print("Combined List:")
print(new_list)
```

To add or remove elements in a list, you can use indexing or the append() function:

```R
# Add and remove elements
list <- list(1, 2, 3)
print("Original List:")
print(list)

list[[4]] <- 4  # Add element
print("List with New Item:")
print(list)

list[[2]] <- NULL  # Remove element
print("List with Second Item Removed:")
print(list)
```
You can access elements in a list by indexing with double square brackets [[ ]], and you can extract multiple elements using single square brackets [ ].

```R
list <- list("a", "b", "c", "d", "e")

print("Retrieve the 3rd element:")
print(list[[3]])  # Retrieve the third element

print("Retrieve elements 1 to 3:")
print(list[1:3])  # Retrieve elements in positions 1-3
```

### Looping Through Lists
