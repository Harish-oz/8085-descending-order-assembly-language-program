Here is the assembly language program to sort numbers in descending order for microprocessor 8085.
<br><br>
```
MVI B, 05H        ; B is number of passes, We repeat passes so every element gets chance to move
                  ; Each pass pushes the smaller values toward the end

LP2: MVI C, 05H   ; C is comparisons per pass, We compare adjacent elements step by step
     LXI H, 3000H ; Enter the numbers here

LP1: MOV A, M     ; Load current element into A
     INX H        ; Move to next element
                  ; Now HL points to next item
     MOV D, M     ; Store next element in D (for temporary storage)
     CMP D        ; Compare A with D,we check which one is bigger
     JNC SKIP     ; If A >= D → correct order for descending
                  ; Bigger value is already on left → no swap needed
     MOV M, A     ; If A < D → wrong order
                  ; Move bigger value (A) forward temporarily
     DCX H        ; Go back to previous position
                  ; Needed to complete swap
     MOV M, D     ; Place bigger value before smaller one
                  ; Now correct descending order achieved
     INX H        ; Restore pointer for next comparison

SKIP: DCR C       ; Reduce comparison count
      JNZ LP1     ; Continue until all pairs in this pass are checked
      DCR B       ; Reduce pass count
      JNZ LP2     ; Repeat passes until fully sorted

      HLT         ; Stop
```
<br><br><br>
**Explaination**<br>
Descending order means arranging numbers from largest → smallest.<br>
For example<br>
Unsorted:  3, 9, 1, 5<br>
Sorted:    9, 5, 3, 1<br>
<br><br>
Look at two neighboring numbers<br>
If left < right → swap<br>
If left ≥ right → leave it<br>
<br>
Repeat this again and again.<br>
Bigger numbers move toward the left and the smaller numbers get pushed to the right. After multiple passes → everything becomes sorted.<br>
<br><br>
**For Example**<br>
Start: 3, 9, 1, 5<br>
Compare 3 & 9 → swap → 9, 3, 1, 5<br>
Compare 3 & 1 → ok<br>
Compare 1 & 5 → swap → 9, 3, 5, 1<br>
<br>
Next pass → keep fixing wrong pairs<br>
Final → 9, 5, 3, 1<br>
