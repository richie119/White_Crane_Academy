#  White Crane Academy 白鹤书院
### FINAL EXAM

SEMESTER SUBJECT NAME SUBJECT CODE
Fall 2023 
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
 You should do a walkthrough on the following code.(10 marks)

**It is important that your walkthrough:**

- List each `LINE NUMBER` in the program which is executed
- `ONLY` describe the lines that are `EXECUTED` (must be in the correct ORDER/SEQUENCE)
- Substitute the `VALUE(S)` for variables when they are present in the line you are describing
- Shows the exact output of print statements (must reflect the variable value substitutions)

**Warning:**

- When a statement is executed more than once, you must show it every time it is executed including the values of the variables
- Statements which are never executed should `NOT` be included in the walkthrough


```
#include <stdio.h>

#define NAME_LEN 20
#define MAX_ITEMS 3

struct Song {
    int songID;
    int artistID;
    char name[NAME_LEN + 1];
    int durationSec;
};

struct Album {
    int albumID;
    char name[NAME_LEN + 1];
    struct Song songs[MAX_ITEMS];
};

void displayDuration(int duration) {
    printf("%02d:%02d", duration / 60, duration % 60);
}

int searchArtists(const struct Song* song, const int artists[]) {
    int i, duration = 0;

    for (i = 0; !duration && i < MAX_ITEMS; i++) {
        if (song->artistID == artists[i]) {
            displayDuration(song->durationSec);
            printf(" -> %03d %03d %s\n",
                song->songID, song->artistID, song->name);
            duration = song->durationSec;
        }
    }

    return duration;
}

int searchSongs(const struct Album* album, const int artists[]) {
    int i, duration = 0;

    printf("Album: %s\n", album->name);

    for (i = 0; i < MAX_ITEMS; i++) {
        duration += searchArtists(&album->songs[i], artists);
    }

    return duration;
}

int main(void) {
    struct Album album = { 11111, "Justice", {
        {100, 174, "2 Much", 432 },
        {200, 632, "As I Am", 263 },
        {300, 241, "Holy", 311 } } };

    const int artistIDs[MAX_ITEMS] = { 241, 958, 632 };
    int time = searchSongs(&album, artistIDs);

    printf("Total Time: ");
    displayDuration(time);
    putchar('\n');

    return 0;
}
```
