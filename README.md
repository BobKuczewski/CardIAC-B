# CardIAC and CardIAC-B

## Introduction

The CardIAC computer was created by David Hagelbarger at Bell Labs in the early
1960's. At that time, real computers were very expensive and very rare. So David
Hagelbarger designed a *Card*board *I*llustrative *A*id to *C*omputation named
"CardIAC". The "computer" was printed and distributed for educational use, and
fortunately some have survived to this day (see ...).

This project implements the CardIAC computer using "virtual cardboard" made of
images that can be slid up and down just like the original CardIAC computer. The
project is implemented in Javascript within an HTML file so it should run in
practically every modern web browser. This Javascript version is technically
named "CardIAC-B" because it has some small differences from the original
Bell Labs cardboard "CardIAC" computer. But those differences are relatively
minor, and most of the documentation will use the terms "CardIAC" and
"CardIAC-B" interchangably.

## "Paper" Version

![Screen Shot](/CardIAC_at_Startup.png?raw=true "Startup Screen")

## Simple Programming Example 1 - Add two numbers

Start by picking two numbers to add. We'll use 14 and 28 (following the
example by Ben Eater at https://youtu.be/35zLnS3fXeA).

Click on the word "INPUT" in the lower left corner of the screen and a
pop-up box should appear. The pop-up box will ask for all input values
separated by spaces. Enter "14 28" and click OK. Those two numbers should
appear at the bottom of the "INPUT" slider. The input numbers may be
partially obscured, but you can click and drag on the slider (above the
input area) to see both numbers in the INPUT window. Leave it set to
showing position number 1 (which should be 14).

Next begin entering a program. The program will need storage space
(addresses) for our two input values. We can pick almost any of the 100
available memory cell addresses. It's sometimes convenient to start with
51 since that's half-way through the available memory and happens to start
with a "1" and is in the top row. So let's assign the first input value
to be stored at 51 and the second to be stored at 52.

Now that we have our addresses we can write our first line of code. We will
want to load the first input card into memory cell 51. The instruction to do
that is "IN 51". In "machine code" that will be "051" (where 0 is the input
instruction, and 51 is the memory cell to get the value. Let's put that
instruction in Memory Cell 00. Click on the yellow rectangle at cell 00 and
you will get a prompt "Enter a value for memory cell 0". Type in "051" and
click OK. That's our first line of code!

We could try to "run" it at this point, but let's add 1 more instruction first.
Let's add the similar instruction to load the second input value into memory
cell 52. The mnemonic instruction would be "IN 52", and the machine code to
enter is "052". Click the yellow rectangle in Memory Cell 01, and enter "052"
into the popup dialog and click "OK".

Now we have 2 instructions that will load (and consume) our two input cards
and put them into memory locations 51 and 52. Let's try to "run" it.

Start by making sure that the "bug" is in memory location zero. If not, click
the small circle ("hole") at memory location zero to move the bug to the starting
point. Now we begin following the "flow" graph near the center of the "computer".
Find the word "START" and follow the instructions in the "INSTRUCTION REGISTER"
above it. The instruction register says "MOVE SLIDES TO AGREE WITH CONTENTS OF
BUG'S CELL". The contents of the bug's cell are our first instruction (051).
So the "OP CODE" slider should be slid up or down until the first digit in the
"INSTRUCTION REGISTER" is a 0. In this case, just slide the "OP CODE" instruction
all the way down until the 0 appears. Similarly slide the "HI ADDR" and "LO ADDR"
sliders until "051" appears in the "INSTRUCTION REGISTER". Doing this is essentially
the "fetch" portion of a normal computer. Before it can do anything, it needs to
"fetch" the first instruction from memory.

Now that the first instruction has been "fetched" into the "INSTRUCTION REGISTER",
the processor must follow that instruction. In CardIAC, that means following the
arrows of the flow diagram. The "INSTRUCTION REGISTER" only has one arrow leaving
it, and it goes to the next step which is "MOVE BUG AHEAD ONE CELL". This simulates
the advance of the program counter for a normal processor. Go ahead and click on
the small round "hole" for Memory Cell 01. The "bug" should move forward to that hole.

After moving the "bug" forward (advancing the program counter), the flow diagram
points upward to the instructions in the "ACCUMULATOR TEST" window. In this case
(for instructions starting with 0) the "ACCUMULATOR TEST" window asks "INPUT CARD BLANK?".
If you've been following along, the "INPUT" window should be showing "014" which was
the first of our two numbers to add. So the "INPUT CARD" is NOT blank. So we take the
"NO" path from the "ACCUMULATOR TEST" question.

The arrow from the "NO" path of the "ACCUMULATOR TEST" question leads upward to an
instruction that says "COPY INPUT CARD INTO CELL 51 AND ADVANCE CARD". So that's what
you'll do. You can see that the input card contains "14" so click on Memory Cell 51
and enter "14" and then click "OK". The number 14 should appear in Cell 51. But don't
forget the second part of that instruction: "ADVANCE CARD". In other words, slide the
"INPUT" slider downward (click and drag on the upper part of the slider) until the
second value (28) appears in the INPUT window.

After advancing the card, follow the arrow downward and back to the "INSTRUCTION REGISTER".
Now the first instruction has been completed and it's time to fetch the next instruction.
The instruction register (again) says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL".
The contents of the bug's cell should be "052" (the second instruction of our grand program).
In this case, the sliders should aleady be at "051" so only the "LO ADDR" slider needs to
be changed from "1" to "2". This completes the "fetch" of the second instruction into the
"INSTRUCTION REGISTER". Now we need to follow this newly loaded second instruction.

Following the second instruction will be nearly identical to the first. As before, we'll
move the bug ahead one memory cell (leaving it on cell 02). As before we'll check if the
INPUT CARD is blank, and again it isn't (it contains 28). Since it's not empty, we'll again
follow the "NO" path of the flow diagram up to the top where it tells us to
"COPY INPUT CARD INTO CELL 52 AND ADVANCE CARD". That's nearly identical to what we did
before, and we can see that the input card is now 28. So we click on the yellow rectangle
for Memory Cell 52 and enter the number 28 and click "OK". We also advance the input card
again by sliding it down to show position 3 (which should be empty). Now we've completed
the execution of our second instruction, and we're ready to fetch the next instruction.

At this point, we have followed 2 instructions. We've moved the values from 2 input "cards"
into 2 locations in memory. But the instruction pointer (the "bug") is now pointing to an
empty cell. In a real computer, there are no empty cells. Every location in memory always
has *something* in it. Each bit will be either a 0 or a 1. But in CardIAC any "undefined"
memory locations (and input cards) will be empty. But that turns out to be handy in this
case because we can continue to write instructions while the "computer" is on hold waiting
to fetch the next instruction (that isn't there yet).

Now that we have our two input values in memory, we can write a few more instructions to
add them together. This is where the "Accumulator" comes in. Most computers have one (or more)
internal registers that can serve as "accumulators" where values can be loaded or manipulated.
In CardIAC, values can be loaded into the Accumulator from memory, and values can be added to
the Accumulator from memory. Those two steps are done with instructions "LD" (for loading) and
"ADD" (for adding). So we will want to load one of our values into the accumulator and then
add the other of our values into the accumulator. It doesn't matter which comes first (at least
for adding), so let's load from memory location 51 and then add from memory location 52. The
load from 51 instruction is "151", and the add from 52 instruction is "252". Click on the
memory cells "02" and "03" and add the instructions "151" and "252" respectively.

We've just written two new instructions while the computer was waiting to execute them. So
let's get back to where the computer left off.

The computer was just getting ready to "fetch" the next instruction at Memory Cell 02. There
had been no instruction there before, but we've just added two of them so we can return to the
"INSTRUCTION REGISTER" and once again "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The
bug's cell now shows 151, so move the sliders to show 151 in the "INSTRUCTION REGISTER".
Following the flow diagram out the left side of the "INSTRUCTION REGISTER" the next thing for
the computer to do is "MOVE BUG AHEAD ONE CELL". So click the small round "hole" on Memory
Cell 03 to move the bug forward.

Now the flow diagram leads upward to the instructions that tell us to "COPY CONTENTS OF CELL 51
INTO ACCUMULATOR". So we look at Memory Cell 51 and see that it contains "014" (14). So we click
on the numbers in the "ACCUMULATOR" (likely all 0's) and that will bring up a dialog box asking
"Enter a value for the accumulator:". Type in "14" and click "OK". The "ACCUMULATOR" should now
show the number "14". We can now follow the flow diagram back to the "INSTRUCTION REGISTER" for
our next "fetch" cycle.

Again, the INSTRUCTION REGISTER tells us to "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL".
The bug's cell is currently showing "252" so we adjust the sliders to show "252" in the
"INSTRUCTION REGISTER". In this case, both the "OP CODE" slider and the "ADDR LO" slider will
need to be moved.

Now that the computer has "fetched" the next instruction ("252") it's time to execute it.
Following the flow diagram out the left side of the "INSTRUCTION REGISTER" we find that we must
again move the bug ahead one cell. So click the small "hole" on Memory Cell 04 to advance the bug.
Then follow the flow diagram up to the top where it says "ADD CONTENTS OF CELL 52 INTO ACCUMULATOR".
Since the value in cell 52 is "28" and the value in the ACUMULATOR is "14", the sum of those would be 42.
So we need to put "42" into the ACCUMULATOR. Once again click on the ACCUMULATOR and enter "42" in the
pop-up dialog, and click OK.

At this point, it might seem that we're done, but not yet. We have summed the values into the accumulator,
but that's deep inside the computer. In a real computer we would not see the 1's and 0's representing
"42" inside the chip. So the computer still needs to send that result to some output device (screen,
printer, disk drive, voice reader, ...) where we can make use of it. For CardIAC, the only "output"
device is the "OUTPUT" card slider. So we'll need to add instructions to produce that output.

Now we scan the list of instructions (shown on the CardIAC computer) and we see that instruction "5" is
"OUT". It says that it will "Output a Memory Value". But our value (42) isn't in memory. It's in the
accumulator. So before we can "output" it, we'll need to move it into memory. So far we've used memory
locations 51 and 52. We could actually re-use either of them at this point (since we're done with them),
and in a very tight memory budget, that's exactly what we might do. But for clarity, let's save the
output in memory location 53, and then output from 53. So we will need to store ("STO") from the
Accumulator into memory location 53, and then we'll need to output ("OUT") from memory location 53.
The "STO 53" instruction will be "653" and the "OUT 53" command will be "553" (see the instruction
table on the computer). So click on memory cells "04" and "05" and enter "653" and "553" respectively.

As before, the computer has been patiently waiting while we added some more instructions for it to
follow. So now we're ready to pick up where it left off. We're looking at the "INSTRUCTION REGISTER"
and we see that it again says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The bug's cell
currently shows the instruction "653" so adjust the sliders to show "653" in the instruction window.
In this case you'll need to move the "OP CODE" slider and the "ADDR LO" slider. Once the new instruction
("653") is in the INSTRUCTION REGISTER, the flow diagram reminds us to "MOVE BUG AHEAD ONE CELL", so
click on the round "hole" for Memory Cell 05 to move the "bug". Then follow the flow diagram up to the
line that tells you to "COPY ACCUMULATOR TO CELL 53". You'll notice that the ACCUMULATOR shows "42" so
click on the yellow rectangle in memory cell 53 and type in "42" and click "OK".

Once again the flow diagram brings us back to the "INSTRUCTION REGISTER" where we will again "fetch"
the next instruction by "MOVING SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". In this case, the bug's
cell contains the instruction "553" so only the "OP CODE" slider needs to be moved (from 6 to 5).
Now we follow the flow diagram to the left where it again tells us to "MOVE BUG AHEAD ONE CELL".
So we click on the round "hole" for Memory Cell 06 to move the "bug". Then we follow the arrow up to
where it says "COPY CONTENTS OF CELL 53 TO OUTPUT, ADVANCE". We can see that cell 53 contains the
number 42 (our answer), so we click on the "OUTPUT" box and enter "42" into the pop-up dialog box and
click "OK". This puts the number 42 into the output slider, and then we advance the output slider by
sliding it downward to make room for the next output (which we won't have in this case).

Now we're surely done, right? Well, not quite. We should still do one more thing. After the computer
produces the output, we need to explicitly tell it to stop. In our case (because this is a human-powered
computer), the computer "stops" whenever we stop moving sliders and clicking tabs. But in a real computer,
it would continue to follow whatever random values were in memory as if they were instructions. So it's
important to always provide some means to stop the computer (or "loop" the computer) to keep it out of
trouble. In the case of CardIAC-B there's an explicit halt instruction ("HLT") that stops the computer
and resets the "bug" to any desired location so it's ready to run again. In most cases, this means putting
the "bug" back to memory location 0 so it can run the same program again. The "HLT" instruction has an
"op code" of 9, and we want it to be stopped at memory location 00, so the instruction would be "900".
So click on the yellow rectangle in memory cell 06 and enter "900" into the pop-up dialog box and click "OK".

Now we can run the final "HLT" instruction. As before, we pick up where we left off - ready to fetch the
next instruction (that we just wrote). The INSTRUCTION REGISTER reminds us to "MOVE SLIDES TO AGREE WITH
CONTENTS OF BUG'S CELL". The bug's cell is currently "900" so all three slides ("Op Code", "Addr Hi",
and "Addr Lo") will need to be changed. As always, after "fetching" this instruction, the bug should be
moved forward one cell (to 07 in this case). Then following the flow diagram to the top we find that it
says "MOVE BUG TO CELL 00 STOP". So we click on the "hole" for memory cell 00 to move the bug and we
can finally ... stop.

