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
1. (3 marks) Why is it important to initialize pointers in C, and what issues can arise from uninitialized pointers?
2. (3 marks) How are pointers used as function parameters in C? Provide an example of modifying the original data.
3. (3 marks) What are the three common modes in the fopen function in C, and what do they represent?
4. (3 marks) How does the binary search algorithm work in C? Describe its basic steps or give the code.

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

```c
1: #include <stdio.h>
3:
4: #define NAME_LEN 20
5: #define MAX_ITEMS 3
6:
7: struct Song {
8:     int songID;
9:     int artistID;
10:     char name[NAME_LEN + 1];
11:     int durationSec;
12: };
13:
14: struct Album {
15:     int albumID;
16:     char name[NAME_LEN + 1];
17:     struct Song songs[MAX_ITEMS];
18: };
19:
20: void displayDuration(int duration) {
21:     printf("%02d:%02d", duration / 60, duration % 60);
22: }
23:
24: int searchArtists(const struct Song* song, const int artists[]) {
25:     int i, duration = 0;
26:
27:     for (i = 0; !duration && i < MAX_ITEMS; i++) {
28:         if (song->artistID == artists[i]) {
29:             displayDuration(song->durationSec);
30:             printf(" -> %03d %03d %s\n",
31:                 song->songID, song->artistID, song->name);
32:             duration = song->durationSec;
33:         }
34:     }
35:
36:     return duration;
37: }
38:
39: int searchSongs(const struct Album* album, const int artists[]) {
40:     int i, duration = 0;
41:
42:     printf("Album: %s\n", album->name);
43:
44:     for (i = 0; i < MAX_ITEMS; i++) {
45:         duration += searchArtists(&album->songs[i], artists);
46:     }
47:
48:     return duration;
49: }
50:
51: int main(void) {
52:     struct Album album = { 11111, "Justice", {
53:         {100, 174, "2 Much", 432 },
54:         {200, 632, "As I Am", 263 },
55:         {300, 241, "Holy", 311 } } };
56:
57:     const int artistIDs[MAX_ITEMS] = { 241, 958, 632 };
58:     int time = searchSongs(&album, artistIDs);
59:
60:     printf("Total Time: ");
61:     displayDuration(time);
62:     putchar('\n');
63:
64:     return 0;
65: }
```

## Section B+ (Code Walkthroughs)
 You should do a walkthrough on the following code.(10 marks)
```c
#include <stdio.h>
#include <string.h>

#define STRING_LEN 20
#define SONG_BANK 5
#define SONGS 3

struct Song
{
    char title[STRING_LEN + 1];
    int seconds;
};

void calculateTimeFormat(int tSeconds, int *minutes, int *seconds);
void createPlaylist(struct Song playlist[], const struct Song bank[], int offset, int seed, int order[]);
void playSongs(const struct Song songs[], const int order[], int crossFade);

int main(void)
{
    struct Song songBank[SONG_BANK] = {{"Careless Whisper", 300},
                                       {"Jailhouse Rock", 156},
                                       {"Oh Pretty Woman", 176},
                                       {"I Dreamed a Dream", 263},
                                       {"Highway To Hell", 207}};

    struct Song playlist[SONGS] = {{0}}; // Fix: Declare playlist as an array of struct Song
    int shuffled[SONGS] = {0}, config1 = 4, config2 = 30, config3 = 8;

    createPlaylist(playlist, songBank, config1, config2, shuffled);
    playSongs(playlist, shuffled, config3);

    return 0;
}

void calculateTimeFormat(const int tSeconds, int *minutes, int *seconds)
{
    *minutes = tSeconds / 60;
    *seconds = tSeconds % 60;
}

void createPlaylist(struct Song playlist[], const struct Song bank[], int offset, int seed, int order[])
{
    int i = 0, idx = seed % SONGS;
    int test;

    do
    {
        test = idx + 2 < SONGS ? idx + 2 : idx + 2 - SONGS;
        order[i] = idx + 2 < SONGS ? idx + 2 : idx + 2 - SONGS;

        if (offset < 1 || offset > SONG_BANK)
        {
            offset = SONG_BANK;
        }

        playlist[i++] = bank[--offset];
        test = idx + 1 < SONGS ? idx + 1 : idx + 1 - SONGS;
        idx = idx + 1 < SONGS ? idx + 1 : idx + 1 - SONGS;

    } while (i < SONGS);
}

void playSongs(const struct Song songs[], const int order[], int crossFade)
{
    int i, min, sec, total = 0;

    for (i = 0; i < SONGS; i++)
    {
        total += songs[order[i]].seconds;

        if (crossFade && (i + 1 < SONGS))
        {
            total -= crossFade;
            calculateTimeFormat(songs[order[i]].seconds - crossFade, &min, &sec);
        }
        else
        {
            calculateTimeFormat(songs[order[i]].seconds, &min, &sec);
        }
        printf("%-20s %2d:%02d\n", songs[order[i]].title, min, sec);
    }

    calculateTimeFormat(total, &min, &sec);
    printf("Total playing time: %3d:%02d\n", min, sec);
}

```

## Section C (Programming Problems)
