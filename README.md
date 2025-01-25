# 🧬 R Fundamentals for Biologists 
I previously created a guide called [Bash Fundamentals for Bioinformatics](https://github.com/evanpeikon/bash_fundamentals), which provided a crash course on essential Bash commands, including how to navigate a file system and move, copy, edit files, and more. After publishing that guide I received a number of messages from students and wet lab biologists who want to break into bioinformatics, but are daunted because they lack a programming background.

In response to that, I created a guide called [Python Fundamentals For Biologists](https://github.com/evanpeikon/Python_Fundamentals_Biology/tree/main), which was intended for those who are interested in learning bioinformatics but are overwhelmed by the sheer volume of coding instructionals available. This guide highlighted key concepts without overwhelming beginners with minutiae or glossing over critical concepts. Now, as a follow up to Python Fundamentals For Biologists, I've created this complimentary guide to R. 

Importantly, this guide assumes you are familiar with basic R syntax. With that foundation, you'll be ready to learn key programming concepts that will appear time and time again. From understanding the logic behind loops and conditionals, to deciphering the power of functions, and creating clean data visualizations, this guide is your short go-to resource, equipping you with the tools to decipher and compose code that unlocks the mysteries hidden in biological data.

## 🔴 Storing Data In Lists and Dictionaries 
Lists and named lists are fundamental in managing and manipulating biological data in R. A list in R is similar to a Python list in that it can store an ordered collection of objects, while a named list is akin to a Python dictionary because it associates values with specific labels or names (keys). These structures are particularly useful for bioinformatics tasks such as sequence analysis, where efficiently navigating and organizing data is essential.

### Working With Lists in R
A list is a built-in data structure that allows you to store elements of different types, including vectors, strings, numbers, or even other lists. In R, lists are defined using the ```list()``` function, and their content can be modified dyamically, meaning you can change their content by adding or removing elements. 

Bioinformatics tasks frequently involve using loops to iterate over large datasets. Lists are well-suited for these loop operations because of their sequential structure, which enables efficient processing of large datasets. Below are examples of how to create lists in R:

```R
# Create lists
list_1 = list(1, 2, 3, 4, 5)  # List of integers
list_2 = list("A", "T", "G", "C")  # List of strings
list_3 = list(list(1, 2, 3), list("A", "T", "G", "C"))  # List of lists
```
The code above shows you how to create lists contains integers, strings, and other lists. Importantly, lists do not need to contain just one data type. You can have a single list that includes integers, strings, and more. Additionally, you can add two lists together to produce a single unified list. In the code below, I'll show you how to combine lsits using R's ```c()``` function:

```R
# Combine lists
list_a = list(1,2,3)
list_b = list("a", "b", "c")
new_list = c(list_a, list_b) #list includes elements 1,2,3, a", "b", "c"
```

Next, I'll demonstrate how to add and remove elements from a list:

```R
# Add and remove elements
list = list(1, 2, 3)
print("Original List:")
list[[4]] = 4  # Add element
list[[2]] =  NULL  # Remove 2nd element
```

Next, i’ll show you how to call items from a list and slice lists:

```R
list <- list("a", "b", "c", "d", "e")
print(list[[3]])  # Retrieve the third element
print(list[1:3])  # Retrieve elements in positions 1-3
```

As you can see in the code above, you can access elements in a list by indexing with double square brackets ```[[ ]]```, and you can extract multiple elements using single square brackets ```[ ]```. You can also slice lists, which is the process of extracting a portion of a given data sequence using the following notation: [start: stop: step]. This notation creates a new list with elements from the index start point up to the stop point, with an optional step specifying the increment (note, this is different from Python, which includes list elements up to, but not including, the stop point). 

To loop through lists in R, iterating over all the elements, you can use the following syntax.

```R
dna_sequences <- list("ACTGGT", "TGGCAG", "CGTTAA")
for (sequence in dna_sequences)
  {print(sequence)}
```
Which produces the following output:
```
[1] "ACTGGT"
[1] "TGGCAG"
[1] "CGTTAA"
```
Looping through lists enables the repeated execution of operations across numerous data points. In general, looping through a list takes the following form:

```R
for (item in list)
  {code to execute for each item}
```

In essence, the code above works because the loop processes each item in the list and then performs the specified operations on that element. Later in this guide, I’ll provide a more comprehensive overview of for loops and while loops under the Control Flow section. 

### Working With Dictionaries (Named Lists) In R
A dictionary is a built-in data type that stores and organizes data in key-value pairs. In other words, it's a collection of items, each identified by a unique key, and each key is associated with a corresponding value. Keys must be strings, numbers, or tuples, and values can be of any data type, including numbers, strings, lists, or even other dictionaries. In the code block below I'll show you how to create a dictionary:

```R
# Create named lists
patient_info = list("Patient 1" = list("Height" = 170, "Weight" = 60),"Patient 2" = list("Height" = 160, "Weight" = 50))
print(patient_info["Patient 1"])

dna_to_rna = list("A" = "A", "T" = "U", "C" = "C", "G" = "G")
print(dna_to_rna[["T"]])  # Retrieve value by key
```
Which produces the following outputs:
```
$`Patient 1`
$`Patient 1`$Height
[1] 170
$`Patient 1`$Weight
[1] 60

[1] "U"
```

As previously stated, dictionaries excel at storing data in key-value pairs. In bioinformatics, this mirrors the relationship between biological entities and their associated attributes. For example, a dictionary can contain patient data, such as in the example above. In this case, the key is the patient's ID, and the value is another dictionary containing information about the patient. In the second example above, we have a dictionary called dna_to_rna, where each key is a DNA nucleotide, and the value is the associated RNA nucleotide. After defining a dictionary, you can retrieve information based on a specific identifier (i.e., key).

Dictionaries are mutable, meaning you can modify their content by adding, removing, or updating key-value pairs. In the code below, I'll demonstrate how to add and remove key-value pairs from a dictionary:

```R
# Add and remove key-value pairs
dna_to_rna[["T"]] = NULL  # Remove key-value pair
print("After Removing T:")
print(dna_to_rna)

dna_to_rna[["T"]] = "U"  # Add key-value pair
print("After Adding T:")
print(dna_to_rna)
```
Which produces the following outputs:
```
[1] "After Removing T:"
[1] "A"
[1] "C"
[1] "G"

[1] "After Adding T:"
[1] "A"
[1] "C"
[1] "G"
[1] "U"
```

In the final demonstration in this section i’ll show you how to convert a tuple into a dictionary:

```R
# Convert tuples to a named list
gene_annotations = list(
  c("GeneA", 1000, 2000, "protein_coding"),
  c("GeneB", 3000, 4000, "non_coding"),
  c("GeneC", 5000, 6000, "protein_coding"))

gene_dictionary = lapply(gene_annotations, function(annotation) {
  list(
    gene_name = annotation[1],
    start_position = as.numeric(annotation[2]),
    end_position = as.numeric(annotation[3]),
    gene_type = annotation[4] )})
```

## 🔴 Control Flow With Conditionals and Loops Using R
Control flow is crucial in bioinformatics for navigating and processing diverse biological data by controlling the order in which statements are executed in a code block. Additionally, control flow provides the flexibility to handle different conditions, iterate over data, implement algorithms, and automate tasks, contributing to the efficiency and effectiveness of bioinformatics analyses and computational biology research.

In this section, I’ll cover the two most common types of control flow you’ll encounter: conditionals and loops. Conditionals help you make decisions in your code by executing specific blocks based on whether a condition is true or false. Loops, on the other hand, enable you to repeat a set of instructions multiple times, making it easier to process data or perform repetitive tasks.

### Control Flow With Conditionals 
Conditionals are structures that allow you to execute certain code blocks based on whether a specified condition is true or false. In the sample code below I’ll demonstrate the simplest type of conditional, called conditional execution:

```R
x = 15
if (x > 10)
  {print("x is greater than 10")}
```
```
[1] "x is greater than 10"
```
In the code above, we have a simple example of conditional execution. If the logical statement x > 10 is true, then the code in the indented statement below it is executed (thus, in the code block above the print statement would be executed). If the logical statement is not true, then the indented statement is skipped, and nothing happens. Next, I’ll demonstrate another type of conditional called alternative execution:

```R
x =5
if (x > 10){
  print("x is greater than 10")
} else {
  print("x is less than or equal to 10") # This line runs since x = 5.
}
```
```
[1] "x is less than or equal to 10"
```

The fundamental logic behind alternative execution is similar to conditional execution, with the slight difference that code is executed whether or not the logic statement is true. For example, we have a logical statement if >10 in the code block above. If the logical statement is true, the indented code on line 4 is executed. Alternatively, the indented code on line 6 is executed if the logic statement is false. Once you understand alternative execution, the next type of conditional, called a nested conditional, is easy to comprehend:

```R
x = 5
y = 6

if (x == y) {
  print("x and y are equal")
} else {
  if (x < y) {
    print("x is less than y") # This block runs.
  } else {
    print("x is greater than y")
  }}
```
```
[1] "x is less than y"
```
A nested conditional refers to a situation where one or more conditional statements are nested inside another conditional statement. In other words, there is a conditional statement within the block of code controlled by another conditional statement. This nesting can occur at any level, creating a hierarchy of conditions. The example above shows an outer if statement that checks if x and y are equal. If that statement is true, the code prints ‘x and y are equal.’ If the outer statement is false, the else block containing another if/else alternative conditional is executed.

Now, before we review loops there is one more type of conditional to review, called a chained conditional:

```R
x = 6
y = 6

if (x > y) {
  print("x is greater than y")
} else if (x < y) {
  print("x is less than y")
} else {
  print("x and y are equal") # This block runs.
}
```
```
[1] "x and y are equal"
```

Whereas a nested conditional refers to one or more conditional statements nested inside another conditional statement, a chained conditional is a conditional statement that contains a series of alternative branches using if, elif, and else statements that are all indented at the same depth, as demonstrated in the code block above.

### Control Flow With Loops 
In R, loops enable you to repeat a block of code multiple times, making it easier to process data or perform repetitive tasks. There are two types of loops you should be familiar with: for loops and while loops. A for loop iterates over a sequence (such as a list, tuple, string, or range) and executes a code block for each element in that sequence. The syntax of a for loop is as follows:

```R
# Syntax of a for loop in R
for (variable in sequence) {
  # Code to execute for each element in the sequence}
```
In bioinformatics, a common scenario involves iterating over a collection of biological sequences, such as DNA, RNA, or protein sequences. In the example below, I’ll show you how to use a for loop for this task:
```R
# Example: Iterating over DNA sequences
dna_sequences <- c("ACTGGT", "TGGCAG", "CGTTAA")

for (sequence in dna_sequences) {
  length = nchar(sequence)
  cat(sprintf("The length of the DNA sequence '%s' is: %d bases\n", sequence, length))}
```
Which produces the folowing output:
```
The length of the DNA sequence 'ACTGGT' is: 6 bases
The length of the DNA sequence 'TGGCAG' is: 6 bases
The length of the DNA sequence 'CGTTAA' is: 6 bases
```
In the example above, the code ```for (sequence in dna_sequences)``` initiates the for loop. For each item ```(sequence)``` in our list, the code then calculates the length and prints the length of each DNA sequence and the sequence itself.

> Note: There is nothing special about the word 'sequence' in the code above. It could just as easily say ```for (peanut_butter in dna_sequences)```.

Whereas for loops iterates over a sequence and executes a code block for each element in that sequence, while loops repeatedly execute a block of code as long as a specified condition is true. The syntax of a while loop is as follows:

```R
# Syntax of a while loop in R
while (condition) {
  # Code to execute as long as the condition is TRUE}
```
As previously mentioned, for loops are commonly used in bioinformatics for iterating over sequences or datasets. While loops, on the other hand, are useful in scenarios where the number of iterations is not known beforehand or when iterating until a specific condition is met.

In bioinformatics, a while loop might be used to simulate a scenario where a biological process continues until a certain condition is met. Let's consider a simplified example where we simulate a mutation in a DNA sequence until a specific mutation pattern is achieved:

```R
# Simulating DNA mutations in R
set.seed(42)  # For reproducibility
dna_seq = "TGGATCCATGCA"
target_mutation = "TGGATCCATGCT"
mutations = 0

while (dna_seq != target_mutation) {
  position = sample(1:nchar(dna_seq), 1)  # Random position in the DNA sequence
  current_base = substr(dna_seq, position, position)
  possible_bases = setdiff(c("A", "T", "C", "G"), current_base)  # Exclude current base
  mutated_base = sample(possible_bases, 1)  # Randomly choose a new base
  dna_seq = paste0(
    substr(dna_seq, 1, position - 1),
    mutated_base,
    substr(dna_seq, position + 1, nchar(dna_seq))
  )
  mutations = mutations + 1
}

cat(sprintf("Target mutation achieved after %d mutations.\n", mutations))
cat(sprintf("Final DNA sequence: %s\n", dna_seq))
```
Which produces the following result:
```
Target mutation achieved after 6 mutations.
Final DNA sequence: TGGATCCATGCT
```
In the code block above, the while loop is active as long as dna_seq and target_mutation are not equal. In each iteration through the while loop, a random position in dna_seq is chosen and the base at that position is mutated. The while loop tracks the number of mutations performed until dna_seq =target_mutation.

## 🔴 Creating Modular Code With Functions
A function is a reusable block of code that performs a specific set of tasks. For example, in bioinformatics, functions are often used for tasks such as sequence manipulation, statistical analysis, or data preprocessing. Functions enhance the readability of code, allowing for the reuse of code snippets and facilitating the development of robust and modular bioinformatics workflows. The code block below provides you with the basic R function syntax:

```R
function_name = function(parameter_1, parameter_2, ...) {
  # Code to perform a task
  # Optionally, return a result}
```
There are a few key components in the code example above. First, ```function_name ```is the function's name, which you'll use to call the function later on. Next, we have the  ```function()``` keyword, which defines a function in R. After that, we have a set of parentheses wherein you can define the parameters that act as inputs to the function. Then, we have a set of brackets which contain the statements that define what the function does. Often, functions will end with a command to return a specific value using the return statement. Below is a simple example of a function that takes a dna_sequence as its single input and then returns the corresponding rna_sequence:

```R
# Define the function
dna_to_rna = function(dna_sequence) {
  # Replace all occurrences of "T" with "U"
  rna_sequence = gsub("T", "U", dna_sequence)
  return(rna_sequence)}

# Example usage
dna_seq = "ACGTGTCAGTGGGAC"
rna_seq = dna_to_rna(dna_seq)
print(rna_seq)  # Prints the RNA sequence: ACGUGUCAGUGGGAC
```

In the example code above, the name of my function is dna_to_rna, and the function takes a DNA sequence as input. Inside the function, my code creates a new object named rna_sequence, which is defined by the code ```gsub("T", "U", dna_sequence)```. My function then returns the rna_sequence using the return statement.

I then call my function with the code ```rna_seq = dna_to_rna(dna_seq)```. Importantly, when you call a function, you must write the function's name, in this case, ```dna_to_rna( )```, and then put the input parameter within the parenthesis. You'll note that the parameter I inputted when I called the function is different than when I defined the function. This is okay as long as the input parameter I choose is formatted correctly for the operations my function performs.

I provided an example of a simple function in the code above. However, in bioinformatics, functions often call other functions to create modular and reusable code. In the code below, i'll provide an example where one function calculates the GC content of a DNA sequence, and another function uses this information to determine whether the GC content is low, moderate, or high:

```R

# Function to calculate GC content
get_gc_content = function(dna_sequence) {
  # Count the number of G and C bases
  gc_count = sum(charToRaw(dna_sequence) %in% charToRaw("G")) +
              sum(charToRaw(dna_sequence) %in% charToRaw("C"))
  # Calculate the total number of nucleotides
  nucleotide_count = nchar(dna_sequence)
  # Compute the GC content percentage
  gc_content = (gc_count / nucleotide_count) * 100
  return(gc_content)}

# Function to analyze GC content level
analyze_gc_content = function(dna_sequence) {
  gc_content = get_gc_content(dna_sequence)
  
  # Determine GC content level
  if (gc_content > 65) {
    return(paste("DNA sequence has high GC content:", round(gc_content, 2), "%"))
  } else if (gc_content < 40) {
    return(paste("DNA sequence has low GC content:", round(gc_content, 2), "%"))
  } else {
    return(paste("DNA sequence has moderate GC content:", round(gc_content, 2), "%"))
  }}

# Example usage
dna_seq = "ATGCCGTTCAATAGACGTA"
result = analyze_gc_content(dna_seq)
print(result)  # Output the result
```
```
DNA sequence has moderate GC content: 42.11 %> 
```

In the code above, the first function, ```get_gc_content( )```, computes the GC content of a given DNA sequence, then the second function, ```analyze_gc_content( )```, calls the first function to get the GC content of a DNA sequence and then analyzes the result.




