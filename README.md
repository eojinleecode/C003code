#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>

#define MAX_STUDENTS 10
#define MAX_NAME_LEN 20

// 한글이 인코딩에 오류가 있어 영어로 기입했습니다.
// find room
int findRoom(int persons[5]) {
    int room;
    while (1) {
        room = rand() % 5; 
        if (persons[room] < 2) { 
            persons[room]++; 
            return room + 1; 
        }
    }
}
// print
void printReport(char mn[MAX_STUDENTS][MAX_NAME_LEN], int mr[MAX_STUDENTS], int mc,
    char wn[MAX_STUDENTS][MAX_NAME_LEN], int wr[MAX_STUDENTS], int wc) {
    printf("\n=== Dormitory Room Assignment Report ===\n");

    printf("\n[Male Students List]\n");
    for (int i = 0; i < mc; i++) {
        printf("%s - Room %d\n", mn[i], mr[i]);
    }

    printf("\n[Female Students List]\n");
    for (int i = 0; i < wc; i++) {
        printf("%s - Room %d\n", wn[i], wr[i]);
    }

    printf("\n[Room Assignment List]\n");


    for (int i = 0; i < 5; i++) {
        printf("1st Floor Room %d: ", i + 1);
        for (int j = 0; j < mc; j++) {
            if (mr[j] == i + 101) {  
                printf("%s ", mn[j]);
            }
        }
        printf("\n");
    }

   
    for (int i = 0; i < 5; i++) {
        printf("2nd Floor Room %d: ", i + 1);
        for (int j = 0; j < wc; j++) {
            if (wr[j] == i + 201) { 
                printf("%s ", wn[j]);
            }
        }
        printf("\n");
    }

    printf("=========================\n");
}

int main() {
    char maleNames[MAX_STUDENTS][MAX_NAME_LEN];
    int maleRooms[MAX_STUDENTS], maleCount = 0;
    char femaleNames[MAX_STUDENTS][MAX_NAME_LEN];
    int femaleRooms[MAX_STUDENTS], femaleCount = 0;
    int malePersons[5] = {0}, femalePersons[5] = {0};

    srand(time(NULL)); 

    int choice;
    while (1) {
        printf("\nMenu: Male Student Registration (1), Female Student Registration (2), Exit (0) > ");
        scanf("%d", &choice);

        if (choice == 0) break;

        if (choice == 1 && maleCount < MAX_STUDENTS) {
            printf("What is the student's name? > ");
            scanf("%s", maleNames[maleCount]);
            maleRooms[maleCount] = findRoom(malePersons) + 100;
            printf("%s student assigned to Room %d\n", maleNames[maleCount], maleRooms[maleCount]);
            maleCount++;
            printf("Current number of male students: %d\n", maleCount);
        } else if (choice == 2 && femaleCount < MAX_STUDENTS) {
            printf("What is the student's name? > ");
            scanf("%s", femaleNames[femaleCount]);
            femaleRooms[femaleCount] = findRoom(femalePersons) + 200;
            printf("%s student assigned to Room %d\n", femaleNames[femaleCount], femaleRooms[femaleCount]);
            femaleCount++;
            printf("Current number of female students: %d\n", femaleCount); // t
        } else if (maleCount >= MAX_STUDENTS || femaleCount >= MAX_STUDENTS) {
            printf("Student registration exceeds the limit. A maximum of %d students can be registered.\n", MAX_STUDENTS);
        } else {
            printf("Invalid selection. Please try again.\n");
        }
    }

    printReport(maleNames, maleRooms, maleCount, femaleNames, femaleRooms, femaleCount);
    return 0;
}
