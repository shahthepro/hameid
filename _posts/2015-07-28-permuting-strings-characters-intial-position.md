---
id: 10
title: Permutation Of A String’s Characters Without Them Being In Their Initial Position
date: 2015-07-28T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/07/28/permuting-strings-characters-intial-position/
permalink: /permuting-strings-characters-intial-position/
categories:
  - Programming
tags:
  - C
  - Code Snippet
  - Permutation
  - Programming
---
Recently, I was told to write a [program](/tag/programming) which will find all the permutations of a string. But, the catch was that no character should end up in the same position as in the given string.

For Instance, if the given string is “ABC”, then the permutation should not have “A” as the first character, “B” as the second and “C” as the last one. So, the possible permutations for the input “ABC” are “BCA” and “CAB”

It might look a bit tricky. But, It’s a piece of cake if you can write a program that can find “all” permutations of the given string. You can have a look at the C program [here at GeeksforGeeks](http://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/).

Now, all we have to do is to write a conditional statement which will restrict the permutations where one or more characters are in their initial position. Below is the program after including one such conditional statements.

* * *

<pre><code class="language-prettyprint lang-c">#include &lt;stdio.h&gt;
#include &lt;string.h&gt;

char str[] = "ABCDEF";  
char str_tmp[] = "ABCDEF";  
int str_len;

void swap(char *x, char *y) {  
    char temp;
    temp = *x;
    *x = *y;
    *y = temp;
}

void permute(char *a, int l, int r) {  
    int i;
    if (l == r) {
        int flag = 0;
        char out[str_len];
        strcpy(out, a);
        for (i=0; i &lt; str_len; i++) {
            if (str_tmp[i] == out[i]) {
                flag = 1;
            }
        }
        if (flag == 0) {
            printf("%s\n", a);
        }
    }
    else
    {
        for (i = l; i &lt;= r; i++)
        {
            swap((a+l), (a+i));
            permute(a, l+1, r);
            swap((a+l), (a+i));
        }
    }
}

int main() {  
    str_len = strlen(str);
    permute(str, 0, str_len-1);
    return 0;
}
</code></pre>

* * *

You can compile and execute the above program to see how well it works. Obviously, it is not an efficient way. Because, We find all the permutations and then decide whether it is valid or not. The longer the length of the string, The more time it is gonna take.