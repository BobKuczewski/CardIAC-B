# CardIAC and CardIAC-B

## Introduction

The CardIAC computer was created by David Hagelbarger at Bell Labs in the early
1960's. At that time, real computers were very expensive and very rare. So David
designed a ***Card***board ***I***llustrative ***A***id to ***C***omputation named
"CardIAC". The "computer" was printed (on cardboard) and distributed for educational use.
Fortunately some of these have survived to this day (see extensive documentation by Brian
Stuart in the [CardIAC section of his computer museum](https://www.cs.drexel.edu/~bls96/museum/cardiac.html)).
There are also CardIAC resources available on line at [Wikipedia](https://en.wikipedia.org/wiki/CARDboard_Illustrative_Aid_to_Computation)
and even a "print it yourself" version at [Instructables](https://www.instructables.com/CARDIAC-CARDboard-Illustrative-Aid-to-Computation-/).

This project implements the CardIAC computer using "virtual cardboard" made of
images that can be slid up and down just like the original CardIAC computer. This
project is implemented in Javascript within an HTML file so it should run in
most modern web browsers. This Javascript version is technically named "CardIAC-B"
because it has some small differences from the original Bell Labs cardboard "CardIAC"
computer. But those differences are relatively minor, and most of this documentation
will use the terms "CardIAC" and "CardIAC-B" interchangably. The numeric instruction
set is identical and all CardIAC programs should run identically on CardIAC-B. There
are also a number of other CardIAC-like simulations that use the CardIAC instruction set
or slight variants. For example, the "Instructional Manual for CardIAC" makes several
references a machine called "SIMCO" which uses the same 10 "binary" (actually decimal)
instructions.

## ["Virtual Cardboard" Version](https://bobkuczewski.github.io/CardIAC-B/)

![Screen Shot](/images/CardIAC_at_Startup.png?raw=true "Startup Screen")

## Using CardIAC-B

This repository only contains a few files. There is one HTML file, one "README" file
(the source of this page) and several image files in the "images" directory. The HTML
file contains the Javascript that loads the images and provides for input, output,
and movement of the images on the page.
Simply download those files to any location on your computer and open the only HTML
file (index.html) with a web browser (usually by double clicking on it). That
should bring up a page similar to the image above. Then follow along with the example
below or any of the examples available on the Internet. Alternatively, you can
also click on **[this link](https://bobkuczewski.github.io/CardIAC-B/)** to open
an on-line version of CardIAC-B. It's best to move that page to a separate
browser window so you can easily switch between these instructions and that
computer simulation.

## CardIAC and CardIAC-B Instruction Sets

The CardIAC "computer" itself only understands 10 basic instructions. These 10
basic instructions are represented as 3 decimal digits per instruction. The first
digit specifies the **type** of instruction (add, load, store, shift, jump, ...).
The last two digits are **parameters** describing what specific data to use for the
instruction.

As with most computers, the "processor" itself only understands these numeric instructions.
However, people generally prefer to think in words rather than numbers. So people
tend to assign a different word or abbreviation to each **type** of numeric instruction.
That allows people to write programs using familiar words and abbreviations rather than
numbers. Then, when a program has been written in words, it can be translated into the numbers
that the computer itself understands. The numerical representation of each instruction
is often called "**machine code**". The people-friendly version is
often called "**assembly code**". So people generally write computer programs in
"assembly code" (or "assembly language") and translate it to "machine code" either
by hand or using another computer program called an "assembler". Then the machine
code can be entered into the computer.

It's important to note that the people-friendly "assembly language" does not need
to be unique for a given instruction set. Different "assembler" programs could convert
different people-friendly instruction words into the same resulting "machine code". There
are, for example, at least two different "assembly languages" for the popular "x86" processor (see
**[Wikipedia x86 Assembly Language article](https://en.wikipedia.org/wiki/X86_assembly_language)**).
The same is true for CardIAC and its variants. The following table lists all 10 instructions
of the CardIAC machine language ("Machine Code") followed by the original CardIAC
instruction name, the CardIAC-B instruction name, and the instruction's description:

| Machine&nbsp;Code | CardIAC | CardIAC&#8209;B | Description |
| :----------- | :---------: | :-----------: | :---------- |
| **0**MM      | **INP**&nbsp;MM  | **IN**&nbsp;MM     | Read an input card into memory location MM and advance the card |
| **1**MM      | **CLA**&nbsp;MM  | **LD**&nbsp;MM     | Load a value from memory location MM into the accumulator |
| **2**MM      | **ADD**&nbsp;MM  | **ADD**&nbsp;MM    | Add the contents of memory location MM to accumulator |
| **3**MM      | **TAC**&nbsp;MM  | **JLZ**&nbsp;MM    | Jump to location MM if the accumulator is less than zero |
| **4**XY      | **SFT**&nbsp;XY  | **SHF**&nbsp;XY    | Shift accumulator left by X digits and then shift it right by Y digits |
| **5**MM      | **OUT**&nbsp;MM  | **OUT**&nbsp;MM    | Print the contents of memory location MM to output card and advance the card |
| **6**MM      | **STO**&nbsp;MM  | **STO**&nbsp;MM    | Store the contents of the accumulator into memory location MM |
| **7**MM      | **SUB**&nbsp;MM  | **SUB**&nbsp;MM    | Subtract the contents of memory location MM from the accumulator |
| **8**MM      | **JMP**&nbsp;MM  | **JMP**&nbsp;MM    | Jump to memory location MM and store previous location into memory location 99 |
| **9**MM      | **HRS**&nbsp;MM  | **HLT**&nbsp;MM    | Halt machine and reset program counter to MM |

The "MM" in most of these instructions stands for a 2 digit memory address which can range from 00 to 99.

## Simple Programming Example - Add two numbers (the hard way)

This tutorial will walk you through writing and executing a simple program
to add two numbers using CardIAC-B. Most of the important controls are
exercised in this "short" demonstration. Since the "CardIAC" computer is
always in "single step" mode, this demonstration will involve writing
portions of the code, executing the portions already written, and then
adding more code and resuming execution. Before you begin, open either your
downloaded version or **[this page](https://bobkuczewski.github.io/CardIAC-B/)**
in another browser window. Arrange that window (as well as you can) so you can
follow these instructions while still seeing that other window as
large as possible. If needed, you can slide most of the "Memory Cells" off
the right edge of your screen since this tutorial mostly uses the left side of
the memory cells (51 and lower). You might even print these instructions on paper
so that you can view the other window in full-screen mode.

### Pick two numbers and enter them on the "INPUT Card"

Start by picking two numbers to add. We'll use 14 and 28 (following the
example by Ben Eater at https://youtu.be/35zLnS3fXeA).

Click on the word "INPUT" in the lower left corner of the screen. A
pop-up box should appear. The pop-up box will ask for all input values
separated by spaces. Enter "14 28" and click OK. Those two numbers should
appear at the bottom of the "INPUT" slider. The input numbers may be
partially obscured, but you can click and drag on the slider (anywhere
but in the input area) to see both numbers in the INPUT window. Leave it
set to showing position number 1 (which should be 14).

### Allocating Storage for Variables

Next we'll begin entering a program to add the two numbers. The program will
need storage space (addresses) for those two input values. We can pick almost
any of the 100 available memory cell addresses. It's sometimes convenient to start
with 51 since that's half-way through the available memory and happens to start
with a "1" (easy to remember) and is on the top row. So let's assign the
first input value to be stored at 51 and the second to be stored at 52.

### First "Line" of Code

Now that we have our addresses we can write our first line of code. We will
want to load the first input card into memory cell 51. The instruction to do
that is "IN 51". In "machine code" that will be "051" (where 0 is the input
instruction, and 51 is the memory cell to put the value). Let's put that
instruction in Memory Cell 00. Click on the yellow rectangle at cell 00 and
you will get a prompt that says "Enter a value for memory cell 0". Type in
"051" and click OK. That's our first line of code!

### Second "Line" of Code

We could try to "run" it at this point, but let's add 1 more instruction first.
Let's add the similar instruction to load the second input value into memory
cell 52. The mnemonic instruction would be "IN 52", and the machine code to
enter is "052". Click the yellow rectangle in Memory Cell 01, and enter "052"
into the popup dialog and click "OK".

Now we have 2 instructions that will load (and consume) our two input cards
and put them into memory locations 51 and 52. Let's try to "run" it.

### "Running" the First Program - Fetch Portion of First Instruction

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
the "fetch" portion of a normal computer instruction cycle. Before it can do anything,
a computer needs to "fetch" its first instruction (and all subsequent instructions)
from memory.

### "Running" the First Program - Execute portion of First Instruction

Now that the first instruction has been "fetched" into the "INSTRUCTION REGISTER",
the processor must follow that instruction. In CardIAC, that means following the
arrows of the flow diagram. The "INSTRUCTION REGISTER" only has one arrow leaving
it, and it goes to the next step which is "MOVE BUG AHEAD ONE CELL". This simulates
the advance of the program counter for a normal processor. Go ahead and click on
the small round "hole" for Memory Cell 01. The "bug" should move forward to that hole.
Advancing the "bug" (program counter) will be the first step in executing any
instruction on this computer.

After moving the "bug" forward (advancing the program counter), the flow diagram
points upward to the instructions in the "ACCUMULATOR TEST" window. In this case
(for instructions starting with 0) the "ACCUMULATOR TEST" window asks "INPUT CARD BLANK?".
If you've been following along, the "INPUT" window should be showing "014" which was
the first of our two numbers to add. So the "INPUT CARD" is NOT blank. So we take the
"NO" path from the "ACCUMULATOR TEST" question.

The arrow from the "NO" path of the "ACCUMULATOR TEST" question leads upward to an
instruction that says "COPY INPUT CARD INTO CELL 51 AND ADVANCE CARD". So that's what
you'll do next. You can see that the input card contains "14" so click on Memory Cell 51
and enter "14" and then click "OK". The number 14 should appear in Cell 51. But don't
forget the second part of that instruction: "ADVANCE CARD". In other words, slide the
"INPUT" slider downward (click and drag on the upper part of the slider) until the
second value (28) appears in the INPUT window. This leaves it ready for the next time
that the computer needs to input a value.

### Fetching the Second Instruction

After advancing the card, follow the arrow downward and back to the "INSTRUCTION REGISTER".
Now the first instruction has been completed and it's time to fetch the next instruction.
The instruction register (again) says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL".
The contents of the bug's cell should be "052" (the second instruction of our grand program).
In this case, the sliders should aleady be at "051" so only the "LO ADDR" slider needs to
be changed from "1" to "2". This completes the "fetch" of the second instruction into the
"INSTRUCTION REGISTER". Now we need to follow this newly loaded second instruction.

### Executing the Second Instruction

Following the second instruction will be nearly identical to the first. As before, we'll
move the bug ahead one memory cell (leaving it on cell 02). As before we'll check if the
INPUT CARD is blank, and again it isn't (it contains 28). Since it's not empty, we'll again
follow the "NO" path of the flow diagram up to the top where it tells us to
"COPY INPUT CARD INTO CELL 52 AND ADVANCE CARD". That's nearly identical to what we did
before, and we can see that the input card is now 28. So we click on the yellow rectangle
for Memory Cell 52 and enter the number 28 and click "OK". We also advance the input card
again by sliding it down to show position 3 (which should be empty). Now we've completed
the execution of our second instruction, and we're ready to fetch the next instruction.

### Adding More Instructions while CardIAC Waits

At this point, we have followed 2 instructions. We've moved the values from 2 input "cards"
into 2 locations in memory. But the instruction pointer (the "bug") is now pointing to an
empty cell. In a real computer, there are no empty cells. Every location in memory always
has *something* in it. Each bit will be either a 0 or a 1. But in CardIAC any "undefined"
memory locations (and input cards) will be empty. That turns out to be fine in this
case because we can continue to write instructions while the "computer" is on hold waiting
to fetch the next instruction (that isn't there yet).

### The Accumulator and Instructions for Loading and Adding

Now that we have our two input values in memory, we can write a few more instructions to
add them together. This is where the "Accumulator" comes in (the "ACCUMULATOR" is found in
the lower left quadrant of the CardIAC-B screen). Most computers have one (or more)
internal registers that can serve as "accumulators" where values can be loaded or manipulated.
In CardIAC, values can be loaded into the Accumulator from memory, and values can be added to
the Accumulator from memory. Those two steps are done with instructions "LD" (for loading) and
"ADD" (for adding). So we will want to load one of our values into the accumulator and then
add the other of our values into the accumulator. It doesn't matter which comes first (at least
for adding), so let's load from memory location 51 and then add from memory location 52. The
load from 51 instruction is "151", and the add from 52 instruction is "252". Click on the
memory cells "02" and "03" and add the instructions "151" and "252" respectively.

### Resume Execution with New Instructions in Memory

We've just written two new instructions while the computer was waiting to execute them. So
let's get back to where the computer left off.

The computer was just getting ready to "fetch" the next instruction at Memory Cell 02. There
had been no instruction there before, but we've just added two of them so we can return to the
"INSTRUCTION REGISTER" and once again "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The
bug's cell now shows 151, so move the sliders to show 151 in the "INSTRUCTION REGISTER".
Following the flow diagram out the left side of the "INSTRUCTION REGISTER" the next thing for
the computer to do is "MOVE BUG AHEAD ONE CELL". So click the small round "hole" on Memory
Cell 03 to move the bug forward.

### Moving Memory into the Accumulator

Now the flow diagram leads upward to the instructions that tell us to "COPY CONTENTS OF CELL 51
INTO ACCUMULATOR". So we look at Memory Cell 51 and see that it contains "014" (14). Next, we click
on either the word "ACCUMULATOR" or the numbers in the ACCUMULATOR (likely all 0's) and that will
bring up a dialog box asking "Enter a value for the accumulator:". Type in "14" and click "OK".
The "ACCUMULATOR" should now show the number "0014". We can now follow the flow diagram back to
the "INSTRUCTION REGISTER" for our next "fetch" cycle.

### Fetching the ADD Instruction

Again, the INSTRUCTION REGISTER tells us to "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL".
The bug's cell is currently showing "252" so we adjust the sliders to show "252" in the
"INSTRUCTION REGISTER". In this case, both the "OP CODE" slider and the "ADDR LO" slider will
need to be moved.

### Executing the ADD Instruction

Now that the computer has "fetched" the next instruction ("252") it's time to execute it.
Following the flow diagram out the left side of the "INSTRUCTION REGISTER" we find that we must
again (as always) move the bug ahead one cell. So click the small "hole" on Memory Cell 04 to advance the
bug. Then follow the flow diagram up to the top where it says "ADD CONTENTS OF CELL 52 INTO ACCUMULATOR".
Since the value in cell 52 is "28" and the value in the ACUMULATOR is "14", the sum of those should be 42.
Of course a real computer would do that addition for us, and there is probably a way to make an adding
machine out of cardboard (similar to a slide rule). But CardIAC demonstrates the flow and processing
of instructions ... and leaves the math up to us. So we need to put "42" into the ACCUMULATOR. Once
again click on the ACCUMULATOR and enter "42" in the pop-up dialog, and click OK.

### Producing a Result with the "STO" and "OUT" Instructions

At this point, it might seem that we're done ... but not yet. We have summed the values into the accumulator,
but that's deep inside the computer. In a real computer we would not see the 1's and 0's representing
"42" inside the chip. So the computer still needs to send that result to some output device (screen,
printer, disk drive, voice reader, ...) where we can make use of it. For CardIAC, the only "output"
device is the "OUTPUT" card slider. So we'll need to add instructions to produce that output.

Now we scan the list of instructions (shown on the front of the CardIAC computer) and we see that instruction
"5" is "OUT". It says that it will "Output a Memory Value". But our value (42) isn't in memory. It's in the
accumulator. So before we can "output" it, we'll need to move it somewhere in memory. So far we've used memory
locations 51 and 52. We could actually re-use either of them at this point (since we're done with them),
and in a very tight memory budget, that's exactly what we might do. But for clarity, let's put the
output in memory location 53, and then execute the "OUT" instruction with memory location 53. So we
will need to store ("STO") from the Accumulator into memory location 53, and then we'll need to output
("OUT") from memory location 53 to the "Output Card". The "STO 53" instruction will be "653" and the
"OUT 53" command will be "553" (see the instruction table on the computer). So click on memory cells
"04" and "05" and enter "653" and "553" respectively.

### Executing the "STO" Instruction

As before, the computer has been patiently waiting while we added some more instructions for it to
follow. So now we're ready to pick up where it left off. We're looking at the "INSTRUCTION REGISTER"
and we see that it again says "MOVE SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". The bug's cell
currently shows the newly added instruction "653" so adjust the sliders to show "653" in the instruction
window. In this case you'll need to move the "OP CODE" slider and the "ADDR LO" slider. Once the new
instruction ("653") is in the INSTRUCTION REGISTER, the flow diagram reminds us to "MOVE BUG AHEAD ONE CELL",
so click on the round "hole" for Memory Cell 05 to move the "bug". Then follow the flow diagram up to the
line that tells you to "COPY ACCUMULATOR TO CELL 53". You'll notice that the ACCUMULATOR shows "42" so
click on the yellow rectangle in memory cell 53 and type in "42" and click "OK".

### Executing the "OUT" Instruction

Once again the flow diagram brings us back to the "INSTRUCTION REGISTER" where we will again "fetch"
the next instruction by "MOVING SLIDES TO AGREE WITH CONTENTS OF BUG'S CELL". In this case, the bug's
cell contains the instruction "553" so only the "OP CODE" slider needs to be moved (from 6 to 5).
Now we follow the flow diagram to the left where it again tells us to "MOVE BUG AHEAD ONE CELL".
So we click on the round "hole" for Memory Cell 06 to move the "bug". Then we follow the arrow up to
where it says "COPY CONTENTS OF CELL 53 TO OUTPUT, ADVANCE". We can see that cell 53 contains the
number 42 (our answer), so we click on the "OUTPUT" box and enter "42" into the pop-up dialog box and
click "OK". This puts the number 42 into the output slider, and then we advance the output slider by
sliding it downward to make room for the next output (which we won't have in this case).

### Are we done yet?

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

### Executing the "HLT" Instruction

Now we can run the final "HLT" instruction. As before, we pick up where we left off - ready to fetch the
next instruction (that we just wrote). The INSTRUCTION REGISTER reminds us to "MOVE SLIDES TO AGREE WITH
CONTENTS OF BUG'S CELL". The bug's cell is currently "900" so all three slides ("Op Code", "Addr Hi",
and "Addr Lo") will need to be changed. As always, after "fetching" this instruction, the bug should be
moved forward one cell (to 07 in this case). Then following the flow diagram to the top we find that it
says "MOVE BUG TO CELL 00 STOP". So we click on the "hole" for memory cell 00 to move the bug and we
can finally ... stop.

### Do it Again?

Once the program has been written and entered (as it has been in this tutorial), new input values can
be entered, and the program can be run again. Indeed, with a few small changes, this program could loop
back to the beginning and continue to add pairs of numbers (taking them from the input cards) and produce
a list of sums (to the output cards). But that's not really the best use of this "virtual cardboard"
computer. The best use is to understand the fundamental notions of how a set of stored computer
instructions can be cycled through a very simple machine to process data (including input and output).
That's what computers do ... all day and all night.

### Macro Instructions and Micro Instructions

The instructions of CardIAC (such as IN, STO, ADD, SUB, JMP) are very similar to the instructions of real
computers. But CardIAC goes one level deeper and shows how each of those "macro" instructions are made up
of several "micro-instructions" such as "fetch an instruction", "increment the program counter", and "move"
data. The process is certainly tedious, but it demonstrates the building blocks of all modern digital computers.

## Additional Features of CardIAC-B

The previous example provides most of the information needed to operate CardIAC-B. However, there are a
few other helpful features that will be explained here.

### Managing Input and Output

Input data and output data are handled as "cards" by CardIAC. In the old days, cards were a common form
of interaction with a computer and a program (as well as input data) would often be entered as a series
(or "deck") of punched cards. The Input and Output sliders reflect that perspective and that's why they
have the upper left corner "cut off" in each cell to look like a series of very small punch cards.

Data is loaded into these cards by clicking on the words "INPUT" or "OUTPUT". Both will bring up a dialog
box showing the current data and both will offer the opportunity to enter data. But the data for input
and output differ. The data entered for input can contain multiple space-separated values, and those
values will replace the **entire** set of "cards" on the slider. But placing data on the output card
should only happen through the "OUT" instruction, and the "OUT" instruction for CardIAC can only output
one value at a time. As a result, new values are entered onto the Output cards one at a time as directed
by the program. So there should be no need to enter multiple values at once for Output. Both dialog boxes
provide an option to clear the entire card with a single "x" as input. In all cases, it can be helpful
to use your computer's cut, copy, and paste features to save and restore copies of the input and output
cards as needed. Clicking on either the "INPUT" or "OUTPUT" will initially show all of the data for those
cards for easy copying and saving.

### The Accumulator

The Accumulator is really just a place to store a number. The value entered there is not used by CardIAC-B
in any way other than to ask you (the real brains of the operation) to change it appropriately. You can
change the Accumulator by clicking on the word "ACCUMULATOR" or the box that holds the number. A dialog
box will come up where you can enter the value to be stored in the Accumulator.

### The "Bug" (Program Counter)

As with the Accumulator, the "Bug" is not used by CardIAC-B in any way other than to ask you (again, the
real brains of the operation) to use it as a reference for fetching instructions. You can change the
location of the "Bug" by clicking on the small circles at each location of the memory. In the original
"CardIAC", those circles were holes where the paper "Bug" could be slid to keep track of the next program
instruction.

### Memory - Individual Cells and Bulk Reading and Writing

The memory of CardIAC is used for storing both programs and data. In fact, program instructions can be
read (as data) and data can be executed (as program instructions). Keeping all of this straight is the
job of the programmer (you). Memory is normally changed by clicking on the yellow rectangle in each
memory cell. This will bring up a dialog box giving you the option to change the value or clear it
completely (with an "x"). This is sufficient for small programs, but would be extremely tedious for
large programs (of course, executing large programs on CardIAC would be even *more* tedious). So CardIAC-B
has a mechanism for bulk reading and writing of memory. If you click on either of the words "MEMORY" or
"CELLS" above the memory area, you will get a pop-up dialog box containing all of the space separated
values currently in memory. Any blank cells will be represented with a single underscore ("_"). This
feature allows you to copy all of memory at once as a string and paste it into some other application
(like a text editor) to save it. It also allows you to paste a string (copied from another application)
to restore all of memory at once. The ability to edit all of memory at once makes it relatively easy to
shift sections of memory by inserting or deleting cell values in the text string representing the memory.

### Behind the Curtain

The original CardIAC computer was a very very clever idea, and it surely took considerable thought and
effort to make all the sliders work in conjunction with each other to produce a "working" computer.
CardIAC-B allows you to see the movement of those sliders by toggling on the "bell" in the lower right corner.
This essentially replaces the front panel with a transparent image that lets you see the sliders moving.
The transparent image also shows the locations of the cutouts of the normal front panel for reference.
Additionally, when in "transparent" mode, the sliders change color so they can be differentiated (since
they have no borders and would otherwise blend together).

## Example programs

The following example programs are essentially memory images which can be copied into memory using
the bulk writing method described in the "Memory" section above. Basically click on the words "MEMORY" or
"CELLS" above the memory area. Then copy and paste the desired example into the text dialog box and click
the "OK" button. That will copy the program from the dialog into memory.


### Add two numbers from input cards and write their sum to an output card

This program adds the first two input card numbers and produces a result on the output card.

> 51 52 151 252 653 553 900


### CardIAC Instruction Manual, Program No. 8: Subroutine for "A" + "B" = SUM

    1 _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ _ _ _ _
    95 96 97 98 886 659 559 598 900 _
    _ _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ _ _ _ _
    _ _ _ _ _ _ 199 694 196 298
    698 403 295 297 800 _ _ _ _ _


