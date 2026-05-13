

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

struct Question
{
    char question[100];
    char op1[50];
    char op2[50];
    char op3[50];
    char op4[50];
    int correct;
};

// Function using pointer + static (storage class)
void askQuestions(struct Question *q, int n, int *score)
{
    static int attempted = 0;   // storage class (static)
    int ans;
    time_t start, end;

    for(int i = 0; i < n; i++)
    {
        printf("\nQ%d: %s\n", i+1, (q+i)->question);
        printf("1. %s\n", (q+i)->op1);
        printf("2. %s\n", (q+i)->op2);
        printf("3. %s\n", (q+i)->op3);
        printf("4. %s\n", (q+i)->op4);

        printf("You have 10 seconds!\n");

        start = time(NULL);

        printf("Enter answer: ");
        scanf("%d", &ans);

        end = time(NULL);

        attempted++;

        if(difftime(end, start) > 10)
        {
            printf("⏰ Time's up!\n");
            continue;
        }

        if(ans == (q+i)->correct)
        {
            printf("✅ Correct!\n");
            (*score)++;
        }
        else
        {
            printf("❌ Wrong! Correct: %d\n", (q+i)->correct);
        }

        // Dashboard
        printf("\n--- Dashboard ---\n");
        printf("Attempted: %d\n", attempted);
        printf("Score: %d\n", *score);
        printf("-----------------\n");
    }
}

int main()
{
    int choice, score = 0;

    // 🟢 Beginner (8 Questions)
    struct Question beginner[8] = {
        {"Who developed C?", "Dennis Ritchie", "Gosling", "Bjarne", "Guido", 1},
        {"Statement ends with?", ";", ".", ":", ",", 1},
        {"Integer type?", "int", "float", "char", "double", 1},
        {"Output function?", "scanf", "printf", "input", "display", 2},
        {"C is?", "OS", "Language", "DB", "Compiler", 2},
        {"Header for printf?", "stdio.h", "math.h", "conio.h", "string.h", 1},
        {"Loop example?", "for", "if", "switch", "case", 1},
        {"Input function?", "scanf", "printf", "read", "write", 1}
    };

    // 🟡 Intermediate (8 Questions)
    struct Question inter[8] = {
        {"Loop runs once?", "for", "while", "do while", "none", 3},
        {"Addition operator?", "+", "-", "*", "/", 1},
        {"Return keyword?", "break", "return", "exit", "goto", 2},
        {"Condition statement?", "if", "for", "loop", "none", 1},
        {"Array index starts?", "0", "1", "-1", "2", 1},
        {"Logical AND?", "&&", "||", "!", "&", 1},
        {"Break does?", "exit loop", "repeat", "skip", "none", 1},
        {"Continue does?", "skip iteration", "stop", "end", "none", 1}
    };

    // 🔴 Advanced (8 Questions)
    struct Question adv[8] = {
        {"Pointer stores?", "Value", "Address", "Name", "None", 2},
        {"Pointer symbol?", "*", "&", "%", "#", 1},
        {"Address operator?", "&", "*", "#", "%", 1},
        {"malloc used for?", "memory", "input", "output", "loop", 1},
        {"Correct pointer?", "int *p", "p int*", "*p int", "int p*", 1},
        {"Free() does?", "deallocate", "allocate", "print", "none", 1},
        {"NULL means?", "0 address", "value", "error", "none", 1},
        {"Pointer access?", "*p", "&p", "p*", "none", 1}
    };

    printf("===== KBP QUIZ =====\n");
    printf("1. Beginner\n2. Intermediate\n3. Advanced\n");
    printf("Choose Level: ");
    scanf("%d", &choice);

    if(choice == 1)
    {
        printf("\n--- Beginner Level ---\n");
        askQuestions(beginner, 8, &score);
    }
    else if(choice == 2)
    {
        printf("\n--- Intermediate Level ---\n");
        askQuestions(inter, 8, &score);
    }
    else if(choice == 3)
    {
        printf("\n--- Advanced Level ---\n");
        askQuestions(adv, 8, &score);
    }
    else
    {
        printf("Invalid choice!\n");
        return 0;
    }

    // Final Result
    printf("\n===== FINAL RESULT =====\n");
    printf("Score: %d\n", score);

    float percent = (score / 8.0) * 100;
    printf("Performance: %.2f%%\n", percent);

    if(percent >= 80)
        printf("🏆 Excellent! You are a Programming Pro!\n");
    else if(percent >= 50)
        printf("👍 Good! Keep improving.\n");
    else
        printf("📚 Practice more!\n");

    // Motivation
    printf("\n✨ Keep learning, keep coding, success is yours! ✨\n");

    return 0;
}
