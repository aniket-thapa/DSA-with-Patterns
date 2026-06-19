Lecture Videos Transcripts

1. Introduction to Sliding Window

Transcript:

## Introduction

A very warm welcome to the second pattern, which is the Sliding Window. For those who have already watched Two Pointers, understanding this Sliding Window will be very easy. For those who haven't, it will still be easy; it's nothing to worry about. But make sure of one thing: this is an introductory video. Right? This means you will get a flowchart in this. You will learn the rules about when and how to use this pattern. So please watch this video until the end because the upcoming videos will depend entirely on this. Understood this much? Let's move forward.

## Understanding the Sliding Window

Now, look at the Sliding Window. What does "window" mean? Window means window. And "sliding" means that this window can shrink or expand on its own. This means right now the size of the window is this much. It's possible that at a future point, the size of the window becomes larger. It might expand, or it might stay the same size at a future point. Or it might shrink. So, it can expand or shrink on its own. That is why it's called a sliding window. Window simply means this is a window. Alright.

Now, how does it slide? How does it shrink? With the help of Two Pointers. That is exactly why we study Two Pointers first. We study Two Pointers first, and then we move on to the Sliding Window.

Now, it shrinks with the help of **low** and **high**. What happens is that you place _low_ at one end and _high_ at the other end. Both of them can only move in one direction. _Low_ can move this way, and _high_ can also move this way.

- **Expansion:** Whenever _high_ moves—whenever you do `high++`—this window will expand because the distance between _low_ and _high_ increases.
- **Shrinking:** Whenever you do `low++` and keep _high_ in one place, the window shrinks because the distance between _low_ and _high_ decreases.

Notice one thing: when it expands, it grows in this direction (to the right), and when it shrinks, the part from this side gets cut off. Meaning, this window is only growing in the right direction. If it shrinks, you cut off a portion from here by incrementing _low_. If it expands, you add a portion here by incrementing _high_. This is how this window works. Right? This pattern is called the Sliding Window.

## The Flowchart: When to Use It

Now, the most important thing: the flowchart. First of all, where will it be applied?

- It will be applied to an **Array**.
- If not an array, then a **String**, because a string is also a type of array.
- It will **not** be applied to a Linked List. In 99.9% of cases, it will not apply to a Linked List. Remember this, tie a knot on it. It won't apply.

So, your very first hint is: it will only apply if it is an Array or String question. Otherwise, it won't. Best thing. Good.

If—and only if—the question mentions **Subarray** or **Substring** (when we are talking about strings), or if you understand that this is what the question implies, _only then_ will the Sliding Window apply. Otherwise, it won't. Alright?

- **Subarray** means continuous. Right?
- **Substring** also means continuous.
- **Subsequence** is different. Remember this, people get confused. They see subsequence and start applying this pattern. Subsequence means non-continuous. Non-continuous means if you have elements in an array, you can pick any two random elements. Take this one and take that one. That is a subsequence.

But if an array is given and you are asked to take a subarray of two, you have to take two _continuous_ elements. You have to take exactly these two, or those two, or any elements as long as they are continuous. Subsequence is non-continuous; you can take any two elements in order. Understood? So: Array, String, Subarray, Substring. Okay?

Now, what are we trying to find? What does the question want from you? The question can ask you for any of these:

- Maximum
- Minimum
- Longest
- Shortest
- Sum
- Count
- Average
- At most K
- At least K
- Exactly K

Look carefully, this is a very long list. But when should you even think about this list? You should only think about it when you pass the first two steps: it must be an Array or String question, Subarray or Substring must be mentioned, and along with that, these specific things are asked. Look carefully, take a screenshot, note it down in your copy: _Maximum, Minimum, Longest, Shortest, Sum, Count, Average, At most K, At least K, Exactly_.

See, if you find these words in the question and you understand that this is exactly what is being asked of you, then you will apply the Sliding Window. Right? Let's review—it was just these three things: Array/String, Subarray/Substring (must be continuous), and if you are finding any of these values, then the Sliding Window will apply. Sliding Window will apply. Sliding Window will apply. Look at the flowchart again. Pause the video and take a look. Note it down in your copy. Look at the flowchart. Note it down. Understood? This is when the Sliding Window will apply. Alright?

## Fixed vs. Dynamic Windows

Now, a small detail. Sliding windows are of two types:

1. **Fixed**
2. **Dynamic**

I just told you that it expands and shrinks. It's possible that it might not do that. How? For example, if the question gives you this array: `1 0 3 5 2 1 4 0 1 2 3 4 5 6`. The question asks you to: _"Take subarrays of length three and find the maximum of all their sums."_

What does the question mean in plain Hindi? Take all subarrays of length three in this array, calculate their sums, and return the maximum among them.

First of all, let's apply our algorithm and flowchart:

- Array is mentioned. Yes, an array is given.
- Subarray is mentioned.
- Find maximum of all their sums.

So all our conditions are satisfied. Maximum of sums. Therefore, the Sliding Window will definitely apply here. If it doesn't apply here, it won't apply anywhere. This is a perfect question to understand the flowchart.

When the question gives you a length of three—in some questions it's not given, some just say take a subarray of any length—but when you are given the size or length of the subarray or substring, you use a **Fixed Window**. How do you take a fixed window? A window of size three. How to write this in pseudocode or actual code, we will teach tomorrow. Right now, we are just teaching the concept. Take a fixed length. Take a length of three. Right?

## Fixed Window Example

Now look. What did we explain in Two Sum? Before writing anything, think of the Brute Force approach.

- **Brute Force:** Take all subarrays of size three from this array. How will you extract them? One will be `1, 0, 3`; then starting from 0 it will be `0, 3, 5`; then starting from 3 it will be `3, 5, 2`; then starting from 5 it will be this much, and so on. You found all these subarrays. Calculate the sum of all of them, and return the max. That's well and good.

But with the Sliding Window, you can do this much faster. You start your window like this. This is your window. Right? You calculate its sum. Its sum is `4`. Right? For the first subarray, when the length is given, you calculate `4`. After that, you shift the window by one position. The size of the window is not changing. Look, the size is still three. Just the position of the window shifted by one.

Now, to calculate its sum, you don't add it from beginning to end again. Look at what happened. You were here. Now you are here, so `0` and `3` are common. What are we saying? Enlarge the array and look at just four elements: `1, 0, 3, and 5`. Okay? Let me explain this again. This is a very important concept to understand; that's why we are putting in so much effort.

Your first subarray was this. Right? Yes. Your second subarray was this. When you shifted it, this became the subarray. Now look, `0` and `3` are common in both. What changed? `1` changed, and `5` changed.

- Your previous sum (Sum 1) was: `1 + 0 + 3`.
- What did your new sum (Sum 2) become? `0 + 3 + 5`.

So what are you doing? Look at the difference between Sum 1 and Sum 2. `0` and `3` are exactly the same. Yes. Sum 2 just doesn't have `1`. So `1` is gone, and `5` is there. This is the only difference. If you do this, you get Sum 2. What is missing in Sum 2? Sum 2 doesn't have `1`, and `5` got added.

Whenever you do this in a Sliding Window, what do we say? We already know the sum of this window; it is `4`. How will we find the sum of the next one? To find its sum, we will do nothing but `4 - 1 + 5`, and you will get `8`. Look, the sum of this window will be `8`. Is it `8`? Yes, it is. The sum of this window is `8`.

How will we find the sum of the next window? Subtract the previous element, add the next element. `10`. You can check by calculating its sum: `3 + 5` is `8`, plus `2` is `10`. This is how we shift the window, and it makes your work very fast. Right?

So, this is for a fixed length.

Whenever the length of the subarray is **not** given in the question—if a dynamic size is given, or the length is not given at all—then you will use a **Dynamic Window**, where _low_ can increase, and _high_ can also increase. So the window will sometimes be this big, sometimes that big, sometimes it will grow, sometimes it will shrink. It will keep getting bigger and smaller.

## Conclusion

So this was the Sliding Window. Its flowchart, its template, and the core concept of when the Sliding Window is used. The Sliding Window is used in any such question where you have to deal with a subarray or substring, and you have to do some nonsense like minimum, maximum, longest, shortest, etc.

Write this down. Note this down. And from tomorrow, whoever hasn't received the pattern sheet yet—whoever hasn't received the pattern sheet yet, download it from the description. From tomorrow, we will start solving its questions one by one. See you tomorrow.

2. Sliding Window Pattern: Questions

Transcript:

## Introduction to Sliding Window

Today's two questions, brother, to my understanding, are the _only_ two questions you need to study for the sliding window. I mean, if I ever had to teach someone just two questions in my life and explain the sliding window, I would share these exact two questions. And the example I've used—the hiring and firing example of how a company keeps hiring, the work gets done, and then it keeps firing—that exact same concept is used in the sliding window. You will not find such an example and such an intuition anywhere else on the internet. You will get the code; code is available everywhere. Keep copying that. But if you want to understand the intuition, watch both questions.

If you are watching this video, whether you are a new student or whoever, don't just watch one question and leave the other. Either don't watch both—just close it right now. It's only been 30 seconds; close it. If you are watching, watch both. If you are not watching, don't watch either. If you go to an interview after watching just one, you won't be able to solve the other. Here is their link. Right? So it was simple, and let's begin. It's going to be a very good, detailed video. Please watch it. And yes brother, there was a long break, but from today, it will run exactly properly. From today, the video will be on, and you won't get that choppy, cutting voice either. Right?

For those coming to the channel for the first time, today is Day 2 of the sliding window pattern. You will find the sheet in the description. And the two questions we are doing today... I'll tell you in a little bit. iPad notes will be in the description. Insta and LinkedIn links will also be in the description. And code links in CPP, Java, and Python will also be in the description. All that is done.

---

## Question 1: Fixed Size Window

Now, the two questions we are doing today—first of all, what is the first question? "Given an array..." these aren't my words, this is written exactly like this in the question. Right? Let's look at the wording of the first question, and then we'll see how the pattern applies, why it applies, what to do to apply it, and how to apply it.

What do you have to do? You are given an array. What do you have to do? Find the **maximum sum of any subarray of size K**. Subarray, not subsequence—subarray of size K. This is your question.

### Identifying the Pattern

Let's quickly recap what happened the previous day because many people have forgotten. When does the sliding window pattern apply?

- First of all, it must be an array question. An array, a list, or a linked list question.
- The question must explicitly mention the word "subarray" or "substring." (String also falls under array/list; a string is basically an array). Right? It should be a subarray or substring question.
- If both of these become true. If both of these are true, then after that, what are we trying to return? Meaning, you are told "find this, do this thing." What are we finding? We are trying to find either the `max`, `min` of something, or the `longest`, `shortest`, or something like `sum`, `count`, or `average`, or `at most K`, `at least K`, `exactly K`. Right? We are trying to find a combination of these things.

If these two are not true, do not come to this step. If they are true, peek into this list to see if we are trying to do a combination of these.

Let's check this question. Is it an array question? Yes, it's an array question. So this is true. Do we have to do work related to a subarray or substring? Yes, you have to do something with a subarray. This is also true. Now let's look at the second list. What do we have to find? Maximum sum. Maximum sum—this combination fits perfectly. If all three things fit, there will never be a time in the world when this is not a sliding window question. You can do it in some other way, but its best, most optimal way will be the sliding window.

So you see how reading a two-line question makes it clear that a sliding window is required. 50% of your work is done. The interviewer is already 50% happy in that time that you understand what kind of question this is. Now, some people start applying graphs, trees, DP, or start doing random things. No. We won't do all that because we study patterns. Reading the question told us this is a sliding window pattern. Right? Good.

### The 4 Steps of Sliding Window

Now, what is the sliding window pattern? First of all, what is a sliding window? That is in the introduction video. Go check the playlist. What's the addition here? Any sliding window question has three steps. It has three steps. Right?

1. **Identify the Pattern:** Meaning, is this a sliding window question or not? We have already done this work. Very good.
2. **Find the Window Type:** Is it a fixed window or a variable window? Meaning, do you remember what we said in the first intro? In any array or list, what does a window mean? A window means this is a segment. Now this window moves, meaning it slides. You must have seen sliding doors, sliding them with your hand. Similarly, first, this window is here, then it comes here, then it comes here, so it keeps sliding. Right? Now, when it slides, is a window of the exact same size sliding every time? Meaning, if the window is of size 3, are we just picking up this window and sliding it one or two steps? First, this size 3 window was here, then we placed it here, then here. This would be a **fixed window**—meaning the size of the window is not changing. If it's a size 3 window, it remains a size 3 window, you are just making it slide from here to there.
   What is a **variable window**? It means the size of the window is also changing. The window's position changes, it slides of course, but the size also changes. Sometimes it decreases from the back, sometimes it increases from the front. Sometimes it shrinks so the window gets smaller, sometimes it expands so the window gets longer. Meaning, first the window was like this, then we cut it so it looked like this, then we expanded it so it looked like this. That is called a variable window. The second step is to find out if this question requires a fixed window or a variable window. Right? How will you do that? We will explain that too.
3. **Find the Data/Information of the Starting Window:** Once you have figured out if it's fixed or variable, wherever you are starting your window from, it will have a size and a position. For example, you say your window starts at the beginning and is of size 3. This is your starting point of the program. What is the next step? Find its data or its information. Any window represents some information. Maybe that window represents the elements inside it. If this window has 3 elements, maybe this window is telling you what its sum is. Or maybe it's telling you who the max is inside it. Or who the min is. This is called the window's information. What does that window mean? When a computer sees that window, it understands zeros and ones. When you see it, what do you understand? That is called information. Meaningful data is called information. The window has three elements: `10, 20, 30`. That's just data. But what information are you getting? Maybe the information is that the sum of `10, 20`, and `30` is `60`. That is the information of that window. First, find that window's information in whatever way you can to start. We'll discuss all this further. This is just the approach to solving any sliding window pattern. There are these four steps; no question asks anything outside of these steps anywhere. Right?
4. **Slide the Window and Update Data:** Now that you've found the starting window, you slide the window or change its size. Whatever the question asks, slide the window or tweak its size. Now, find the data for the new window. Before, your window was this, now your window is this. The new window that is formed might have one more element added, so its sum might have increased, decreased, changed, or stayed the same. Find the information of that new window. Keep repeating this work until you reach the end of the array, until you get your answer, or until your window itself finishes.

In total, there are four steps. There are only four steps in any sliding window pattern. Look again. Identify if it's a sliding window. Done. Fixed or variable? Will the size change or remain the same? Find that out. Whichever window you start with, find its info. And the fourth step is, when the window slides and a new window is formed, you have to find its information too. Only then can you compare. What does sliding mean? Sliding means you keep looking at different parts of the array, right? If there are 10 houses, and you can only look at 2 houses at a time. You look at 2 houses and find out which one is more beautiful. Very good. Now you look at the next two houses. You need to find their information too. That's the only way you can look at all 10 houses and compare to find the most beautiful house among them! So do this. Your program will be solved in four steps. Right?

### Applying the Steps to Question 1

Now we will solve our question using these four steps. Your question gives you an array. What does the question mean in Hindi? What is a subarray in an array? Any continuous part of an array is called a subarray. For example, this is a subarray. The array is also a subarray of itself. Like subsets, right? A small part of it.

Now, what is the question telling you? You will be given an input `K`. All the subarrays of size `K` in that array—you have to find their sums. Find the sum of all of them, and from those, return the maximum sum. This is the meaning of the question in plain Hindi. Right?

If `K` is 2, keep all subarrays of size 2, find the sum of all of them, and whatever sum is maximum, return it.
For example: `100, 200, 300, 400` at indices `0, 1, 2, 3`.
It tells you `K` is 2. Now it asks for the answer.

- One subarray of size 2 is `100` and `200`.
- The second subarray is `200` and `300`.
- The third is `300` and `400`.

You have 3 subarrays. You need to find the sum of all three. So, it could be `S1`, `S2`, `S3`. Return the maximum among them.

- First subarray sum: $100 + 200 = 300$
- Second: $200 + 300 = 500$
- Third: $300 + 400 = 700$

Which is the highest? `700`. Your answer should be `700`. Correct? Understood? Okay.

Why does the sliding window apply here? We are looking at subarrays of size two. First, we looked at `100` and `200`. After that, we removed `100`. `200` is still there, and we added `300`. After doing some work with the first two and getting an answer, we left the previous one (`100`) behind and took the next one (`300`) inside. Then the same thing happened with `200`. We crossed `200` out, saying "you go away too," and took `400` inside. Now you are looking at `300` and `400`. If you try to remove `300`, there is no element left to bring inside because the array is finished. This is why we can only form three subarrays.

Every time we are kicking one guy out from the back and taking one guy in from the front. So the size of the subarray is being maintained. Because the question explicitly says subarray of size `K`. It doesn't say any size. Every time you have to look at a size 2 subarray.

So our Step 2: Is our window fixed or variable? **Our window is fixed.** Why? Because the question tells you to find one of size `K`. If `K` is 2, the subarray must be 2. `400` alone is technically a subarray, `200, 300, 400` is also a subarray. But we aren't taking them because the size would change. We only want two. We are taking a window of exactly size 2. First this window, then this, then this. The window is sliding—leaving the back one, taking the front one—but its size remains exactly the same. We know the window is fixed. Step 2 is done.

Now come to Step 3. Step 3 said wherever you start your window, find its information. Where do we start? Naturally, you'll start from the beginning of the array. This is your starting point. The window size is `2`. So your starting window is `100` and `200`. What is its information? What are we trying to find? Its sum! We aren't trying to find its name. The information of that window is the sum of its elements. How do you find the sum? You iterate. From `0` to where the subarray ends. You find the sum is `300` ($100 + 200$). Step 3 is complete. Don't think like a computer right now; think like a human. It makes it easier. Many people read the question and start thinking "which loop should run, what algorithm, what graph?" Let the computer think about that. You are human! Just do $100 + 200 = 300$.

Step 4: When your window slides to `200` and `300`, you have to find its info. How will you find it? One way is to iterate again and add `200` and `300` to get `500`. Then for the next, add `300` and `400` to get `700`. But this is a ridiculous way. Why?

Imagine you have 5 people at your house. Every person gives you money: ₹5, ₹4, ₹2, ₹10, ₹5. You collect their money and count it: ₹26. You sit back comfortably. Now the middle guy says, "Sir, I can't give money, I'm going home. Give me my ₹2 back. My brother will come instead, but he will only give ₹1." What do you do? Do you return everyone's money, empty your hands, and recount from scratch? No. You already counted those other four guys. They aren't going anywhere or asking for their money back. You simply return the ₹2 to the guy leaving, take the ₹1 from his brother, and do the math: $26 - 2 + 1 = 25$. Humans do this. Banks do this. If you have ₹1 Lakh, you drink a cold drink for ₹100, and someone gives you ₹50, the bank doesn't empty your account and recount. It does $100,000 - 100 + 50$.

So why do unnecessary work? Let's trace it properly:
Array: `100, 200, 300, 400`.

- **First window** (`100, 200`): You have to calculate this manually because you have no reference. $S1 = 100 + 200 = 300$.
- **Next window** (`200, 300`): `100` goes home. `300` comes in.
  $S2 = S1 - 100 + 300 = 300 - 100 + 300 = 500$.
- **Next window** (`300, 400`): `200` goes home. `400` comes in.
  $S3 = S2 - 200 + 400 = 500 - 200 + 400 = 700$.

Now you see how you are doing less work in less time. This is the beauty of the sliding window. Otherwise, we could have extracted all subarrays and summed them individually. But we study patterns for this exact reason.

### Writing the Code (Fixed Window)

Now let's bring it down to computer language.
In a sliding window program, there are two pointers. A window needs a start and an end to be a segment, otherwise, it spills over. Different teachers use different names, but I use `low` and `high`. `low` is where it starts, `high` is where it ends.

When we start, we start from the beginning of the array. So `low = 0`. Since `K=2`, the window ends at index 1, so `high = 1`. This format shows that if the window size is `K`, your `high` will generally be at `K - 1`.

To get the first sum, write a simple `for` loop:

```cpp
for (int i = low; i <= high; i++) {
    sum = sum + array[i];
}

```

At this point, your sum registers `300`. `low = 0`, `high = 1`.

Now we have to slide the window. When do we stop sliding? As `low` and `high` increase, eventually `high` will step outside the array. Once `high` goes out of bounds, your program ends. So we use a `while` loop: `while (high < n)` (where `n` is array size).

Inside the `while` loop:

1. **Process Result:** Right now you are on the first window, and you know its sum. We need the maximum sum. So take a `res` variable and update it: `res = max(res, sum)`. Now your `res` has `300`.
2. **Slide the Window:** `low++` and `high++`. Automatically, your window slides one step forward.
3. **Update Data:** Now we need the sum of this new window. `low` moved forward, so the guy at `low - 1` went back to his village. Remove him: `sum = sum - array[low - 1]`.
4. **Boundary Check:** _Wait_, what if `high` was already at the last index and `high++` pushed it out of bounds? If you try to add `array[high]`, you'll get a segmentation fault. So check: `if (high == n) break;`. _(Self-correction: Actually, put this check condition and loop break logic properly to be perfectly safe, especially for edge cases like K=1)._ 5. **Add New Element:** `sum = sum + array[high]`. Now your sum is `500`.

The loop repeats. At the end, return `res`.

**Time Complexity:** $O(N)$ because you are traversing the array just once. The `while` loop runs `n` times, and the work inside (plus/minus) is independent of input size, so it's constant time.
**Space Complexity:** $O(1)$ because we used no extra input-dependent space.

You have learned the solution to the fixed window problem. Very good.

---

## Question 2: Variable Size Window

Go do the fixed one... or actually, watch both. If you understand these two questions, 70% of the sliding window pattern is finished, brother.

What is the next question? **Minimum Size Subarray Sum**.
You are given an array with positive integers, and you are given a `target` variable. You have to return the **minimum length of any subarray** whose sum is greater than or equal to the target.

Subarrays can be of any length—2, 3, 4, 5. If any subarray's sum is greater than or equal to the target, you have to return the length of that subarray. Find the minimum length among all such valid subarrays.

Is it an array question? Yes. Subarray or substring mentioned? Yes. Are we finding a combination (minimum length $\ge$ sum)? Yes. 80% chance it's a sliding window question. It's not graph, tree, DP, or greedy.

Step 1: Identify pattern. Done.
Step 2: Find Window Type.

This is where this question differs completely from the previous one. The previous was an Easy question; this is a Medium question. A whole level higher. This question is actually difficult for a beginner. If you only learned the previous question, you wouldn't be able to solve this. Why? Because this is a **Variable Size Window**.

How did I know? The question doesn't say "variable size." It also doesn't say "subarray of size K." Go check, I'm not lying. It just says "minimum length subarray." Whenever a question doesn't specify the size of the subarray, and the answer could be a window of length 2, 3, or 4, it is a variable size window.

Whenever you have a variable length window, you cannot set `low = 0` and `high` to something else (like $K-1$). Why? Because the smallest subarray is of length 1 (empty subarrays don't exist here). Therefore, in a variable window, you **always start with `low = 0` and `high = 0**`. Your starting window has a length of 1. Start small and then see what to do next.

### The Hiring and Firing Analogy

Let's think like a human again. Imagine a company, Amazon. Amazon needs to get a task done. You might have heard Amazon fired people a few days ago. Why? Amazon needs work done, so they hire a person. They don't know how many people it takes to do this job. One guy can't do it. They hire another. They keep hiring. The boss isn't paying attention, the HR just keeps hiring. Eventually, 6 people are hired.

Now, the work finally starts happening! Amazon could just say, "Okay, we need 6 people to do this work." But among those 6 people, some might be brilliant, and some might be fools. Maybe one guy can do the work of 3 people alone, and another guy does nothing but cause trouble. How will Amazon find out? They will only know if they start firing people!

Amazon has a policy: First in, First out. You have to fire in the same order you hired. You can't fire from the middle. Amazon thinks, "Work is happening with 6, but maybe it can be done with 5. Let's fire the first guy." They fire him. They check: is the work still happening? Yes! Now Amazon gets even greedier. "If it works with 5, maybe it works with 4. You, get out!" Now 4 are doing the work. "Okay, you get out too." Now 3 are doing the work. Work is still happening!

But the moment Amazon fires the next guy, leaving only 2 people, the work stops. Now it's stuck. And you can't re-hire the guys you just fired. What does Amazon do? Goes back to the college and hires a new person. Work still not happening? Hire another. Now work starts again! And Amazon sits back comfortably again. Now only 5 people are working instead of 6.

Do you see what's happening? This is a window. 6 people hired, then slowly fired until work stopped. Then hired again until work resumed. Then started firing again. This is exactly what we have to do. The same thing Amazon does.

### Tracing the Logic

Array: `1, 2, 4, 4`
Target: `4`

Forget `for` loops and `while` loops. Let's do it by hand.

- Currently, `low = 0`, `high = 0`. No one is in your company. Sum is `0`.
- Hire the first guy: `1`. Sum is `1`. Is `1` greater than or equal to `4`? No, work is not happening.
- Hire next: `2`. Sum is `1 + 2 = 3`. Is `3 >= 4`? No.
- Hire next: `4`. Sum is `3 + 4 = 7`. Yes! $7 \ge 4$. Work is happening!
- How many people did you hire? 3. So, even if the world falls apart, `3` is a possible answer. Note it down comfortably.
- Now what did Amazon do? As soon as work started, they started firing to see if one guy could do the whole job. Fire from the back (`low`).
- Fire `1`. Sum = $7 - 1 = 6$. Is $6 \ge 4$? Yes.
- Now your window size is 2. `2` is smaller than `3`, so update your answer to `2`.
- Fire `2`. Sum = $6 - 2 = 4$. Is $4 \ge 4$? Yes! That `4` alone was doing the whole job.
- Your window size is 1. Update your answer to `1`.
- Amazon is foolish, they fire him too. Fire `4`. Sum = $4 - 4 = 0$.
- Now work has stopped. What to do? Hire!
- Hire the last `4` from the array. Sum = `0 + 4 = 4`. Work is happening. Size is 1. Answer remains `1`.
- Fire `4`. Sum = 0. Work stopped.
- Try to hire... but the college is empty. The array is finished! Program ends.
- The smallest number noted down is `1`. Return `1`.

With the Amazon example, I don't think you need anything else to understand this. You start with nothing. You keep hiring until work gets done. Once work is getting done, note the number of people, and start firing from one end to minimize the count.

### Writing the Code (Variable Window)

Let's translate this to computer language.
`low = 0`, `high = 0`.
If no subarray is found, return `0`. For the result variable `res`, initialize it with `INT_MAX`.
Rule: Whenever you need to return the minimum of something in programming, start your result with `INT_MAX` (infinity). If you need the maximum, start with `INT_MIN` (-infinity). Because any valid value you find will be smaller than infinity, so it naturally overrides it.

The information is the sum. Currently, `sum = 0`.
Hiring means expanding the window to the right. Firing means shrinking the window from the left.

- **Hiring:** Add the new element to `sum`, which is dictated by `high`. (`sum += array[high]`, then `high++`).
- **Firing:** Subtract the old element from `sum`, dictated by `low`. (`sum -= array[low]`, then `low++`).

The code is a bit tricky and very beautiful.

```cpp
while (high < n) {
    // Hire the person at 'high'
    sum = sum + array[high];

    // Check if work is getting done
    while (sum >= target) {
        // Find how many people are working right now
        int length = high - low + 1;
        res = min(res, length);

        // Mass firing process: fire the person at 'low'
        sum = sum - array[low];
        low++;
    }

    // Go to the next person to hire
    high++;
}

```

What is happening here?

1. We bring `high` in and hire them (`sum = sum + array[high]`).
2. If the work is getting done (`while sum >= target`), we figure out how many guys are currently in the window. The formula for the length of a segment from `low` to `high` is `high - low + 1`. (E.g., indices 0 to 2 is $2 - 0 + 1 = 3$ elements).
3. Record the minimum length in `res`.
4. Then, fire the guy at `low` (`sum = sum - array[low]`) and increment `low` (`low++`).
5. This inner `while` loop keeps firing people until the sum drops below the target (work stops).
6. Once the inner loop breaks (work stopped), the outer loop increments `high` (`high++`) to hire the next guy from the array.

When the outer `while` loop finishes (`high == n`), your window breaks down, and you are done. Just return `res`. (If `res` is still `INT_MAX`, return `0` as per the problem requirements).

**Time Complexity:** Just like the previous question, it is $O(N)$. Even though there is a `while` inside a `while`, each element is processed (added to the window) at most once by `high`, and removed at most once by `low`.
**Space Complexity:** $O(1)$ space. This is the beauty of the sliding window.

---

## Conclusion

Two very important questions, very strong questions in my opinion, and I took a lot of time to explain both. Go submit the code. The links to my submissions are in the description. First, try to write the pseudo-code and code it yourself. If you don't understand, look at mine. But just looking at mine won't help much; you won't learn anything unless you try.

Two questions. Sliding window is completely wiped clean. We will pick up speed like this and keep studying. Maintain consistency every day and keep studying. If you have doubts, ask. I will try to reply. Alright?

3. Sliding Window Pattern: Questions

Transcript:
Yes brother, welcome. For the new kids here, we don't make you memorize questions. We teach you the DSA pattern. Pattern doesn't mean that star pattern, but the pattern or template to solve questions so you can solve any new question. And for the old kids, come on in.

Today is Day 3 of Sliding Window. You know you'll find the notes, question code, and links in the description. So, alright. The Sliding Window we are going to do today is a very important session because we will completely finish all possible questions of the variable size window from the roots. Right? Meaning, you'll start feeling that, 'okay, the same thing is happening in every question'. You just have to apply the same thing, tweak a line or two here and there, and the question will be solved. Understood? Right?

Sliding window is also very important because in any interview, there's a 50% probability that you will be asked sliding window. The probability of asking DP or Graphs isn't that high. Very few companies ask them. But almost every company will ask sliding window. If they have to ask a medium-level question, they will ask sliding window. Alright?

Today we are going to do three questions. Three. You guys were saying the speed isn't increasing. So come, let's increase the speed.

1. First is **Longest Substring with K Distinct Characters**. First is what? Longest Substring with K Distinct Characters. Right? You will find everything in the pattern sheet. Perfect.
2. Second is **Fruits into Baskets**. Fruits into Baskets.
3. And third is **No Repeat Substring** (Longest Substring Without Repeating Characters). Third is No Repeat Substring.

Don't panic looking at three questions. I will explain the first question so well that the remaining two you will be able to solve yourselves, or you should be able to. I have that much faith. Alright?

---

## Recap: Fixed Size Window

What we discussed yesterday—those who haven't watched yesterday's lecture, please watch it, or at least watch a little bit of it. What all did we discuss yesterday? Yesterday we solved two questions. One was of Fixed Size Window and one was of Variable Size Window. Right? I told you four steps for the sliding window. Everyone must remember those four steps and what is done in them. The most important step was this one: is it fixed or variable? Understood? Okay.

For fixed, there is a set pattern, a set template. What is it? Let me quickly revise it again.

- In fixed, what do we do? We keep **`low = 0`**. **`high =`** whatever window size is given to you. If $K$ is given, we keep it at $K - 1$. If 2 is given, keep it at 1. If 3 is given, keep it at 2.
- What did we do after that? After that, we kept running `high`. From where to where did `high` run? From wherever it is up to $n$.
- After this, we did some work with the result. That could be any work.
- After that, what did we do? We incremented `low` and removed `low` from the result. We removed `low` from the result.
- After this, what did we do? We incremented `high`. We checked once if `high` hasn't gone out of $n$. If it hasn't gone out, what did we do? In the result, whatever your result could be—sum, frequency, average—we added `high` to it. We did exactly this.

Doing this, we used to get the answer. So it's very simple. Whatever question comes for fixed, you have to do just this.

---

## Variable Size Window Template

Variable gets a little bit difficult. Why does variable get difficult? First of all, it gets difficult to understand _how_ to do it, and its time complexity—there were many comments saying you didn't explain time complexity, I will explain it.

What to do in variable? First of all, how will you understand that it is a variable window? Whenever you are not given any size $K$. Whenever no size $K$ is given—it isn't said that the size of the subarray should be this much or the size of the substring should be this much. It's just said to find any subarray, find the longest, find the shortest, find this and that—then it is variable. This is a very simple thing. Right?

Now, if it is variable, we can't do that thing where we keep `low` at 0 and `high` at $K - 1$ because $K$ is not given at all. So what do we do in this? We keep `low` at 0. We also keep `high` at 0. This much was discussed yesterday itself, you guys might remember. After that... after that, we keep increasing `high`. After that, what do we do? We keep increasing `high` and then we also keep shrinking `low`. I will explain all this. If it's going over your head, don't worry. We keep shrinking it.

Yesterday I made a mistake where I used a `while` loop to increment `high`. A `while` loop shouldn't be used. A `while` loop won't strike you that much right now. Today I will explain with a `for` loop. And the pattern I will tell you today, that same template will be applied in every similar question. Any longest substring, longest subarray, the same pattern will keep applying. Right?

Look at what we do in this. Let's understand the template from the beginning. What do we do in this? Where is your `high`? Your `high` is at 0. Right? What do we do? For `high =` ... I am explaining for any question. The question hasn't even started yet. I haven't even read the question. I'm explaining. `i = 0`, `high < n` (your string size or array size), and `high++`. Right? Now the need for the `while` loop is completely gone. A `for` loop is running.

**Step 1:** The first thing to do in any similar question where you have to find the longest substring or longest array which has $K$ distinct or exactly $K$, whatever it is: First of all, right now where your `high` is, you have to include it in your result/information. Result means what information that window is giving you. It could be giving a sum, it could be giving a frequency, it could be giving an average, it could be giving anything. Whatever information you have of that window, you have to include `high` in it. What does include mean? If it is a sum, add `array[high]` to it. If it is an average, add `array[high]` and divide. If it is a frequency, take a hash map and do `++` for `high` in it. Do you guys understand? You have to include `high` in the information. Good.

**Step 2:** Now, a very important step. A very important step. Once `high` is included. Right? Now you will be given some condition that if this information is like this, then we want this. If this information is not like this, then we don't want this. Something must be given, right? That the current substring you have should have exactly $K$ distinct elements in it, or it should have less than $K$ distinct elements, or more than $K$. Some condition must be given that if the information is of this type, then we want it in the answer. Right? So two things can happen: either your information is of that type, it is perfect, meaning you want to take this window. Or, your information is not of that type. Only two cases can happen.

So here comes the most important step. I am drawing a box right now, I will tell you guys what to do in it. As soon as you guys included `high`, it might happen that the information got something that you don't want. So here, **until the information is wrong**. It is wrong. What is the sense of wrong? That either it has exceeded it or it has become less. It is wrong. Basically, for example, you are told to find such a window whose sum is 10. Right? It could happen that as soon as you included this `high`, your sum became 11 or your sum became 9. Anything can happen. So it's wrong, right? So as long as it's wrong—why did this happen? You increased `high` once, so this happened. Now we will fix it. Here we have to fix it. How will we fix it?

Look, in any variable window, in such a question, once `high` is set, `high` will only increase through this `for` loop. You shouldn't mess around with `high` in 90% of the cases. Where can you mess around? Why is it called a variable size window? Because it is variable. It keeps increasing and decreasing. When `high` increases, this variable increases. The window increases. And to reduce the window, we bring `low` from behind. This is what happens, right? Your `high` keeps increasing here. And as soon as we want to reduce the window, we start decreasing `low` from here. We have to do the exact same thing. You have to fix this. How will you fix it? By **shrinking `low**`. Shrink meaning decreasing it.

Along with decreasing, what will we do? First of all, remove `low` from your information. The same thing happened in fixed size. If you have a sum, subtract `array[low]` from that sum, and increment `low`. And this work, how many times do you have to do this work? Not once or twice. You have to keep doing this work. You have to keep doing it in a loop. Until when do you have to keep doing it? Until your information becomes correct. Now 'correct' can have many meanings from question to question, we will read this further. But the general rule is this: until your information becomes correct, you have to keep doing this work. You have to keep incrementing `low` and you also have to keep removing `low`. Meaning you are making the window smaller. Your `high` is increasing. `high` stopped at one place. Then you are bringing `low` slowly, slowly, slowly closer. Until the information becomes correct. Right? Good.

**Step 3:** Now, once you have done it. Now what does doing this mean? That now your information must have become correct. Right? Look, it is not this simple. It is not as simple as I am telling you. Question by question, a line or two changes. But the thinking is this. The logic is this. Now your information must have become correct. Now here, you have to calculate the length. How do we do length? `high - low + 1`. And include this length in your result. Min or max whatever is asked of you, longest is asked, shortest is asked, whatever is asked. So, suppose longest is asked, then what will we do? `max(result, length)`. And we will close this `for` loop here. Which `for` loop? The `high` one. We will close the `high` `for` loop here.

So this is a general pattern of the Variable Size Sliding Window. Whenever you have such a question like longest substring must have $K$ in it, it should have at most $K$, it should have at least $K$, exactly $K$, anything. Take a look at this once. This is the general format. What is the format? Let me read it once again.

1. Keep increasing `high` from 0 to $n$. `++high`. Your `high` will keep increasing with the `for` loop.
2. First of all, include `high` in the information.
3. As long as your information is wrong, keep moving that `low` forward (shrink).
4. Once your information becomes correct, write it in your result, close the `for` loop, and return the result.

Remember this. Write this down in your notebook. Write this down right now. Wrote it in the notebook? Good. Now come on. Right? Now let's come to its questions. Time complexity, we will do a question once and I will explain it. Right?

---

## Question 1: Longest Substring with K Distinct Characters

What does it mean? What is given in the question? You are given a string. Okay. There are some characters in the string. All are lowercase characters. Okay, good. And you are given a $K$. $K$ is an integer. Right? What do we have to find? Longest substring. What should be in it? In this, **exactly $K$ distinct** (meaning unique) alphabets. What is the complete question? A string is given. Find the longest substring in the string which has $K$ distinct characters. Meaning $K$ unique characters. Understood?

Let's follow the sliding window steps one by one.

- **Step 1: Will the sliding window pattern apply or not?** Is this an array or string question? Yes, it's a string question. Is "longest substring or subarray" written anywhere in it? Yes. Is "exactly $K$" or "less than $K$" or "at most $K$" written anywhere? Yes. What is written? "Exactly $K$". If anyone is wondering where this came from, this was in Day 1's flowchart. Before starting any pattern, keep its flowchart handy. That's how you know it's a sliding window. All three hit here. So this is a 90% sliding window question. Okay, why do I say 90% and not 100%? It might happen that some questions look like sliding window but there's an off chance it's not. It might be Greedy. It might be DP. So how should you approach it in an interview? You should start with sliding window. Right? Because you study 20-30 types of algorithms, you don't know where to start. Maybe you started with binary search, wasted 15 minutes on it, then realized, 'oh, this wasn't binary search'. So this increases your probability of choosing the right algorithm. First step is done.
- **Step 2: Is it fixed or variable?** Is it given anywhere in the question that the substring's length should be this much? No. The question told you 'longest substring', its length can be anything. Whenever it comes up that its length can be anything, then blindly assume that this is a variable question. In fixed, you will always be told to find a subarray of size $K$. Right? So it's understood that it is variable.
- **Step 3: Information.** What is its information? What do you understand by looking at that substring? In this, you were given 'K distinct characters' in the question. Whatever window you have, it will have some characters. Suppose this is your substring or window, where your `low` is here and `high` is here. You have been told that if there are $K$ distinct characters in it, then it is correct, otherwise it is wrong. Meaning it could happen that here is A, A, B, B, and C. How many distinct characters are in this? One is A, one is B, one is C. There are three. So what is the information of this window? How many unique characters are in it. How will we calculate this? We will calculate this with a hash map. If you keep a hash map, and whenever you go to any character, increase its frequency. So if you cover this entire window, your hash map will look like this: A's frequency would be 2. B's frequency would be 2. C's would be 1. The total characters in this are five. But what is the size of the hash map? The size is three. Understood? What is a hash map? Characters and their frequency. So there will only be three unique elements in the hash map. This is how you can find the information. Very good.
- **Step 4: Updating Information.** When you move the window, how will you change this information? Will you iterate from `low` to `high` repeatedly to find out? No. If `high` moves, we just do `++` for the `string[high]` one. Meaning wherever `high` moves, we will add its frequency. To shrink `low`, what will we do? We will do `--` and we will do `low++`. Simple.

There is one confusion in this. Suppose your array was like this, this is your current hash map. A is 1, B is 2, C is 2. Your `low` is pointing to A. Now you have to remove A. In a hash map, you will decrease its frequency. If you decrease its frequency, it will become zero. Now, in a hash map, in any language, if you make it zero, it doesn't get removed from the hash map. Pay attention. This A is still in the hash map. Only its frequency has become zero. If someone asks how many characters are unique? You were saying that whatever the size of my hash map is, that many characters are unique. But A's frequency is zero. What is this hash map telling us? That we have such a window in which A is not there even once, B is there twice, C is there twice. So should its size be three? Its size should be two. Because A is zero. For this thing, after this, we will have to check: `if (f[s[low]] == 0) then f.erase()`. This is C++ syntax. In Java/Python, how to remove from a hash map? Check that. What does this mean? That if any character's frequency becomes zero, there's no point in keeping it in the hash map. It will be wrong. Remove it. Erase it. So this is a small step. People don't explain it, they go into the code and you see, 'oh, this `f.erase` is written, why is this written?' It's written because it became zero, remove it. Okay?

Now watch carefully. The template we learned above. How to use it.
First of all, keep `low` as 0, `high` as 0. Let's create an input array: A, A, B. 0 1 2 3 4 5, this is your string. Your $K$ is 2. First thing is to run a `for` loop. `for (i = 0; i < n)`.

1. **Include `high` in your information.** So where is our information stored? In the hash map. `f[s[high]]++`. Right now there's nothing in your hash map, right? Right now your character is A. A is not in the hash map. But when you do this work, if it's not there, it inserts it, and starting from zero, it makes it one. Now your hash map has A, 1.
2. **Is my information correct?** What does 'information being correct' mean? What is written in your question? "Which has exactly K characters". $K$ unique characters. Your window's length can be anything. But the unique characters in it should only be $K$. Meaning even if A is repeating 100 times, it will be counted as one. How did we learn this? The size of the hash map. If the hash map's size becomes exactly $K$, then it will be correct. Right now what is the hash map's size? One. What does this tell us? That there is only one distinct character in my window.

The information can either be correct or it can be wrong. The correct one has one case: `f.size() == K`. What is wrong? Wrong is either `f.size() > K` or `f.size() < K`. Only these three types of cases can exist.

Now what I said, that as long as the information is wrong, you shrink the window. That doesn't happen in every case. Look at this case. Right now your `f.size()` is less than $K$. Your hash map's size is 1. The length of $K$ is 2. So this is wrong information. So in this case too, should we shrink? No. Why? Shrinking the window means you bring `low` towards `high`. When you come making the window smaller, you will keep kicking them out of the hash map one by one. So meaning if `f.size()` is less than $K$, if we shrink `low`, then `f.size()` will decrease or remain the same. It won't increase. Listen very carefully. This is exactly what people don't understand. If we are shrinking `low`, the hash map's size will either remain the same, or its size itself will decrease. So you see, when your `f.size()` is already less than $K$, then why do you need to increase `low` so that it becomes even less? We don't want less. We want exactly.

Therefore, if `f.size()` is already less than $K$, then there is no use in shrinking it. By increasing `high`, `f.size()` increases. And by shrinking `low`, its size decreases. So whenever your `f.size()` is less than $K$, there is no benefit in shrinking `low`. Right now you need to increase `high`. You have to go to 2, you are sitting at 1, will you decrease it further and bring it to 0? No, you will increase it. Therefore there is no need to handle this case in the `low` part. If `f.size()` is less than $K$, you need to increase `high`.

But now look, what if `f.size()` is greater than $K$? This can also happen. Now you had to go to 2. Now you are sitting at 3. Will you increase `high`? No. Then you will go to 4. In this, you have to decrease `low` (increase the `low` pointer). Why? Because when `low` increases, the hash map's size slowly decreases. So that `low` part will definitely be there, but under what condition it will happen, you have to decide. When we have exceeded $K$, we have to decrease a bit to come back to $K$. There is only one way to decrease: increase `low`. If we increase `low`, the size will decrease, and if we increase `high`, the size will increase.

So when information is greater than $K$, we make it shrink. `while (f.size() > K)`. As long as `f.size()` is greater than $K$, keep decreasing `low`. What is the way to decrease `low`? First of all, `s[low]--`, it got removed. After that, `if (f[s[low]] == 0)`. It might happen that while decreasing someone, its frequency becomes zero. If this happens, blow it away. Erase it from the hash map, only then the size will decrease. If you don't do this, your size will never decrease. Work done. Blew `low` away. Now increment `low`. `low++` and close this `while` loop. This is fixing it. As long as the information is wrong (more), keep incrementing `low`.

Now this is very important. When this `while` loop breaks, when will it break? Either `f.size()` becomes equal to $K$, then it will break. Or `f.size()` was never greater than $K$. It was always smaller. So you never even ran this. So when you break this `while` loop and come here, there can be two types of cases. `f.size()` could be equal to $K$ or less than $K$. What was in the template? That if the information is correct, add it to the result. Which one do you want? You want the one equal to $K$. "Exactly K" is written. So put an `if`. `if (f.size() == K)`. Then include this in your final answer. `high - low + 1`. And `res = max(len, res)`. Close this `if`. This `for` loop is closed. And come down and `return res`. Simple.

Look what happened here? Three steps.

1. Include `high` in the information.
2. As long as it is wrong (greater), decrease `low`.
3. And the information that is correct, include it in the result.

It's a three-step process for any sliding window. This code is done. What is its time complexity? Many people were saying its time complexity is $O(n^2)$. Because a `while` loop is inside a `for` loop, so $n \times n = n^2$? No. Look, till where is the `high` loop running? `high` is running from 0 to $n$. Every time `high` runs, what happens? You are either increasing `low` or doing nothing. If `f.size()` is greater than $K$, only then are you messing with `low`. Otherwise you are not touching `low`. It becomes $n^2$ when `i` runs from 0 to $n$ and for every `i`, `j` also runs from 0 to $n$. But look what is happening here? `low` will go and stop till `high` or it will stop before `high`. It won't happen that `low` crosses `high`. So your `low` is going up to `high` or stopping before `high`. Is it happening that for every `high`, `low` is running from 0 to $n$? No. It is never happening that for every `high` of mine, I am doing $n$ operations for `low`. Generally speaking, your `high` will go from 0 to $n$. In the worst case, your `low`, that too will reach from 0 to $n$ while walking. So its time complexity is not $n \times n$. It is $n + n$. In total, `high` is going from 0 to $n$ and `low` is going from 0 to $n$ slowly in between that. Therefore its complexity is $O(n)$. It is not $O(n^2)$. Right?

So this is your first question, finished.

---

## Question 2: Fruits into Baskets

Come to the next question. Fruits into Baskets. Look how simply I will explain it to you. The question will be finished in 10 minutes. It won't even take 10 minutes.

Now in this question, no substring or subarray is written for you. This is a real-world question. Meaning a story is told to you. And this was asked in front of me in an Amazon interview a few days ago to some kid. Right? So it's very important.

It is said that you have a farm where fruit trees are arranged left to right. This is your farm. 0 1 2 3 4 this is your array. There are fruits kept in this. There is a type of fruits like mango, orange, whatever, so they represent it with numbers. So your fruits are this: 0, 1, 2, and suppose 0. This is your fruit type. You have a basket. You have to collect fruits from left to right. There is a limitation to this basket, that you can only fit **at most two distinct types** in it. Now you have to tell what is the maximum number of fruits you can collect?

The question is the same as the previous question. What is the question saying? You have to take fruits from left to right. Meaning you cannot take one fruit and go and take the fourth one. You have to walk in a line. How many fruits can you take in a line such that the distinct fruits in it are two or less than two? Less than two will also work. It shouldn't be more than two. Either it is one or it is two. If you take this window 0 and 1. What is the number of distinct fruits in this? Two. What is the number of fruits? 2. If you take the next one, the number of distinct fruits is one and two. But in this you get three fruits. So its answer will be three.

I will write the question in sliding window terms: **Find the longest subarray which has at most two distinct numbers**. Here you go, your question has become a sliding window question. It's the same question, right?

Now this has become the same question as the previous one. There is one twist. I will not explain steps and all in this. It is variable because no such length is given for the window. It is said, pick up as much as you want to pick up. The distinct in it should be at most two. So there's one difference: 'at most two' is written here. What was in the previous one? 'Exactly $K$'. The $K$ that was there is the 2 here. This is it. Instead of exactly $K$, at most is written.

Recall the exact same previous code. Everything will run the same. When you reduced `low` and came here. When did you reduce it? `f.size() > K` this is what you did, because what do you have to do? You have to go up to at most $K$. So meaning when will your information be correct? Either it is less than $K$ or it is equal to $K$. If it is greater than $K$, then you decreased `low`.

Now last time, which information was correct? Last time, exactly equal was correct. That is why we calculated this one by putting an `if`. This time, both information are correct. This time, this is an even simpler question. This question should have been done first. What does at most $K$ mean? Less than $K$ or equal to $K$. Not more. So there is no need for any `if` in this. Make it simple. Just do `high - low + 1`. Do `res = max(res, len)`. Close the `for` loop. `return res`. Program finished.

Same program, the hash map that you will make, last time we were writing character frequency, this time it is an integer number, so we will write integer to integer. Everything else will run the same line by line. Here instead of string, an array is given. And instead of exactly, at most $K$ is given. So it's even better, our code became smaller. We didn't need to put that `if`. The rest of the code is exactly the same. You try it and see. Its time complexity and space complexity is also exactly the same, $O(n)$ time and $O(1)$ space. Look how easily this question was solved. Meaning a question that can be solved instantly.

---

## Question 3: Longest Substring Without Repeating Characters

Now let's come to the third question. Consider the third question also 70% the same. What is the third question? Longest Substring **Without** Duplicate Characters. Look how easy I will make it. You guys will be able to do this too.

String is given. Okay, in the string you have to find the longest substring. Very good. What is the condition? The condition for the last two times was something related to $K$. There is no $K$ in its condition. What is written in this? Without duplicate characters. Meaning whatever substring you take, all characters in it should be unique.

So this is stuck. I keep saying that this question is in the same format, but there is no $K$ in this. So if there is no $K$, the whole logic will get messed up. Okay. Now think a little bit. Open your mind a little bit in this. A B C A B, suppose that's yours. In this window, how many distinct characters are in this window? 3. Okay let's make another one. How many distinct characters are in this window? There are only two in this. A and B are there. A is not there. But how is this known? We found out by looking. Okay how do we know that all are distinct or are some duplicate too?

Suppose your question is a very simple question. This is your array: A A B C. You are told to tell if everything in this is unique or not? How will you tell? One way could be that you go from beginning to end and keep making a hash map. Then you can see that if anyone's frequency is more than one then it is a duplicate. Okay. Is there any other way?

Look, suppose you have a hash map of this array. I don't feel like traversing the entire hash map. What is the size of the array? The size of the array is 4. What is the size of the map? The map's size is 3. Why is the hash map's size 3 and not 4? Because the element repeated. The hash map's size always gives us the number of unique characters. So if someone asks you if every character in the whole array is unique or not? There is only one test for this: that if the hash map's size is equal to the array's size, then mine is unique. If this is less, then it is not unique. Did you understand or not? You must have understood. If anyone has repeated, then it is natural that the hash map's size will be less than the array's size, so it's not unique. So there you go, found out. We didn't need $K$.

Now look, I will tell you where and how the need for $K$ will not arise. Come to the same template. Write `low = 0`. Write `i = 0`. Write `res = INT_MIN`. `for (i = 0; i < n; i++)`.

1. **Add information.** Add `high`'s information. Added `f[s[high]]++`, it's added.
2. **Is the information correct or wrong?** If it is wrong, then shrink `low`. But now look, how will we know if it is correct or wrong? There is no $K$. But what did we just see? That if the hash map's size is less than the size of that window, then it does not have unique ones, so it is wrong. Okay. Which window's size is in the hash map? From `low` to `high`. So what is the size of that window whose information is in the hash map? You guys know how to calculate its size, right? Let's take this. Make this $K$. `int k = high - low + 1`. This is the size, right? This is where we will find out if everything in this window is a duplicate or not. $K$ is known.

Now look. The information can be wrong, it can be correct. How can it be correct? It can be correct if `f.size() == K`. This is good information. `f.size() < K` is wrong. Can it ever happen that `f.size() > K`? Think about it. What is $K$? $K$ is the size of this window. This is never possible. Why? What is in the hash map? It is the frequency of whatever characters are in that window. So suppose there are only five characters in the window. Can there be 6 characters in the hash map? It can never be. When there are 5 characters, from where will the 6th one come in the hash map? So this is a useless thing. We don't even have to think about this.

Okay. This is correct. This is wrong. Now we saw that in the wrong one, we shrink `low`. Now in the previous question, we were shrinking `low` in the _greater_ case, that when `low` increases, the hash map's size decreases. So here it is already _less_. So should we shrink `low` because it will become even less? Yes, we should shrink, and this is the twist in the question. Don't memorize that we do it in 'greater' and not in 'less'. It can happen in every one.

Look, what is $K$? In the previous question, $K$ was a fixed value. So when your hash map's size was 1, we didn't increase `low` because 1 would decrease further to 0. But here $K$ is not given. What is $K$? Your window's size. `high - low + 1`. So what does it mean? Suppose your `f`'s size is less right now (2), and your `high - low + 1` is 3. So when we increase `low`, your `f`'s size will either remain the same or it will decrease. But, when you increase `low`, the size of $K$ will also decrease. Why? `high - low + 1` is the size of $K$. When you are increasing the size of `low`, the window's size is also decreasing, right? So when you are increasing `low`, $K$ is definitely decreasing. It will never remain the same. That is why it could happen that suppose right now `f`'s size is 3 and the window's size is 4. Now you decreased it by one, so suppose `f`'s size became 2 and $K$ became 3. You decreased it by one more, so it might happen that $f$'s size remains 2, but $K$ becomes 2. Now look, these two matched! This is your correct one.

That is why here, when `f`'s size is less than $K$, then `low` should be shrunk. Because it might happen that at some point both meet. Think logically whether there could be any benefit from increasing `low` or not. If $K$ is fixed, then there is never a benefit. Here what is changing? That `f`'s size is either staying the same or decreasing. $K$'s size will continuously decrease when we bring `low`. So it might happen that at some point both meet and that is what we want.

So come on. Write the code ahead. `while (f.size() < K)`. As long as it is less, keep doing it.
First of all, what should we do? Do `f[s[low]]--`. And `if (f[s[low]] == 0)`, erase it brother. Reduce the size. And do `low++`. We have been doing this much since last time too. But now look here. In the previous question, $K$ was fixed. Here $K$ is `high - low + 1`. So when you are increasing `low` here, you will have to calculate this $K$ again. You cannot do the previous $K$. That is why you will have to calculate `high - low + 1` here again. And this `while` loop is closed here. So a one-line change was added. What was added? We are calculating the value of $K$.

Now when will this `while` break? Only two cases were possible. Either it was less or it was equal. For the less one, we put on the `while`—as long as there is mischief in this, keep reducing. Meaning it has come out here. Coming here means what? It is equal. That's why we came. Just, now what you do here, your information is correct, so do `high - low + 1` and `res = max(res, len)`. Just do `return res`, game over. Game over.

Look what changed in this. Almost nothing changed. This $K$ changed. How we were knowing if our information is correct or wrong, that changed. $K$ used to be given before. Now $K$ is not given, so calculated $K$. Based on that, the decision in shrinking changed slightly. Before it was more, so we were shrinking. Now it is less, so we are shrinking. Never memorize that shrinking happens in 'more', doesn't happen in 'less'. Think logically whether it can happen or not.

Same $O(n)$ time. $O(1)$ space. Why is it $O(1)$ space? Because we are using a hash map, right. You might think why $O(1)$? But what can be the maximum size of the hash map? 26 because it is given that it is lowercase characters. So at maximum your hash map will start looking till Z and its maximum size will be 26. We consider this constant only. That is why it is $O(1)$.

So this is today's third question. You will find the code link in the description. Go and submit all three questions, and from now on we are trying to pick up a little speed. So you guys should also increase your speed a bit now. Right? See you tomorrow and stay consistent.

4. Sliding Window Pattern: Questions

Transcript:

## Addressing the Recent Video & Comments

Today is the last day of the sliding window pattern. After this, the sliding window will end. But before that, listen to something important. It will take two minutes. I posted a video 30 minutes ago. That wasn't a DSA lecture. It was a different type of video. Different doesn't mean I was dancing in it. But it was somewhat about how you should study and why you guys are wasting time topic-wise, whatever it was. You guys can go and watch it. There was nothing wrong with it.

Now, what happened with that video? Two things happened. First, that video got a ton of views. I will show you a screenshot if I have one. It's "1 out of 10," meaning out of 10 videos, that one is performing the best. It got a lot of comments saying, "Hey brother, you promised DSA videos, what is all this you are doing? Post DSA videos every day. Don't make these kinds of videos." Which is a good thing because I said in the previous video that you can comment whatever you feel like.

But where does the problem arise? It is necessary to say all this because maybe you guys are kids and you don't understand. There is a guy named Arvind Yadav. You guys can look at his comment. The comment must still be there. His comment was, _"Hey, teach DSA, what are you babbling about?"_ If you guys start commenting like this—"What are you babbling about? Teach DSA"—then look, whatever I teach you guys, you have to have some trust that if I said I will teach, I will teach. Now, I do post study content on the channel. Besides that, whatever other videos I post, it's my channel, right? I might feel like dancing. I might feel like singing, so I post it. Study videos are coming.

Now, if the next day you guys start saying things like, _"Hey, teach DSA man. What are you babbling about? What is this nonsense?"_ nothing will happen from these comments. What will happen from these comments is that I don't teach by writing a script. I don't have a script in front of me that I just speak from here. Whenever I teach, I look at the question and teach whatever comes to mind, and you guys say that I teach well. So, making such comments will only create a bit of irritation in my mind. I mean, don't be thankless. Do you know the meaning of thankless? In Hindi, it's called _'Kritaghn'_. Being thankless means acting like, "I don't care at all. I should only get what I want. Otherwise, everything is wrong." Don't make such comments.

And there are very few kids who make such comments. I mean, the majority of people's comments... if you are commenting, _"Brother, please post DSA, what are you doing?"_ that is a very good comment. I have never said anything against it, nor will I. But when you post a comment like, _"Hey, what are you babbling man,"_ kids like this are very few. So that's a good thing. But I don't like kids like this. Now, this is a public channel, so I can't tell you not to watch my video. But if this were my home or my private batch, I would say, "Leave. I don't need you."

And Arvind Yadav ji's entire comment history comes up, right? In YouTube Studio, you get to know what all they have commented so far. Ironically, the four comments he has made so far are all on these types of videos—where something other than lectures is being discussed. He likes to comment on these. But he doesn't have a single comment on any lecture saying, "I studied today," or "I have a doubt in this," or "I understood this," or "I didn't understand this." He has no comment on those. It means he is only watching these kinds of videos and commenting on them saying don't make such videos. This person is not watching the DSA videos. So when you are not even watching that, and you are only watching the 'Gyan' (advice) videos, then 'Gyan' videos will be made. You can comment on that, but keep it a bit respectful. Right?

Nobody loses anything in this. I don't lose anything either. You also... I mean, I don't know you, and you don't know me. So nothing is lost. I definitely don't lose anything. It's a good thing. So it was just a small thing. Keep it in mind a little that it is online, okay? You might feel that you can say anything or write anything online and nobody can do anything. It's true, nobody will do anything, but it doesn't feel good, right? So be a bit mindful. What will happen from this is that the more you irritate me, my teaching quality will keep going down, right? Anyway, enough of this advice and preaching. Even now, many kids will only watch this much, just three minutes, and then they will comment, _"Hey, you are giving advice again, teach DSA."_ So have some patience; your age is like that right now, but it's okay.

---

## Today's Problems

Today, the two questions we are going to do are very, very important questions. My sincere request to you is that when I solve one question, just pause the video right there. Try to do the second question yourself. Like what happened yesterday? Yesterday we did three questions. 80% of the comments said, _"Brother, you did one. We studied one from you, and we were able to do the second and third questions ourselves."_ This is what I want: that you study one question. It's a good thing. It's a new concept; you should study it. But the second, third, and fourth which are the same questions—where you have to change one line, or two lines—do that yourself.

We will do the same today. We are doing two questions today. I will explain the first question to you because it is a slightly new question. The probability of you doing it yourself is very low. But the second question—if you do the first one, then the second one is equivalent to the most basic question for you. You should do the second question yourself. I will teach that too, but try to do it yourself, okay?

The two questions we are going to do today are:

- **Longest Substring with Same Letters After Replacement**
- **Longest Subarray with Ones After Replacement**

The pattern sheet is in the description, go and check it out. Row number 29 and 30 in the Sliding Window pattern. I am going to cover this.

---

## Longest Substring with Same Letters After Replacement

Alright, now let's come to our question. _Longest Substring with Same Letters After Replacement_. Hearing the question itself sounds very dangerous, but it is not that dangerous. If it is a little dangerous, then open your ears and listen carefully, open your notebooks, keep your eyes and ears open, and listen carefully.

What are you told? That you have a string. Okay. And an integer **K**. Very good. Now, what does this question say in plain terms? Read the question. What does it say? That you can choose any character in this string and make it any other character. Meaning, you can change it as you wish. Meaning, if it is **A**, you can make it **B**, you can make it **C**, **D**, anything. You can make it any character. Very good.

But, but, but... this operation, this changing operation, you can only do it **K** times. K times. This is the twist here. Meaning, if K is two, then you can swap two characters in the string. Meaning, if there is an A here, and a B here, you can make this C. You can make this D. You can do it twice. Okay? Or not more than two, meaning whatever K is, you can do it that many times. Okay? So this is the premise of the question.

What do you have to do in the question? You have to find the length. Whose length do you have to find? Not mine. You have to find the length of the longest substring. Okay? Containing same letters. Meaning, same letters provided what? Provided you are doing this operation. Understand the question again. Look, the question is complex. This question is not a traditional question where you look at it and it just clicks how to do it. That's why this is a hard question. It's also written as "Hard" on the sheet.

What is it saying? If this is your string, there will be characters in the string. You have to find the longest substring anywhere in the string which has the same letters. And to make it the same, you can use this change facility that is given. Using it K times, the largest substring that can be formed is what you have to return. Okay?

Meaning, suppose it is `ABC`, like this, `ABA` suppose it is like this, okay, and here it is `CDE`. You are told that you can change one letter. So logically speaking, from what you see, if we make this **A**, then look, this substring, all of them are A. There is one B in it, but we are told that you can change it. You can make B into A. How many times? Once. Can you make this one A too? No. Not together, you have to make only one, right? So either change B or change this one. If you make this A, make this A, then you will have to take this substring whose length will be two. But the length of this substring is three. You have to return three. This is the question.

---

## The Sliding Window Flowchart

Alright, first things first, what we always do: keep the pattern, flowchart all ready in your mind. Whose question is this? What do you have to do in this? I mean, I've never even heard of such a question where you have to flip it and can only do it K times. But is this a string question? Array or string, whatever it is. A string is also a kind of array. Whenever I say string, you have to understand it as an array. Yes.

1. **Do you have to find any window or substring in it?** Yes. You have to find a substring.
2. **Do you have to find the longest substring?** Yes.
3. **Is there any condition given for the longest substring?** Yes. What is the condition? That whatever letter is in the substring, either it should be the same initially, or even if it is different, you can make it the same by changing it K times.

So this is our question. For those who don't remember the flowchart, please watch the previous videos. Those who know the flowchart must have realized that this is a sliding window question. Okay? This is the easy part. This is easy for you guys now that it's a sliding window question.

How many steps did I tell you in the sliding window? There were four steps.

- **Step 1:** Is it a sliding window question or not? Yes, it is, so very good.
- **Step 2:** Is it fixed or variable? Is it written anywhere in the question that the substring you will find must be exactly of length three or four? No. It said "longest substring," brother. Expand it as much as you want. The condition is just this. Whenever it is like this, it is variable. Very good.
- **Step 3:** Information. What is the information of whatever window from low to high you make? What do you have to check in it? You have to check whether all the characters are the same or not. So its information can be extracted if we keep the frequency of the characters in a hash map. What do you have to check? That everything is A in this substring. Now how will everything be A? Remember last time, its length is four and the frequency of A is four. So if the size of this hash map is one, it means there is only one element. If the size of this hash map were two, it means there are two elements. Three means three unique elements. This can also be interpreted as there should be one unique element. A is uniquely one and A comes any number of times, then this is correct.
- **Step 4:** How will the information move forward? Same, `low` will be removed and the `high` one will be taken. When we remove `low`, if any frequency becomes zero, then it will be erased. This is identical to the previous question. No need to do much fuss in this. You guys understood this.

---

## Core Logic and Templates

Now comes the most important part of the question. There is a template for the sliding window variable. Does everyone remember the template? If you don't remember, please go and watch. What is the template? `low = 0`. `high = 0`. Result equal to, if it is longest then it is `INT_MIN`. If it were shortest then it would have been `INT_MAX`. Very good.

First of all, what happens? A loop runs. Okay, from where to where does the loop run? And whose loop runs? It runs for `high`. We increment `high` in the loop. Look, 70-80% of the template will remain the same. I am saying it again and again, watch the template videos from the beginning. If you miss one video, it won't be fun. We are doing the same template question by question.

What was after that? First take `high`'s information. You are incrementing `high`, right? First take `high` inside. Whatever character is at `high`, we increased its frequency. Very good.

Now what was the part? As long as this information is wrong, keep incrementing `low` and shrink the window. This is what we have been doing since yesterday. Look, the whole game is in this box. Top and bottom will remain the same. The box changes a little bit. As long as the information is wrong, keep incrementing `low`. And after coming here, when you have incremented `low`, check here. If the information became correct, then find the length. How will we find the length? `high - low + 1`, and update the length with your result. We have been seeing this exact thing since yesterday. The whole game is in these two boxes. The rest before and after remains the same.

Now look at what the question is trying to tell you. Let's go. `a A B A B B A N`. It stopped, man, today my hand doesn't feel like teaching at all. Okay. `a A B A`, this is an example. `0 1 2 3 4 5 6`, this is given to you. The value of K is given as 1. Very good.

Suppose there was no K. Suppose the question didn't mention K. It said find a substring in which all the letters are the same. If K was not given, then it was a very easy question—that the size of the hash map should be one. True. If the size of the hash map is not one, it has become more than one, then it is wrong. If it is more than one, then keep incrementing `low` until the size of the hash map becomes one. As soon as it becomes one, write it down.

But now you are given a K, saying that you can modify any one element. Now don't think like a computer. Think like a human. Think like who? Like a human. Suppose you are currently on this window. You are at `low` here. `high` is here. How many unique elements are there in this window? There are two unique elements: A and B. So is your information correct? It's not correct. If there was no K, this would be wrong, so we would move forward.

Now K is there. Think like a human, what would you do? If you were told that you can change one thing in this, and change it in such a way that all the information becomes the same. What would we do? We would remove this B and write A here. This is what we would do, right? Then everything would become A, so its answer would be three. Could we do anything else? Changing B to C is of no use. Changing B to D is of no use. Changing B to A is useful.

Would you guys try to make A into B? Then it wouldn't be possible because only one change is allowed. Then you would get stuck. So think right here, open your mind and think. Why aren't we changing A to B? Look at what I am trying to say. `A a B`. Look, `A A B` is your substring. You have to change one because K says that I have one. So either you change B to A, or you change A to B. There are only two options.

Now, would you prefer making both A's into B or making B into A? How will you know this? Why am I saying that we should make B into A? Because the K I have is only one. So making B into A is more beneficial. A is here two times in the whole substring. B is once. If you have a limitation that you are told you only have K power to make modifications, what would any intelligent human being prefer to do? The one which is less, changing that is more beneficial, right? If K is only one, why would you start changing the one that is more? Change the thing that is less.

Let's do one more thing here, suppose there was also a C here. Now what will you do? Now there are three options:

- Change both A's to C, change B to C as well.
- Change both A's to B, and change C to B.
- Let A remain A, change B to A, and change C to A.

In this too, you will feel that letting A remain A is better. Why is this one better? Because A is maximum, so let A remain A. The rest that is left, change all of them and make them A. What does it mean? Suppose there is a very large substring, you know that 70% of it is already A. 30% is something else. So will you change the 70% to make it like the 30%? Or will it be easier to change the 30% to make it like the 70%? The 30% because it is less. It is already less. Even if we make all of them A, it will take us 30 operations. But if you try to change A, then it will take at least 70 operations.

It is like there are two parties in the country. One is BJP, one is the entire India Alliance. BJP is in the majority. And India Alliance is small, small parties making up 30%. If you change the India Alliance into BJP, then there will be one party, one rule in the whole country. But if you try to change BJP to make it like the others, you will have to convert at least the 70%. And there are many parties in the India Alliance too, you will have to change them as well. So it will take a lot.

That's why the thing which is the most in the substring, leave it as it is. Whatever else is there, change it and make it like that maximum one. This should be your algorithm by logic. Okay? What did you understand from this? Now it will slowly open up. I am saying the question is hard. I myself am saying the question is hard. It took me half an hour yesterday too. I hadn't solved it in a long time, so it took time. That's why I am pausing and explaining. Let's take our time comfortably on this question.

---

## Window Checking & Execution

Suppose this is your `low`. This is your `high`. Your A is two times. B is one time. You have one power. Can you make this substring good with the power you have or not? This is what you have to find in the question. Can you do it in this? Yes, you can. Why? Because looking at it, we know that K is one. A is in the majority, so leave A, and the rest is B, which is one time, so we can do it one time. Meaning this is either less than K or equal to K.

But suppose there was a C here. Now your `high` is here. Meaning your hash map looks like this: `A2`, `B1`, and `C1`. Now look, your K is 1. Can you make this substring good? Let's see. A is in the majority, leave it, it's the BJP. The rest in the India alliance, how much is there? Two. So you will have to change two anyway. You cannot make this substring good and this is our check! Whether this information is correct or wrong. Which substring is correct? If K was not given, then the substring in which everything is the same is the correct one. But if there is a substring in which you can change it using K, then it is correct. If there is a substring in which you cannot make it correct using K, then it is wrong. This is our whole algorithm.

Now look how beautifully we will solve this. First of all, come here. Again, write the format. Your template. Write it again and again so you practice it. `i < n` okay `i++` understood okay. First of all take this `i` inside. Took it. Now, what do you have to find out? You have to find out two things: unique, and which character is in the maximum frequency. For this, better than a hash map is that you make a big array. Why am I not saying hash map? Because finding the majority from a hash map is difficult. How will the map know whose frequency is in the majority? It won't know.

Whenever it is a string question, you can use space. It is constant. Make an array of size 26. Keep all of these at zero initially. Whenever you get a capital A, change this to one. Whenever you get a capital B, change the one to one. If you get B again, change this one to two. If you ever need to find the maximum, then iterate the array. Return whichever is the maximum. This will take constant time because there are 26 alphabets. So the size of this array will also be 26. So even if you iterate 26 again and again, it won't make a difference.

One more thing: if you make a 26 size array, how will you know that A should be kept at zero, B at one, and C at two? There is an ASCII value. The ASCII value of A is 65. Because I don't want you to have to read that at that time, don't make an array of 26. Make an array of 256. Because the number of types of characters in Computer Science is 256. Space bar, inverted comma, ABCD, small abcd, numbers, all combined make 256. If you do that, you won't need to shift indices here and there. Your A will go to 65 in that array. So make an array of 256, we will put it at zero. Did `i++`. Wherever it went, its character would have come. Very good.

Now, is this information right or wrong? How were we finding out? What does this tell you—how many letters are there in it? Not unique letters, total letters. This you will also get to know from the length. What is the length? Length is `high - low + 1`. In total characters, there will be two things. One will be the maximum, whose frequency is maximum. For example, the total character length that will come out will be four. The frequency of your maximum count that will come out will be two. How much is left? The difference. The difference is `4 - 2`. There are 100 crore people in India. If 70 crore are voting for BJP, then how much is left? 30 crore. The difference came out to be two. And this difference is exactly what you have to change!

So if we find the difference, then we will know how many need to be changed. And if that change is less than K or equal to K, then it is fine. But if your K is 1, then this won't be possible. Then you will have to slide the window. First of all, find a length: `high - low + 1`. Find a `maxCount`. For `maxCount`, write a function that traverses the array. It gives you the maximum frequency. Find the difference. What will be the difference? `length - maxCount`. It's possible this difference comes out to zero. If 100% of the country's people will vote for BJP, then how many votes will India get? Zero. So it can also be zero, there is nothing to worry about.

---

## Shrinking the Window

How were we deciding if the information is right or wrong? If this difference is less than K, then it is fine. If this difference is equal to K, then too it is fine. But as long as this difference is greater than K, until then our information is wrong. The `while` loop that we used to run will now run like this. Slide the window until the information is wrong.

As long as this is greater than K, there is no scope at all. What did we do in this? First of all, remove `low`. Increment `low`. Now you don't need to erase anything in this because this is not a hash map. It is an array, so it would have already become zero. Okay? Now look, what was `maxCount` dependent on? `maxCount` was dependent on F. You changed F here. You subtracted something in F, right? So you will have to find the `maxCount` again. `length` is dependent on `high` and `low`. Are you changing `low`? Yes. `length` will also have to be calculated again. And what was `difference` based on? `difference` was `length - max`. Now length and max both changed. Difference will also change. Change it.

Close the `while` loop. Now we have come here. Until when are you running the `while` loop? Until the difference is greater than K. So if this `while` loop has broken and come here, then it simply means that either my difference is less than K or my difference is equal to K. Both conditions are correct. In both conditions, you can proceed freely. That is the correct information. The correct window. Calculate `length` again. And do `res = max(res, length)`. Close the for loop for the `high` one and return `res`.

Look at it. Same pattern as yesterday. What changed? Had to write these three extra lines. Here we had to think of some logic and write it extra. The concept is the same. When is the information right and when is it wrong, you have to identify this, the rest happens automatically. This just has to be put into the same format. As long as the information is wrong, keep incrementing `low`. As soon as the right information comes, write it down in the result. It is the same question. Okay?

I don't think there should be any doubt in this. But there could be because it is a hard question. That is why I am not teaching the next one today. The next question is "Max Consecutive Ones III". I think that if you have understood this one well, then you will be able to do that one in 2 minutes. The same thing happened to me yesterday. It took me 15-20 minutes for this question. "Max Consecutive Ones", I looked at the question, coded it in 2 minutes, it got submitted, and it was done. Both are the same question. Not even almost, it's exactly the same and in fact, it's easier. If this question was an 8 out of 10 in difficulty, then that one is a 6 out of 10 in difficulty. So if you understood this, that will be solved. Go, submit it, and try submitting that one too. Comment and let me know whether it was solved or not, then I will explain it tomorrow. If it is done, then that's a good thing. I'll leave it. We will start a new pattern tomorrow. Okay?

So this was today's class, and look, don't feel bad about what I said. But you guys also need to understand a bit. Right? You guys should also keep a little patience. Don't panic. Don't spread rumors like, _"Oh, you didn't teach, our whole career is ruined. You've ruined our whole lives."_ Don't spread such rumors. It will happen, everything will be covered. Whatever I have promised, that much will be done and it will be done well. It's not like I will just come and do a formality, write something here like, "Yes, come on, do it like this, do it like that." I don't do all that. So you guys cooperate a little too. If I take nine steps forward, you guys take one step forward too. We should maintain some decorum, right?

Alright, I will upload this video. It will get a bit late at night. Those who won't be able to watch it today, watch it tomorrow. And alright, let's meet in the next one. Right?

5. Sliding Window Pattern: Revision Part-1

Transcript:
Yes brother. So today the revision pattern of the sliding window is going on. Right? Some people will say, "Brother, you come wearing the same t-shirt every day." So it is true that I haven't bathed for two-three days. But anyway, what is this today? It's a revision video. A revision video, or for those who are coming to the channel for the first time, what is it for you? It's a summary video. In **10 to 20 minutes**, we will slide the entire sliding window inside you.

And I would only say that if you are coming to the channel for the first time, then watch the rest of the videos first. There aren't many. There are three or four videos, watch them and come here, then you will understand better. Even if you don't want to watch them, just watch this, you will understand **50, 60, 70%**. Right?

---

### Flowchart & Conditions

Come, when we started the sliding window pattern, I told you guys about a flowchart; let's quickly look at that flowchart. What is the flowchart?

- The question should be of an array or a string. It's not for a linked list either. I have seen very, very few—maybe one or two—questions of linked lists where the sliding window is applied. But let's say, mainly the question should be of an array or a string. This is the first condition. If this is not the case, the sliding window will not be applied.
- Okay, what is the next question, the next condition? Subarray or substring. Substring or window, this should be talked about in the question. You should have to find this. Meaning, you have to find something out of this. Find this. If you don't have to find this, then the sliding window will not be applied. Right?

Now what to find in this? In a subarray, it won't be like you have to print the subarray. Such questions do not come. You have to find something about the subarray. Like it might say longest, "longest" is written. "Shortest" is written. Right? And you have to find the sum in it. This is in addition. Right? This is one part, longest, shortest. You have to find its sum. Find the frequency. Uh, find something like "at least **K**". Find something like "at most **K**". Or some condition like "exactly **K**" is given, find the average, find its maximum, or find the minimum.

Meaning, take a subarray and either tell the length of the longest subarray, or tell some sum of such a subarray, or it should have at least **K** of this thing, exactly **K** of that thing, at most **K** of some other thing, then what will be applied? Sliding window. There is a **90%** chance that it will be applied.

So reading the question, it's understood like this, meaning it's possible that this exact word is not written. But when you think about the question in Hindi (your native language), this is what you will have to find. So try to think of any question in Hindi, what is the question asking? Even if it has its own name written, what is the question trying to ask? Like "Fruits into Baskets", nothing was written in that. About a subarray, it just said that there is an orchard, there are such and such things. But what did you have to find? Meaning, what did you have to do? You have to keep that in mind. This is the flowchart. Right?

---

### The Four Steps of Sliding Window

Now there are four steps in a sliding window. To solve any question, there are four steps.

**Step 1:** Is to identify whether it is a sliding window or not, whether it is sliding or not. So you identified this from the flowchart. Very good.

**Step 2:** Is it a fixed or a variable window? Fixed or variable window. So if it is written in the question that you have to find a window of size **K**, or find a subarray of size **K**. Find a substring of size **K**, then son, it is fixed. Whatever is given to you, even if **K** is not given, it might say "Find a subarray whose size is exactly three." What fixed means is that the size of the window remains the same. The size remains the same and we keep sliding that same window, then it is fixed. If nothing like this is written. If it says to find something longest or find shortest or do something like that, then it is variable. It's very simple, you will understand by looking at what it is saying, whether the window size should be this or the subarray should be this much. If it's not saying that, it will be variable. No need to apply more brain into it.

**Step 3:** What is step three? What is the window's information? Window's information, what do I mean by this? Those who have watched the video will understand, those who haven't... Suppose you are in an array and you create a window; window means you are currently in some subarray. Right? So you are in some subarray. Okay, you are in a subarray. Your `low` is here and `high` is here. So this became your window. This is your window. Yes. What do you understand from this window? When we create this window, what are we doing in this window? Maybe in this window, there is **1, 2, 3, 4**, maybe you want to find the sum of this window because the question is telling you to. Maybe you want to find the max of this window. Maybe you want to find the min of this window. Maybe you want to find the average of this window. It could be anything. It can be according to the question. Maybe it is a string and you want to do character frequency. What do you want to do with the character? You want to find the frequency. You might want to find the number of unique characters. The question is telling you to find it. All these things are the window's information, so you have to understand what it is asking, brother: "Find a longest substring," okay, but in "Find a longest substring," what does it mean? What should be in that substring? All the letters in that substring should be unique, all the numbers in that substring should be negative, all the numbers should be even; this is the information of that window. So you will have to understand this, and how to extract it, you will also have to understand that. Right?

**Step 4:** When you slide that window, when you slide this window—sliding means the window is going like this, going like this, either this is coming in or this is going out. So how will you pass the information? How will you change it? How will you change the information? If the window changes, for example, your array is **100**, **200**, and **300**. Currently, your window is here. Currently, this is your window. Suppose your information was sum, so you will write its sum as **300**. But when this window slides from **100** and goes here, when your window becomes **200** and **300**, its sum will come to **500**. How will you calculate this? You will calculate this from the existing sum which was **300**. Which was **300**. From that, you will subtract **100**, which was the value of `low`. And you will add the new one that is coming, **300**, to it. So this $300 - 100 = 200$, $200 + 300 = 500$. Like this, you will have to see that when the window slides, how is its information calculated? For the new window. You won't do it by traversing again and again to extract the information. Right? Suppose it's character frequency, then how will you do it? So suppose you have stored the character in a hash map. It's A1, so the character you are sliding away from, the one where `low` is and you are sliding, remove it. Either decrease its frequency. If it becomes zero, remove it. Add the new frequency that is coming at `high` to the hash map. If its frequency is there, increase it. If it is not in the hash map at all, then write it as one. So you have to understand how the information will change. Right?

---

### Fixed Window Pattern

Now the two types of questions are fixed and variable. In fixed, I don't think anyone will have any kind of doubt, but I will tell you quickly. There is a pattern for fixed. Fixed window questions have a pattern.

Now what does a fixed window mean? What did I say, whenever you are told that there is a window of a particular size, meaning a window of size **K**. For example, **K = 3** just for example. So from where to where will your window be formed? It's obvious that if this is an array, if this is an array, an array like this, then it is **0, 1, 2, 3, 4, and 5**. If your **K** is three, your window will always start, right, it will start from the beginning. Starting from the beginning, where will it go? You only have to make it of size three, so it will go up to here. So what are you able to see here, that now in a window, what happens is that `low` is its starting point. Meaning where the window is starting, and `high` is its end. This happens. Now you have to start from the beginning itself, it wouldn't be said to start from the middle of the array, that has no head or tail. So `low = 0` will always be there. Where will `high` be? If `low` is zero and the window size is three, where will `high` have to be? `high` will have to be at $K - 1$. Where two... two... look, if `high` stays here and your `low` stays here, your window size automatically becomes three. It did, right? Always, always in a fixed window, this will be your starting point. Right?

After that, in fixed, extract the information of the starting window, meaning `low = 0` and `high = K - 1`. Extracting its information means that it also depends on the information, if it is the sum, then run `i` from `low` to `high`, run it, do `i++`, write it in a `for` loop and whatever its information tells you, suppose its information is sum, then in a sum do `sum = sum + a[i]`. If it is saying that we have to find its maximum, then take a `max` variable and calculate max in it, max of what? `maxi` and `a[i]`. So this is simple, that you traverse the array. Meaning, if you had to do that in the whole array, what would you do? You would traverse the array. You would do that. So store its information. Whose? The first window's. The first window's.

After that, after that, now we will start the work. Now we will slide the `high`. Look, we will write `while (high < n)`. Why will we write it? Because every time, right, we have to slide the window. In every step, we have to slide the window. And do we slide only one? No. We have to slide both. Let's see what we will do.

First of all, first of all, right now you have the answer for this window, the first window when `low = 0` and `high = K - 1`. I already told you about that, that has to be extracted anyway. For now, write this in the answer. Now it also depends on what the answer is asking for. The answer is telling you to give me the maximum among the information of all the windows. Or give me the minimum among the information of all the windows. So accordingly, suppose it is telling you to find the sum of all windows. Give me some maximum from that sum. So do `max`. And where do you have the answer for this window? The answer for this window is in `sum`. So first of all, do this task. First of all, you have to do this task.

After that, after that, now let's slide the window and pass the information as I taught earlier. First of all, what should you do? `low` is currently at zero, so now you will slide `low`, when `low` was here earlier. Now you want to take `low` to `+1`, so first remove the `low` one from the information. How will you remove it? Again it will depend on what your information is. For example, your information is sum. So `sum = sum - array[low]`. Is it clear? It's a simple thing. And `low++`. Very good. It's done, right? That you removed `low` and increased `low`. So okay. Now you have to increase `high`. You have to increase `high` and take its information. This is how the information will pass. So increase `high` and, and take its information. Do not memorize this `sum`. Sum can be one question. Maybe it is an average. Maybe it is something else. A product. So accordingly, `sum = sum + array[high]`.

But, but, but in between this, between this step and between this step, there is an edge case. It's possible that when you entered this loop, when you entered the while loop, `i = n - 1`. It might be at the end, `high`. As soon as you increased `high`, did `high++`, right, then `i` became `n`. There is no index `n` in an array. In an array, it is up to `n - 1`. So this will be wrong. This work that you are doing will be wrong. That's why check here. Before doing this, check `if (high == n) break`, break, check this and close it. Here, after doing all this rigorous process, you must have got the answer. Return the answer.

Take a look once. This is the template. You have to do any fixed sliding window question in the world. This is it. Look, what did we do first? First of all, we extracted the answer of the starting window. Extracted the answer. After that, we are calculating. What did we do first? We wrote it down in our answer. The one of the starting window. Increased `low`. Meaning removed it and increased it. Then increased `high` and included it in the answer. Here, this is the template of any fixed window. Very good. So I don't think there will be any doubt in this. It is very simple. This is what happens in every question, man. Only that information changes.

---

### Variable Window Pattern

Now come. Now come to variable. This is what's hard. Now come. It's not hard. Meaning it seems a bit hard. It is not hard. For those who watched the video, it is not hard. Right? Come to variable.

Now in variable, the sliding that was fixed, what were we doing in that? We were keeping `low = 0` and keeping `high = K - 1`. But why is it variable? Because you are not given **K** that it is of this size. So how will you do this? You won't be able to do this. That's why you don't have to do anything in this. Keep `low` also at zero because the start will be from zero, brother. And keep `high` also at zero. Keep `high` at zero. We will start from zero. Slowly we will increase, decrease, and see.

Variable literally means that the window is not of a fixed size. The window can increase as well, it can decrease as well. How will the window size decrease? When you increase `low`. And how will the window size increase? When you increase `high`. Right? Meaning currently this is your window. You have `low` here. You have `high` here. You might increase `low` and bring it here. So this much window reduced. So the window size decreased. Maybe your `high` is here. And you increase `high` and bring it here, so your window size increased. It increases like this. Right?

Simple, don't have to do anything. Where is our `high` right now? It is at `i = 0`. We will take `high` from **0** to `n`. We will keep increasing `high`. How will we increase it? We will increase it with a loop. So don't write a while loop. If you don't understand, simply write this. With the help of a `for` loop, we will increase `high` every time for sure. `high` has no other option. It will definitely increase. Right? Before doing all this, you will think about the information etc. Right? Let's go.

What is the first thing you should do? Include `high` in the answer. You are increasing `high` in the answer, right? So when we increase it, we include it. First of all, in the answer, sorry not in the answer, whatever your information is. Right? It's information. Information means it could be the sum of the window. Include `high` in the information. Include `high`. This is the very first thing to do without thinking anything. Let's include `high`. Meaning if it is sum, then add `a[i]` to sum. If it is product, then do that to `a[i]` in product, meaning multiply it. If it is frequency, then add that letter where `high` is in the hash map. Did you understand the first thing? Very good.

Now, now look, what do you have to do now? Now you have to decide. Now what do you have to decide? Information, this information you are calculating right now, is it correct or incorrect? Correct or incorrect? Incorrect. What does this mean? How will this be decided? This is the most important part of the question. Is the information correct or incorrect? How will you know if the information is correct or incorrect? You will understand by reading the question.

For example, you are told to find such a window in which a person is standing. Right? What are you told, that many people are standing here. In a line. Right? Many people are standing. You are told this is the array of people. Right? It happens like this. You are told to find such a longest subarray, meaning as longest subarray as possible, in which the total weight of the people, the total weight, is **100 kg**. Every person has some weight. Suppose this one is **20**, this one is **50**, this one is also **50** right now. Like this, it is told to find any such longest window in which the weight is exactly **100**. This what we said right, exactly **K**, at most **K**. So it can be like this, that the weight is **100**. Right?

Now what will be your information in this? What information do you have to extract? Weight, total weight of the window. So what will your information be in this case? Total weight of the window. Window or subarray, from where to where? From `low` to `high`. Wherever `low` and `high` are, including them, we extracted the weight information.

- **When is your information correct?** When is your information correct, meaning according to the question? Whenever your information, meaning the weight you extracted, is `== 100`, then this is correct, this, this is correct, this is what you have to find. Right?
- **When is your information incorrect?** Your information is incorrect in two cases. Your information is incorrect in only two cases. If the weight you have is less than **100**, or your info is greater than **100**. Both of these are incorrect information. Sorry, both of these are incorrect information. This is correct information. Right?

So first of all, you understood this, when is the information correct? When is it incorrect. Right?

Now, now there is a part. Now there is a part. Where are we right now? Right now we are right here. In this very line, right now we are in this very line. All these drawings and scribbles, I am making them to explain it to you. If the information is incorrect, right, what is the general logic? What is the general logic? After this, we write a part here that: _As long as, as long as the information is incorrect. Is incorrect. Until then, until then, increase `low`._ Increase `low`. Meaning shrink the window. Shrink it. Shrink it. Right? Here too, it's not that simple. It is simple. What did we say? As long as your information is incorrect, keep increasing `low`. What does that mean? But here, when is the information incorrect? The information is incorrect in two cases.

But along with this, you also have to think whether by increasing `low`, will we ever be able to correct that information or not? Meaning, the purpose of increasing `low` is that if the information is incorrect, we want to correct it. Now look, what does increasing `low` mean? That first of all, what did you say, that whenever you increase `low`, right, you will remove `low` from the information and then increase `low`.

So if this person is standing. Suppose this is a person. `low` is here. His weight is **20 kg**. And here is another person, his weight is **50 kg**, and `high` is here. Right? Right now what will be in your information? Right now what will come in your information? $20 + 50$, we said right, information means the sum of everyone's weight. So its answer will be **70**. This will be the answer of the information. Right? Now what are we saying? Is this information correct? No, it's not correct. It's not correct, right. **70** is less than **100**. **100** was told. **100** is correct. Okay.

So in this case, should we increase `low`? The purpose of increasing `low` is that we have to make the information correct. Because as long as the information is incorrect, we will increase `low`. But think about one thing. Increasing `low` means that you will have to decrease this **20** from your **70**. And only then will you be able to increase `low`. Be able to come here. So think about one thing and see. **70** is already less than **100**. You are saying that we will keep increasing `low`. What will happen by increasing `low`? What difference will increasing `low` make to the information? The information will keep getting even lesser in this case. Right? By increasing `low`, your **70** will get even lesser, sir. So if **70** gets even lesser and becomes **50**, then this too will remain less than **100**. If this decreases and becomes **30**, then this too will remain less than **100**. So here the information doesn't seem to be getting corrected at all. It doesn't seem like it, right. Something is already less. To correct it, there is a need to increase it, right? There isn't a need to decrease it. If you keep decreasing it, it will never be correct. That is why in this wrong case, there is no benefit in decreasing `low`. And where there is no benefit, we do not do that work. Right?

Did you understand or not? I have explained in the simplest way possible what will happen by increasing `low`. By increasing `low`, the weight will decrease even more. You are saying your weight is already less than **100**, so why are you increasing `low` further. Now you should add more people, right, so that it becomes **100**. You have to make **70** into **100**. So would you want to add something to it or subtract? You would want to add. But by increasing `low`, it is decreasing. In this case, this logic failed. So there is no need to do this.

When is there a need to do this? When is it? Suppose, suppose, suppose this is your array. Right? This is your **70** and this is your **50**. Suppose. Right? So where is your `low` now? Now your `low` is here and your `high` is here. Right? Now look, what will be the information of this window? The information of this window will be **120**. Yes, is this incorrect? Yes, it is incorrect. Why? Because it is greater than **100**. We saw two incorrect cases. Now can increasing `low` be beneficial? Yes, why? Because we have to make **120** into **100**. So we will have to subtract something from this, only then will it happen. We don't know how much. So we will definitely subtract something, only then will we reach close to **100**. How will we correct the information. You have **120**. You need **100**, so you will remove a little, right sir. That is why, and what happens by increasing `low`? The same thing happens, it subtracts. In this case, we will keep doing `low`.

Now come to how do we write this? What did we say? As long as it's incorrect, we will increase `low`. We will increase `low`. In this hope, in this hope, there was one more line missing in this. In this hope that the information, the information becomes correct. It becomes correct. That is why we didn't increase it when it was less, and we are increasing it when it is more. So how do we write this? Write this. Until when do we have to increase? Until the information becomes correct. Right? So `while` or as long as the information remains incorrect, we will increase it. This will make better sense. `while` whatever your information is, whatever your information, `while` the information is incorrect. Incorrect. As long as this is incorrect.

Now when you write this in code, it might be that your `sum > 100`, this could happen because according to this question there were three cases. `sum == 100`, very good. `sum < 100`, then there is no need to do this. But `sum > 100`, so as long as `sum > 100`, until then, until then what will we do? First of all, `sum = sum - array[low]`. Extracted `low` from the information. `low++`, that's it. Until when will this run? Until when will this run? This will run as long as your `sum > 100`. Until then we will keep reducing the sum little by little and keep increasing `low`.

Now as soon as this breaks, as soon as this breaks, then comes the third and last step. Third and last step. Now here in this part, if, if the information, if the information is correct, has become correct. Has become correct or was correct from before, no difference. If it is correct, then, then find the length of the window. How do we find the length? `high - low + 1`, not the length of `low` and `high`. We are not doing any math in this. Your **0, 1, 2**, if `low` is here and `high` is here, then its length will come to $2 - 0 + 1 = 3$. Right? Calculate the length and add this length to your answer according to your convenience. If maximum is asked, then do maximum, if minimum is asked, then do minimum, anything. That depends from question to question. And close the while loop. Close the while loop. Close the while and just come. Comfortably return the answer.

---

### Conclusion

Let me make you revise once again. You have to keep increasing `high`. You have to keep increasing `high` one by one. With a `while` loop. You have to include `high` in the information. You have to include `high`. After that, as long as, as long as the information is incorrect, is incorrect. Is incorrect. And meaning it can be corrected by increasing `low`. There is a hope. Whether it can be corrected or not? That's a later thing. But there is a little hope from `low` that by increasing `low` it can happen. There is a hope. Until then in this part, until then increase `low`. `low` means first remove it then increase it. So do it. Let's move to the next part after this. If the information has become correct, it's possible it might not have, it's possible it might not have—meaning people are not gods, we are no gods, it's possible the information didn't become correct. If it has happened, if it has happened, it has happened, include it in the result. Result means take its length, whatever you normally do, include it in the result and close the `while` loop and return the answer.

Any variable sliding window problem in the world is done with this flowchart. It is done with this template. This is a template. Whatever questions I have made you do, I think how many, **1, 2, 3, 4, 5, 6, 7**, eight... I made you do eight questions, right. By changing one line or two lines, it's similar only. One line or maximum two or three lines. That too, maybe we wrote something above, something below. Question by question, changed the information a little. Deciding whether the information is correct or incorrect, we might have had to write two lines more, but **70%** will remain this template. Now maybe not even **70**, sir, **80%**, **80%** template will remain this.

So if you are watching this video till here, many, many congratulations, you have learned fixed and variable. You will practice one to two questions from that pattern sheet which you will find in the description. You will get the sliding window. Sliding window, now if you explain it like this to any interviewer, he will be happy that yes, okay, the kid is smart. Right? So alright, this was a revision, and from tomorrow Linked List is going to start. The Linked List pattern, I mean not the Linked List topic, and so from tomorrow come regularly, stay consistent.

6. Sliding Window Pattern: Revision Part-2

Transcript:

### Introduction and the Missing 50%

Today you guys will get to know why I am the best teacher on the internet for teaching DSA. Right? Yesterday I uploaded a video in which there was a revision of the sliding window. I got a lot of comments on it saying, "Sir, very good explanation, Sir, it completely opened up my mind. The whole world has changed."

But right now you only know 50% of the story. One very important thing, I made a mistake too. I missed it. You guys missed it too. So it's 90% my fault, 10% is yours. Right? So today I was solving an Amazon question to teach you how a pattern is applied. Then it struck me that, man, I didn't even teach this. Then you would have gone and tried, and you wouldn't have been able to solve it.

Alright, the template we have studied so far for the sliding window, the template I told you yesterday in which `high` used to move forward. Then we used to shrink it as long as it was invalid. Then we would write it in the result and return the result. This will only work 50% of the time. Yes, 50%—you guys still don't know half of the things. Let me tell you why you don't know.

---

### The Maximum Window Concept (Sum < 80)

Let's play a game. You have a lot of men standing here. Right? You have a lot of men standing in a line. You have been given a task to find the longest window in this, and whose total sum—meaning the total sum of however many men are in it—should be less than 80. Less than what? It should be less than 80. This is your question.

So naturally, what would you do? What you have to do is find the longest window whose sum is less than 80. So naturally, first of all, you will pick this man up. His weight will be 30. You will see that 30 is less than 80, so this satisfies your condition, but is it the longest? It could be the longest. At least we found one. So that is why you write **1** in your result and keep moving forward.

Then you catch the next one too. So yours becomes 70. 70 is still less than 80. So you feel it's fine. Meaning we found two men. Now it's two, right. Now your window length has become two. You still haven't crossed 80, so this is definitely one. Two is definitely there, there could be more ahead. So you write **2** in your result.

But as soon as you include this next one, your weight becomes 120. Now 120 is greater than 80. So now your information becomes invalid. Now what you do is, okay, it became 120. Now you have to remove the men in the same order you took them. So now you start crossing out the men one by one. So now you say, "You get out." As soon as you remove him, your 120 decreases and becomes 90. It is still greater than 80, so it's still invalid, so it is still beneficial for us to shrink the `low`. Right?

Tell this one too, "You get out." As soon as you remove him, the weight becomes 50. Now again 50 is more than 80. _(Note: Contextually 50 is less than 80, translating literally)_ So now we go again and write this in the result. How much do we write? We try to write **1**, but since there is a **2** here, we cannot write it. This is basically what we have been doing since then; we were doing exactly this. Okay.

---

### Reversing the Problem: The Minimum Window Concept (Sum > 80)

Now see, now we will reverse this question. Now we are going to reverse this question. Right? What are we going to do? Reverse. Come, write 30, write 40, write 50, write 10, and write 50.

Now listen carefully. You have to find a shortest window. Among these men or women, find the shortest window—not the longest, now the question has changed. Shortest window whose sum is **more than 80**. More. See, the condition also changed and longest became shortest. But the condition became opposite. What was the condition earlier? The sum should be less than 80. What is the condition now? The sum should be more than 80.

Now how will we do it? Now if you were an intelligent person, what would you do? You would pick the very first man. So your weight became 30. Now is 30 your valid information? No. 30 is smaller than 80. Right? So your information became invalid.

So now according to what we were doing earlier, what will we do now? Will it be beneficial to shrink here? Because your information has become invalid. For shrinking, that's what was told, that when the information is invalid, then you have to shrink. Right? So is 30 already less than 80? By shrinking it will become even less. So we won't be able to shrink right now. So don't shrink right now. Right?

Move forward. Your weight became 70. 70 is also less than 80. But still, there is no benefit in shrinking because by shrinking it will become even less. Still don't do it. No problem, come here. Pick this one up. Now what is the weight? 80 + 50 = 130. This information is valid. This information is valid. Right?

So we didn't use to shrink during valid earlier. Earlier, shrinking happened during invalid, so even now we won't shrink. And you will try to write this in our result. Write it in our result. Right? So what will you write in your result? You will write the length. You will write **3** in your result. Right?

Didn't understand? Look carefully. Look carefully. I am explaining it very simply and opening it up slowly. I am not telling it all at once. Okay, so you didn't shrink? Didn't shrink. Then increase it. Come. What did the weight become? 130 + 10 became 140. It became 140, right? Yes. 140 is also greater than 80. So still your information is valid, but when did we learn to shrink? When it used to be invalid, but it's not invalid. The information is valid. Right?

So write this down too. Now your length is 4. But since you have to find the minimum, you won't be able to write 4. So you still have 3 written in the answer. Right? Very good. Now find this. What is this? It's 50, so your weight has now become 190. Still, the information is valid. Still, the information is valid, so okay. We didn't learn to shrink when it's correct. We didn't do it incorrectly. Try to write this again, so if you try to write 5, then you won't be able to write over 3.

Now what will happen is that your program will end. Why? Your `high` will go out of bounds. Now what are you returning? Look carefully. Look carefully with an open mind. You are returning **3** as the answer. Meaning you are saying that the minimum window, the minimum two men line by line whose weight is more than 80, its length is 3. But look carefully at the question, isn't the combined weight of these two men also... I mean greater than 80? 40 and 50, what is the weight of both of them? It's 90, right? So isn't their weight more than 90? _(Translating literal speech)_ But where were you able to find this? Now you are saying 3, it should have been 2, right? So this went wrong. It went wrong, didn't it? How will we get it? That went wrong. Why did it go wrong? I will tell you, I will tell you why it went wrong.

---

### Why the Condition Reverses (Less Than vs. Greater Than)

See, this is the difference between maximum window and minimum window. In minimum window. See, there is a basic difference between the two. What does maximum window tell you? What does the maximum window tell you in Hindi? Tell the maximum length of the window. Maximum window which is valid according to the condition. Valid according to the condition. Valid. Right?

So in this, you see how do you start? At the beginning of any question, your information will definitely be invalid. Most probably it will be invalid because if you are told what the sum should be? Less than 80. So initially, it's possible that the information could be invalid or valid. Anything can happen. So let's suppose you start with invalid. Start with invalid or wrong. Let's write wrong, scratch that. Let's start with wrong. It's not like we actually start, I am just telling you to explain.

Then from wrong, suppose you keep increasing `high`, so suppose it's still wrong. Sometime or the other it goes and becomes right. Right? But when it becomes right for the first time, your window length is this much. Do you have to stop right here? No. You have to increase it more to the maximum and make it correct. It might be correct further ahead too. So what do you try to do? You try to make it more correct, and make it correct, and make it correct, and write its answer every time. You keep writing its answer every time, so every time your answer keeps increasing.

Now as soon as your answer becomes wrong, we shrink in the wrong; until when do we shrink the wrong? Until it becomes right. So shrinking the wrong, now it shrinks here. Then it becomes right. Then now suppose you shrunk the wrong, then your window must have become this somewhere. Again you try to write this in your answer. Meaning if you have to find the longest, the moment you see that it has become right. You don't stop there, you want to make it more right and more right. When it becomes wrong, you shrink.

The simple reason for this is that any maximum window question in the world... The condition in it will be given to you. For example, if sum is given, it will always be **less than or equal to**. Always be equal to. Both are opposite. This is max and it is always saying less and equal.

What is the reason for this? The reason for this is that suppose I asked you in terms of men. The men example from just now. Right? Suppose this one is 30, 40, 50 kilos, this one is 10 kilos, this one is 50 kilos. Recall what I asked you in the question? Sum less than 80. If we ask to find such a longest whose sum is **greater than 80**. Then there is absolutely no need to do anything in this. Suppose you took this, so you have 30. No problem, it's wrong right now. You took this, it became 70. You took this, it became 120. Now this is greater than 80. Now this is greater than 80, so you wrote it as 3.

So now a man's weight is not negative. So now however many men you take, this will definitely be correct. Once the weight of three men becomes more than 80 kilos, then you add three more men to it or add six more men or add 50 more men. The weight will remain more, right brother. So what did this question become? In this, wherever you find it for the first time, you will take the whole array from there. So in this, just return the entire array. Check whether it's the sum of the entire array or not? So you return the length of the entire array, return `n`. So this didn't even become a question. The question made no sense.

That is why with longest it is always said that you are being given such a constraint that it should be less than that much. Take the longest window but that weight should be less, take any number of them with weight less than some 80 kilos. More than 80 kilos, we will take the whole world! 4 crore men live in the whole world. So combining everyone's weight, it will definitely become more than 80, so we'll take that. No. You can find such a longest window which has something less than something.

Meaning no matter how many men you hire, combined, everyone's salary should be less than 1 crore. That's what the company tells the HR, right? Hire as many as you want, but the salary should be less than 1 crore. If the company said hire as many men as you want and the salary should be more than 1 crore... Then the HR would hire the whole world. By hiring the whole world, she would distribute one crore to everyone. So this is not possible, so it's not logical, that's why.

That is why always remember. What will happen with maximum window questions? Your constraint will be **less than or equal to**. This constraint can be anything. Number of unique elements should be less. Number of repeating elements should be less. It will be anything. But this thing will definitely be there. Less or equal to. Because the opposite one doesn't make sense.

Come to its opposite example. It's a minimum window question. In this, you will always have **greater than equal to k**. See, it's opposite. This is minimum and this is greater equal to. Why is this? Because suppose one man's weight is 30. One man's weight is 40 and one man's weight is 50. If you are told that the sum should be less than 80, find such a minimum window. So this is simple, right. Its weight itself is less than 80. So this is also a window. So quietly return 1. So nothing even happened in the question. Check in the array if there is anyone or not. We will return that. So this was no question at all.

It is a minimum window but even the minimum's capacity, the sum, that should be more. Only then will it make a good question. Only then will you be able to think something. Meaning what will the company say? Hire minimum men who can do the work together. The company doesn't say hire minimum men who cannot do the work, then hire just one man, he won't be able to do the work, then nothing happened at all, right. Okay. But that is why in the minimum window you will have this plus. This is a minimum question, maximum is exactly its opposite question. Right.

---

### Updating the Sliding Window Template

So this was about understanding, but the template we have built, how will that change? I will tell you now how it will change. Right. Suppose you are minimum, meaning in minimum what did I say? Your sum greater than 80 is written. So obviously when you start, your sum will be zero in a simple question, so you are right now invalid or wrong. Wrong, right? Okay.

You don't have to take the wrong. So you will start from wrong. You increase `high` so that the wrong becomes right by adding up. Right? Sometime or the other it went and became right for the first time. It clicked right for the first time. Now it has become right. Meaning your window is this big. Your window is of 3. So this is an answer. 3 is an answer. We should write it down right now.

But it's possible that this is that example where you hired five men, okay. You hired five men, then you came to know that the work is getting done. But what is the company's target? Hire minimum men. Then you used to start firing. What was this firing? Firing was just shrinking.

So now in minimum we just do the opposite of maximum. What did we do in maximum? When the information was invalid, we used to shrink. We used to shrink on wrong. And see, when will the information be invalid? What did I just tell you? What will be any question of maximum? Sum less than equal to k. So what will invalid information mean? Sum > k. Now in Sum > k, it makes sense that you shrink. Because only by shrinking will the sum come below k. If you increase `low`, something will happen. So it makes sense in this that you shrink. Right?

But now, when yours has become right in minimum, so first thing is it makes sense that we write this down. And, it is possible that an answer smaller than our current answer is also possible. Now see, by increasing this, this answer will increase. Whenever you increase `high`, the size of the window increases. You have already found 3 here. So what should we try for? We should try for 2, for 1. How will that happen? That will happen by shrinking.

That is why as soon as we get the right one in minimum, we start shrinking. So as soon as the information becomes valid—not invalid—the information becomes valid, so the very first thing is we write it down in the answer. We write it in the answer and start shrinking. We start shrinking from `low`. Until when? Until that information damn well becomes invalid, and we leave the same.

Now why does this make sense? When will your information be valid in minimum? You are told the sum should be greater than 80 or equal. So when will your information be invalid? It will be invalid in this case. Now in this, there is no benefit in shrinking because if you increase `low`, it will keep getting even less. But now here your sum has become greater than 80. For example, your sum has become 100. But your condition is 80. It's possible that 90 also has some answer. It's possible that 85 also has some answer. It's possible that 81 also has some answer. How will we know this? This will be known by shrinking.

And you are trying to come down. Meaning once the target is achieved. Now you are removing men, that now you go, let's see if the work gets done or not. And every time we count. The work is getting done by four men. Counted it, the work is getting done by four, keep 4. Removed one man, 3. Work is getting done with three as well, very good. Count 3, you also go. Work is getting done with two, very good. Two, you also go. It's not getting done with one. Come forward.

So as long as the information remains valid, till then shrinking happens, and here before shrinking it is included in the answer. Did you understand this or not, please tell me in the comments whether you got it or not, I will explain again because... meaning if you don't understand this, then you understand, right, that your half knowledge was incomplete till now. Till today's class, till these 16 minutes your half knowledge was incomplete. No matter how many good comments you make that "I understood everything." You had understood half. You were feeling that you understood everything.

So it was my responsibility, if I wanted I could have ignored it, that yeah okay I made a mistake so it's fine, we will do it later. But it's a very important thing that now I will also tell the template. Will write its template too and solve questions too. So this becomes different for you in minimum. Why does this have logical sense? Because what did I just say? You start with invalid, eventually you become valid.

So firstly, you write this down that this is my 3, and you shrink until when? Until it is not right. So every time it is valid, every time you shrink the size is decreasing. So for example, you found out that we were valid in size 4 too. We shrunk, so we are valid in size 3 too. Yes, okay? So write 3, right. Who refused? That's what we have to find. We are valid in 2 as well. Write 2 in the answer. We are not valid in 1. Not valid, so meaning what is the meaning of not being valid? Being valid means that the sum is 80. Not being valid means that your sum became less than 80. If the sum became less than 80, then anyway there is no point in increasing `low`. When it is less and you have to reach 80, then now you need to increase `high`. So that we have been doing anyway. Right?

---

### Comparing the Maximum and Minimum Window Templates

Let's quickly write its pattern. It's just one or two lines here and there. First of all, this same thing will go on brother. This is an absolute truth of any sliding window. What is this? It's an absolute truth, brother. Come. Have to include `high`. This is also an absolute truth. Right?

Now come. Now what did I say? Now what is your sum right now? Sum is information. What did I say? While, while whatever is your condition for the information to be valid—the information is valid meaning sum is greater than something, frequency is greater than sum, anything, right. First step, first step, write this in the answer, write it already. You found one valid, write it down somewhere. You might get a better one, but at least write this down, if you don't write this you will forget, right.

So quickly write this down, what is the process of writing it in the answer? Length is calculated and answer is equal to `min(answer, length)`, because it is a minimum window question. This work is done. Very good. Now, what you have been doing, this you already know. Meaning removed `array[low]` from sum and increased `low`. Understood?

Now this is finished. When will this finish? When the information is valid. Now you will come here then. You will come here when your information has become invalid. The information has become invalid. What has happened? It has become invalid. So there is no need to do anything here. In the previous one, we used to write the result here because when did we come here? In the maximum one, we used to come here when your information was valid. Now you guys have come here when our information is invalid. There is no need to write it. Just return it from the result. Result or answer whatever is yours. Take a look at this.

This is the pattern. You might not feel like much has changed. But this entire algorithm has changed. The entire algorithm has become upside down. Meaning it's standing on its head. In Max, we used to do it when it was invalid. In Min, we are doing it when this is valid. Now we used to write the answer here earlier. Now why do we write this thing? We don't have to memorize. Now when do we write this thing brother? When the information is valid, only then will you write it in the answer. So we are writing where the information is valid. Earlier it used to be valid here, so we used to write it here. Understood this template? Right?

Let me tell you a small comparison. On the very left is the maximum window question and this is the minimum window question.

- **Condition**: In the condition, Max will always be told to you that this should be **less than equal to** something. And Min will always be told to you that this should be **greater than equal to** something, because I already told you, it doesn't make sense to ask otherwise. Right?
- **Looping**: In both you have to run `high`. In both you have to run from `0` to `n`. Right?
- **Including High**: In both you have to include `high`. In this also you have to do the same.
- **Shrinking**: But the difference that is coming now, shrink when? In Max, when it is invalid. Here, when to shrink? When it is valid. And here the result has to be written right here.
- **Result Placement**: This has to be done in one part. And here it has shrunk now. Now yours must have come valid. Outside the loop, outside the while loop, here you have to write the result. In Min, here you have to do nothing. Do nothing and come outside.

So see, this thing has come here. And this has completely reversed. This is it.

---

### Conclusion and Homework

Why has it reversed? This is my hope that you would have understood. If I wanted, I wouldn't have told or would have skimmed over it telling yeah yeah this is what needs to be done. It's just a line here and there. A line here and there is a different thing. But completely reversing the algorithm itself is a different thing. This is not a line here and there.

You might be thinking that hey sir, why do you make these useless videos. Now again some people will say that sir, teach linked list, what is all this you made? No. It's not a matter of a line here and there, son. This whole algorithm has reversed. You wouldn't have understood. So you wouldn't have been able to make this.

50%, now see, it's general probability, right brother. 50% questions will come from Max. 50% questions will come from Min. You have only learned the Max template, so you will solve this. When this one comes, you will be in a tight spot. Then you will bare your teeth saying I don't know. Then you will come here and hurl abuses that hey you teach uselessly. You don't know anything. "I am leaving, I will solve 10,000 questions, only then will I get it." No.

Now, from my understanding you are complete. You 100% if you are watching the video till here. Many many congratulations. You have become a master in the sliding window. Especially in the variable sliding window.

So I am telling you one question on this. Do it yourself. I will not make you do it. Do it yourself. Right? One question on this, although we have already covered it in this sheet. But at that time I think I was at home so it wasn't in my mind. Right? The name of the question is, the name of the question is **Minimum Size Subarray Sum**. Do it yourself. With this template, exactly with this template, do it. Go and do it yourself. Minimum Size Subarray Sum. Go and do it yourself. It's a minimum question. It's a very good question. Right?

Tomorrow I will cover two Amazon questions. I will cover two Amazon questions with patterns. Will teach you how a pattern is applied when a question comes in an interview. Wait for tomorrow's video. We were going to do it today. In the process of doing this question, this struck me. So watch this, and if you have watched it till here then it's a very good thing. Those who haven't watched it till here, it's not a good thing at all. Well, those people won't even listen anyway. They are master people. Alright, see you tomorrow. Right? Alright.

7. Sliding Window Pattern: Question

Transcript:

### Introduction & The Problem with Memorization

Before my students say to make a study video—they won't watch all this. This is a study video itself. Open your mind and listen carefully. The new students who are joining, today in this video you will find out why what I have been shouting for so many days, what I am teaching, and why this guy is better than your Striver _bhaiya_, your Love Babbar _bhaiya_, Apna College, Aapka College, or any college.

Look at this question on your screen. What is this question? It's a Hard question. A LeetCode Hard question. Facebook, Amazon, LinkedIn, Microsoft—whatever company name you can think of, it has been asked in all of them. Four types of hints are given in this question. Meaning, it's quite hard.

Now see, the problem is that if you have studied from these three _bhaiyas_ or any of your _bhaiya/didi_. If this question is in their course, then you can solve this question. But if this question is not in their course, then you won't be able to solve it. And always remember one thing: interview questions don't come from anyone's course. They don't come from anyone's sheet because all the interviewers haven't studied from me, nor have they all studied from them. That is why I teach you patterns or templates. What do I teach? Templates or rules. Once you learn this rule, you'll be able to solve any question without needing to memorize them question by question. Because how many questions will you memorize? 500, 1000, 10,000, 20,000—there is no limit to it.

---

### Problem Statement: Minimum Window Substring

Let's open up this question and see how fake, how absurd a question is asked even in a company like Amazon. What is the question telling you? What is the question saying?

You are given two strings, `S` and `T`. Its length is `N` and this one's length is `M`. You have to search in `S`. In what? In `S`. What do you have to search for? You have to search for the minimum window. What to search? Minimum window substring. You have to find the minimum window substring. That is what you have to find.

But what is the condition? There must be some condition. Its condition is that the entire `T` string—including duplicates, including duplicates—must be present in this window. Every character of it must be present in this window. The order doesn't matter. For example, if `T` is A B C, then you make any window in `S`. Make any window. For example, if you want to make this window, then A, B, and C must be present in it somewhere. It could be that B is here. It could be A is here and C is here. So B, A, C should be present once each.

If, if, if this string of yours was A B C C, then whatever window you choose, C must be there twice. C must be there twice. Wherever it is in the window, in any order. But C must be there twice. A must be there once. B must be there once. Apart from this, there can be anything else. Anything else besides this. But this much must be there. And you have to find the minimum substring of such a window. What to find? Substring. Not length. Not length. Not length, child. Substring—meaning you just have to return the substring of any such window. This is your question.

---

### The Sliding Window Pattern

Now, my students who have studied and come, who have come revising the sliding window: Pause it. Think about it yourself first. The new students who are watching, come along. You wouldn't know the template or pattern. I will tell you. Any sliding window question, any sliding window question in the world is only of two types. One is max window, one is min window.

What type is this question? It's of min window. In any min window question in the world, the condition—the condition based on which you have to return the window—that condition will be something like if there is a sum, it should be greater than or equal to. It should be greater than or equal to something. What? Sum is not necessary; whatever is asked of you, it will be given as greater than or equal to something in the condition.

What is the condition in this question? In this question, it is that there is some substring in `S`, meaning a window in which all characters of `T` are present. All characters must be present, and they must definitely be present with that much frequency. All characters must be there. Must be there. Must be there. Meaning, all characters of `T` must be present. After that, you can have anything. So it essentially means that whatever frequency you build, or whatever substring you form, it must be _at least_, at least greater than or equal to `T`. In a way, it should at least be larger than that. Meaning it should have all of `T`. Besides that, anything else can keep happening. Understood?

So we now know that this is a minimum pattern. We also got the condition. Come. Let's see. How many steps were there, brother? What was step one? What was step one?

Now look, I am not telling you all this anew; I have been telling you this all along. You can check, watch the previous two, the last two lectures, and you will understand this flowchart. Okay? If you don't know, no problem. Come, I'll explain it in two minutes.

- **Step One:** Identify what kind of question this is. So it's clear that it's a sliding window question. I don't think anyone will have a second thought or doubt about this because it's asking for a substring. It's a string question. A condition is given. A perfect example of a sliding window question. Very good.
- **Step Two:** Is it a fixed or a variable window? Is it fixed or variable? Is it saying anywhere that give a substring of this length or give a substring of that much length? No. It is saying give the minimum. Give the minimum substring. Meaning, as soon as it said give minimum or give maximum, it became a variable question. Very good.
- **Step Three:** Here is where we have to play the game. Here is where the game is. What is the information of your window? And how will you store it? Information means whatever window you are holding onto, whatever this window you are capturing is, what is this window? What will this window tell you? What do you want to find out from this window?

So what do we want to find out in this window? Whether the frequency of all the characters of `T` is there or not? For this, what information will we store for this window? Frequency. Frequency means a hash map or an array, anything. Meaning, the frequency of whatever characters are in this window, only then will you know, right, brother.

---

### Validating the Information

For example, if an `S` window is formed in such a way that A is there twice, B is there once, and C is there twice. Your `T` was like this, where A was there once, B was there once, and C was there once. So will these two match or not? How will you find out if they match or not? Look. What was your `T`? Your `T` is this. Meaning A was there once in `T`. So A must be there at least once in this. Are two A's more than one? Yes, it is more. So very good. It matched. B was there once in it, so B in the `S` window must be there at least once, it should be more than once. Is it once or more than once? Yes, it is. Very good. C is there once in `T`, meaning C in the `S` window should also be one or more than one? Is it? Yes, it is. So this means your information is what? It is correct. The information is correct.

When would the information become wrong? When would the information be wrong? For example, you captured a window where A was there once, B was there once, and C wasn't there at all. And your `T` is given that A should be there once, B should be there once, and C should be there once. So now look. Your `T` says that A should be once or more than once, so it is, very good. B should be once or more than once, that is also there, very good. But your `T` says that C should also be one or more than one. But how much is your C? C is 0, C is not there, so C is 0. If C is not there, it means C is 0, C hasn't appeared even once. So this information of yours has become what? It has become wrong. This is wrong.

Now see, now see, how will we know if it's right or wrong? It's very simple, what have we been doing in every string question? If you need to find the frequency anywhere and you don't even know hash maps. What don't you know? You don't even know hash maps. What's simple? Just take an array of size 256. What size? 256. Why 256? Because my birthday comes on 256. No, no. In C++, the total number of characters itself is 256. In any programming language, the total number of characters is 256. You take an array of size 256. Make them all zero. When you have to include the frequency of a character, increase it. When you have to kick a character out, decrease it. By doing this, your frequency will be formed. It's an array, a simple array, no hash map is being used here.

Now see. Now see. Now see. What was the next thing? Is the information right or wrong? Is the information right or wrong? Right or wrong? How will we know this? Because this is a very major part of our flowchart. It is a very major part of our flowchart. How do we know? What did we do last time, brother? For example, you will have some window of `S` and your `T` is A B C. `T` is A B C. `T` will be given to you. So first make this thing for `T`. What to make? Make this 256-sized array. Make the array for `T`. So what will happen is that A, B, C, whatever index it is on, will have a one on it. Okay?

Now suppose such a window of `S` is formed... um, such a window of your `S` is formed where A is there, B is also there, but C is not there. C is not there, so now this information, now this window, now your window and the rest can be anything... Let the rest be anything, it doesn't make a difference, D could be there 10 times, E could be there 15 times, it doesn't matter to us. Where does it make a difference for us? It should be greater than this, we will check with the characters in the `T` string, it just needs to be greater than that, you can keep whatever else you want.

Now look, check it, how will you know if this is a right window or a wrong window? Check it, brother. What is the question telling you? That A, B, and C, the characters in it, their frequency, their frequency in what? In that window array. In the window array, it should be equal to or greater than it. So check one by one. If A's frequency is one, is it equal to or greater than one? Yes, it is. If B is one here, is it greater than or equal to B? Yes, it is. But if C is one, is C greater than or equal to one here? It is not, it is zero. So what happened to your window? This window of yours became wrong, wrong.

It doesn't matter if your D has 10 or E has 15. We don't even need that. We just need to match the frequency with the characters that are in `T`. Okay? Understood how we will decide if the information is right or wrong? If you have understood this much, then come, I will show you how to solve the question in 2 minutes.

---

### Flowchart Execution

Minimum window, what was the flowchart for the minimum window? What was the flowchart for the minimum window? Where to where did `high` run? My students, pause it right now. Go and make it yourself. I have cleared everything for you. Where to where did `high` run? From zero to `n`.

What did we do after that? Remember yesterday's lecture. Those who are coming directly after watching the day before yesterday's, don't watch. Watch yesterday's lecture. Yesterday's lecture. The flowchart for the minimum was explained in yesterday's lecture. The flowchart for the maximum was explained in the day before yesterday's lecture. A single flowchart will apply to everything in the world. Come on.

What did we do? What did we do after this? What to do after this? As long as, as long as, as long as your information, the information of this window... wait, what to do before this? Include `high` in your information. Where to include `high`? In your information. How will we include it? We will increment the `high` character in the array. Simple as that.

Now, as long as the information is correct, correct. Correct, not wrong. Those coming after watching the day before yesterday's might feel I am saying the opposite. Please watch yesterday's. As long as the information is correct, what do you have to do? You have to do two things.

1. First of all, write this in your result. Why? Because the information is correct, we need this. Write this in your result.
2. And what is the next thing to do? Remove `low`, remove `low` from your information. Remove it from your information and increment `low`. That's all you have to do.

Close `high` and return your result. Return your result. This is the exact pattern for any minimum window substring.

---

### Coding the Solution

Now come, let's see how we will do this. How to do it? First of all, we will make two arrays. Make two arrays. Make two arrays of 256. Make it of 256. Why? One array is for your `S`'s window. One array is for your `T`. For `T`. Now suppose this is your `T`'s array. So name it `need`, `needed`. `needed`, at least this much is required. This much is required. What I was saying right, the condition sum greater than or equal to K. So what is this K? K is your `needed`. `needed` means it should be greater than this. And what name will we give to this one? Name this `have`. How much is it right now? How much do I have right now?

Now see, how will you know your `needed`, `needed`, how much it is? Traverse `T`. Traverse `T`. Traverse it. And whatever characters are in `T`, put them in `needed`. Meaning if `T` is A B C, then first change A from zero to one. If B is there, change B from zero to one. If C is there, change C from zero to one. Suppose there is another C, then change it from one to two. First of all, build your `needed`. Your `needed` is built.

Now come, now we will start our sliding window. Write `for high = 0; high < n`. This is nothing new. We are repeatedly doing the same memorized thing. What is the first thing to do? Take `high` inside. Take `high` inside. What is your window's... array? What is its name? It is `have`. `have`, `have`. Who to take inside `have`? Take `high` inside. Of the `high` character. So your `S`'s `high`, `S[high]` and plus plus. `high` came inside.

Now what to do? As long as the information is correct, keep doing something. So come, write the loop. While... now look, I have already told you how the correct or wrong information will be calculated. We will write a function for it. We will write the function now. I will write and show it right now. For now, assume the function's name is `m fun`. What is the function's name? Okay, let's go with `sahi` (correct). The function's name is `sahi`. And in `sahi`, what were you really doing? You were comparing `have` with `needed`. Whatever `needed` is, that much should be in `have`. So what will we pass in this? `have` and `needed`. I will write and show this to you right now. And close this.

Meaning as long as it is `sahi` (correct), as long as it is `sahi`, as long as it is `sahi`, what do you have to do? You have to keep storing the result. One more thing, you don't have to give the length in the result here. You don't have to give the length in the result here. You have to return the entire substring. You have to return the entire substring. So to do this, when you were doing length, what did you do? You used to write the result as `result = min(result, length)`. Okay? So first of all, you will have to find the length. First of all, you will have to find the length. So just find the length first. We used to find this every time anyway.

You found the length, meaning the length of this window which is correct right now is so-and-so. You can do one thing. For those who don't know substring, I'll tell you. `if (res > len)`. This is what we used to do, right? That if `res` is greater than `len`, only then is there a benefit in updating it. Otherwise, there is no benefit. We need the minimum. So first of all, make `res = len`.

And do one thing. Now, how do you find a substring in C++? You have to pass two things to extract a substring. You can extract the substring of any string. How? You have to pass its starting point and you have to pass its length, of the substring. For example, if you have something like A B C, 0 1 2. So if you write zero in the starting and write two in the length, it will take A and it will take B. So your answer will come as A B. If you write three in the length, it will take A, it will take B, it will take C. So its answer will come as A, B, C. Meaning set the starting point and take a substring of that length starting from there.

Now see, you found out the length from here, that length is going to be its result. Length is finally going to be the result we have, and how will the starting point change? Every time what you finally need is the minimum substring. For that, you need two things. One, the length of that substring, which we will repeatedly store in `res`, that will come at the end. But the starting point, which one will be the starting point? The starting of this window, what is the starting point of any window? It is always `low`. A window essentially means `low` to `high`. So you take another variable, and in a `start`, store `low` in `start`. We are doing this work only when your `res` is greater than length because we need the minimum. We used to do this same work in one line: `res = min(len, res)`. Just because we have to give a substring in this, you will have to do it like this. You can do it in some other way too, thinking according to yourself. And what to do? Close it. The first task is done.

What was the first task? We took the `low` one into the result. Now what to do with that window? Kick `low` out, brother. Hey, kick `low` out, man. How will we kick `low` out? Kick `low` out fast. `S[low]` minus minus, the game is over. Do `low++`. That's it, this while loop is over.

After that, do we need to do anything or not? Nothing needs to be done. This `high` loop is over. The `high` for loop is over. Now what did we use to do? We used to `return result`. But right now, what do you have in the result? Right now, you have its length in the result. There is length in the result. And what is in `start`? It has its starting point in `start`. So how is a substring extracted, we have to return a substring, right? Just do it, man. Do it. `return S`, you have to return `S`'s window, right? `substr`, `substr`, we write it like this. What do we give here first? Starting point and length. Where would the length be stored? In the result, for the minimum one.

---

### Writing the Helper Function

That's it, it's over. You have now solved a Hard question. How much? It took 16 minutes. Even after giving such a long speech. It's a Hard question from LeetCode. A Hard question with four types of hints. Meaning, quite a hard question. It's solved. What did we use in this? We used a simple template. Did anything change in this rule? Did anything change in this rule so far regarding what we used to do in the minimum? Did I tell you even one such step that became extra for you, making you think, "Oh, what did you do here? This is not right, yesterday you said this, today you did this." No, we are doing the same steps, brother. Run `high`. Take `high` into the result. As long as the information is correct, keep taking it into the result and keep decreasing/increasing `low`. Finally, return that result.

Now come to what I had said. How will we know if the information is right or wrong? So come, now many people face problems in writing code. I will write it. How did we know right or wrong? So in right and wrong, first of all, what were we passing? What were we passing? We were passing two arrays. `vector<int> have`, `have` meaning what is currently there, what is currently in `S`'s window. Very good. And what was the next vector we passed? The one that is your `needed`. What is it? It's `needed`. What was `needed`'s name? `needed`. Right?

What was its logic? That whatever value is in `need`, there will be some value in `need`. There will be. In `need`, A's value will be one, B's will be two, C's will be three, whatever it is. The rest will all be zero. So, whatever value a character has in `need`, that character's value in `have` should either be equal to it or greater than it. Regardless of anything else.

So come, it will be found out with a simple loop, right? What is the size of both your arrays? 256. That's why 256 is taken. It makes it very easy, okay? Come, run it. Take 256 and do `i++`. Now, when will this information of ours become wrong? When will this information become wrong? When any value of `have` is less than any value of `need`. That's it, right? Suppose `have`'s A has zero and `need`'s A has one, then this will become wrong. So run an `if`, that if `have`'s `i` is less than `need`'s `i`, ever, ever, ever, anytime in the 256, then `return false`, meaning it's not `sahi` (correct). The name of this function is `sahi`.

Now if this loop runs completely, if this loop runs completely 256 times, meaning your condition was never caught. Your condition was never executed. What does this condition never executing mean? That `have`'s `i` is always either equal to `need`'s `i` or greater than it. This itself is our condition for being correct. Here, quickly, quickly `return true`. Here you go, I have written that `sahi` function for you. What is this? I wrote the `sahi` function. Here you go. `bool sahi`. `bool sahi`.

What is the name of this function? `bool sahi`. `sahi`. This is the same `sahi` that was being used here. Where? Here. This very same `sahi` was being used here. See, it's the same now. The question is finished.

---

### Conclusion

This question, and if you explain it to an interviewer in this way, his legs will tremble, thinking, "Oh, what has he just told me? He is explaining it in such a systematic way." What would be the opposite of this? That you go memorizing it. Striver _bhaiya_ made you memorize it. There he will ask, why are you doing this, brother? There he will ask you, why are you doing this, brother? Why are you doing it this way? Where did you come memorizing all this from? Then you will realize that you don't know this.

And the new students might be thinking that, brother, you also made us memorize. You also said that as long as the information is correct, keep doing this. Watch yesterday's lecture. I haven't made you memorize anything. I had to explain this to you quickly, so I did. Nothing has been rote-learned. It has been explained completely logically why it shrinks. Why is the logic for shrinking different in a maximum window and a minimum window? Why is it the opposite? Everything has been explained. Go and watch carefully, enjoy, and go submit this question right now.

It's a very important question from an interview perspective, so jokes aside, it's a very important question. Right? Let's meet tomorrow. Tomorrow we will definitely start Linked List. Right? Let's go.
