---
layout: post
title: Finding Prime Numbers with Python
description: Python to find prime numbers between a given range of integer numbers
image: "/posts/primes_image.jpeg"
tags: [Python, Primes]
---

In this post I'm going to run through a function in Python that can quickly find all the Prime numbers between a range given by user.  For example, if user passed the values 12 and 60, it would find all the prime numbers between 12 and 60(both inclusive) using a Python function!

If you're not sure what a Prime number is, it is a number that can only be divided wholly by itself and one so 7 is a prime number as no other numbers apart from 7 or 1 divide cleanly into it 8 is not a prime number as while eight and one divide into it, so do 2 and 4

Let's get into it!

---

First let's decide what we need from the user and how we can it be used in a function. Our intention here is to get receive two input values for the number range and use it as lower and upper boundaries to find prime numbers. So let's ask the user to input those values by using Input statement. 

```ruby
# pass lower and upper bound as input parameter
print(f"Please enter your integer number range below to find the prime numbers in between.")
l_bound = int(input(f"Enter your starting number : "))
u_bound = int(input(f"Enter your ending number : "))
```
We need to ensure the user input range is valid to proceed with further execution. If the difference between the lower and upper boundaries is greater than 0, we can decide to go with further execution.

```ruby
num_cnt = u_bound - l_bound
```

Now that we have received a valid input range, we can design a function prime_finder that accepts two values(lower bound and upper bound) and does the prime number computation.

```ruby
if num_cnt > 0:
    prime_list = prime_finder(l_bound,u_bound)
```

Our function is prime_finder and define it as

```ruby
def prime_finder(l_bound,u_bound):
```

We will then create a list to hold all numbers between the user input range,inclusive of input numbers. As we know about the range function, the upper limit need to be set one more than the required upper boundary to get it included in the range.

```ruby
# number range that needs to be checked
num_range = list(range(l_bound,u_bound+1))
```
Create a list to store the identified prime numbers from the number range.

```ruby
prime_list = []
```
We will now iterate through each element of number range and assume each number that we pick up is prime, unless we prove it is not by using a flag.

```ruby
for i in num_range:
    prime_flag = True
```
        
The smallest true Prime number is 2, so if the lower boundary of user input is 1, we can ignore that and continue with rest of elements in our num_range list.For example, if user input range is 1 and 50,we can ignore 1 from the list and start checking prime numbers between 2 and 51 (remember upper boundary has been set to upper boundary + 1).

```ruby
    if i > 1: 
        check_range = range(2,i)
```
For each element of the input range, check whether it is completely divisible by the checking range value and remainder is 0 using the modulus function. If remainder is 0, it has proven that number is not prime and should set the Prime flag to False. Also, skip the iteration as we have clearly determined the number is not prime.

```ruby
        for j in check_range:
            # check if remainder is zero                    
            if(i % j) == 0:
                prime_flag = False
                break
```
If Prime flag continues to be True, that means we never found this number is completely divisible by any other number, so consider it as Prime and include in our prime list.

```ruby
        if prime_flag == True:
            prime_list.append(i)
```

Now, that we are done with the prime processing, let's see how amny Prime numbers we have found within the input range.

```ruby
# get the total number of Prime numbers found
prime_cnt = len(prime_list)
```
Also, it would be excitng to see the largest among the Prime number list.

```ruby
# find the largest prime from the list
largest_prime = max(prime_list)    
```
It's time to let the user know what we found! Let's print a summary.
```ruby
print(f"There are {prime_cnt} prime numbers between {l_bound} and {u_bound}.Prime numbers found are {prime_list}. The largest prime number found is {largest_prime}.")
```
Also, we will return the prime list from the Primer finder function so that it can be further used in the program, if needed.
```ruby
return prime_list
```


Now, let's run it...

```ruby
Please enter your integer number range below to find the prime numbers in between.
Enter your starting number : 12
Enter your ending number : 60
There are 12 prime numbers between 12 and 60.Prime numbers found are [13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59]. The largest prime number found is 59.
```

Let's print and see what values the variables hold.
print(l_bound)
>>> 12

print(u_bound)
>>> 60

print(num_cnt)
>>> 48

Since num_cnt is greater than 0, prime_finder function is invoked. 

num_range = list(range(12,61))
print(num_range)
>>> [12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 58, 59, 60]

# Empty prime_list created.
prime_list = []
>>> []

# The first element of For loop is going to be 12. We are assuming this as Prime by setting the flag true unless it is proved otherwise.
for i in num_range:
    prime_flag = True

    # 12 is greater than 1 and hence set check_range as [2,3,4,5,6,7,8,9,10,11]
    if i > 1: 
        check_range = range(2,i)

        # for each element of check_range, see if 12 is completely divisible by that number. First check_range number is going to be 2.So we would be checking if           12 modulus 2 is zero. If so, consider 12 as non prime and set prime_flag to False.Else, continue finding modulus of 12 with 3,4,5 and so on upto 11 to             see any of those gives remainder non-zero. 
            
          So here, 12 modulus 2 is 0 and hence it is not prime. Set prime_flag to False. Since we now know that 12 is not a prime, we do not want to continue               looking modulus with other numbers and so break the iteration and conitunue with our next number from num_range which is 13.
        
        for j in check_range:
            if(i % j) == 0:
                prime_flag = False
                break
        # When prime_flag is True,append the num_range value(i) to prime_list. Here, 13 would be the first prime number to be added to the list.
        
        if prime_flag == True:
            prime_list.append(i)
    
            
I hoped you enjoyed learning about Primes, and one way to search for them using Python.