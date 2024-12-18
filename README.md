# library-management-system-with-user-authentication
#include <stdio.h>
#include<string.h>
struct library
{
	int id,bp,f;
	char bn[100],an[100];
}l[100];
struct User {
    char username[50];
    char password[50];
};
int s=1;
void signup();
int signin();
void report ();
void add ();
void view();
void issue ();
void viewissue ();
void Return ();
void Exit ();

int main()
{
printf("            Welcome");
printf("\n--------------------------------------\n");
while(1){
printf("1.ADMIN\n");
printf("2.STUDENT\n");
printf("3.Exit\n");
int usercount =0;
int pw=123,pass;
int k;
scanf("%d",&k);


if(1==k){
      int x;
    printf("enter the password:\n");
scanf("%d",&pass);
    if(pw==pass){
    do{
    printf("\n1.addbooks\n");
    printf("2.view issuebook\n");
    printf("3.report\n");
    printf("4.Exit\n");
    scanf("%d",&x);
    switch(x)
    {
        case 1: add();
        break;
        case 2: viewissue();
        break;
        case 3: report();
        break;
        case 4: Exit();
        break;
        default:
        printf("invalid");
        break;
    }
}while(x!=4);
}

else
{
    printf("\nWRONG PASSWORD\n");
}
}
if(2==k){
    int choice;
    do {
        printf("1. Sign up\n2. Sign in\n3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        if(1==choice)
        {
            signup();
            break;
        }
        else if(2==choice)
        {
            // signin();
            if(signin()==1){
            int y;
    do{
    printf("STUDENT ARE WELCOME\n");
    printf("1.view book\n");
    printf("2.lendbook\n");
    printf("3.return book\n");
    printf("4.Exit\n");
    scanf("%d",&y);
    switch(y){
        case 1: view();
        break;
        case 2: issue();
        break;
        case 3: Return();
        break;
        case 4: Exit();
        break;
        default:
        printf("\ninvalid");
        break;
    }
    }while(4!=y);
        }
           else
            printf("\nIncorrect password\n");
        
        }
    } while (choice != 3);
}
}


    return 0;
}

void add()
{
    while(1){
	int n,i;
	
		printf("How many book to be added: ");
		scanf ("%d",&n);
		for (i=1;i<=n;i++)
		{
			printf("\nBook Name: ");
			scanf ("%s",l[s].bn);
			printf("Book ID: ");
			scanf ("%d",&l[s].id);
			printf("Author Name: ");
			scanf ("%s",l[s].an);
			printf("Book price: ");
			scanf("%d",&l[s].bp);
			l[s].f=1;
			s++;
		}
		break;
    }
	
}
void issue()
{
	int id,i,k=1;
	printf("\nBook ID: ");
	scanf("%d",&id);
	for (i=1;i<=s;i++)
	{
		if (l[i].id==id)
		{
			l[i].f=0;
			printf("\nBook issued successfully\n");
			k=0;
			break;
		}
	}
		if(k)
	     printf("Book were not issued \n");
}
void report()
{
    int i;
    for(i=1;i<=s;i++)
		{
			if(l[i].f==1)
			{
			FILE *f;
            f=fopen("report.txt","a");
			fputs(l[i].bn,f);
			fprintf(f,"\nBook ID: %d\n",l[i].id);
			fputs(l[i].an,f);
			fprintf(f,"\nBook price: %d\n",l[i].bp);
			fclose(f);
			}
		}
}

void Exit()
{
	printf("Thank You\n");
}
void view()
{
    	int i;
		for(i=1;i<=s;i++)
		{
			if(l[i].f==1)
			{
			printf("Book Name: %s\n",l[i].bn);
			printf("Book ID: %d\n",l[i].id);
			printf("Book Author Name: %s\n",l[i].an);
			printf("Book price: %d\n",l[i].bp);
			}
		}
	
}
void viewissue ()
{
	int i,j=1;
	for (i=1;i<s;i++)
	{
		if(l[i].f==0)
		{
			j=0;
		printf("\nBook Issued :%s ",l[i].bn);
		printf("\nBook price : %d",l[i].bp);
		printf("\nBook Author: %s",l[i].an); 
	    }
	}
	if(j){
	     printf("Book were not issued \n");
}
}
void Return ()
{
	int n,i,g=1;
	printf("\nBook ID: ");
	scanf("%d",&n);
	
	for (i=1;i<=s;i++)
	{
	 
		if(l[i].id==n)
		{
		l[i].f=1;
		printf("Book Returned Successfully\n");
		g=0;
		break;
		
	    }
	    
	    
	}
	if(g)
	     printf("Book were not returned \n"); 
}
void signup() {
    struct User newUser;

    printf("Enter username: ");
    scanf("%s", newUser.username);

    printf("Enter password: ");
    scanf("%s", newUser.password);
    FILE *file = fopen("users.txt", "a");

    if (file != NULL) {
        fprintf(file, "%s %s\n", newUser.username, newUser.password);
        fclose(file);

        printf("Sign-up successful!\n");
    } else {
        printf("Error opening file for sign-up.\n");
    }
}
int signin() {
    struct User checkUser;
    char inputUsername[50];
    char inputPassword[50];

    printf("Enter username: ");
    scanf("%s", inputUsername);

    printf("Enter password: ");
    scanf("%s", inputPassword);

    FILE *file = fopen("users.txt", "r");
    
    if (file != NULL) 
        while (fscanf(file, "%s %s", checkUser.username, checkUser.password) != EOF) {
            if (strcmp(inputUsername, checkUser.username) == 0 && strcmp(inputPassword, checkUser.password) == 0) {
                printf("\nsignin sucessfullly\n");
                return 1;
                fclose(file);
            }
        }
            //else
           // printf("\nIncorrect password\n");
        
    

    return 0; 
}


























