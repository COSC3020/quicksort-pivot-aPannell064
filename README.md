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
the chosen pivot is in the middle half of the values. There are three cases in
which the median will fall into that category. This first is if all three chosen
elements are in the middle half. The second is if two of the elements are in the
middle half. The final case is if only one element is, but that element is the median. 
To find the probability of each case, you can take the total number of valid elements left
and divide it by the total number of elements left, then multiply the three values together
with the number of ways each case can occur. Finally, we can add the probabilities of each of 
the three cases together to get the total probability.

### First Case - All three chosen elements are in the middle

There are n/2 elements in the middle and there is only one unique combination that puts all three
elements in the middle. 

$1 \cdot \frac{n/2}{n} \cdot \frac{n/2-1}{n-1} \cdot \frac{n/2 - 2}{n - 2} = \frac{1}{8} \cdot \frac{n(n-2)(n-4)}{n(n-1)(n-2)} 
= \frac{1}{8} \cdot \frac{n^3-6n^2+8n}{n^3-3n^2+2n} = \frac{2n^3-12n^2+16n}{16n^3-48n^2+32n}$

### Second Case - Two chosen elements are in the middle

There are n/2 elements in the middle and n/2 elements that are not in the middle. There are
three combinations because there is one for every chosen value as each chosen value can be in 
the middle once. 

$3 \cdot \frac{n/2}{n} \cdot \frac{n/2-1}{n-1} \cdot \frac{n/2}{n - 2} = \frac{3}{8} \cdot \frac{n(n-2)n}{n(n-1)(n-2)} 
= \frac{3}{8} \cdot \frac{n^3-2n^2}{n^3-3n^2+2n} = \frac{6n^3-12n^2}{16n^3-48n^2+32n}$

### Third Case - Only the median is in the middle

To get the median to be the only value in the middle half, the two other elements need to be split
between the first and fourth quartile. There are n/2 elements in the middle, n/4 elements in the 
first quartile, and n/4 elements in the last quartile. The are six combinations because we are 
essentially finding the number of ways that we can order three elements, which is 3! or 6. 

$6 \cdot \frac{n/2}{n} \cdot \frac{n/4}{n-1} \cdot \frac{n/4}{n - 2} = \frac{6}{32} \cdot \frac{n^3}{n(n-1)(n-2)} 
= \frac{3}{16} \cdot \frac{n^3}{n^3-3n^2+2n} = \frac{3n^3}{16n^3-48n^2+32n}$

### Final Probability and Analysis

To get the probability of the good pivot, we can add the probabilites of each of the previous cases together:

$\frac{2n^3-12n^2+16n}{16n^3-48n^2+32n} + \frac{6n^3-12n^2}{16n^3-48n^2+32n} + \frac{3n^3}{16n^3-48n^2+32n} = 
\frac{11n^3-24n^2+16n}{16n^3-48n^2+32n}$

Right now, this formula doesn't mean much as it is in terms of n. Additionally, this probability won't be
100% correct for certain values of n. If n is 3, for example, this formula gives us 1.34375, when the
correct value should just be 1, as this method will always give a good pivot for three elements. This
is because you can't get the middle 1.5 values of a list. To make the answer more clear, we can take the
limit of this formula:

$\lim_{n\to\infty} \left(\frac{11n^3-24n^2+16n}{16n^3-48n^2+32n}\right) = \frac{11}{16}$

Obviously, the median-of-three method is still not perfect, but it only takes constant time. 
Additionally, using this method, you are indeed more likely to choose a good pivot as, the probability
calculated in the slides is only $\frac{1}{2}$.

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. 
All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that 
if plagiarism is suspected, charges may be filed against me without prior notice."
