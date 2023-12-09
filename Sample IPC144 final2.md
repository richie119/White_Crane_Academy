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
 1 #include <stdio.h>
 2 #include <string.h>
 3
 4 #define STRING_LEN 20
 5 #define SONG_BANK 5
 6 #define SONGS 3
 7
 8 struct Song
 9 {
10     char title[STRING_LEN + 1];
11     int seconds;
12 };
13
14 void calculateTimeFormat(int tSeconds, int *minutes, int *seconds);
15 void createPlaylist(struct Song playlist[], const struct Song bank[], int offset, int seed, int order[]);
16 void playSongs(const struct Song songs[], const int order[], int crossFade);
17
18 int main(void)
19 {
20     struct Song songBank[SONG_BANK] = {{"Careless Whisper", 300},
21                                        {"Jailhouse Rock", 156},
22                                        {"Oh Pretty Woman", 176},
23                                        {"I Dreamed a Dream", 263},
24                                        {"Highway To Hell", 207}};
25
26     struct Song playlist[SONGS] = {{0}}; // Declare playlist as an array of struct Song
27     int shuffled[SONGS] = {0}, config1 = _______, config2 = _______, config3 = _______;  // Fill in the blanks with appropriate values
28
29     createPlaylist(playlist, songBank, config1, config2, shuffled);
30     playSongs(playlist, shuffled, config3);
31
32     return 0;
33 }
34
35 void calculateTimeFormat(const int tSeconds, int *minutes, int *seconds)
36 {
37     *minutes = tSeconds / 60;
38     *seconds = tSeconds % 60;
39 }
40
41 void createPlaylist(struct Song playlist[], const struct Song bank[], int offset, int seed, int order[])
42 {
43     int i = 0, idx = seed % SONGS;
44     int test;
45
46     do
47     {
48         test = idx + 2 < SONGS ? idx + 2 : idx + 2 - SONGS;
49         order[i] = idx + 2 < SONGS ? idx + 2 : idx + 2 - SONGS;
50
51         if (offset < 1 || offset > SONG_BANK)
52         {
53             offset = SONG_BANK;
54         }
55
56         playlist[i++] = bank[--offset];
57         test = idx + 1 < SONGS ? idx + 1 : idx + 1 - SONGS;
58         idx = idx + 1 < SONGS ? idx + 1 : idx + 1 - SONGS;
59
60     } while (i < SONGS);
61 }
62
63 void playSongs(const struct Song songs[], const int order[], int crossFade)
64 {
65     int i, min, sec, total = 0;
66
67     for (i = 0; i < SONGS; i++)
68     {
69         total += songs[order[i]].seconds;
70
71         if (crossFade && (i + 1 < SONGS))
72         {
73             total -= crossFade;
74             calculateTimeFormat(songs[order[i]].seconds - crossFade, &min, &sec);
75         }
76         else
77         {
78             calculateTimeFormat(songs[order[i]].seconds, &min, &sec);
79         }
80         printf("%-20s %2d:%02d\n", songs[order[i]].title, min, sec);
81     }
82
83     calculateTimeFormat(total, &min, &sec);
84     printf("Total playing time: %3d:%02d\n", min, sec);
85 }


```

## Section C (Programming Problems)
