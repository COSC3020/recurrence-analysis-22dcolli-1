# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Plagarism Statement

All exercises must contain the following statement:
“I certify that I have listed all sources used to complete this exercise, including the use
of any Large Language Models. All of the work is my own, except where stated
otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is
suspected, charges may be filed against me without prior notice.”

## Note
I am attempting this from scratch, I will compare it to my last semester repository and make any corrections needed base on that.

## Answer

Just looking at the code first I believe we need to note 3 main things:

It will teminate with $T(n)=1$ which is our base case, mystery is called 3 times with $n/3$, and the inner loops looping through $n^5$ times.

Combining all this knowledge we get a relation that looks like $T(n)=3T(\frac{n}{3}) + n^5$

Then we start looking for a reoccurring pattern to become evident.

=> $=3(3T(\frac{n}{9})+(\frac{n}{3})^{5})+n^{5}$

=> $=9T(\frac{n}{9}) + n^{5} + 3(\frac{n}{3})^{5}$

=> $=9(3T(\frac{n}{27})+(\frac{n^{5}}{9}))+n^{5}+\frac{n^{5}}{3^{4}}$

=> $=27T(\frac{n}{27}) + n^{5} + \frac{n^{5}}{3^{4}}+ \frac{n^{5}}{9^{4}}$

Now writing in terms of I for iterations

=> $T(n) = 3^{i}(\frac{n}{3^{i}}) + \frac{n^{5}}{3^{4(i-1)}} + \frac{n^{5}}{3^{4(i-2)}} + \frac{n^{5}}{3^{4(i-3)}} + ... + n^{5}$

UPDATE-
To achieve the base case($T(1)$) we assume i would be $log_{3}(n)$

 => $T(n) = 3^{log_{3}(n)}T(\frac{n}{3^{log_{3}(n)}}) + \frac{n^{5}}{3^{4(log_{3}(n)-1)}} + \frac{n^{5}}{3^{4(log_{3}(n)-2)}} + \frac{n^{5}}{3^{4(log_{3}(n)-3)}}... + n^{5}$
 
=> $T(n) = 3^{log_{3}(n)}T(\frac{n}{3^{log_{3}(n)}}) + \frac{n^{5}}{3^{4log_{3}(n)-4}} + \frac{n^{5}}{3^{4log_{3}(n)-8}} + \frac{n^{5}}{3^{4log_{3}(n)-12}} +... + n^{5}$

=> $=nT(1) + \frac{n^{5}}{(n^{4}*3^{-4})} + \frac{n^{5}}{(n^{4}*3^{-8})}+ \frac{n^{5}}{(n^{4}*3^{-12})} +...+n^{5}$

=> $=n+(3^{4}*n)+(3^{8}*n)+(3^{12}*n)...+n^{5}$

Looking at these $n$ terms, we see many different rates of growth as there are more terms, but the most imoactful growth rate is $n^{5}$ because all the other growth rates are smaller than that so we look at the largest one, from that we can infer that the bound for this is $O(n^{5})$

## New Update:

We focus on $n^{5}$ because is it the dominant term, we dont drop the other terms, be we focus on $n^{5}$ because it grows fastest.



