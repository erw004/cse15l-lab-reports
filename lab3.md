## Part 1 - Bugs

### `ListExamples.java` `filter()` bug

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



## Part 2 - Researching Commands

### `find`

#### `find /path/to/search -type f`

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Post_Rate_Comm/ -type f
./government/Post_Rate_Comm/Cohenetal_comparison.txt
./government/Post_Rate_Comm/Cohenetal_Cost_Function.txt
./government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt
./government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt
./government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt
./government/Post_Rate_Comm/Cohenetal_Scale.txt
./government/Post_Rate_Comm/Gleiman_EMASpeech.txt
./government/Post_Rate_Comm/Gleiman_gca2000.txt
./government/Post_Rate_Comm/Mitchell_6-17-Mit.txt
./government/Post_Rate_Comm/Mitchell_RMVancouver.txt
./government/Post_Rate_Comm/Mitchell_spyros-first-class.txt
./government/Post_Rate_Comm/Redacted_Study.txt
./government/Post_Rate_Comm/ReportToCongress2002WEB.txt
./government/Post_Rate_Comm/WolakSpeech_usps.txt
```
Here, we find all the files in the directory `./government/Post_Rate_Comm/`. This is useful to see all the files in a certain directory. We can also change the `-type` option from `f` to `d` to see all the directories within a certain directory.

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Env_Prot_Agen/ -type f
./government/Env_Prot_Agen/1-3_meth_901.txt
./government/Env_Prot_Agen/atx1-6.txt
./government/Env_Prot_Agen/bill.txt
./government/Env_Prot_Agen/ctf1-6.txt
./government/Env_Prot_Agen/ctf7-10.txt
./government/Env_Prot_Agen/ctm4-10.txt
./government/Env_Prot_Agen/final.txt
./government/Env_Prot_Agen/jeffordslieberm.txt
./government/Env_Prot_Agen/multi102902.txt
./government/Env_Prot_Agen/nov1.txt
./government/Env_Prot_Agen/ro_clear_skies_book.txt
./government/Env_Prot_Agen/section-by-section_summary.txt
./government/Env_Prot_Agen/tech_adden.txt
./government/Env_Prot_Agen/tech_sectiong.txt
```
Here is another example of the same command, but instead we are using the command on the directory `./government/Env_Prot_Agen/`. We see all the files in `./government/Env_Prot_Agen/`.
