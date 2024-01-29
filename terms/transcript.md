# Transcript

The transcript(or trace) of a [RAM](random_access_machine.md) $M$'s execution on input $x$ describes the changes to $M$’s
configuration at each step of its execution.\
For each step $i$, the transcript lists the value of each register and the program counter at the end of the step. Since $M$ has only
$O(1)$ registers, the transcript can be specified using $O(T)$ [words](word.md).
