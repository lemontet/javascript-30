# Array.prototype.sort()

## Key points
* Sort mutates the existing array
* Sort converts array elements into strings
* Sort doesn't require an argument, but will accept one
* If no function is supplied as an argument, all non-undefined elements are converted to strings and compared according to their UTF-16 (2 byte) code units
* If supplied, the argument must be a 'sort' function which expects two arguments for comparison: a (first element) and b (second element)
* If the comparison returns < 0, sort switches a to an index lower than b 
* If the comparison returns > 0, sort switches b to an index lower than a
* If the comparison returns 0, sort leaves a and b unchanged with respect to each other, but sorts them among the rest of the array elements (see bugs section for more on this)
* undefined elements are sorted to the back of the array
* Sort uses a sorting method called 'bubble sort'

---

## Opportunity for bugs
* The ECMAscript standard does not support sorting 0, but some browsers will. It's handy to remember that this behaviour is not supported in all browsers. If you intend to use it, you might need a polyfill.
* The comparison function must always return the same value given a specific pair of elements and arguments. If it doesn't, then the sort order is undefined.

## A note on string comparison
* JavaScript uses 'simple lexicographic ordering on sequences of code unit values'. It doesn't attempt to use 'more complex, semantically oriented definitions of character or string equality'. This means JS doesn't think 'a' and 'A' are equivalent. It doesn't go to any extra effort to infer equality. Therefore, it's wise to use something like compareLocale() to help set rules about what chars you consider to be 'equal'. See Note 2: https://tc39.github.io/ecma262/#sec-abstract-relational-comparison

---

## Quiz yourself
**Q: What is the result of [100, 9].sort()?**  
**A:** [9, 100]

**Q: What is the result of [undefined, 16, 'a']?**  
**A:** [16, 'a', undefined]

**Q: How can I sort alphabetically?**  
**A:** Pass sort a custom function which returns `a.localeCompare(b)`

**Q: How can I sort reverse alphabetically?**  
**A:** The same as above, but do the reverse: `b.localeCompare(a)`

**Q: How can I sort numbers?**  
**A:** Supply a comparison function which return `a - b` for ascending order, or `b - a` for descending order.

**Q: I sorted my array. Now I can't compare it with the original. Why?**  
**A:** Sort mutates the existing array. You need to copy the unsorted array and sort it if you want to keep a copy of both. To copy the array, you can use `array.slice()`

**Q: I sorted my array, but React didn't updated the component on the page. Why?**  
**A:** React doesn't know if you update a global variable. When you sort data and want to display it, you need to trigger an action which updates the state and tells React to re-render.

**Q: If my comparison function returns 8, how will sort order a and b?**  
**A:** b will be moved to an index lower than a

**Q: What happens if an array contains infinity or NaN?**  
**A:** NaN will always in place. Infinity will be sorted to the back of the array.

**Q: What does 'a' > 'b' return? Why?**  
**A:** false. Because JavaScript looks at the character codes of the strings.
