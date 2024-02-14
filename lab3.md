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


---


## Part 2 - Researching Commands

### `find`

For the following, I used this [resource](https://www.redhat.com/sysadmin/linux-find-command) to help guide me.

---

#### `find / -type f`

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
Here, we find all the files in the directory `./government/Post_Rate_Comm/`.

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

This is useful to see all the files in a certain directory. We can also change the `-type` option from `f` to `d` to see all the directories within a certain directory.

---

#### `find / -name "*.txt"`

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Env_Prot_Agen/ -name "*.txt"
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
Here, we find and list all the files with a `.txt` extension in the directory `./government/Env_Prot_Agen/`.

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Post_Rate_Comm/ -name "*.txt"
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
Here, we find and list all the files with a `.txt` extension in the directory `./government/Post_Rate_Comm/`.

This is useful to find all the files in a certain directory with a certain filename extension. For example, we can find all the `.java` files in a directory or `.txt` files as seen in the above examples.

---

#### `find / -mtime -7`

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Post_Rate_Comm/ -mtime -7
./government/Post_Rate_Comm/
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
Here, we find all the files that were last modified within the last week in the directory `./government/Post_Rate_Comm/`.

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Env_Prot_Agen/ -mtime -7
./government/Env_Prot_Agen/
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
Here, we find all the files that were last modified within the last week in the directory `./government/Env_Prot_Agen/`.

This is useful because we can find which files were updated within the last X days in a certain directory. We can also change the `-7` to `+7` to find files modified more than a week ago.

---

#### `find / -type f -empty`

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Env_Prot_Agen/ -type f -empty
```
Here, we try to find all the empty files in the directory `./government/Env_Prot_Agen/`. Since none of the files are empty in `./government/Env_Prot_Agen/`, nothing is printed out.

```
19252@wangomen MINGW64 ~/docsearch/technical (main)
$ find ./government/Post_Rate_Comm/ -type f -empty
```
Here, we try to find all the empty files in the directory `./government/Post_Rate_Comm/`. Since none of the files are empty in `./government/Post_Rate_Comm/`, nothing is printed out.

This is useful because if we want to look for an empty file in a certain directory, we can use this command. We can also find empty directories by changing the `-type` option to `d` instead of `f`.
