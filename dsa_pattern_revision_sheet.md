# DSA Pattern Revision Sheet


## <span style="color:orange"> 1. Arrays & Hashing </span>

### When to use

-   Need fast lookup, membership checks, counting, grouping, or
    detecting duplicates.
-   Need to relate values to their frequencies or previously seen
    positions.
-   A nested-loop comparison can potentially be replaced with a lookup.

### How to identify it

-   Ask: **Am I repeatedly searching the array for a value?**
-   Ask: **Do I need to remember what I have already seen?**
-   Ask: **Does the answer depend on counts, duplicates, or
    value-to-index mapping?**
-   If yes, consider a `HashSet` or `HashMap`.

### Clues in the question

-   "Duplicate", "unique", "frequency", "count", "anagram".
-   "Find a pair" or "does a complement exist?"
-   "Group words/items by a common property".
-   "First/repeated occurrence" or "seen before".
-   "Top K frequent" may combine frequency counting with a heap or
    bucket sort.

### Common techniques

-   **HashSet:** membership and duplicate detection.
-   **HashMap:** value → count, index, or other associated information.
-   **Frequency map/array:** count occurrences; use an array when the
    value range is small and known.
-   **Complement lookup:** for target `T` and current value `x`, look
    for `T - x`.
-   **Canonical key:** sort a string or build a frequency signature to
    group equivalent items.
-   **One-pass lookup:** check the needed prior value, then store the
    current value. This avoids using the same element twice in pair
    problems.

### Questions to recognize

-   Contains Duplicate → set.
-   Valid Anagram → character frequencies.
-   Two Sum → complement lookup.
-   Group Anagrams → canonical key/frequency signature.
-   Top K Frequent Elements → frequency map + heap or bucket sort.
-   Product of Array Except Self → prefix/suffix products (no division
    when required).
-   Valid Sudoku → sets or frequency tracking per row, column, and box.
-   Longest Consecutive Sequence → set; start counting only at sequence
    starts.

### Common traps / checks

-   Clarify whether duplicates are allowed and whether indices must be
    distinct.
-   Check empty input, one element, negative values, and repeated
    values.
-   Avoid assuming values fit in a small frequency array unless
    constraints guarantee it.
-   For `HashMap`, distinguish missing key from a key mapped to
    zero/null when relevant.
-   Hashing usually gives expected `O(1)` lookup, not guaranteed
    worst-case `O(1)`.

### Complexity reminders

-   One pass with hash lookup: expected `O(n)` time, `O(n)` space.
-   Sorting to create a key: commonly `O(k log k)` per item of length
    `k`.

------------------------------------------------------------------------

## <span style="color:orange"> 2. Two Pointers</span>

### When to use

-   Need to compare or process elements from two positions.
-   Input is sorted, or the problem has a structure that allows one
    pointer to move safely.
-   Need an in-place operation or want to avoid nested-loop pair
    checking.
-   A contiguous range or pair can be narrowed by moving boundaries.

### How to identify it

-   Ask: **Can I start at both ends and eliminate impossible choices?**
-   Ask: **If I move one pointer, can I prove I won't miss a valid
    answer?**
-   Ask: **Does sorting make the relationship between values
    predictable?**
-   Do not use two pointers just because the input is an array; justify
    each pointer movement.

### Clues in the question

-   "Sorted array", "pair/triplet", "target sum".
-   "Palindrome", "reverse", "from both ends".
-   "In-place", "remove duplicates", "move elements".
-   "Container", "maximum area", or choosing between left/right
    boundaries.
-   "Subsequence" or comparing two sequences can suggest two pointers,
    depending on the exact requirement.

### Common variations and movement rules

-   **Opposite-direction pointers:** start at left and right; move the
    pointer whose value/side can improve or eliminate candidates.
-   **Same-direction read/write pointers:** one scans; the other marks
    where the next kept/valid element belongs.
-   **Fast/slow pointers:** move at different speeds to detect cycles or
    find a middle.
-   **Sorted pair sum:** if sum is too small, move left up; if too
    large, move right down.
-   **Three Sum:** sort, fix one value, then use opposite-direction
    pointers for the remaining pair.
-   **Container With Most Water:** move the shorter boundary; the taller
    boundary cannot be the limiting side after keeping the shorter one.

### Questions to recognize

-   Valid Palindrome → compare from both ends.
-   Two Sum II → sorted pair sum.
-   3Sum → sort + fixed index + two pointers.
-   Container With Most Water → opposite ends; move shorter height.
-   Trapping Rain Water → two boundaries + running maximums; process the
    side with the smaller known maximum.
-   Remove Duplicates from Sorted Array → read/write pointers.
-   Linked List Cycle → fast/slow pointers.

### Common traps / checks

-   State the pointer invariant: what does each pointer represent?
-   Explain why moving a particular pointer is safe; don't move pointers
    by intuition alone.
-   For sorted pair sum, account for duplicates if unique pairs are
    required.
-   In `3Sum`, skip duplicate fixed values and duplicate pointer values.
-   Check pointer crossing, empty input, one element, and all-equal
    values.
-   Be careful with off-by-one conditions: `left < right` versus
    `left <= right`.

### Complexity reminders

-   Two-pointer scan after sorting: typically `O(n log n)` total due to
    sorting, then `O(n)` scan.
-   Two-pointer scan on already sorted input: often `O(n)` time and
    `O(1)` extra space.
-   Fast/slow linked-list traversal: `O(n)` time and `O(1)` extra space.

------------------------------------------------------------------------

## <span style="color:orange"> 3. Stack </span>

### When to use

-   Need the most recent unresolved item first (LIFO).
-   Need to match nested structures or reverse the order of processing.
-   Need the next/previous greater or smaller element.
-   A decision for an earlier element becomes clear when a later element
    arrives.

### How to identify it

-   Ask: **Does the newest item need to be handled before older items?**
-   Ask: **Are there opening/closing pairs or nested expressions?**
-   Ask: **Does a new value resolve the answer for previous values?**
-   For next/previous greater/smaller questions, consider a **monotonic
    stack**.

### Clues in the question

-   "Valid parentheses", "matching brackets", "nested".
-   "Next greater/smaller", "previous greater/smaller".
-   "Daily temperatures", "stock span", "largest rectangle".
-   "Evaluate expression", "decode", or undo/reverse-like processing.
-   "Remove adjacent duplicates" can use a stack because the latest item
    may interact with the previous one.

### Common variations and techniques

-   **Basic stack:** push opening/unresolved items; pop when matched or
    resolved.
-   **Monotonic increasing stack:** maintain increasing values (or
    indices); pop while the new value violates the order.
-   **Monotonic decreasing stack:** maintain decreasing values; pop
    while the new value violates the order.
-   **Store indices, not just values:** needed to calculate distance,
    width, or access the original array.
-   **Sentinel:** add a boundary value or process one extra iteration to
    flush remaining stack items, when appropriate.
-   **Expression evaluation:** use stacks for operators/operands,
    respecting precedence and parentheses.

### Questions to recognize

-   Valid Parentheses → push opening brackets; match on closing
    brackets.
-   Min Stack → maintain current minimum alongside values.
-   Evaluate Reverse Polish Notation → operand stack.
-   Generate Parentheses → backtracking (not a stack-first problem).
-   Daily Temperatures → monotonic decreasing stack of indices.
-   Car Fleet → sort by position; compare arrival times; stack can
    represent fleet times, but one variable is enough.
-   Largest Rectangle in Histogram → monotonic increasing stack of
    indices.
-   Car Fleet II → monotonic stack with collision-time reasoning.

### Common traps / checks

-   Decide whether the stack stores values or indices.
-   Define the monotonic direction and the exact pop condition (`<`,
    `<=`, `>`, `>=`).
-   Equal values matter: choose strict/non-strict comparison based on
    whether equal elements should remain.
-   After the scan, check whether unresolved elements need processing.
-   For bracket matching, reject a closing bracket when the stack is
    empty and check the stack is empty at the end.
-   Check empty input and cases with all increasing, all decreasing, or
    equal values.

### Complexity reminders

-   Many monotonic-stack algorithms are `O(n)` because each item is
    pushed and popped at most once.
-   A stack may use `O(n)` extra space.

------------------------------------------------------------------------

## <span style="color:orange"> 3. Binary Search </span>

### When to use

- Need to search in a sorted array or data structure.
- Need to find the first/last occurrence, insertion position, or a boundary.
- Need to find the minimum or maximum value satisfying a condition.
- The search space has a monotonic property: once a condition becomes true/false, it stays that way.
- Can eliminate half of the possible search space at each step.

### How to identify it

- Ask: **Am I searching in sorted data?**
- Ask: **Can I eliminate half of the search space based on a comparison?**
- Ask: **Does a condition change monotonically from false to true or true to false?**
- Ask: **Am I looking for an exact value, a boundary, or an optimal answer?**
- If yes, consider binary search.

### Clues in the question

- "Sorted array", "search", "target".
- "First occurrence", "last occurrence", "lower bound", "upper bound".
- "Minimum possible maximum" or "maximum possible minimum".
- "Smallest value that satisfies a condition".
- "Find the minimum in a rotated sorted array".
- "Search in a rotated sorted array".
- "Can we solve this in logarithmic time?"
- A problem where trying a candidate value gives a predictable true/false result.

### Common techniques

- **Exact search:** Search for a target in a sorted range.
- **Lower bound:** Find the first element greater than or equal to the target.
- **Upper bound:** Find the first element strictly greater than the target.
- **Boundary search:** Find the first true or last true position in a monotonic condition.
- **Binary search on answer:** Search over possible answers instead of array indices; use a feasibility check.
- **Rotated array search:** Identify the sorted half and decide which half can contain the target.
- **Duplicates in rotated arrays:** When boundaries are equal, shrink the search space because the sorted half may be ambiguous.

### Questions to recognize

- Binary Search → exact search.
- Search Insert Position → lower bound.
- Find First and Last Position → lower and upper bound.
- Search in Rotated Sorted Array → modified binary search.
- Find Minimum in Rotated Sorted Array → find rotation point.
- Search a 2D Matrix → binary search on flattened sorted data.
- Koko Eating Bananas → binary search on answer.
- Capacity to Ship Packages Within D Days → binary search on answer.
- Time Based Key-Value Store → binary search on timestamps.
- Median of Two Sorted Arrays → partition-based binary search.

### Common traps / checks

- Choose the correct range convention: inclusive `[left, right]` or half-open `[left, right)`.
- Match the loop condition to the range: `left <= right` for inclusive exact search; `left < right` for typical half-open or boundary search.
- Avoid infinite loops when using `left = mid`; use upper midpoint when necessary.
- Use `left + (right - left) / 2` to avoid midpoint overflow for non-negative indices.
- For binary search on answer, clearly define the feasibility condition and prove it is monotonic.
- For minimum feasible answer, move `right = mid` when feasible.
- For maximum feasible answer, use upper midpoint and move `left = mid` when feasible.
- In rotated arrays, verify which half is sorted before eliminating a half.
- With duplicates, equality may prevent identifying the sorted half; shrinking boundaries can degrade complexity to `O(n)`.
- Check empty input, one element, target outside the range, and duplicate values.
- Always verify what the final `left` or `right` represents.

### Complexity reminders

- Standard binary search: `O(log n)` time, `O(1)` extra space.
- Recursive binary search: `O(log n)` time, `O(log n)` stack space.
- Binary search on answer: `O(log R × C)` time, where `R` is the search-space size and `C` is the cost of the feasibility check.
- Rotated array search with distinct values: `O(log n)` time.
- Rotated array search with duplicates: typically `O(log n)`, worst case `O(n)`.

------------------------------------------------------------------------

## <span style="color:orange"> 4. Sliding Window </span>

### When to use

- Need to process a contiguous subarray or substring.
- Need to find the maximum/minimum sum, length, or number of elements in a window.
- Need to find the longest or shortest substring satisfying a condition.
- Need to calculate something repeatedly over adjacent ranges.
- Can maintain window information incrementally instead of recalculating it from scratch.

### How to identify it

- Ask: **Am I working with a contiguous subarray or substring?**
- Ask: **Can I expand the window by moving the right pointer?**
- Ask: **Can I shrink the window by moving the left pointer?**
- Ask: **Can I maintain the required information as elements enter and leave the window?**
- Ask: **Does the problem ask for the longest, shortest, maximum, or minimum window?**
- If yes, consider sliding window.

### Clues in the question

- "Longest substring" or "shortest substring".
- "Maximum sum of a subarray of size K".
- "Minimum window containing all characters".
- "At most K distinct characters".
- "Without repeating characters".
- "Contiguous subarray" or "contiguous substring".
- "Find the maximum/minimum in every window of size K".
- "Find the number of subarrays satisfying a condition".

### Common techniques

- Fixed-size window: Window size remains constant. Add the new element and remove the element leaving the window.
- Variable-size window: Expand the right pointer and shrink the left pointer whenever the window violates a condition.
- Longest valid window: Expand the window, shrink while invalid, and update the maximum length.
- Smallest valid window: Expand until the condition is satisfied, then shrink while the window remains valid.
- Frequency map: Maintain character or element frequencies inside the current window.
- Running sum: Maintain the sum by adding the incoming element and subtracting the outgoing element.
- Sliding window + HashMap: Track frequencies, distinct elements, or required character counts.
- Sliding window + Monotonic Deque: Maintain maximum or minimum values efficiently inside a fixed-size window.
- Prefix sum + Sliding Window: Useful in certain counting problems where a simple sliding window cannot maintain the required condition.

### Questions to recognize

- Maximum Average Subarray I → fixed-size window.
- Maximum Sum Subarray of Size K → fixed-size window.
- Longest Substring Without Repeating Characters → variable-size window + HashSet/HashMap.
- Longest Repeating Character Replacement → variable-size window + frequency tracking.
- Permutation in String → fixed-size window + character frequencies.
- Find All Anagrams in a String → fixed-size window + frequency tracking.
- Minimum Window Substring → variable-size window + frequency map.
- Sliding Window Maximum → fixed-size window + monotonic deque.
- Minimum Size Subarray Sum → variable-size window.
- Subarray Product Less Than K → variable-size window with positive numbers.

### Common traps / checks

- Sliding window generally works on contiguous ranges, not arbitrary subsequences.
- Identify whether the window size is fixed or variable.
- For variable-size windows, clearly define what makes the window valid or invalid.
- When shrinking, remove the outgoing element's contribution from the window state.
- Update the answer at the correct point: before or after shrinking, depending on the problem.
- Be careful with duplicate characters and frequency counts.
- Do not assume a variable-size sliding window works when negative numbers are present; the required monotonic behavior may break.
- For longest valid window, shrink until valid before updating the maximum.
- For smallest valid window, update the minimum while the window is valid, then shrink.
- Check empty input, one element, window size equal to array length, and window size greater than array length.
- For frequency maps, remove keys when their frequency becomes zero if needed.
- For sliding window maximum, remove indices outside the current window and maintain deque ordering.

### Complexity reminders

- Fixed-size sliding window: typically `O(n)` time, `O(1)` extra space.
- Variable-size sliding window: typically `O(n)` time because each pointer moves at most `n` times.
- Sliding window with HashMap/HashSet: typically `O(n)` time, `O(k)` space, where `k` is the number of tracked distinct elements.
- Sliding window maximum with monotonic deque: `O(n)` time, `O(k)` extra space, where `k` is the window size.
- Recalculating every window from scratch can take `O(n × k)` time; maintaining window state can reduce it to `O(n)`.

------------------------------------------------------------------------