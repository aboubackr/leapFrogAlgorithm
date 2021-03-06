<img src="https://weaknetlabs.com/images/mathematicslogo.png"/>

# Leap Frog Algorithm
My algorithm and answer to closest sequence problem as challenged here: https://codefights.com/challenge/Qjts7cukDvYpDW4Bc. As I find the time, I will be writing this in many programming languages, but the initial development was done in Perl so the descriptions and definitions will be displayed in Perl, initially at least. This problem led me to found the "*Leap Frog*" algorithm, which leaps back and forth over the value until a match is found.

##The Problem - Explained:

>_The difference between two sequences of the same length a1, a2, a3,..., an and b1, b2, b3,..., bn can be defined as the sum of absolute differences between their respective elements:_

>_diff(a, b) = |a1 - b1| + |a2 - b2| + ... + |an - bn|._

>_For the given sequences a and b (not necessarily having the same lengths) find a subsequence b' of b such that diff(a, b') is minimal. Return this difference._

>_Example_

>_For a = [1, 2, 6] and b = [0, 1, 3, 4, 5], the output should be
closestSequence2(a, b) = 2._

>_The best subsequence will be b' = [1, 3, 5] which has a difference of 2 with a._

>_Input/Output_

>_[time limit] 4000ms (js)
[input] array.integer a_

>_Constraints:
3 ≤ a.length ≤ 1000,
-1000 ≤ a[i] ≤ 1000._

>_[input] array.integer b_

>_Constraints:
a.length ≤ b.length ≤ 1000,
-1000 ≤ b[i] ≤ 1000._

>_[output] integer_

##The Code/Answer - Explained

The program is broken up into two functions, `main()` and `findClosest()`.

###main()
The purpose of `main()` is to encapsulate our variables and provide a place for entry in our application for the loader. We start off `main()` with two arrays, `@a` and `@b`. These will be the arrays of sequences that we will test to find the new sequence and ultimately the returned difference. The `$diff` integer is simply a placeholder for the difference of the two sequences. For instance, the problem explains that the returned result must be:

>|a1 - b1| + |a2 - b2| + ... + |an - bn|.

so we can simply add up the differences of the sequences without even creating a new sequence array as you see in the `foreach()` loop below the `$diff` definition. `$diff += abs($j - findClosest($j,1,@b)) if(!($j~~@b))` will be performed by the compiler in a PEMDAS order, meaning, parenthesis nested will be executed first. So the absolute value, using `abs()` will be executed after the `findClosest()` function which will be execute after the truth check of whether or not `$j` is in the second sequence array, `@b`. When this for loop has completed iterating through the values in the `@a`, initial sequence, it will print the result in `$diff`.

###findClosest()
This is the linear "*Leap Frog*" algorithm that I was able to come up with. I call it the "*Leap Frog*" because of the way in which the algorithm leaps back and forth over our value from the first sequence, we'll call this value *i*, incrementing and decrementing *i*, recursively, until a match of *i* is found in the second sequence. The "*leaps*" just get larger, thus we end up with the closest number in the second sequence to *i*. This is sort of a "middle-out algorithm," because at any integer on the number-line, *i*, will be between two other numbers and the function will work it's way out starting at *i*, then *i*+1, then *i*-*i*+1, then *i*+2, then *i*-*i*+2, ..., etc. 

As for the linear big O notation of this simple algorithm, the best case scenario as previously mentioned as *n*, is simply O(1), with a single execution/return. Worst case scenario, is still pretty simple, as O(*n*), were *n* is the difference between *i* and it's matching value in the second sequence.

The code, `return ($_[0]+$_[1]) if(($_[0]+$_[1])~~@{$_[2]}); # leap right` hops right, or adds `1` to the number (or shifts the number-line if you think of it in simple mathematics). While the code, `return $_[0]-$_[1] if(($_[0]-$_[1])~~@{$_[2]}); # leap left` leaps left to decrement the value. I guess that when I picture numbers in sequence, I cannot help to think of them on a strangely distorted number-line with the value in quest in the dead center. So, again, the action of "*leaping*" just made sense to me. This is obviously faster than going through EVERY single element in `@b`, finding the difference, then calculating which difference is lowest.

Please note that this function/program will break, or result in undefined behavior, at VERY large numbers. Billions for 32 bit machines, (-2,147,483,648 (-231) through 2,147,483,647 (231 - 1) for signed numbers [Wikipedia.org](https://en.wikipedia.org/wiki/32-bit)) and quintillions for 64 bit processors (Signed: From −9,223,372,036,854,775,808 to 9,223,372,036,854,775,807, from −(263) to 263 − 1 [Wikipedia.org](https://en.wikipedia.org/wiki/Integer_(computer_science)#Common_integral_data_types)). This is because the leaps will go out of bounds or loop around.

~Douglas
