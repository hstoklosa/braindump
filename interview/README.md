# 🏆 Interview

An ongoing grind to secure that cool entry-level programming job (SWE).

## Quick Access

<details>
<summary>&nbsp;Tips for Leetcode Patterns</summary>
<br />

&nbsp;&nbsp;&nbsp;**_IF INPUT ARRAY IS SORTED THEN_**

- &nbsp;Binary search
- &nbsp;Two pointers

&nbsp;&nbsp;&nbsp;**_IF ASKED FOR ALL PERMUTATIONS/SUBSETS THEN_**

- &nbsp;Backtracking

&nbsp;&nbsp;&nbsp;**_IF GIVEN A TREE THEN_**

- &nbsp;DFS
- &nbsp;BFS

&nbsp;&nbsp;&nbsp;**_IF GIVEN A GRAPH THEN_**

- &nbsp;DFS
- &nbsp;BFS

&nbsp;&nbsp;&nbsp;**_IF GIVEN A LINKED LIST THEN_**

- &nbsp;Two pointers

&nbsp;&nbsp;&nbsp;**_IF RECURSION IS BANNED THEN_**

- &nbsp;Stack

&nbsp;&nbsp;&nbsp;**_IF MUST SOLVE IN-PLACE THEN_**

- &nbsp;Swap corresponding values
- &nbsp;Store one or more different values in the same pointer

&nbsp;&nbsp;&nbsp;**_IF ASKED FOR MAXIMUM/MINIMUM SUBARRAY/SUBSET/OPTIONS THEN_**

- &nbsp;Dynamic programming

&nbsp;&nbsp;&nbsp;**_IF ASKED FOR TOP/LEAST K ITEMS THEN_**

- &nbsp;Heap
- &nbsp;QuickSelect

&nbsp;&nbsp;&nbsp;**_IF ASKED FOR COMMON STRINGS THEN_**

- &nbsp;Map
- &nbsp;Trie

&nbsp;&nbsp;&nbsp;**_ELSE_**

- &nbsp;Map/Set for O(1) time & O(n) space
- &nbsp;Sort input for O(nlogn) time and O(1) space

<br />
</details>

<details>
    <summary>&nbsp;How to crack LeetCode problems?</summary>

<br />

Source: https://github.com/tiationg-kho/leetcode-pattern-500

- For beginners tackling 0-50 problems, I suggest starting with curated lists like the Blind 75, Grind 75, or NeetCode 150. It's crucial to begin with EASY problems. If you stumble upon unfamiliar concepts, don't hesitate to seek explanations from sources like ChatGPT or the LeetCode discussion section. Aim to accomplish three key objectives during this phase: familiarize yourself with the syntax of common data structures like hashmaps or stacks, gain a holistic understanding of necessary DSA topics, and grasp at least the brute force solution approach, along with basic analyses of time and space complexity for each problem.

- For intermediates solving 50-150 problems, understanding how and why to evolve from brute force to more efficient or optimal solutions is vital. Grasping this transition process is crucial, not just memorizing solutions. At this stage, deeply comprehending the improvement mechanism is the key focus. Often, the breakpoint for a better solution comes from identifying and refining repetitive elements in the old approach.

- After solving over 150 problems, you'll likely have covered around 85% of the topics that could appear in coding interviews. The key at this phase is to recognize patterns across the multitude of problems available. Most questions are variations of a few core concepts or classic problems you've already encountered. Identifying these patterns allows you to apply known solutions to new, seemingly complex problems effectively. Additionally, you should start using different approaches to solve the same problem you already know. For example, if it is a DFS problem, then try both recursive and iterative methods; if it is a DP problem, try both top-down and bottom-up approaches; if it is a top-k problem, then try using a heap or sort. Furthermore, attempt to understand other solutions that use approaches that are not as straightforward as your old solutions. At this stage, it's crucial to recognize recurring patterns across various problems, understanding both the application of consistent approaches to different questions and the exploration of multiple strategies for a single problem. This dual awareness enables a more adaptable and comprehensive problem-solving skill set.
</details>

<details>
    <summary>&nbsp;How to prepare for a coding interview?</summary>
<br />

Source: https://github.com/tiationg-kho/leetcode-pattern-500

During the interview, consistently share your thoughts with the interviewer and use code comments to note down things while speaking. This ensures both of you are aligned.

1. Clarify the requirement of the question. You must truly understand what the question is asking for. Once you understand the question's description, make sure to generate a simple input and expect output other than the given one based on your understanding and ask the interviewer if it is correct or not.

2. Clarify the input and output and edge cases. For instance, ask if the input array is sorted or not, whether numbers can include positives, negatives, or zeros, or if the input contains duplicate elements or not, and how to handle multiple valid answers, whether to return the first one or if outputs need sorting, and what is the expected outcome when there are no valid solutions. Take LC 209. Minimum Size Subarray Sum as example, if numbers in the input array can be negative, the question will become LC 862. Shortest Subarray with Sum at Least K, and will need a totally different approach to solve.

3. Start from a brute force approach, just write some very simple pseudo steps of it. If you have ideas to improve it, then you can continue to explain how and where you can improve and use which DSA or classic pattern (like prefix sum, trie, or two pointers) to solve it. Mention the expected time and space complexity. If you do not have any clue to improve the naive approach, then just ask the interviewer, can we start from implementing this naive approach or not, sometimes you would find out the key point during implementing. If it is not allowed, then try to analyze some common DSA which might be useful here to the interviewer and try to get some feedback or hints from the interviewer. (If brute force is still too hard to get, then try to simulate the whole process in the description of the question or try to enumerate things).

4. Implement the solution, adhering to proper coding style and indentation. If stuck on certain code, ask to finish the main logic first and leave comments for unimplemented parts. If stuck on the main logic, share your thoughts and discuss potential next steps with the interviewer.

5. Final check and dry run. Once finished, do not directly run the code, because there might be some stupid typos in the code. Ask if you can dry run one time, and explain the whole process and your thoughts.

6. Test and debug. Generate 1 or 2 standard cases and 1 or 2 edge cases which are related to the problem. And start testing and debugging. Avoid trial and error multiple times when debugging. Fix the error you find, and try to quickly dry run once and explain why you fix the error.

7. Complexity analysis. Try to analyze the time and space complexity about your solutions and try to mention some potential follow up questions you have thought of. Like what if we change the condition of the input, or what if we have a limitation on time or space usage.

</details>

<details>
    <summary>&nbsp;DSA Topics Importance</summary>
    <p style="display:flex;" align="">
        &nbsp;&nbsp;&nbsp;&nbsp;<img src="./images/dsa_roi.png" width=500 />
    </p>

</details>

<details>
    <summary>&nbsp;Big-O Cheatsheet I</summary>
    <p align="display:flex;">
        &nbsp;&nbsp;&nbsp;<img src="./images/big-o-cheat-sheet-poster.png" width="95%"/>
    </p>
</details>

<details>
    <summary>&nbsp;Big-O Cheatsheet II</summary>
    <p align="">
        &nbsp;&nbsp;&nbsp;<img src="./images/dsa_cheatsheet.png" width="95%" />
    </p>
</details>

## Resources & Tools

### 🧑‍💻 [NeetCode](https://neetcode.com/)

A collection of Leetcode questions organised by topic/pattern and 580 distinct video solutions.

### 🔍 [Leetcode Patterns](https://seanprashad.com/leetcode-patterns/)

It helps to recognise the patterns when solving coding problems found on Leetcode (coding problems are all about pattern recognition and recall). Also, it is recommended to focus on the [most common patterns](https://algo.monster/problems/stats) first.

### 📚 [Tech (SWE) Interview Handbook](https://www.techinterviewhandbook.org/)

A collection of interview preparation materials, which is ideal for last-minute interview prep or quick brush-ups.

Another version is the [Front End Interview Handbook](https://www.frontendinterviewhandbook.com/).

### 🎓 [Grokking the Coding Interview: Patterns for Coding](https://www.designgurus.io/course/grokking-the-coding-interview)

This course expands upon the questions on the recommended practice questions but approaches the practicing from a questions pattern perspective.

#### Related links:

- [dipjul/gcipc-questions](https://github.com/dipjul/Grokking-the-Coding-Interview-Patterns-for-Coding-Questions) ⭐ 2.3k - alternative leetcode questions and summary of patterns - [GitBook](https://dvpr.gitbook.io/coding-interview-patterns)

- [navidre/new_grokking_to_leetcode](https://github.com/navidre/new_grokking_to_leetcode) ⭐ 200 - a list of the closest leetcode problems (related to newer course)

- [tykurtz/grokking_to_leetcode.md](https://gist.github.com/tykurtz/3548a31f673588c05c89f9ca42067bc4) ⭐ 2.3k - a list of the closest leetcode problems (related to older course)

- [AAdewunmi/gcipc-questions](https://github.com/AAdewunmi/Grokking-the-Coding-Interview-Patterns-for-Coding-Questions) ⭐ 20 - notes on patterns + questions & solutions in java

### 🎓 [HelloInterview Guide](https://www.hellointerview.com/learn/code)

A visual guide to the most important patterns and approaches for coding interviews using Python (free alternative to Grokking the Coding Interview).

<details>
<summary>&nbsp;Comparing to HelloAlgo</summary>

- provides only an overview of the concepts (imo still detailed enough)

- uses the concepts in practice by going through problems, which helps to develop the ability to recognise various patterns

- imo, better visualisations due to the interactivity (slider + speed, hiding code)

In addition, the site provides more (paid) services such as [guided practice](https://www.hellointerview.com/practice) and [mock interviews](https://www.hellointerview.com/mock/schedule).

</details>

### 🎓 [HelloAlgo Course](https://www.hello-algo.com/en/)

An open-source (comprehensive) course on DSA providing easy-to-understand animations with code examples in 14 different languages.

### 🤖 [Marble: AI Leetcode Assistant](https://withmarble.io/)

A chrome extension that provides AI-powered interactive walkthroughs for any LeetCode problem.

### [LeetCode Solutions](https://leetcode.ca/)

### [Python DSA Cheatsheet](https://github.com/AbdulMalikDev/PythonCheatSheet)

## Articles

### Coding

#### Patterns

- [tiationg-kho/leetcode-pattern-500](https://github.com/tiationg-kho/leetcode-pattern-500)

- [Grokking LeetCode: A Smarter Way to Prepare for Coding Interviews](https://interviewnoodle.com/grokking-leetcode-a-smarter-way-to-prepare-for-coding-interviews-e86d5c9fe4e1)

- [Don't Just LeetCode; Follow the Coding Patterns Instead](https://levelup.gitconnected.com/dont-just-leetcode-follow-the-coding-patterns-instead-4beb6a197fdb)

- [AlgoMaster: LeetCode was HARD until I Learned these 15 Patterns](https://blog.algomaster.io/p/15-leetcode-patterns)

#### Questions

- [Dynamic Programming Patterns](https://leetcode.com/discuss/general-discussion/458695/Dynamic-Programming-Patterns)

- [List of questions sorted by common patterns](https://leetcode.com/discuss/career/448285/List-of-questions-sorted-by-common-patterns)

### System Design

- [System Design Interview Survival Guide (2024): Preparation Strategies and Practical Tips](https://levelup.gitconnected.com/system-design-interview-survival-guide-2023-preparation-strategies-and-practical-tips-ba9314e6b9e3)
