## Part 1: Bugs
The bug I'm choosing to focus on is in `reverseInPlace` shown below:
```
static void reverseInPlace(int[] arr) {  
	for(int i = 0; i < arr.length; i += 1) {  
 	arr[i] = arr[arr.length - i - 1];  
  }
```
1. A failure inducing input for the buggy program:
```
@Test
public void testReverseInPlace2() {
	int[] input1 = {1,2,3,4};
	int[] input2 = {4,3,2,1};
	ArrayExamples.reverseInPlace(input1);
	assertArrayEquals(input2, input1);
}
```
3. An input that doesn't induce a failure:
```
@Test
public void testReverseInPlace() {
	int[] input1 = { 3 };
	ArrayExamples.reverseInPlace(input1);
	assertArrayEquals(new int[]{ 3 }, input1);
}
```
5. The symptom, as the output of running the tests:
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/eaf4d13e-f25c-43ae-be26-1d115ca2b7b7)
![image](https://github.com/divine9223/cse15l-lab-reports/assets/147002921/9508914c-f3d4-4c6a-a885-9ac7172d7c26)

6. The bug before:
```
static void reverseInPlace(int[] arr) {
	for(int i = 0; i < arr.length; i += 1) {
	arr[i] = arr[arr.length - i - 1];
	}
}
```
The bug fixed:
```
static void reverseInPlace(int[] arr) {
	for(int i = 0; i < (arr.length/2); i++){
		int hold = arr[i];
		arr[i] = arr[arr.length-i-1];
		arr[arr.length-i-1] = hold;
	}
}
```
Fixes the issue of overwriting the original value which switches the later values to the new element instead of the original one. The new code swaps the indexes so that it doesn't get overwritten.

## Part 2: Researching Commands
The command I chose to foccus on is grep.
1. grep -c pattern [files]
```
$ grep -c "health" 1468-6708-3-1.txt
44
```
Searching through `1468-6708-3-1.txt` and is looking for "health" it outputs the number of lines where "health" was found. Helpful in trying to finding the count of the number of lines of the pattern.
```
$ grep -c "plane" chapter-1.txt
71
```
Looks through `chapter-1.txt` and finds every line that the pattern "plane" is on and outputs that. Helpful in trying to finding the count of the number of lines of the pattern.

3. grep -i pattern [files]
```
$ grep -i "three" chapter-2.txt
respected Islamic authority, but neither Bin Ladin, Zawahiri, nor the three others
Three months later, when interviewed in Afghanistan by ABC-TV, Bin Ladin enlarged on
Three basic themes emerge from Qutb's writings. First, he claimed that the world was
Twenty-three when he arrived in Afghanistan in 1980, Bin Ladin was the seventeenth of
When the Sudanese refused to hand over three individuals identified as involved in
```
Searches through `chapter-2.txt` and finds any variation in capital letters for the pattern "three" and prints that. Helpful in making the search case insensitive.
```
$ grep -i "time" 1468-6708-3-3.txt
elevation more than three times the upper limit of normal
Time to change current practice
MIRACL, these agents are safe when initiated at the time of
```
Looks through `1468-6708-3-3.txt` and finds any variation in capital letters for the pattern "time" and prints those lines. Helpful in making the search case insensitive.

5. grep -n pattern [files]
```
$ grep -n "bias" 1468-6708-3-4.txt
17:        subject to a potential bias. This review attempts to raise
231:        treatment group separately. The bias seen in the medical
241:        to a biased result. The approaches in (a) and (b) take this
243:        biased by over-correction.
266:        biased to a certain extent. Had the authors given the
397:          bias it introduces if the assumption of stability does
404:          treatment effects will be less biased. Since PI does less
405:          imputation, it is less biased than LOCF because the
496:        study, bias can only be reduced but not entirely eliminated
```
Searches through `1468-6708-3-4.txt` and finds the lines in which the pattern "bias" is found and prints the entire line out, including the line number. Helpful in finding the pattern easily in the text due to the line number being printed out.
```
$ grep -n "Yousef" chapter-3.txt
33:                Ramzi Yousef, the Sunni extremist who planted the bomb, said later that he had hoped 
48:                and charged with document fraud. His traveling companion was Ramzi Yousef, who had
50:                admitted. It quickly became clear that Yousef had been a central player in the
67:                Salameh, Ayyad, Abouhalima, the Blind Sheikh, and Ramzi Yousef, for crimes related
73:                Blind Sheikh and Ramzi Yousef behind bars would really protect Americans against the
84:                April 1992 to go there to learn how to construct bombs. He had met Ramzi Yousef in
90:            Yousef was captured in Pakistan following the discovery by police in the Philippines
93:                Mohammed-Yousef 's uncle, then located in Qatar-was a fellow plotter of Yousef 's in
111:                evidence of Yousef 's technical ingenuity. Yet the public image that persisted was
112:                not of clever Yousef but of stupid Salameh going back again and again to reclaim his
2483:                    'Abd al-Rahman, Ramzi Yousef, and Muhammad Sadiq 'Awda. One source quoted a
```
Looks through `chapter-3.txt` and finds the lines in which the pattern "Yousef" is found and prints the entire line, including the line number, out. Helpful in finding the pattern easily in the text due to the line number being printed out, in this case it found the lines in which a specific person was mentioned.

7. grep -o pattern [files]
```
$ grep -o "car bombing" chapter-5.txt
car bombing
```
Searches through `chapter-5.txt`, finds the pattern "car bombing", prints only the matched substrings corresponding to the pattern. Helpful in extracting certain patterns in a large text. In this case, found the certain instance of "car bombing" in comparison to "plane bombing".
```
$ grep -o "doxazosin arm" 1468-6708-3-7.txt
doxazosin arm
doxazosin arm
doxazosin arm
```
Looks through `1468-6708-3-7.txt`, finds the pattern "doxazosin arm", prints only the matched substrings corresponding to the pattern. Helpful in extracting certain patterns in a large text. In this case, found the certain instance of "doxazosin arm" in comparison to "doxazosin".

###All options were found in the following URL:
https://www.geeksforgeeks.org/grep-command-in-unixlinux/
