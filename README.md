# CardIAC
Implementations of "Computers" based on the CardIAC and similar machines

## "Paper" Version

![Screen Shot](/CardIAC_at_Startup.png?raw=true "Startup Screen")

## Simple Programming Example 1 - Add two numbers

Start by picking two numbers to add. We'll use 14 and 28 (following the example by Ben Eater at https://youtu.be/35zLnS3fXeA).

Click on the word "INPUT" in the lower left corner of the screen and a pop-up box should appear. The pop-up box will ask for all input values separated by spaces. Enter "14 28" and click OK. Those two numbers should appear at the bottom of the "INPUT" slider. The input numbers may be partially obscured, but you can click and drag on the slider (above the input area) to see both numbers in the INPUT window. Leave it set to showing card 1 (which should be 14).

Next begin entering a program. The program will need storage space (addresses) for our two input values. We can pick almost any of the 100 available memory cell addresses. It's sometimes convenient to start with 51 since that's half-way through the available memory and happens to start with a "1" and is in the top row. So let's assign the first input value to 51 and the second to 52.

Now that we have our addresses we can write our first line of code. We will want to load the first input card into memory cell 51. The instruction to do that is "IN 51". In "machine code" that will be "051" (where 0 is the input instruction, and 51 is the memory cell to get the value. Let's put that instruction in Memory Cell 00. Click on the yellow rectangle at cell 51 and you will get a prompt "Enter a value for memory cell 0". Type in "051" and click OK. That's our first line of code!

We could try to "run" it at this point, but let's add 2 more instructions first. Let's add the similar instruction to load the second input pard into memory cell 52. The mnemonic instruction would be "IN 52", and the machine code to enter is "052". Click the yellow rectangle in Memory Cell 01, and enter "052" into the popup dialog and click "OK".

Now we have 2 instructions that will load (and consume) our two input cards and put them into memory locations 51 and 52. Let's try to "run" it.

Start by making sure that the "bug" is in memory location zero. If not, click the small circle at memory location zero to move the bug to the starting point. Now we begin following the "flow" graph near the center of the "computer". Find the word "START" and follow the instructions in the "INSTRUCTION REGISTER" above it. The instruction register says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The contents of the bug's cell are our first instruction (051). So the "OP CODE" slider should be slid up or down until the first digit in the "INSTRUCTION REGISTER" is a 0. In this case, just slide the "OP CODE" instruction all the way down until the 0 appears. Similarly slide the "HI ADDR" and "LO ADDR" sliders until "051" appears in the "INSTRUCTION REGISTER". Doing this is essentially the "fetch" portion of a normal computer. Before it can do anything, it needs to "fetch" the first instruction from memory.

Now that the first instruction has been "fetched" into the "INSTRUCTION REGISTER", the processor must follow that instruction. In CardIAC, that means following the arrows of the flow diagram. The "INSTRUCTION REGISTER" only has one arrow leaving it, and it goes to the next step which is "MOVE BUG AHEAD ONE CELL". This simulates the advance of the program counter for a normal processor. Go ahead and click on the small round "hole" for Memory Cell 01. The "bug" should move forward to that hole.

After moving the "bug" forward (advancing the program counter), the flow diagram points upward to the instructions in the "ACCUMULATOR TEST" window. In this case (for instructions starting with 0) the "ACCUMULATOR TEST" window asks "INPUT CARD BLANK?". If you've been following along, the "INPUT" window should be showing "014" which was the first of our two numbers to add. So the "INPUT CARD" is NOT blank. So we take the "NO" path from the "ACCUMULATOR TEST" question.

The arrow from the "NO" path of the "ACCUMULATOR TEST" question leads upward to an instruction that says "COPY INPUT CARD INTO CELL 51 AND ADVANCE CARD". So that's what you'll do. You can see that the input card contains "14" so click on Memory Cell 51 and enter "14" and then click "OK". The number 14 should appear in Cell 51. But don't forget the second part of that instruction: "ADVANCE CARD". In other words, slide the "INPUT" slider downward (click and drag on the upper part of the slider) until the second value (28) appears in the INPUT window.

After advancing the card, follow the arrow downward and back to the "INSTRUCTION REGISTER". Now the first instruction has been completed and it's time to fetch the next instruction. The instruction register (again) says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The contents of the bug's cell should be "052" (the second instruction of our grand program). In this case, the sliders should aleady be at "051" so only the "LO ADDR" slider needs to be changed from "1" to "2". This completes the "fetch" of the second instruction into the "INSTRUCTION REGISTER". Now we need to follow this newly loaded second instruction.

Following the second instruction will be nearly identical to the first. As before, we'll move the bug ahead one memory cell (leaving it on cell 02). As before we'll check if the INPUT CARD is blank, and again it isn't (it contains 28). Since it is not empty, we'll follow the "NO" path of the flow diagram up to the top where it tells us to "COPY INPUT CARD INTO CELL 52 AND ADVANCE CARD". That's nearly identical to what we did before, and we can see that the input card is now 28. So we click on the yellow rectangle for Memory Cell 52 and enter the number 28 and click "OK". We also advance the input card again by sliding it down to show position 3 (which should be empty). Now we've completed the execution of our second instruction, and we're ready to fetch the next instruction.

At this point, we have followed 2 instructions. We've moved the values from 2 input "cards" into 2 locations in memory. But the instruction pointer (the "bug") is now pointing to an empty cell. In a real computer, there are no empty cells. Every location in memory always has *something* in it. Each bit will be either a 0 or a 1. But in CardIAC any "undefined" memory locations (and input cards) will be empty. But that turns out to be handy in this case because we can continue to write instructions while the "computer" is on hold waiting to fetch the next instruction (that isn't there yet).

Now that we have our two input values in memory, we can write a few more instructions to add them. This is where the "Accumulator" comes in. Most computers have one (or more) internal registers that can serve as "accumulators" where values can be loaded or manipulated. In CardIAC, values can be loaded into the Accumulator from memory, and values can be added to the Accumulator from memory. Those two steps are done with instructions "LD" (for loading) and "ADD" (for adding). So we will want to load one of our values into the accumulator and then add the other of our values into the accumulator. It doesn't matter which comes first (at least for adding), so let's load from memory location 51 and then add from memory location 52. That gives us these two instructions:

LD 51
ADD 52

