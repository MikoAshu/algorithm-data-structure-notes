# Summary of Questions

[https://leetcode.com/discuss/study-guide/1688903/Solved-all-two-pointers-problems-in-100-days.](https://leetcode.com/discuss/study-guide/1688903/Solved-all-two-pointers-problems-in-100-days.)

Hello,\
I have been solving all two pointers tagged problems in last 3.5 months, and wanted to share my findings/classifications here. If you are preparing for technical interview, two pointers is one of the popular topics that you can't skip :).

There are around 140 problems today, but I only solved the public ones (117 problems).\
Majority of them is in easy or medium so, if you understand the basic ideas then it should be solvable without much hints and editorials.

I see 4 bigger categories and many sub categories in it, and marked the typical example problems with (\*).\
I would recommend you to start solving these example problems, and apply the knowledge to the other problems. I don't want to copy & paste my ugly codes here, you would easily find fantastic solutions from the problem discussion page.

\


The first type of problems are, having two pointers at left and right end of array, then moving them to the center while processing something with them.\
![image](https://assets.leetcode.com/users/images/83674944-3be0-4974-b7a8-e59319b896c7\_1642138224.1528904.jpeg)

* 2 Sum problem\
  (\*) [https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)\
  [https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/)\
  [https://leetcode.com/problems/4sum/](https://leetcode.com/problems/4sum/)\
  [https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/](https://leetcode.com/problems/number-of-subsequences-that-satisfy-the-given-sum-condition/)\
  [https://leetcode.com/problems/two-sum-iv-input-is-a-bst/](https://leetcode.com/problems/two-sum-iv-input-is-a-bst/)\
  [https://leetcode.com/problems/sum-of-square-numbers/](https://leetcode.com/problems/sum-of-square-numbers/)\
  [https://leetcode.com/problems/boats-to-save-people/](https://leetcode.com/problems/boats-to-save-people/)\
  [https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array/)\
  [https://leetcode.com/problems/3sum-with-multiplicity/](https://leetcode.com/problems/3sum-with-multiplicity/)
* Trapping Water\
  (\*) [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)\
  [https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)
* Next Permutation\
  (\*) [https://leetcode.com/problems/next-permutation/](https://leetcode.com/problems/next-permutation/)\
  [https://leetcode.com/problems/next-greater-element-iii/](https://leetcode.com/problems/next-greater-element-iii/)\
  [https://leetcode.com/problems/minimum-adjacent-swaps-to-reach-the-kth-smallest-number/](https://leetcode.com/problems/minimum-adjacent-swaps-to-reach-the-kth-smallest-number/)
* Reversing / Swapping\
  [https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)\
  (\*) [https://leetcode.com/problems/reverse-string/](https://leetcode.com/problems/reverse-string/)\
  [https://leetcode.com/problems/reverse-vowels-of-a-string/](https://leetcode.com/problems/reverse-vowels-of-a-string/)\
  [https://leetcode.com/problems/valid-palindrome-ii/](https://leetcode.com/problems/valid-palindrome-ii/)\
  [https://leetcode.com/problems/reverse-only-letters/](https://leetcode.com/problems/reverse-only-letters/)\
  [https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/)\
  [https://leetcode.com/problems/sort-colors/](https://leetcode.com/problems/sort-colors/)\
  [https://leetcode.com/problems/flipping-an-image/](https://leetcode.com/problems/flipping-an-image/)\
  [https://leetcode.com/problems/squares-of-a-sorted-array/](https://leetcode.com/problems/squares-of-a-sorted-array/)\
  [https://leetcode.com/problems/sort-array-by-parity/](https://leetcode.com/problems/sort-array-by-parity/)\
  [https://leetcode.com/problems/sort-array-by-parity-ii/](https://leetcode.com/problems/sort-array-by-parity-ii/)\
  [https://leetcode.com/problems/pancake-sorting/](https://leetcode.com/problems/pancake-sorting/)\
  [https://leetcode.com/problems/reverse-prefix-of-word/](https://leetcode.com/problems/reverse-prefix-of-word/)\
  [https://leetcode.com/problems/reverse-string-ii/](https://leetcode.com/problems/reverse-string-ii/)\
  [https://leetcode.com/problems/reverse-words-in-a-string/](https://leetcode.com/problems/reverse-words-in-a-string/)\
  [https://leetcode.com/problems/reverse-words-in-a-string-iii/](https://leetcode.com/problems/reverse-words-in-a-string-iii/)
* Others\
  [https://leetcode.com/problems/bag-of-tokens/](https://leetcode.com/problems/bag-of-tokens/)\
  [https://leetcode.com/problems/di-string-match/](https://leetcode.com/problems/di-string-match/)\
  [https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/](https://leetcode.com/problems/minimum-length-of-string-after-deleting-similar-ends/)\
  [https://leetcode.com/problems/sentence-similarity-iii/](https://leetcode.com/problems/sentence-similarity-iii/)\
  [https://leetcode.com/problems/find-k-closest-elements/](https://leetcode.com/problems/find-k-closest-elements/)\
  [https://leetcode.com/problems/shortest-distance-to-a-character/](https://leetcode.com/problems/shortest-distance-to-a-character/)

\


Next type is using two pointers with different speed of movement. Typically they starts from the left end, then the first pointer advances fast and give some feedback to the slow pointer and do some calculation.\
![image](https://assets.leetcode.com/users/images/f6ecb6b1-679e-48f9-91b5-de4602436865\_1642138215.8872066.jpeg)

* Linked List Operations\
  (\*) [https://leetcode.com/problems/linked-list-cycle/](https://leetcode.com/problems/linked-list-cycle/)\
  [https://leetcode.com/problems/linked-list-cycle-ii/](https://leetcode.com/problems/linked-list-cycle-ii/)\
  [https://leetcode.com/problems/remove-nth-node-from-end-of-list/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)\
  [https://leetcode.com/problems/rotate-list/](https://leetcode.com/problems/rotate-list/)\
  [https://leetcode.com/problems/reorder-list/](https://leetcode.com/problems/reorder-list/)\
  [https://leetcode.com/problems/palindrome-linked-list/](https://leetcode.com/problems/palindrome-linked-list/)
* Cyclic Detection\
  (\*) [https://leetcode.com/problems/find-the-duplicate-number/](https://leetcode.com/problems/find-the-duplicate-number/)\
  [https://leetcode.com/problems/circular-array-loop/](https://leetcode.com/problems/circular-array-loop/)
* Sliding Window/Caterpillar Method\
  ![image](https://assets.leetcode.com/users/images/29d2e356-77fe-4caf-8921-7a39d06e56d2\_1642139764.6173265.jpeg)\
  (\*) [https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/](https://leetcode.com/problems/number-of-subarrays-with-bounded-maximum/)\
  [https://leetcode.com/problems/find-k-th-smallest-pair-distance/](https://leetcode.com/problems/find-k-th-smallest-pair-distance/)\
  [https://leetcode.com/problems/moving-stones-until-consecutive-ii/](https://leetcode.com/problems/moving-stones-until-consecutive-ii/)\
  [https://leetcode.com/problems/count-pairs-of-nodes/](https://leetcode.com/problems/count-pairs-of-nodes/)\
  [https://leetcode.com/problems/count-binary-substrings/](https://leetcode.com/problems/count-binary-substrings/)\
  [https://leetcode.com/problems/k-diff-pairs-in-an-array/](https://leetcode.com/problems/k-diff-pairs-in-an-array/)
* Rotation\
  (\*) [https://leetcode.com/problems/rotating-the-box/](https://leetcode.com/problems/rotating-the-box/)\
  [https://leetcode.com/problems/rotate-array/](https://leetcode.com/problems/rotate-array/)
* String\
  (\*) [https://leetcode.com/problems/string-compression/](https://leetcode.com/problems/string-compression/)\
  [https://leetcode.com/problems/last-substring-in-lexicographical-order/](https://leetcode.com/problems/last-substring-in-lexicographical-order/)
* Remove Duplicate\
  (\*) [https://leetcode.com/problems/remove-duplicates-from-sorted-array/](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)\
  [https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)\
  [https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)\
  [https://leetcode.com/problems/duplicate-zeros/](https://leetcode.com/problems/duplicate-zeros/)
* Others\
  [https://leetcode.com/problems/statistics-from-a-large-sample/](https://leetcode.com/problems/statistics-from-a-large-sample/)\
  [https://leetcode.com/problems/partition-labels/](https://leetcode.com/problems/partition-labels/)\
  [https://leetcode.com/problems/magical-string/](https://leetcode.com/problems/magical-string/)\
  [https://leetcode.com/problems/friends-of-appropriate-ages/](https://leetcode.com/problems/friends-of-appropriate-ages/)\
  [https://leetcode.com/problems/longest-mountain-in-array/](https://leetcode.com/problems/longest-mountain-in-array/)\
  [https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)

\


In this category, you will be given 2 arrays or lists, then have to process them with individual pointers.\
![image](https://assets.leetcode.com/users/images/2a44123b-9acb-4dbc-b230-d313a37039c9\_1642138206.7972002.jpeg)

* Sorted arrays\
  (\*) [https://leetcode.com/problems/merge-sorted-array/](https://leetcode.com/problems/merge-sorted-array/)\
  [https://leetcode.com/problems/heaters/](https://leetcode.com/problems/heaters/)\
  [https://leetcode.com/problems/find-the-distance-value-between-two-arrays/](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/)
* Intersections/LCA like\
  (\*) [https://leetcode.com/problems/intersection-of-two-linked-lists/](https://leetcode.com/problems/intersection-of-two-linked-lists/)\
  [https://leetcode.com/problems/intersection-of-two-arrays/](https://leetcode.com/problems/intersection-of-two-arrays/)\
  [https://leetcode.com/problems/intersection-of-two-arrays-ii/](https://leetcode.com/problems/intersection-of-two-arrays-ii/)
* SubString\
  (\*) [https://leetcode.com/problems/implement-strstr/](https://leetcode.com/problems/implement-strstr/)\
  [https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/)\
  [https://leetcode.com/problems/long-pressed-name/](https://leetcode.com/problems/long-pressed-name/)\
  [https://leetcode.com/problems/longest-uncommon-subsequence-ii/](https://leetcode.com/problems/longest-uncommon-subsequence-ii/)\
  [https://leetcode.com/problems/compare-version-numbers/](https://leetcode.com/problems/compare-version-numbers/)\
  [https://leetcode.com/problems/camelcase-matching/](https://leetcode.com/problems/camelcase-matching/)\
  [https://leetcode.com/problems/expressive-words/](https://leetcode.com/problems/expressive-words/)
* Median Finder\
  (\*) [https://leetcode.com/problems/find-median-from-data-stream/](https://leetcode.com/problems/find-median-from-data-stream/)
* Meet-in-the-middle / Binary Search\
  (\*) [https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/](https://leetcode.com/problems/partition-array-into-two-arrays-to-minimize-sum-difference/)\
  [https://leetcode.com/problems/closest-subsequence-sum/](https://leetcode.com/problems/closest-subsequence-sum/)\
  [https://leetcode.com/problems/ways-to-split-array-into-three-subarrays/](https://leetcode.com/problems/ways-to-split-array-into-three-subarrays/)\
  [https://leetcode.com/problems/3sum-closest/](https://leetcode.com/problems/3sum-closest/)\
  [https://leetcode.com/problems/valid-triangle-number/](https://leetcode.com/problems/valid-triangle-number/)
* Others\
  [https://leetcode.com/problems/shortest-unsorted-continuous-subarray/](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/)\
  [https://leetcode.com/problems/most-profit-assigning-work/](https://leetcode.com/problems/most-profit-assigning-work/)\
  [https://leetcode.com/problems/largest-merge-of-two-strings/](https://leetcode.com/problems/largest-merge-of-two-strings/)\
  [https://leetcode.com/problems/swap-adjacent-in-lr-string/](https://leetcode.com/problems/swap-adjacent-in-lr-string/)

\


The last one is similiar to previous category but there is one thing is added. First, you need to split the given list into 2 separate lists and then do two pointers approach to merge or unify them. There aren't many tasks here.\
![image](https://assets.leetcode.com/users/images/1d3c2ed7-95ca-440d-9693-f3e31360b826\_1642138190.9125686.jpeg)

* Partition\
  (\*) [https://leetcode.com/problems/partition-list/](https://leetcode.com/problems/partition-list/)
* Sorting\
  (\*) [https://leetcode.com/problems/sort-list/](https://leetcode.com/problems/sort-list/)
