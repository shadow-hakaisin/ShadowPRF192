#include <stdio.h>
#include <string.h>
#include <stdlib.h>

typedef struct {
    char id[15];
    char name[50];
    float gpa;
} Student;

// === FUNCTION DECLARATIONS ===
void inputStudents(Student st[], int *n);
void printStudents(Student st[], int n);
void calculateGpaExample();
void sortByName(Student st[], int n);
void printGpaAbove3(Student st[], int n);
void saveToFile(char *filename, Student st[], int n);
int loadFromFile(char *filename, Student st[]);
void deleteStudent(Student st[], int *n, char id[]);
int searchById(Student st[], int n, char id[]);
void menu();
void pauseScreen();

// === MAIN PROGRAM ===
int main() {
    Student st[50];
    int n = 0, choice;
    char id[15];
    char filename[] = "students.txt";

    do {
        menu();
        printf("Choose an option: ");
        scanf("%d", &choice);
        getchar();

        system("cls"); // Xóa menu ngay sau khi chọn

        switch (choice) {
        case 1:
            inputStudents(st, &n);
            pauseScreen();
            break;
        case 2:
            printStudents(st, n);
            pauseScreen();
            break;
        case 3:
            calculateGpaExample();
            pauseScreen();
            break;
        case 4:
            sortByName(st, n);
            printf("\nSorted by name successfully!\n");
            pauseScreen();
            break;
        case 5:
            printGpaAbove3(st, n);
            pauseScreen();
            break;
        case 6: {
            printf("Enter ID to search: ");
            fgets(id, sizeof(id), stdin);
            id[strcspn(id, "\n")] = 0;
            int pos = searchById(st, n, id);
            if (pos != -1)
                printf("Found: %s - %s - %.2f\n", st[pos].id, st[pos].name, st[pos].gpa);
            else
                printf("Student not found.\n");
            pauseScreen();
            break;
        }
        case 7:
            printf("Enter ID to delete: ");
            fgets(id, sizeof(id), stdin);
            id[strcspn(id, "\n")] = 0;
            deleteStudent(st, &n, id);
            pauseScreen();
            break;
        case 8:
            saveToFile(filename, st, n);
            pauseScreen();
            break;
        case 9:
            n = loadFromFile(filename, st);
            pauseScreen();
            break;
        case 0:
            printf("\nExiting program... Goodbye!\n");
            break;
        default:
            printf("Invalid choice! Please try again.\n");
            pauseScreen();
        }
    } while (choice != 0);

    return 0;
}

// === FUNCTION DEFINITIONS ===
void menu() {
    system("cls"); // Xóa màn hình trước khi in menu
    printf("==============================================\n");
    printf("        STUDENT MANAGEMENT SYSTEM\n");
    printf("==============================================\n");
    printf(" 1. Input students\n");
    printf(" 2. Display students\n");
    printf(" 3. Example: Calculate GPA (Lab 03)\n");
    printf(" 4. Sort by name\n");
    printf(" 5. Show students with GPA > 3\n");
    printf(" 6. Search student by ID\n");
    printf(" 7. Delete student by ID\n");
    printf(" 8. Save to file (Lab 05)\n");
    printf(" 9. Load from file (Lab 05)\n");
    printf(" 0. Exit\n");
    printf("==============================================\n");
}

void pauseScreen() {
    printf("\nPress Enter to return to menu...");
    getchar();
}

void inputStudents(Student st[], int *n) {
    printf("Enter number of students: ");
    scanf("%d", n);
    getchar();

    for (int i = 0; i < *n; i++) {
        printf("\nStudent %d:\n", i + 1);
        printf("ID: ");
        fgets(st[i].id, sizeof(st[i].id), stdin);
        st[i].id[strcspn(st[i].id, "\n")] = 0;

        printf("Name: ");
        fgets(st[i].name, sizeof(st[i].name), stdin);
        st[i].name[strcspn(st[i].name, "\n")] = 0;

        printf("GPA: ");
        scanf("%f", &st[i].gpa);
        getchar();
    }
}

void printStudents(Student st[], int n) {
    if (n == 0) {
        printf("No students available.\n");
        return;
    }
    printf("\n%-10s %-25s %s\n", "ID", "Name", "GPA");
    printf("----------------------------------------------\n");
    for (int i = 0; i < n; i++)
        printf("%-10s %-25s %.2f\n", st[i].id, st[i].name, st[i].gpa);
}

void calculateGpaExample() {
    float grade[3];
    printf("\n--- Example GPA Calculation (Lab 03) ---\n");
    printf("Enter 3 grades: ");
    for (int i = 0; i < 3; i++)
        scanf("%f", &grade[i]);

    float total = 0;
    for (int i = 0; i < 3; i++)
        total += grade[i];

    printf("Calculated GPA = %.2f\n", total / 3);
}

void sortByName(Student st[], int n) {
    for (int i = 0; i < n - 1; i++)
        for (int j = n - 1; j > i; j--)
            if (strcmp(st[j].name, st[j - 1].name) < 0) {
                Student tmp = st[j];
                st[j] = st[j - 1];
                st[j - 1] = tmp;
            }
}

void printGpaAbove3(Student st[], int n) {
    printf("\nStudents with GPA > 3.0:\n");
    for (int i = 0; i < n; i++)
        if (st[i].gpa > 3)
            printf("%-10s %-25s %.2f\n", st[i].id, st[i].name, st[i].gpa);
}

void saveToFile(char *filename, Student st[], int n) {
    FILE *f = fopen(filename, "w");
    if (!f) {
        printf("Error saving file!\n");
        return;
    }
    for (int i = 0; i < n; i++)
        fprintf(f, "%s|%s|%.2f\n", st[i].id, st[i].name, st[i].gpa);
    fclose(f);
    printf("Saved to %s successfully!\n", filename);
}

int loadFromFile(char *filename, Student st[]) {
    FILE *f = fopen(filename, "r");
    if (!f) {
        printf("File not found!\n");
        return 0;
    }
    int count = 0;
    while (fscanf(f, "%[^|]|%[^|]|%f\n", st[count].id, st[count].name, &st[count].gpa) == 3)
        count++;
    fclose(f);
    printf("Loaded %d students.\n", count);
    return count;
}

int searchById(Student st[], int n, char id[]) {
    for (int i = 0; i < n; i++)
        if (strcmp(st[i].id, id) == 0)
            return i;
    return -1;
}

void deleteStudent(Student st[], int *n, char id[]) {
    int pos = searchById(st, *n, id);
    if (pos == -1) {
        printf("Student not found.\n");
        return;
    }
    for (int i = pos; i < *n - 1; i++)
        st[i] = st[i + 1];
    (*n)--;
    printf("Deleted successfully.\n");
}
