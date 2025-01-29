# Learned-Indices (C Language)

**Storyline:**

Given an array of n sorted numbers, binary search offers a fast O(log2 n)-time search to look up for a search key (that is, a number to be located in the array). This means, given an array with one billion numbers, it takes only log2 109 ≈ 30 comparisons to locate a search key. While this is very fast, the modern “big data era” calls for even faster solutions. Think about Black Friday shopping events, Amazon needs to support queries to their inventory with billions of products given a product ID, for millions of users (if not more) at the same time. Google Maps is another example, where millions of users may be querying for points of interest given coordinate ranges (e.g., for restaurants within a user’s Google Maps app view). Tremendous efforts have been made to scale up these services, including investments on more hardware which later led to the Amazon Web Services.

In this assignment, we will design an algorithmic solution for the problem. Our aim is to further bring down the search time complexity to O(1) (in an ideal case) – too good!

As just mentioned, the goal of number searching is to locate a search key in an array of numbers. This translates to returning the subscript index of a number in the array that equals to the search key (if the search key if found). For example, given an array **dataset[] = {5, 12, 18, 44, 52, 58, 64, 93, 98, 98}**, and a search key **key = 18**, a search algorithm should return 2 (the subscript index of 18), as **dataset[2] = 18**.

A search algorithm thus can be thought of as a mapping function f(key) that takes a search key as the input and outputs the subscript index of key in array dataset. The key to achieve an O(1)-time search algorithm is to find a mapping function that runs in O(1)-time

<img width="467" alt="Screenshot 2024-04-26 at 2 57 22 PM" src="https://github.com/eugeneyap03/Learned-Indices/assets/167855582/7638e653-03d6-4c5e-8e8c-bba46cc25579">

**Task:**
You will be given a skeleton code file named program.c for this assignment on Canvas. The skeleton code file contains a main function that has been partially completed. There are a few other functions which are incomplete. You need to add code to all the functions including the main function for the following tasks.

The given input to the program consists of 12 lines of positive integers as follows:

• The first 10 lines contains 10 unsorted integers separated by whitespace in each line. Together this forms an array of 100 numbers (between 1 and 999, inclusive) to run our search algorithm upon.

• The next line contains a single integer representing a target maximum prediction error errm that we aim to achieve. This integer will be greater than 1.

• The final line contains one or more integers (separated by whitespace) representing the search keys. There is no predefined upper limit on the number of search keys.

Below is a sample input.

<img width="401" alt="Screenshot 2024-04-26 at 3 03 49 PM" src="https://github.com/eugeneyap03/Learned-Indices/assets/167855582/72c22107-ec00-4889-8bd9-4cfed86df54f">

**Stage 1: Read Input Numbers, Sort Them, and Output the First Ten Numbers**

Your first task is to understand the skeleton code. Note the use of the data_t type for generalisability in the skeleton code, which is essentially the int type. Then, you should add code to the stage_one function to 

1. Read the first 10 input lines into the dataset array.

2. Call the quick_sort function provided in the skeleton code to sort the dataset array in ascending order (for marking purposes, you are not allowed to use sorting code from other sources, or to create your own sorting function from scratch).

3. Output the first 10 elements in the sorted array.

**Stage 2: Index with a Single Linear Function**
Now add code to the stage_two function to:

1. Compute the values of parameters a and b for function f(key) = key + a/b using the first two elements dataset[0] and dataset[1] of the dataset array. Note that given two points (x0,y0) and (x1,y1) in Euclidean space.
Note a special case where dataset[0] = dataset[1]. In this case, f(key) should just return the subscript index of the first of the two elements, which is 0. You can set b = 0 and a to be the subscript index of the first of the two elements (that is, 0) to record this special case, such that your function f can be generalised in Stage 3.

2. Compute the maximum prediction error of function f over the sorted array dataset (not the target maximum prediction error given in the input data). Hint: You may need the ceil and abs functions from math.h for this computation.
   
3. Output the maximum prediction error, the dataset array element with this error, and the subscript index of the element. If there are multiple elements with this error, output the smallest among them.

**Stage 3: Index with More Linear Functions to Reduce the Maximum Prediction Error**

Add code to the stage_three function to read the target maximum prediction error errm given in the input and implement a strategy that achieves this target by using multiple mapping functions as follows.
1. Compute the values of parameters a and b for functionf(key) = key + a using the first two elements of the dataset array as done in Stage 2.

2. Starting from the third element of the dataset array, compute the prediction error of f for the element. If the prediction error does not exceed errm, we say that the element is “covered” by function f. Otherwise, we say that the element cannot be covered by f.
   
3. Repeat Step 2 with the rest of the elements until the first element that cannot be covered by f is found. Let this element be dataset[i].

4. Store the parameter values of a and b as well as the value of data[i-1]. Hint: A struct typed array will do this nicely. Read Chapter 8 of the textbook if you would like to take this approach, or you can use three arrays for the same purpose. You will need to work out a proper size for the array(s). You can work out this size based on the input data format as described above. You will not need to use dynamic memory allocation for this assignment.
   
5. Repeat Step 1, this time using data[i] and data[i+1] to compute a new mapping function (note: i and i+1 will also be needed in the process; revisit the example equation in Section 2). If there is just one element left, a mapping function with a = n - 1 and b = 0 should be created. Here, n is the number of data elements in the dataset array.
   
6. The algorithm should terminate when no more points are to be covered by new mapping functions.


**Note**: This was completed as part of COMP10002: Foundations of Algorithms
