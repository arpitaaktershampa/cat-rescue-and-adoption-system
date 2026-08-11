#include <stdio.h>
#include <string.h>

#define MAX 10



// CAT INFORMATION


int id[MAX] =
{
    101, 102, 103, 104, 105
};

char name[MAX][20] =
{
    "Mio",
    "Chiku",
    "Simba",
    "Minu",
    "Billu"
};

int age[MAX] =
{
    6, 12, 4, 8, 10
};

char breed[MAX][20] =
{
    "Persian",
    "Local",
    "Local",
    "Domestic",
    "Domestic"
};

char area[MAX][20] =
{
    "mirpur",
    "uttara",
    "pallabi",
    "ashulia",
    "badda"
};

char status[MAX][20] =
{
    "Available",
    "Available",
    "Available",
    "Available",
    "Available"
};


int cat_count = 5;



// ADOPTION QUEUE


char applicant[MAX][30];

int requested_cat[MAX];

int front = 0;
int rear = 0;



// SHOW RESCUED CATS


void show_cats()
{
    int i;

    printf("\n");
    printf("================================\n");
    printf("          RESCUED CATS\n");
    printf("================================\n");


    for(i = 0; i < cat_count; i++)
    {
        if(strcmp(status[i], "Available") == 0)
        {
            printf("\nID     : %d", id[i]);
            printf("\nName   : %s", name[i]);
            printf("\nAge    : %d months", age[i]);
            printf("\nBreed  : %s", breed[i]);
            printf("\nArea   : %s", area[i]);
            printf("\nStatus : %s", status[i]);

            printf("\n------------------------------\n");
        }
    }
}



// SEARCH CAT BY AREA
// LINEAR SEARCH

void search_area()
{
    char search_area[20];

    int i;
    int found = 0;


    printf("\nEnter Area: ");
    scanf("%s", search_area);


    for(i = 0; i < cat_count; i++)
    {
        if(strcmp(area[i], search_area) == 0)
        {
            if(strcmp(status[i], "Available") == 0)
            {
                printf("\nCat Found!");

                printf("\nID    : %d", id[i]);
                printf("\nName  : %s", name[i]);
                printf("\nAge   : %d months", age[i]);
                printf("\nBreed : %s", breed[i]);
                printf("\nArea  : %s\n", area[i]);

                found = 1;
            }
        }
    }


    if(found == 0)
    {
        printf("\nNo available cat found in this area.\n");
    }
}



// APPLY FOR ADOPTION
// QUEUE - ENQUEUE


void apply_adoption()
{
    if(rear >= MAX)
    {
        printf("\nAdoption queue is full!\n");
        return;
    }


    printf("\nEnter Your Name: ");
    scanf("%s", applicant[rear]);


    printf("Enter Cat ID: ");
    scanf("%d", &requested_cat[rear]);


    rear = rear + 1;


    printf("\nAdoption request submitted!");
    printf("\nPlease wait for processing.\n");
}



// PROCESS ADOPTION
// QUEUE - DEQUEUE

void process_adoption()
{
    int i;
    int found = 0;


    if(front == rear)
    {
        printf("\nNo adoption requests.\n");
        return;
    }


    printf("\n==============================");
    printf("\n       ADOPTION REQUEST");
    printf("\n==============================");


    printf("\nApplicant : %s", applicant[front]);

    printf("\nCat ID    : %d", requested_cat[front]);


    // Find requested cat

    for(i = 0; i < cat_count; i++)
    {
        if(id[i] == requested_cat[front])
        {
            found = 1;


            if(strcmp(status[i], "Available") == 0)
            {
                strcpy(status[i], "Adopted");


                printf("\nCat Name : %s", name[i]);

                printf("\nStatus   : Adopted");

                printf("\n\nAdoption Successful!\n");
            }

            else
            {
                printf("\nSorry, this cat is already adopted.\n");
            }
        }
    }


    if(found == 0)
    {
        printf("\nCat ID not found.\n");
    }


    // Move queue forward

    front = front + 1;
}



// MAIN FUNCTION

int main()
{
    int choice;


    while(1)
    {
        printf("\n\n");
        printf("====================================\n");
        printf("              PAWCARE\n");
        printf("       Cat Rescue & Adoption\n");
        printf("====================================\n");


        printf("\n1. View Rescued Cats");
        printf("\n2. Search Cat by Area");
        printf("\n3. Apply for Adoption");
        printf("\n4. Process Adoption");
        printf("\n5. Exit");


        printf("\n\nEnter Your Choice: ");
        scanf("%d", &choice);


        if(choice == 1)
        {
            show_cats();
        }

        else if(choice == 2)
        {
            search_area();
        }

        else if(choice == 3)
        {
            apply_adoption();
        }

        else if(choice == 4)
        {
            process_adoption();
        }

        else if(choice == 5)
        {
            printf("\nThank you for using PawCare!");
            printf("\nHelp a cat. Give them a home. \n");

            break;
        }

        else
        {
            printf("\nInvalid choice!");
        }
    }


    return 0;
}
