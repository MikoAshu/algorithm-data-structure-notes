# Arrays

Array data structure is a collection of elements where elements are stored in contagious memory locations. As such, looking up elements is quick as searching elements will be a matter of doing some operation to a base value

## Key Words

Almost always, an array question will be denoted by an **array** keyword

### Notes

If, we need to compare two values, two pointers might be a good approach

If the array is sorted, we can use a two pointers approach

if the array is not sorted and we need to compare two values, we can still use two pointers under the condition that the values contain other information that we care about like the index - checkout the question [leetcode 11 - container with most water](leetcode-11-container-with-most-water.md)

Since arrays have a defined size, sum or difference type questions will have some kind of pattern like e.g  the sum total - left sum - current element will give some kind of value that is the same computed from left and right (no need for two arrays) see question [leetcode 724 - find pivot index](leetcode-724-find-pivot-index.md)
