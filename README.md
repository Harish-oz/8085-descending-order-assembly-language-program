8085 microprocessor assembly language program to sort numbers in ascending order.



; Program: Bubble Sort (descending order → big to small)

MVI B, 05H        ; B = number of passes
                  ; We repeat passes so every element gets chance to move
                  ; Each pass pushes the smaller values toward the end

LP2: MVI C, 05H   ; C = comparisons per pass
                  ; We compare adjacent elements step by step

     LXI H, 3000H ; HL points to start of array
                  ; Needed to traverse elements in memory

LP1: MOV A, M     ; Load current element into A
                  ; A is required because CMP works with accumulator

     INX H        ; Move to next element
                  ; Now HL points to next item

     MOV D, M     ; Store next element in D
                  ; D acts as temporary holder

     CMP D        ; Compare A with D (A - D internally)
                  ; We check which one is bigger

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

      HLT         ; Stop execution


Descending order means arranging numbers from largest → smallest.
👉 Example:
Plain text
Unsorted:  3, 9, 1, 5  
Sorted:    9, 5, 3, 1
🧠 Core Idea
Look at two neighboring numbers
If left < right → swap
If left ≥ right → leave it
Repeat this again and again.
⚙️ What actually happens
Bigger numbers move toward the left
Smaller numbers get pushed to the right
After multiple passes → everything becomes sorted
📌 Example
Plain text
Start: 3, 9, 1, 5

Compare 3 & 9 → swap → 9, 3, 1, 5  
Compare 3 & 1 → ok  
Compare 1 & 5 → swap → 9, 3, 5, 1  

Next pass → keep fixing wrong pairs
Final → 9, 5, 3, 1
