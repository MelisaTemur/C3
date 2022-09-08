# C3
Exact same words count
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

#define MAX_WORD_COUNT 10000
#define MAX_WORD_LENGHT 1000

void TransferArray();
void Print();
int Search();

char input[MAX_WORD_LENGHT];
char words[MAX_WORD_COUNT][MAX_WORD_LENGHT];

int main()
{
	// Print the robinson.txt
	Print();

	// take an input from keybord
	printf("Please enter a word:");
	scanf("%s", input);

	// Transfer all word in txt file to array
	TransferArray();

	int ich = 0;
	//infinite loop
	while (1)
	{
		// function return same word or letter count
		int value = Search();
		printf("The exact same word count is: %d\n", value);
		printf("Exit (0) - Continue (1): ");
		scanf("%d", &ich);
		if (ich == 0)
			break;

		printf("Please enter a word:");
		scanf("%s", input);
	}
	return 0;
}


void TransferArray() 
{
	FILE* ptr;
	// file open with read 
	ptr = fopen("ınput.txt", "r");

	// check file is exists or opened?
	if (NULL == ptr)
		printf("file can't be opened \n");

	char x[1024];
	int i = 0;
	while (fscanf(ptr, " %1023s", x) == 1) 
	{
		// check if words first character or last character is alphabet

		// get last char in word
		char last = x[strlen(x) - 1];

		// if last char is not alphabet, remove the char
		if (!isalpha(last))
		{
			int size = strlen(x);
			x[size - 1] = '\0';
		}

		// copy word from txt to array
		strcpy(words[i], x);
		i++;
	}

	fclose(ptr);
}

void Print()
{
	FILE* ptr;
	char ch;

	ptr = fopen("ınput.txt", "r");

	if (NULL == ptr)
		printf("file can't be opened \n");

	printf("\n------ınput.txt Content------\n");
	do
	{
		ch = fgetc(ptr);
		printf("%c", ch);
	} while (ch != EOF);

	fclose(ptr);
}

int Search()
{
	// initial value for strcmp
	int value = -1;

	// initial value for same word count
	int same = 0;

	for (int i = 0; i < MAX_WORD_LENGHT; i++)
	{
		// check is word same?
		value = strcmp(input, words[i]);
		// if same, increase same value 1
		if (value == 0)
			same++;
	}

	return same;
}
