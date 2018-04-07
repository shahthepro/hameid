---
id: 18
title: '“Sherlock and Squares” Solution in C#'
date: 2015-09-16T06:30:00+00:00
author: Shah
layout: post
guid: http://hameid.net/2015/09/16/sherlock-and-squares-solution-in-csharp/
permalink: /sherlock-and-squares-solution-in-csharp/
categories:
  - Programming
tags:
  - 'C#'
  - Code Snippet
  - HackerRank
  - Programming
---
Recently, I came to know about [HackerRank](https://www.hackerrank.com/). After signing up, I was browsing through the challenges under [Algorithms](https://www.hackerrank.com/domains/algorithms) domain. After a while, I found myself submitting solutions to the problems one by one.

It was all going well until I came across this particular challenge named **“Sherlock and Squares“**. The main objective of this challenge is to find the number of perfect squares between two given integers.

> Watson gives two integers (A and B) to Sherlock and asks if he can count the number of square integers between A and B (both inclusive).

The first solution that hit my mind after reading the problem statement was to take square root of each integer in between the given integers and check if ceiling & floor values of the resultant are equal. If they are equal, We can count the integer as a perfect square.

* * *

<pre><code class="language-prettyprint lang-csharp">using System;  
using System.Collections.Generic;  
using System.IO;  
class Solution {  
    static void Main(String[] args) {
        int T = Convert.ToInt32(Console.ReadLine());
        List&lt;int&gt; op = new List&lt;int&gt;();
        for(int i=0; i&lt;T; i++){
            String[] t = (Console.ReadLine() as String).Split(' ');
            int count = 0;
            for(int j = Convert.ToInt32(t[0]); j &lt;= Convert.ToInt32(t[1]); j++ ) {
                double rt = Math.Sqrt(j);
                if(Math.Ceiling(rt) == Math.Floor(rt)) {
                    count++;
                }
            }
            op.Add(count);
        }
        foreach(int c in op) {
            Console.WriteLine(c);
        }
    }
}
</code></pre>

* * *

Then, I wrote the above code and tested it. It passed the initial test cases. So, with all confidence, I [submitted the code](https://www.hackerrank.com/challenges/sherlock-and-squares/submissions/code/13759151). To my surprise, there were 5 timeout out of 9 test cases.

I didn’t expect those timeout. I decided to recheck my solution and see what was wrong with my code. That’s when I realized that if the difference between the given integers is large, It takes a lot of time to compute square root for each integer in between them. That explains the reason for timeout.

After spending some time, I came up with yet another solution. Generally for any two numbers x and y, if x < y then definitely x2 < y2. So, finding difference between the square root of the given two integers should give us the number of perfect squares in between them. I rewrote the code with this logic in mind and [submitted it](https://www.hackerrank.com/challenges/sherlock-and-squares/submissions/code/13786597).

* * *

<pre><code class="language-prettyprint lang-csharp">using System;  
using System.Collections.Generic;  
using System.IO;  
class Solution {  
    static void Main(String[] args) {
        int T = Convert.ToInt32(Console.ReadLine());
        List&lt;int&gt; op = new List&lt;int&gt;();
        for(int i=0; i&lt;T; i++){
            String[] t = (Console.ReadLine() as String).Split(' ');
            int count = 0;
            int x1 = (int)Math.Ceiling(Math.Sqrt(Convert.ToInt32(t[0])));
            int x2 = (int)Math.Floor(Math.Sqrt(Convert.ToInt32(t[1])));

            if ((x2 - x1 + 1) &gt; 0 ) {
                count = x2 - x1 + 1;
            }

            op.Add(count);
        }
        foreach(int c in op) {
            Console.WriteLine(c);
        }
    }
}
</code></pre>

* * *

This time, It passed all the 9 test cases as expected. Above all, the program runs at **O(1)** time, which makes it the optimal solution for the **“Sherlock and Squares”** problem.