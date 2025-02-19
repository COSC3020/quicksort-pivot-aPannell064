# Quicksort Pivots

In the lectures I only briefly mentioned strategies for determining a good pivot
for quicksort. The implementation on the slides simply picks the leftmost
element in the part of the array that we consider as a pivot. I also mentioned a
few other ways of picking a good pivot, e.g. randomly.

Median-of-three is also a good way of picking a pivot -- inspect the first,
middle, and last elements of the part of the array under consideration and
choose the median value. Using the probabilities for picking a pivot in a
particular part of the array (in the same way as we did on slide 34), argue
whether this method is more or less (or equally) likely to pick a good pivot
compared to simply choosing the first element. Assume that all permutations are
equally likely, i.e. the input array is ordered randomly.

Your answer must derive probabilities for choosing a good pivot and
quantitatively reason with them.

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Answer

Using the metric from the slides, we know that a "good pivot" occurs whenever,
the chosen pivot is in the middle half of the values. To find the probability that
we get a good pivot, it is easiest to find the probability that we don't get a good pivot
and then subtract that from 1. This is possible because if we get three indexes and any of
the values at those indexes is in the middle half, we will end up with a good pivot. 

When we chose the first element, there are $\frac{n}{2}$ bad choices with $n$ total choices.
If we chose a second element, we have $\frac{n}{2} - 1$ bad choices left with $n-1$ total choices 
left. When we chose the third element, we have  $\frac{n}{2} - 2$ bad choices left with $n-2$ 
total choices left. To get the probability that we have the bad pivot, we can divide the number
of bad options for each choice by the total number of options and then multiply the three values
together. This gives us:

$\frac{n/2}{n} \cdot \frac{n/2-1}{n-1} \cdot \frac{n/2 - 2}{n - 2} = \frac{n(n-2)(n-4)}{8n(n-1)(n-2)} =  \frac{n^3-6n^2+8n}{8n^3-24n^2+16n}$

The probaility of getting a good pivot can be represented as $1-\frac{n^3-6n^2+8n}{8n^3-24n^2+16n}$. 
Obviously, this doesn't mean much as it is in terms of n. Additionally, this probability won't be
100% correct for certain values of n. If n is 3, for example, this formula gives us 1.0625, when the
correct value should just be 1, as this method will always give a good pivot for three elements. This
is because you can't get the middle 1.5 values of a list. To make the answer more clear, we can take the
limit of this formula:

$\lim_{n\to\infty} \left(1-\frac{n^3-6n^2+8n}{8n^3-24n^2+16n}\right) = 1 - \frac{1}{8} = \frac{7}{8}$

Obviously, the median-of-three method is still not perfect, but it only takes constant time. 
Additionally, using this method, you are indeed more likely to choose a good pivot as, the probability
calculated in the slides is only $\frac{1}{2}$.

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. 
All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that 
if plagiarism is suspected, charges may be filed against me without prior notice."
