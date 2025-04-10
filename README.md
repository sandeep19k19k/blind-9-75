# blind-9-75
3 SUM.

Actually , a very good question to demonstrate the importance of pre-processing data before working on it.

key point:
When input type is list and there is gut feel that question can't be solved in O(n) time,  i.e we take atleast O(nlogn)/O(n^2) , gives us the freedom to use inbuilt sort function in python .( which is O(nlogn) - timsort )

Now that we are speaking about sorting. let me insert key difference b/w 
1)sorted(x)  . creates new sorted list .works on any iterable. i.e tuple also

 2) x.sort()  . in place sorting. no extra space consumption. only works on lists.

Here , this program can be greatly simplified ,if we sort it.
i.e sum of 3 values = 0.  
That means, if all elements positive , result not possible.
(if we want ,we can use this condition to reduce time in some specific test cases.)
If list contains only 0's and positive elements , then it is mandatory that atleast 3 0's are present in the list.

In general case, where the list contains negative,0's and positive elements , sorting allows us to structure / pre-process the data ,on which application of further logic becomes easier.

Now , we iterate through the list .
During iteration, we fix an element.
Inside the iteration, take 2 pointers . left , right=i+1 , len(nums)-1.
i.e fix one element, then in the right sub array , use 2 pointer approach to sweep through through rest of the elements , to pick remaining 2 elements , such that these 3 add upto 0.
Here to avoid overlapping triplets, the condition , while (left<right ) , is very crucial .( making sure second and third element don't exchange their orders in the triplet , which leaps to overlapping triplets)
And this condition is used at multiple locations ,  to make sure , we optimize the process. i.e without this condition , we also risk increasing the time complexity . i.e with condition, it is guaranteed that we sweep at max 'n' elements inside loop. 
Without condition , instead of sweeping , we might lead to nesting.
TO Summarise , Avoid overlapping triplets, Avoid out of bound errors, Optimize the inner loop time complexity . (i.e Do not nest , just sweep the elements).

Then we add this triplet (which itself is a list)  to final list named result using append method.
After we found a valid triplet,
One more key analytical aspect is that , once we find a valid triplet, we update both left pointer and right pointer, bcoz , in a triplet, if one element is fixed , and now you found second & third elements, mere changing of only  one element out of second ,third elements is not enough( against the logic of the fact that they should add upto Zero. )
Second element is changed( most likely increased in this case) , directly infers the fact that , third element should also be changed ( most likely decreased in this case).

Where as before/ until we find a valid triplet ,  updation of one pointer is enough.
 i.e when sum of triplet is greater than zero, we pull right  pointer to left, to reduce triplet value.
whereas, when sum of triplet is less than zero, we push left pointer to rightside, to increase triplet value.

i.e while (left <right):
         case 1: triplet sum equal to zero , append triplet to result list. update left and right pointers.(skip duplicates and find new pair of second& third element). Make sure to adhere to left< right condition even while updating the left , right pointers.
         case 2: triplet sum greater than zero, update right pointer. pull to left
         case 3: triplet sum less than zero, update left pointer. push to right
Here , important thing is how we deal with that 2 pointers logic.
because there is a possibility of duplicate elements in the list.

skip through duplicates for first element .
Also skip through duplicates of second and third element found through 2 pointers.

Time complexity analysis is crucial here .
O(n) for fixating on first element.
Inside loop ,we are not nesting ( most important thing,bcoz nesting 3 loops leads to O(n^3) ), we are just sweeping through rest of the elements .
i.e it is O(n).

Final Time complexity : O(n^2)  ( observe how sorting didn't affect final time complexity. bcoz it is O(nlogn), which doesn't grow as rapid as O(n^2) and can be ignored.  )
Space complexity : O(1) if we ignore output list.
Else may be O(logn) .
