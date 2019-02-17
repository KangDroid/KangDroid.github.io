# 20190217_Unfinished_Coding
## Yesterday?
So about 2 days, I was learning about what is stream, and something standard thing called "stdin, stdout, stderr" with puts/fputs get blahblahblah. That's good, no problem at all. But the thing was, the 'questions'
## What is it?
Basically it was to program adding everything together in char array. It looks way-weird but it is this:<br/>
1. Get Char array using gets/fgets<br/>
2. Add every integers in array<br/>
So for example, if user put A#15eqeqr145345, we have to add 1 + 5 + 1 + 4 + 5 + 3+ 4 + 5 and print it out with results. Meaning excluding something isn't an integer. 
## Now?
Yup, stuck. That's all I need to say. I am stuck with this, I bet It won't finish till today - tomorrow.

## The Code:

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
    	int a = 0, z = 0;
    	char test[100];
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
    	//printf("%d\n", strlen(test) - a - 1);
    	
    	printf("TEST:%d\n", atoi(&test[0]));
    	
    	/*for (int i = 0; i < strlen(test) - a; i++) {
    		printf("z:%d\n", z);
    		z += atoi(&test[i]);
    		//printf("TEST:%d\n", atoi(&test[i]));
    	}*/
    	puts(test);
    	printf("Final Result is:%d\n", z);
    	return 0;
    }


## SO?
I pretty hope myself to write any - progress about this tomorrow. 