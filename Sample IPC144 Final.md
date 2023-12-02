#  White Crane Academy 白鹤书院
### FINAL EXAM

SEMESTER SUBJECT NAME SUBJECT CODE
Fall 2022 
Introduction to Programming Using C IPC144

#### SPECIAL INSTRUCTIONS:
1. Write your answers in the spaces provided

2. You can have a non-scientific calculator, you are not permitted to use your cell phoneThis test includes a cover page, plus 8pages of questions.

#### ACADEMIC INTEGRITY POLICY
As a WCA student, you must conduct yourself in an honest and trustworthy manner in allaspects of your academic career. A dishonest attempt to obtain an academic advantage isconsidered an offense, and will not be tolerated by the College

## Section A (Concepts)
1. (3 marks) What is the efficient way of passing a struct to a function? Why?  
2. (3 marks) In one or two sentences explain the concept of low coupling with reference to a function call?  
Low coupling is a concept that ensures that a function call is independent of other functions, so that itcan be called without the need for any other functions to be called first.
3. (3 marks) In 2 or 3 sentences explain in non-technical terms what is meant by the term “modular programming”Modular programming  
4. (3 marks) In one or two sentences explain why const is used to qualify a function parameter

## Section B (Code Walkthroughs)
Create a Walkthrough table for the following program to show how values inside variables progress as theprogram runs. Furthermore, incorporate the output (from printf statements) to the walkthrough as well(10 marks)

```c
#include <stdio.h>

int main(void) {
    const int no = 4;
    int i, j;
    char letters[] = "Evening";

    for (i = 1; i < no; i++) {
        for (j = 1; j <= no - 1; j++) {
            printf("%c", letters[(i + j + 2) % no]);
        }
        printf("\n");
    }

    return 0;
}

```

## Section C (Programming Problems)
This is a program to find the estimated Train Fare for a destination from a group of Three destinations. TrainFare includes complementary (free) TWO check-in luggage and TWO carry-on luggage. Anything above theselimits are subjected to additional charges. The program estimates total Train Fare including (if there is)additional bag charges. The program also checks to see whether the bag dimensions are within thespecifications provided below. (28 marks)
