# dz_lab14
1. Заголовочный файл: course.h

```c
#ifndef COURSE_H
#define COURSE_H

typedef struct {
    char name[50];
    char teacher[50];
    int hours;
    char control[20];
    int students;
    float avg_grade;
} Course;

void input_course(Course *c);
void print_course(Course c);
void filter_courses(Course arr[], int n, int min_students);
void find_best_course(Course arr[], int n);

#endif
```

2. Файл с функциями: course.c

```c
#include <stdio.h>
#include "course.h"

void input_course(Course *c) {
    printf("Название: ");
    scanf("%s", c->name);
    printf("Преподаватель: ");
    scanf("%s", c->teacher);
    printf("Часы: ");
    scanf("%d", &c->hours);
    printf("Форма контроля: ");
    scanf("%s", c->control);
    printf("Студентов: ");
    scanf("%d", &c->students);
    printf("Средний балл: ");
    scanf("%f", &c->avg_grade);
}

void print_course(Course c) {
    printf("%s | %s | %d | %s | %d | %.1f\n", 
           c.name, c.teacher, c.hours, c.control, c.students, c.avg_grade);
}

void filter_courses(Course arr[], int n, int min_students) {
    int found = 0;
    printf("\nКурсы с баллом >= 4.0 и студентов >= %d:\n", min_students);
    for (int i = 0; i < n; i++) {
        if (arr[i].avg_grade >= 4.0 && arr[i].students >= min_students) {
            print_course(arr[i]);
            found = 1;
        }
    }
    if (found == 0) {
        printf("Таких курсов нет.\n");
    }
}

void find_best_course(Course arr[], int n) {
    int best = 0;
    for (int i = 1; i < n; i++) {
        if (arr[i].avg_grade > arr[best].avg_grade) {
            best = i;
        }
    }
    printf("\nКурс с самым высоким баллом:\n");
    print_course(arr[best]);
}
```

3. Главный файл: main.c

```c
#include <stdio.h>
#include "course.h"

#define N 3

int main() {
    Course courses[N];
    int min_students;

    printf("Введите данные для %d курсов:\n", N);
    for (int i = 0; i < N; i++) {
        printf("\n--- Курс %d ---\n", i + 1);
        input_course(&courses[i]);
    }

    printf("\nВведите минимальное количество студентов: ");
    scanf("%d", &min_students);

    filter_courses(courses, N, min_students);
    find_best_course(courses, N);

    return 0;
}
```
