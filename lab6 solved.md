
team members contributed - Anhad Puri,yogesh attri,Lavakeshon Selvarajah



1. What sorting algorithm was the speaker trying to improve?

Alexandrescu was trying to improve the quicksort algorithm in reference to binary search. He wanted to find a way to quickly sort medium sized array. The results of his experiment demonstrated that binary insertion sort consistently performed slower than linear insertion sort. In an attempt to improve the performance of binary insertion sort, Alexandrescu increased the threshold, but this adjustment actually resulted in even slower execution times.


2. At what partition size does VS perform a simpler sort algorithm instead of continuing to partition?

During the partition a pivot happens and this is where it will put the array in order. The order is everything smaller than the pivot number goes on the left side and everything larger goes on the right side and then it sorts through the algorithm.  Take a set and repeat the steps until there are 4 main sets. In this way you would do as many necessary depending on how many elements you have in your algorithm, considering Alexandrescu is talking about a quicksort implementation there won't be too many to go through and the best case is you find the median.

---
3. At what partition size does GNU perform a simpler sort algorithm instead of continuing to partition?

The partition size, crucial for determining when GNU initiates a simpler sorting algorithm, is set at 16 units, but it may vary based on the operating system. Additionally, this limit is dynamic and adjusts according to the input provided to the algorithm. This adaptability is essential for accommodating new operating systems and facilitating the efficient rearrangement of data.


4. Regular insertion sort does a linear search backwards from end of array for correct spot to insert. According to the speaker, why does switching to a binary search not improve performance?

In the context of regular insertion sort, a linear search conducted in reverse from the end of the array to the correct position proves to be consistently faster than employing a binary search method.Alexandrescu explained this by contending that it entails less effort to achieve equivalent results, thus making it a superior approach. Upon further investigation, employing a 32-threshold and conducting a comparison revealed a 15% reduction in terms of the same number of actions. However, it also resulted in a 13% performance reduction, indicating a runtime increase. This underscores that, despite the lower number of comparisons, binary search tends to be slower due to the additional runtime overhead.

---
5. Describe what is meant by branch prediction? (this may require further research)

Branch predictor works well with highly predictable comparisons. This is because it a branch predictor likes to attempt to guess the outcome/destination between the operation is complete with very minimal context. This is supposed to increase the flow in instructions. Conditional branches, such as if statements or loops, introduce a challenge because the processor must decide which branch to take before the condition is fully evaluated.However there is also something called "branchless binary" which is much more slow since it doesn't stop until it's finihsed going through all the bits.


---
6. What is meant by the term **informational entropy**? (this may require further research)

Informational entropy is very useful for things such as building tress. is a concept that measures the uncertainty or surprise associated with a random variable or a set of data. It is a measure of the average amount of information, or lack of predictability, contained in a message or dataset. . This is also why it goes in hand with branch predictability. The success rate would also be much higher passing percentage. Entropy looks at the amount of random variables or the results of them in a random process which can give different values that are present in the variable but also by the amount of surprise that the value of the variable holds. This explains a random variable as an average amount of information that can hold the variable's possible outcome.


---
7. If size == 15, what is size & 1?  if size == 16, what is size & 1?  Explain how right = first + 1 + (size & 1) avoids a conditional check.

	Hint:
	* The & is the bitwise AND operator in C/C++.  It takes the bit representation of the two operands and perform an AND operation on each of the corresponding bits to form a result
	* To do this question first convert 15, 16 and 1 to base 2 (use 5 digit representation for all of them).  Then perform an AND operation of the correseponding bits of the operands... this will get you a 5 digit binary value.  Convert the value back to base 10 .

In bitwise of size == 15, the size of &1 is 01111. if we convert the value from binary to base 10 then it would be 15 base-10. 

If the value of size == 16, the size of &1 is 10000. if we convert the value from binary to base 10 then it would be 16 base-10

`right = first + 1 + (size & 1)` - first is explained as positioning ourself in the middle of the array but then depending on how that is with the number of elements This avoids the conditional check because there is no if condition in the code, meaning no `if(size = 1; right++)` which means this is going to be alot faster because it is a code with a jump.

---
8. Speaker suggests the following algorithm:
	* make_heap()
	* unguarded_insertion_sort()

	He suggests that by doing make_heap() first then you can do something called unguarded_insertion_sort().  Explain what is unguarded_insertion_sort() and why it is faster than regular insertion sort.  How does performing make_heap() allow you to do this?
	
Performing insertion_sort() involves more extensive work because it necessitates initially creating a heap using make_heap(). The make_heap() operation is intricate, encompassing various tasks. Consequently, when transitioning to insertion_sort(), the established heap structure is disrupted.

In contrast, the approach of unguarded_insertion_sort() eliminates the need for exhaustive bounce checking with make_heap(). This is because, during traversal through the array, it only encounters the smallest value. As the algorithm progresses, when a value smaller than the current one is encountered, it is inserted in order. This streamlined process does not require meticulous rearrangement, contributing to its swiftness compared to the more involved insertion_sort().

9. The speaker talks about incorporate your conditionals into your arithmetic.  What does this mean?  Provide an example of this from the video and explain how the conditional is avoided.

When the speaker talks about incorporating the conditional into the arithmetic he explains that there is a method that pushes an element that's not in the heap into the heap, called `push_heap()` which helps to optimize the code outside the outer loop. Alexandrescu then goes into explaining that when you integrate conditionals within the arithmetic, you want to make sure everything is a bool, no `if`. The example code he used shows `if (size < 3) { sort2(first[0], first[size == 2]);` which means that that it will swap the elements if size is less than 3 and not in the right order. This is the example that he showed on integrating conditionals in our arithmetic and why it's important. 

---
10.  The speaker talks about a bug in gnu's implementation.  Describe the circumstances of this bug.


In Alexandrescu's discussion on push_heap, he highlights its inefficiency in GNU due to structured loops and finite iterations, leading to sluggish performance. The bug in push_heap() arises from prematurely breaking out of the loop after the initial condition check. This premature break results in additional work for the remaining code, contributing to suboptimal runtime performance. Alexandrescu proposes a solution by advocating for the use of an infinite loop, eliminating the need for multiple executions and ensuring more efficient code execution.
---
11.  The speaker shows several graphs about what happens as threshold increases using his new algorithm.  The metric of comparison is increased, the metric of moves are increased but time drops... What metric does the author think is missing?  Describe the missing metric he speaks about in the video.  What is the metric measuring?

The author identifies a crucial metric that seems to be absent, labeled as `Collect D(n), average distance between two subsequent array accesses`. This metric is proposed to offer insights into cache behavior without relying on a cache-specific metric. It becomes evident that this metric's effectiveness is limited when considering different ends of the array. In exploring the distance for quicksort, Alexandrescu observes a significant value, particularly as quicksort starts with the worst-case scenario for partitioning. Despite both `D(n)` and the graph showing decreasing trends, Alexandrescu suggests a solution: constructing a composite metric that encompasses all three implementations. This composite metric aims to provide a comprehensive assessment of computational cost, especially in the context of improving sorted algorithms.
---
12.  What does the speaker mean by fast code is left leaning?

When Alexandrescu discusses the principle of "fast code is left-leaning," he suggests that for optimal speed, crucial code segments should be positioned towards the left margin of the page. This concept reflects the idea that critical and frequently executed code is more efficiently placed closer to the beginning of the code.

Considering typical coding structures such as if statements, for loops, switch statements, and other decision points, the reasoning is that when these constructs are located towards the left side of the code, it contributes to a more streamlined and potentially faster execution. This perspective takes into account that these constructs often involve decision-making and looping, and arranging them towards the left margin can enhance the overall efficiency of the code. A code that wants to be fast is left-leaning because it doesn't want to mix hot and cold operations which is explained more in the next question.

---
13.  What does the speaker mean by not mixing hot and cold code?

In discussing hot and cold code, Alexandrescu characterizes the separation of these elements as an "anti-pattern inefficiency," an aspect that can be avoided. Ideally, hot code, which involves critical and frequently executed segments, should be grouped together, distinct from cold code, which is less crucial and often pertains to "fix-up" tasks. For instance, hitting a break and returning to exit the code represents hot code, while less critical fix-up operations constitute cold code. The goal is to organize hot and cold code efficiently to enhance overall code performance.

## Reflection:
1. When he talked about the unguarded_insertion_sort() for the generic type, I had trouble understanding. I had to watch this section again several times before I really grasped his explanation, but once I did, I realised how the code affected the heap as previously said. Unlike standard insertion_sort(), which impacts the heap differently, unguarded_insertion_sort() does not require a bounce check. For instance, in insertion_sort(), the first element is sorted, but since the heap is still valid, the second and third elements may be out of order. 1, 7, and 4 are acceptable as the roots as they are less than the second and third components combined with their offspring, which makes them a legitimate heap. This wouldn't matter, though, because unguarded_insertion_sort() will still function and be legitimate.
2. Learning about the many intermediary structures besides the heap was intriguing. My belief is that building a heap mostly enhances speed since it is already partially sorted, leading to quicker or more uniform linear searches, which may also improve branch prediction. In week two of data structure classes, I believe we were introduced to big-O, which is comparable in terms of performance and easier to construct. For linear insertion sort, though, the outcome would be comparable.The use of a fibonnaci heap, for example, may provide different findings from Alexandrescu's demonstration of heap performances, which was limited to two simple child heaps. Reseasoning can lead to inferior overall results, but it can also move harder in the direction of strong invariants. Moreover, these heaps remain below the 255-element maximum size criterion, and the heap must be within the array that is being sorted.
3. I got a lot of ideas from this video about how to make my code better, especially when I compare it to the provided examples. Plotting gnu would alter the chart, as demonstrated by Alexandrescu in his movie, along with other concepts like insertion_sort() and unguarded_insertion_sort(). He talks over how important this is and how to do it more effectively.  It was also fascinating to hear another speaker's viewpoint on comprehending the subject more thoroughly using examples and visuals while he was discussing bubble search sort and linear search sort, as those are topics we focus on in class.

## References:
- https://machinelearningmastery.com/what-is-information-entropy/
- https://pvk.ca/Blog/2012/07/03/binary-search-star-eliminates-star-branch-mispredictions/



