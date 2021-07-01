# Complex Superpositions

## Superpositions with More than 2 Terms

We've covered a lot so far - we've gone through qubits, superpositions, the Bloch Sphere, single-qubit gates, registers, multi-qubit gates, entanglement… but I've purposefully kept things (relatively) simple until now.
All of the superpositions we've looked at only have two states in them.
For example, in Exercise 3 you saw the four Bell States, which only have two terms in their superpositions:

$$
\begin{aligned}
\ket{\Phi^+} = \frac{1}{\sqrt{2}} \ket{00} + \frac{1}{\sqrt{2}} \ket{11}
\\~\\
\ket{\Phi^-} = \frac{1}{\sqrt{2}} \ket{00} - \frac{1}{\sqrt{2}} \ket{11}
\\~\\
\ket{\Psi^+} = \frac{1}{\sqrt{2}} \ket{01} + \frac{1}{\sqrt{2}} \ket{10}
\\~\\
\ket{\Psi^-} = \frac{1}{\sqrt{2}} \ket{01} - \frac{1}{\sqrt{2}} \ket{10}
\end{aligned}
$$

Real quantum algorithms don't usually have this restriction.
Now that you know how registers and multi-qubit gates work, it's time we take off the training wheels and talk about superpositions with more than 2 terms.

You're already pretty familiar with the $\ket{+}$ state at this point, which we've constructed by applying the H gate to one qubit in a register.
Now, we're going to see what happens when you apply the H gate to multiple qubits in a register.
We'll start with a simple 2-qubit register:

$$
\begin{aligned}
\ket{\psi} &= \ket{00}
\\~\\
H(\psi_0), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \ket{00} + \frac{1}{\sqrt{2}} \ket{10}
\\~\\
H(\psi_1), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \left( H_1( \ket{00} ) \right) + \frac{1}{\sqrt{2}} \left( H_1( \ket{10} ) \right)
\end{aligned}
$$

To help illustrate what happens here, I'll color code the individual states:

$$
\begin{aligned}
\ket{\psi} &= \frac{1}{\sqrt{2}} \left( \textcolor{green}{ H_1( \ket{00} )} \right) + \frac{1}{\sqrt{2}} \left( \textcolor{red}{H_1( \ket{10} )} \right)
\\~\\
&= \frac{1}{\sqrt{2}} \left( \textcolor{green}{ \frac{1}{\sqrt{2}} \ket{00} + \frac{1}{\sqrt{2}} \ket{01} } \right) + \frac{1}{\sqrt{2}} \left( \textcolor{red}{ \frac{1}{\sqrt{2}} \ket{10} + \frac{1}{\sqrt{2}} \ket{11} } \right)
\\~\\
&= \textcolor{green}{ \frac{1}{\sqrt{4}} \ket{00} + \frac{1}{\sqrt{4}} \ket{01} } + \textcolor{red}{ \frac{1}{\sqrt{4}} \ket{10} + \frac{1}{\sqrt{4}} \ket{11} }
\\~\\
&= \frac{1}{2} \left( \ket{00} + \ket{01} + \ket{10} + \ket{11} \right)
\end{aligned}
$$

**This** superposition has four different terms in it.
In fact, it has all four possible states that the two qubits could be in.
Because each one has the same amplitude, this is called a uniform superposition.
Essentially, this means that both qubits have a 50% chance of being $\ket{0}$ and a 50% chance of being $\ket{1}$, but unlike the Bell states, the qubits aren't entangled so they have no relation to one another.
Measuring the first qubit as $\ket{0}$ doesn't tell you anything about the second qubit; it still has a 50% chance of being either state.

We could do the same thing for a 3-qubit register by applying the H gate to all 3 qubits.
As you can probably guess, the end result will be this:

$$
\begin{aligned}
H_{ALL}(\ket{000}) = \frac{1}{\sqrt{8}} \left( \right. &\ket{000} + \ket{001} + \ket{010} + \ket{011} + \\
&\left. \ket{100} + \ket{101} + \ket{110} + \ket{111} \right)
\end{aligned}
$$

Like the 2-qubit example, every qubit in this register has a 50% chance of being $\ket{0}$ and a 50% chance of being $\ket{1}$, and they're all independent.
This is analogous to having three sequential coin flips - the flips have nothing to do with one another, so there are 8 equally probably outcomes.

Essentially, applying the H gate to every qubit in a register will transform the register into a uniform superposition of *all $2^n$ possible states*, each with an amplitude of $\frac{1}{\sqrt{2^n}}$, where $n$ is the number of qubits in the register.
Exactly why this is useful and how it is used will be discussed further in the quantum algorithm section - soon enough, you'll actually get to write some code that leverages these saturated superpositions to solve some very interesting problems.


## Constructing Complex Superpositions

Most of the time in quantum computing, this is how registers are going to be presented - long strings of superposition terms that show which of the possible states are included and what their amplitudes are.
Superpositions don't have to be nice and neat, and often times they're actually pretty convoluted, but that doesn't mean they're always hard to construct.
For example, this is a perfectly valid superposition that we can easily create by applying a few gates:

$$
\ket{\psi} = \frac{1}{2} \left( \ket{000} + \ket{010} + \ket{100} + \ket{111} \right)
$$

This may look daunting at first, but I'll make one tiny change that will help - remember that ket notation allows us to add commas anywhere in a ket to help semantically separate two different registers or qubits:

$$
\ket{\psi} = \frac{1}{2} \left( \ket{00,0} + \ket{01,0} + \ket{10,0} + \ket{11,1} \right)
$$

Can you see a pattern now? Try to work out what it is before reading on.

Okay, so the first two qubits look identical to the double-Hadamard state we constructed above.
That means we can just apply the H gate to both of them:

$$
\begin{aligned}
\ket{\psi} &= \ket{00,0}
\\~\\
H(\psi_0), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \left( \ket{00,0} + \ket{10,0} \right)
\\~\\
H(\psi_1), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \left( \frac{1}{\sqrt{2}} \left( \ket{00,0} + \ket{01,0} \right) + \frac{1}{\sqrt{2}} \left( \ket{10,0} + \ket{11,0} \right) \right)
\\~\\
&= \frac{1}{2} \left( \ket{00,0} + \ket{01,0} + \ket{10,0} + \ket{11,0} \right)
\end{aligned}
$$

The third qubit looks like it's been entangled with them so it's only 1 when both of the others are 1.
We can accomplish that with the CCNOT gate:

$$
CCNOT(\psi_0, \psi_1, \psi_2), \qquad \ket{\psi} = \frac{1}{2} \left( \ket{00,0} + \ket{01,0} + \ket{10,0} + \ket{11,1} \right)
$$

Tada!
That wasn’t so bad.
How about another weird looking superposition like this one?

$$
\ket{\psi} = \frac{1}{2} \left( \ket{001} + \ket{010} - \ket{101} - \ket{110} \right)
$$

Try to see if you can find the pattern and figure out what gates to use before reading ahead.

For this state, we see three things:

1. The first and second qubits are equally likely to be in either state, so they're probably Hadamard'd.
1. The second and third qubits are always opposites, so they're definitely entangled.
1. The phase is negative when the first qubit is 1.

We think we can build this state by first putting the first and second qubits into the double-H state:

$$
\begin{aligned}
\ket{\psi} &= \ket{000}
\\~\\
H(\psi_0), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \left( \ket{000} + \ket{100} \right)
\\~\\
H(\psi_1), \qquad \ket{\psi} &= \frac{1}{2} \left( \ket{000} + \ket{010} + \ket{100} + \ket{110} \right)
\end{aligned}
$$

Next, let's entangle the second qubit with the third, putting them into the $\ket{\Psi^+}$ state:

$$
CNOT(\psi_1, \psi_2), \qquad \ket{\psi} = \frac{1}{2} \left( \ket{000} + \ket{011} + \ket{100} + \ket{111} \right)
$$

Now let's flip the last qubit so it's the *opposite* of the second:

$$
X(\psi_2), \qquad \ket{\psi} = \frac{1}{2} \left( \ket{001} + \ket{010} + \ket{101} + \ket{110} \right)
$$

Finally, let's apply the Z gate to the first qubit to flip the phases:

$$
Z(\psi_0), \qquad \ket{\psi} = \frac{1}{2} \left( \ket{001} + \ket{010} - \ket{101} - \ket{110} \right)
$$

And with that, we've created it. No big deal.


### Ancilla Qubits and Phase Kickback

Sometimes when we're trying to construct a superposition, it's actually pretty tough to come up with an easy way to create it.
For example, take a look at this one:

$$
\ket{\psi} = \frac{1}{2} \left( \ket{00} + \ket{01} + \ket{10} - \ket{11} \right)
$$

In this superposition, it looks like both qubits are in the double-H state, but one of the states has its phase flipped.
How do we pull this off? We need an operation that does something like,

	"If the first qubit is 1 and second qubit are both 1, negate the state's phase."
	
We've seen something like the first half of that sentence before - that looks like a doubly-controlled gate, like CCNOT.
But with CCNOT, we use the two control qubits to flip a third, target qubit.
We don't have a third qubit here, and even if we did, how would it help us flip the phase of the state?

It turns out, if we did have a third qubit, this would be a lot easier.
Take a look at this state, which is similar to the above one:

$$
\ket{\psi \prime} = \frac{1}{2} \left( \ket{00,1} + \ket{01,1} + \ket{10,1} - \ket{11,1} \right)
$$

In this state, we've added a new qubit to the register which is always in the $\ket{1}$ state.
Because it's in the $\ket{1}$ state, we can actually flip its phase with the Z gate.
That means we can apply a doubly-controlled Z gate with the first and second qubits as the controls, and this new "spare" qubit as the target, and it will end up flipping the state for us!

$$
\begin{aligned}
\ket{\psi} &= \ket{00}
\\~\\
H(\psi_0), \qquad \ket{\psi} &= \frac{1}{\sqrt{2}} \left( \ket{00} + \ket{10} \right)
\\~\\
H(\psi_1), \qquad \ket{\psi} &= \frac{1}{2} \left( \ket{00} + \ket{01} + \ket{10} + \ket{11} \right)
\end{aligned}
$$

Now, we allocate a spare qubit (called $a$) and use it temporarily:

$$
\begin{aligned}
\ket{a} &= \ket{0}
\\~\\
\ket{\psi,a} &= \frac{1}{2} \left( \ket{00,0} + \ket{01,0} + \ket{10,0} + \ket{11,0} \right)
\\~\\
X(a), \qquad \ket{\psi,a} &= \frac{1}{2} \left( \ket{00,1} + \ket{01,1} + \ket{10,1} + \ket{11,1} \right)
\\~\\
CCZ(\psi_0, \psi_1, a), \qquad \ket{\psi,a} &= \frac{1}{2} \left( \ket{00,1} + \ket{01,1} + \ket{10,1} - \ket{11,1} \right)
\end{aligned}
$$

At this point, note that the spare qubit is still always 1.
Even though we applied a doubly-controlled Z gate to it, it didn't actually get entangled with the other qubits.
We just used it to help "kick" the phase-flip from the Z gate back into the original two control qubits.
Because it's not entangled, we can simply throw it away:

$$
\ket{\psi} = \frac{1}{2} \left( \ket{00} + \ket{01} + \ket{10} - \ket{11} \right)
$$

And we're done!
It turns out we need to "borrow" a spare qubit fairly frequently in quantum computing.
When we do this, the extra qubit is called an **ancilla** qubit.
The particular technique shown here, where we used an ancilla to help flip the phase of a specific superposition term without entangling the ancilla, is called **phase kickback**.
It is an extremely powerful technique that we're going to leverage in the quantum algorithms sections coming up next.


## Non-uniform Superpositions

Before we get to the quantum algorithms, we want to point out that the above superpositions are still fairly simple, despite requiring a little engineering to construct.
More often than not we actually end up dealing with superpositions that are quite strange, such as this one:

$$
\ket{\psi} = \frac{1}{\sqrt{3}} \left( \ket{00} + \ket{01} + \ket{10} \right)
$$

This state looks like $\ket{++}$, but it's missing the $\ket{11}$ term.
It turns out that getting an even amplitude on three of the four possible states in a two-qubit register only takes a few gates, but conceptually it's not an easy thing to grasp.
Here's another weird state - this one is even worse, because it has uneven amplitudes:

$$
\ket{\psi} = \frac{1}{2} \ket{000} + \frac{1}{2 \sqrt{2}} \ket{001} - \frac{1}{2 \sqrt{2}} \ket{011} - \frac{1}{2} \ket{100} - \frac{1}{2 \sqrt{2}} \ket{101} + \frac{1}{2 \sqrt{2}} \ket{111}
$$

This state actually encodes 8 evenly-spaced samples of a full cosine wave into the amplitudes of a 3-qubit register, which is useful when studying sine and cosine waves with quantum computers.

We aren't going to deal with superpositions like these in this class; that's more in the realm of advanced algorithm design, and this is just an introduction.
Still, if you want to take a crack at them, these states (and some other ones) are provided as a set of **challenge problems** in Lab 3.

Before we go onto the lab though, you may have noticed that you've spent a lot of time in the past few lessons effectively building quantum programs.
Let's talk about the formal notation and structure for quantum programs, and go over some tools to help you quickly build, visualize, simulate, and study them.