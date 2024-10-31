## Assignment B1 - STAT 545B
#### Laura Simonson, Student ID: 60858685
##### This Github Repository contains the code for Assignment B1 in STAT 545B. 

The function created in this assignment is called mean_median_range and was created to calculate the mean, median and range for different numerical datasets. 
This repository contains a .rmd file containing the code for this assignment as well as the knitted .md file to format the text. 

There were four exercises within this assignment:
* Exercise 1: Make a function
  * This exercise involved creating a function, in this case, the mean_median_range function.
* Exercise 2: Document the function
  * This exercise involved using the roxygen2 skeleton to create the proper documentation for the mean_median_range function.
  * The documentation contains:
      * The title of the function
      * Descriptions of the parameters in the function
      * A description of details which shows how the function handles non-numeric inputs
      * A description of what the values in the output of the function mean in the return section
      * Two examples showing how to use the function.
  * Exercise 2 and Exercise 1 are in the same code chunk because the documentation for a function has to come before the code of the function.
* Exercise 3: Include Examples
  * There are three examples showing how to use the mean_median_range function
      * Example 1 includes a custom data set with 14 numbers to show how the user can input specific variables and calculate the mean, median and range of them.
      * Example 2 uses an already existing dataset, palmer penguins, to calculate the mean, median and range of one of the variables in the dataset.
      * Example 3 also uses an already existing dataset but shows how the function is not able to calculate the mean, median and range of non-numeric vectors.
* Exercise 4: Test The Function
    * This exercise involved three tests to show that the function is working as expected
        * The first test shows that the function works correctly when tested on a vector that does not have any missing values.
        * The second test shows that the functions works correctly when tested on a vector that does have missing values by removing the missing values in part 1 and not removing the missing values in part 2.
        * The third test shows that the function will not work if the input is not numeric. 

[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/s4oIzs8K)
