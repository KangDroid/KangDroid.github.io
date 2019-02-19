# 20190219_Finally Finished
## Yesterday?
I was basically thinking of how to solve this damn problem all day!

## Today?
Finally solved with some researches(I will call that a 'cheat').

## What was the question?
Basically I will skip 'what is it - explaining what is the question' - Refer to [this](https://kangdroid.github.io/unfinished-coding) if you want to see one.<br/>

## I Thought..
Yesterday, I finished "Shifting Process", which means 'sorting' in char array. It works like this: if user inputs something like 'qwerty12345asdfsa', starting 'loop - shifting process' with how many letters(not integers) in char array. It looks like '12345qwertyasdfsa' after finishing loop - shifting process. <br/>
The next question was this: How to change Char array to Integer array?<br/>
Firstly I thought changing char array to integer array with atoi will work, but it wasn't. Atoi converts char array starting from given numbers to end - integer. So it means, atoi(&array[0]) means convert every char array from array[0] to end! So I fell down deep-thinking-swamp.

## The Cheat.
Well, I was figuring out what to do really, cuz I wasn't really able to find out how to change char array to integer array!<br/>
So cheat started. Finally I find out how to change char - array integer to normal integer array. The hint was hidden inside ASCII Code.  Code is this: <br/>

    dummy[i] = test[i] - '0';

Dummy is int array, test is char array. If we substitute '0' from integer - char array, it comes with real integer number(not ascii number). Make a loop with it, and done!

## The First Code:
It looks pretty dirty though;

    #include <stdio.h>
    #include <string.h>
    #include <stdlib.h>
    
    void removeBSN(char t[]) {
    	int a = strlen(t);
    	t[a-1] = 0;
    }
    
    void checkOtherValue(char a[]) {
    	char test[2];
    	for (int i = 0; i < strlen(a); i++) {
    		if (a[i] < 48 || a[i] > 57) {
    			//printf("I:%d\n", i);
    			if (i + 1 < strlen(a)) {
    				test[0] = a[i];
    				a[i] = a[i + 1];
    				a[i + 1] = test[0];
    			}
    		}
    	}
    }
    
    int main(void) {
    	int a = 0, z = 0, result = 0;
    	char test[100];
    	int dummy[100];
    	fgets(test, sizeof(test), stdin);
    	removeBSN(test);
    	for (int i = 0; i < strlen(test); i++) {
    		if (test[i] < 48 || test[i] > 57) {
    			a++;
    		}
    	}
    	for (int i = 0; i < a; i++) {
    		checkOtherValue(test);
    	}
    	//checkOtherValue(test);
    	//printf("%d\n", strlen(test) - a);
    	
    	for (int i = 0; i < strlen(test) - a; i++) {
    		dummy[i] = test[i] - '0';
    		printf("Dummy:%d\n", dummy[i]);
    		result += dummy[i];
    	}
    	
    	/*for (int i = 0; i < strlen(test) - a; i++) {
    		printf("z:%d\n", z);
    		z += atoi(&test[i]);
    		//printf("TEST:%d\n", atoi(&test[i]));
    	}*/
    	//puts(test);
    	//printf("Final Result is:%d\n", z);
    	
    	printf("Final Result:%d\n", result);
    	return 0;
    }


## Optimized Code.
As first code was soooo dirty and un-organized to look - see, I optimized code with separating functions.

    #include <stdio.h>
    #include <string.h>
    #include <stdlib.h>
    
    void removeBSN(char t[]) {
    	int a = strlen(t);
    	t[a-1] = 0;
    }
    
    void checkOtherValue(char a[], int * counta) {
    	char test[2];
    	for (int i = 0; i < *counta; i++) {
    		for (int i = 0; i < strlen(a); i++) {
    			if (a[i] < 48 || a[i] > 57) {
    				if (i + 1 < strlen(a)) {
    					test[0] = a[i];
    					a[i] = a[i + 1];
    					a[i + 1] = test[0];
    				}
    			}
    		}
    	}
    }
    
    void howMany(char a[], int * counta) {
    	for (int i = 0; i < strlen(a); i++) {
    		if (a[i] < 48 || a[i] > 57) {
    			*counta = *counta + 1;
    		}
    	}
    }
    
    int main(void) {
    	//Declaration
    	int howTimes = 0, result = 0, dummy[100];
    	char test[100];
    	
    	//Get User - Input Value
    	fgets(test, sizeof(test), stdin);
    	
    	//Remove Backslash(Enter)
    	removeBSN(test);
    	
    	//Determine loop execution count
    	howMany(test, &howTimes);
    	
    	//Shift Every non-integer to back
    	checkOtherValue(test, &howTimes);
    	
    	//Move char array to integer array(for integer only)
    	for (int i = 0; i < strlen(test) - a; i++) {
    		dummy[i] = test[i] - '0';
    		result += dummy[i];
    	}
    	
    	//Print Final one
    	printf("Final Result:%d\n", result);
    	return 0;
    }
