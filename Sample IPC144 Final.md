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
```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

#define NOPAS 50 // Max Commuters
#define NOROUTES 3  // Number of Routes
#define MAXBAGS 8   // MAX CHECKIN + CARRY BAGS

/* Check-In Bag Limits */
#define MAXCHECKIN 2 // Check-in limit for ticket
#define MAXDIMENSIONCHECK 70 // width+height+length should be <=70inch
#define MAXWEIGHTCHECK 23.5 // Maximum Weight allowed for CheckIn (per Bag)
#define PERKGEXTRACHECK 99.9 // Kgs above 23.5 are charged at this rate(per Kg)

/* Carry-On Bag Limits */
#define MAXCARRYON 2 // Carry-on limit for ticket
#define MAXDIMENSIONCARRY 50 // width+height+length should be <=50inch
#define MAXWEIGHTCARRY 10   // Maximum Weight allowed for Carry On (per Bag)
#define PERKGEXTRACARRY 69.9 // Kgs above 10 are charged at this rate(per Kg)

struct Bag {
    int type; // 1 for Check-in , 2 for carry-on
    double weight;
    double width, height, length;
    double extraCost;
};

struct Route {
    char trainLine[31];  //Train Route
    char destCountry[31]; //Destination (country)
    char destCity[31]; //Destination (City)
    double baseFare; //Base Ticket Price
};

/*Create a struct called Commuter with the following properties  
name - can store up to 40 characters  
age - an integer  
nationality - can store up to 30 characters
struct Bag array called "bagArr" that can store MAXBAGS
struct Route called routex   [2 marks]*/

____________________________  
____________________________  


void setOneBag(struct Bag* bg) {
    int flag;
    printf("\t\tEnter Bag Weight: ");    
    ______________________________;// Obtain and assign bag weight [0.5 marks]

    do {
        printf("\t\tEnter Width height length: ");
        ____________________// Obtain and assign bag dimension in one line through bg [1.5 marks]
        _________________________// Switch to case 1 when bag type is 1, case 2 when bag type is 2 [0.5 marks]
        switch (bg->type) {
        case 1:
            __________________// Set flag 1 when the obtained width+length+height is greater than MAXDIMENSIONCHECK using conditional statement [0.5 mark]
            if (flag == 1) {
                printf("\t\tcheck-in (width+height+length) should be <= 70\n\n");
            }
            else {
            ___________________-// Calculate the extra cost for a check-in bag and assign to Commuter's bag cc's extraCost [1.5 mark]
            }
            break;
        case 2:
            ____________________// Set flag 1 when the obtained width+length+height is greater than MAXDIMENSIONCARRY using conditional statement [0.5 mark]
            if (flag == 1) {
                printf("\t\tcheck-in (width+height+length) should be <= 50\n\n");
            }
            else {
            _______________________ // Calculate the extra cost for a carry-on bag and assign to Commuter's bag cc's extraCost [1.5 mark]
            }
            break;
        default:
            flag = 1;
            printf("\t\tWrong Bag Type !!! \n");
        }
    } while (flag == 1);
}

void setBagsInfo(struct Bag bgs[]) {
    int i;
    int checkB, carryB;
    printf("\tHow many Check-Ins: ");
    scanf("%d", &checkB);
    for (i = 0; i < checkB; i++) {
    ____________________// set type of bgs element to check-in type(1) [0.5 mark]
    _________________ // Call setOneBag with the relevant data [1 mark]
        printf("\n");
    }
    printf("\tHow many Carry-Ons: ");
    scanf("%d", &carryB);
    for (; i < (checkB + carryB); i++) {
    ______________ // set type of bgs element to carry-on type(2) [0.5 mark]
    _____________// Call setOneBag with the relevant data [1 mark]
    }
}

void setCommuter(struct Commuter *p) {
    do {
        printf("Enter Commuter Name: ");
        printf("Enter Commuter Age : ");
        printf("Enter Nationality   : ");
        ___________// Obtain and store Commuter Information [1.5 marks]
        _______________{// Display an error when name or nationality is an empty string or age is not in between 0 and 120 [1 mark]
            printf("Input Error on Name or Age or Nationality !!!\n");
        _______________// Reset name and nationality strings to be empty strings [1 mark]
        }else {
            printf("Enter Bag Info      : \n");//Call setBagsInfo with the relevant data [1 mark]
        }
    } while (_______________);// Loop back when name or nationality is an empty string//or age is not in between 0 and 120 [1 mark]
}

struct Route selectTours(struct Route tr[], int len) {
    int i, dest;
    for (i = 0; i < len; i++) {
        printf("\nRoute Destination:  %d\n", i + 1);
        printf("====================\n");
        // Display Route Info using tr array [2 marks]
        printf("Train Line   : %s\n", _________);
        printf("Country    : %s\n",____________);
        printf("City       : %s\n", ___________);
    }
    do {
        printf("\nEnter Route Destination #: ");
        scanf("%d%*c", &dest);
        _____________________// Display the below error when the selected destination is not in between 1 and 3(inclusive) [0.5 mark]
        _____________________// Iterate when "dest" is not between 1 and 3(inclusive) [0.5 mark]
        ___________________// Return the selected destination [1 mark]
    } while (____________);
}

int main() {
    struct Route info[] = {
        {"Mountain Line","Hungary","Budapest", 1500.00},
        {"ScenicRoute", "Germany","Cologne", 999.99},
        {"Pacific Line","France", "Dijone", 1111.11}
    };
    ______________// Declare a Commuter array called com and initialize to zero (Size should be set to NOPAS) [1 mark]
    printf("== Welcome to European Travel Agency ==\n\n");
    do {
        printf("Do you have a Commuter (Enter yes/no or 'quit' to Quit Program): ");
        _________________// Read user Input and assign to "userInput variable" [1 mark]
        _______________// Add ONE commuter information to "com" if the userinput is "yes": Note: Use strcmp to compare strings [1 mark]
        ______________// Select a Route by calling "selectRoute" and assign the returned route to Commuter's route routex [2.5 marks]
        ______________// Call setCommuter and pass the relevant data[1.5 mark]
        i++;
    } while ( ______________);// Iterate as long as the user input is not "quit" [2 mark]
    return 0;
}

```
