## Part 1 - Bugs

### ListExamples.java filter() bug

### Failure Inducing Input:
```
@Test 
	public void testFilter() {
        List<String> input = new ArrayList<>();
        input.add("Eric");
        input.add("Jose");
        input.add("Brandon");
        List<String> result = new ArrayList<>();
        result.add("Eric");
        result.add("Jose");
        assertArrayEquals(ListExamples.filter(input, new ListExamples()).toArray(), result.toArray());
	}
```

### Input that does not induce failure:
```
@Test
    public void testFilter2() {
        List<String> input = new ArrayList<>();
        input.add("Eric");
        List<String> result = new ArrayList<>();
        result.add("Eric");
        assertArrayEquals(ListExamples.filter(input, new ListExamples()).toArray(), result.toArray());
    }
```

### The symptom:
![Image](symptom.png)

### The bug:

Before:
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s); //the bug before
      }
    }
    return result;
}
```

After:
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(s); //the bug fixed
      }
    }
    return result;
}
```
The bug is fixed by changing `result.add(0, s);` to `result.add(s);`. In the bugged code, elements are added to the front of `result`, which does not keep the same order as `list` for sizes greater than 1. The fix makes it so elements are added to the back of `result`, which keeps the proper order.
