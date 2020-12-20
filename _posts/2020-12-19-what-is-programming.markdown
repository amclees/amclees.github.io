---
layout: post
title:  "What is programming?"
date:   2020-12-19
---
Sometimes you see articles with a philosophical discussion of what it means to program a computer.
That's not what this is, though it is about computer programming.

This is intended to be an introduction to what programming is, for those with no programming experience
and not necessarily any intention of learning how to program.

If you've ever wondered what programmers are doing all that time spent typing in front of a computer, this
post is for you. No background knowledge is needed, just an interest in learning.

### What is a computer?

Before we get into programming, it helps to understand what a computer is.
There are a bunch of parts in a modern computer, even most programmers have a fairly minimal understanding
of everything that goes into a computer.

Before humans even imagined computers as machines, there were human computers.

[![Human computers](/images/human_computers.jpg)](https://www.dfrc.nasa.gov/Gallery/Photo/Places/HTML/E49-54.html)

Human computers have been around nearly as long as human civilization, though the profession became more organized
as advances in engineering require more and more complicated calculations.

In the mid-1800s, there were theories of mechanical (read - "many gears inside") computer which could add, subtract, mutliply, and divide numbers
according to a set of instructions on a punched card. There were also theories of how to instruct, or program this first computer.
A working version was not built, however.

In the early 1900s, a spur of innovations in theories of computing and electrical engineering laid the foundations for a digital computer.
The first programmable digital computers were developed for military applications (artillery, codebreaking, nuclear weapons, and the likE).
There is a great deal of history in this area, but it's far more than what is needed to understand what a computer is.

There are a few things that distinguished these computers from there predecessors:

1. They were programmable. Humans could describe different sets of computations to run, and they would run them.
   Human computers were always programmable, but earlier attempts at computing machines were not.

2. They were Turing-complete, a property computer scientists use to describe a computer that can compute anything that can be computed.

3. They were digital. Rather than using gears, levers, and such, they used electronic circuits. This eventually made them very fast and flexible.

Even some of the earliest computers, long before anything resembling a modern computer, could calculate all the same things as a modern computer.
Anything possible to calculate, they could calculate if given the right instructions. The same is true of a modern computer.

The parts of a modern computer are essentially the same as one of these early digital computers, the [EDSAC](https://en.wikipedia.org/wiki/EDSAC):

* Input devices. Your mouse and keyboard, the touchscreen on your phone.

* Output devices. The screen you're viewing this post on. Or perhaps a printer or speakers.

We call these two parts I/O (sometimes spelled IO). Internet connection involves I/O as well, but that opens many cans of worms and is a topic for
another time.

A computer can be viewed as a magic box that accepts inputs, does *something* to them, then provides outputs.
This is fine, but to understand programming (or to understand how best to use a computer), we need to dig
deeper. A computer has many things inside it:

* A processor. These can do basic arithmetic and logic based on a program.

* Memory. A processor doesn't have room to store all the numbers and other data it works with. They go in memory.

[![Von Neumann Architecture](/images/von_neumann.png)](https://commons.wikimedia.org/wiki/File:Von_Neumann_Architecture.svg)

There are different kinds of processors and different kinds of memory.

The most important kind of processor in a consumer computer is the central processing unit (CPU).
These do arithmetic and logic, and they don't specialize in anything. Think of the CPU as a jack of all trades.

The most important kind of memory to programming a consumer computer is the main memory (RAM, for random-access memory).
This memory is not the kind you usually thing about - documents or other data go on the slower hard drive or solid state drive.
The reason we don't use RAM for this is that all the numbers in RAM go away when you power down your computer (it's volatile).
The processor also has some kinds of memory that are volatile like RAM (but smaller than RAM and faster).

[![Memory hierarchy](/images/memory_hierarchy.svg)](https://commons.wikimedia.org/wiki/File:ComputerMemoryHierarchy.svg)

A computer then, is a collection of parts. Different kinds of inputs, outputs, memory, and processors all work together
to **compute** something. The processor reads data from memory or inputs, works on it, then writes the results back to memory or outputs.

But how does it know what work to do, what problems to work on? They are an input called a program. Programmers are people who provide this input.

### What is a program?

Now we know what programmers do - write programs - and a rough idea of where programs come in. But what do they look like?

Consider you want to program a cash register to calculate sales tax. What are your input(s) and what are your output(s)?
Think a bit, then continue reading.

For the inputs, you have:

* A total price for an order. This is going to vary from order to order. It probably is in RAM.

* A sales tax rate. This probably doesn't change that often, and is probably in long-term memory somewhere.

For the output, you have:

* The sales tax

* Maybe also a total price with tax included

A program specifies how to go between the inputs and the outputs. Try to think of how you would compute the above outputs given the inputs.
Could you write the instructions in a way that someone else could follow them? For example,

```
Multiply the sales tax rate by the order price. This is the sales tax for the order.
Add the sales tax for the order to the price without tax. This is the total price for the order.
```

This is a program. Programs are written in a language. This one is written in plain English.

Natural languages like English are excellent for human communication. They are very expressive and can capture subjective concepts.
For example:

```
If the food looks tasty, eat it.
```

This is a very simple program for humans. However, a lot goes into deciding whether food looks tasty or not. A computer does not have
a sense of taste or sight, and must be told not only how to decide if a picture looks tasty, but how to see in the first place.
Teaching all these things to a computer (let alone teaching it to understand English) is very difficult.

This is why we have computer programming languages. They allow a purely objective specification of exactly how to calculate something.
For example:

```
Read total price from memory address 0 into register A
Read sales tax from memory address 1 into register B
Multiply register A and register B, store to register B
Add register A and register B, store to register A
Store register A to memory address 2
Store register B to memory address 3
```

Before you can understand the above, you should know:

* A processor has several slots called registers that are just big enough to hold a single number. Processors can read from memory into registers and write from registers into memory. All the actual calculations are done on values in the registers.

* Memory has addresses - you can think of memory as a series of blocks, each block able to hold a single number.

(These "numbers" are usually called "words", but using precise terms when dealing with memory and registers opens several large barrels of worms.)

At the start of the above program, the memory might look like:

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
</table>

This would indicate we are working with an order costing $10.50 with a sales tax rate of 9.75%. Computers are not build with special handling of percentages, dividing by 100 makes the tax rate the same format as the price.
(If you ever write your own program - don't use decimals for calculations with money. There are nuances but that's too much to get into here.)

Now, let's run this program from the computer's perspective.

```
Read total price from memory address 0 into register A
```

Okay, we see 10.5 in the zeroeth spot in memory. Let's copy that into the register.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>10.5</td></tr>
</table>

```
Read sales tax from memory address 1 into register B
```

It's the same idea here.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>10.5</td></tr>
  <tr><td>B</td><td>0.0975</td></tr>
</table>

```
Multiply register A and register B, store to register B
```

First, we multiply 10.5 and 0.0975 and get the value 1.02375.
Then we put this result back into register B.
This is the sales tax.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>10.5</td></tr>
  <tr><td>B</td><td>1.02375</td></tr>
</table>

```
Add register A and register B, store to register A
```

This adds the sales tax we just got to the order total, giving
us a total with tax included.
Now our registers have all the outputs we wanted.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>11.52375</td></tr>
  <tr><td>B</td><td>1.02375</td></tr>
</table>

```
Store register A to memory address 2
```

We can't do anything with the results unless
we put them back in memory first.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
  <tr><td>2</td><td>11.52375</td></tr>

</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>11.52375</td></tr>
  <tr><td>B</td><td>1.02375</td></tr>
</table>

```
Store register B to memory address 3
```

We have one more result to store back.

<table>
  <tr><th>Address</th><th>Value</th></tr>
  <tr><td>0</td><td>10.5</td></tr>
  <tr><td>1</td><td>0.0975</td></tr>
  <tr><td>2</td><td>11.52375</td></tr>
  <tr><td>3</td><td>1.02375</td></tr>
</table>

<table>
  <tr><th>Register</th><th>Value</th></tr>
  <tr><td>A</td><td>11.52375</td></tr>
  <tr><td>B</td><td>1.02375</td></tr>
</table>

Now that we've run the program, you've probably realized a few things:

* It would not be fun to manually compute things like this all day. This wouldn't be a good language for human computers.

* It would be really hard to make computers do anything complicated with a program like this.

The program above is a very low-level program. It can be converted into numbers, stored in memory (yes, programs
go the same memory too, usually),
and interpreted directly by the electronic circuits in your processor.
Some computers have separate memory for all their programs, but they are the exception.
If the program is in memory, the program can read and write to itself.
This feature is the source of many a security vulnerability - if you can trick a program
into writing one of its inputs into the right place in memory, you can change the program.

We have to start somewhere, but it's disappointing to see so many steps involved in such a simple
program. It's also a very complicated way of saying we should multiply a couple numbers and add
a couple numbers. On the bright side, a modern computer can execute this program millions of times
every second. A single computer could swiftly and accurately handle all the sales tax calculations
in the world, so long as all the data was delivered to and from it's memory. That's the hard part,
and one way of viewing the internet.

To simplify the process of writing a program, programmers usually use a higher-level programming language.
There is much debate over what makes a language high-level and whether individual languages are indeed
high level. But most widely-used programming languages are significantly higher-level than the example program above.

An example of a higher-level program written in a language called Ruby:

```ruby
# A '#' at the start of a line is a comment.
# Comments are not run by the computer.
# Programmers put comments in between lines of code the computer runs,
# usually explaining what the program does.

# 'def' is a function definition.
# A function is a piece of code another programmer can use.
# The name of the function is 'calculate_sales_tax_and_total'.
# It has two inputs - 'order_total_before_tax' and 'sales_tax_rate'.
def calculate_sales_tax_and_total(order_total_before_tax, sales_tax_rate)
  # Multiply the two inputs, calling the result 'sales_tax'.
  # We can reference this result later.
  sales_tax = order_total_before_tax * sales_tax_rate
  # Add the order total before tax to the sales tax we just calculated.
  # Note how all the names appear above - they are inputs,
  # or we already wrote down how to calculate them.
  order_total = order_total_before_tax + sales_tax
  # The end of the function specifies our outputs.
  # Here, we output a list with the sales_tax and the total with sales tax added.
  [sales_tax, order_total]
end
```

This does effectively the same thing, but in a way that is easier to read as it obscures the details of
memory and registers.

The rules that determine how a written program should be interpreted are called syntax.
Like writing in natural language, there may be syntax errors. Can you find two below?

```
def calculate_sales_tax_and_total(order_total_before_tax,_ sales_tax_rate)
  sales_tax = order_total_before_tax * sales_tax_rate
  order_total = order_total_before_tax + sales_tax
  [sales_tax, order_total
end
```

Not knowing Ruby syntax, you may still be able to find them for two reasons:

1. You have a correct program as a reference point.

2. Programming languages tend to be more orderly than natural language, so irregularities are often wrong.

Syntax errors are most programmer's favorite kind of errors because they are easy to spot and fix.
Errors from bad assumptions or bad interaction with other programmers' code are much more difficult to deal
with.

The program above illustrates how to do a very basic computation. There is one path through the program
from start to finish. This is the exception. Here's an example that is less of an exception:

```ruby
def multiply(num1, num2)
  result = 0
  num1.times do
    result += num2
  end
  result
end
```

One way to view multiplication is as adding a number some number of times. That is what the above does - it
runs the same code, `result += num2`, some number of times - `num1` times. This is an example of something
called control flow - where there are multiple paths through the instructions the computer has.
A great deal of the complexity in programs comes from control flow, more than anything else in many cases.
This is analagous to instructions referring back to themselves.

```
1. Wait 1 second.
2. Go back to step 1 if the food isn't done cooking.
3. Remove the food.
4. Take a bite.
5. Go to step 6 if thirsty, step 7 if food is depleted, step 8 if full.
6. Take a drink, then go back to step 6.
7. Go for a walk.
8. Put away the food.
```

Can you spot the unreasonable parts of these instructions? Fixing bugs in computer programs is often a
very similar task, but there may be millions of steps written by different people. There are usually
hints to where the problem is, so there isn't a need to look at each and every step individually.

We've covered what programs are and how computers run them. But how do computers do more interesting things
like send or receive emails, edit documents, or support internet browsing? They are programmed to.

### Programming is just typing

Programming is as simple as typing out a program like the example above.

The example above is about 200 characters long, and each could be a number, letter, or punctuation mark of some sort,
with about 50 possibilities. This means there are about 50 to the power of 200 possible texts as long as the above.
There are fewer (far, far fewer) stars in the universe.

Of course, most of these are invalid and many are gibberish (not the stars, they're all valid).
But there are still billions of valid programs this long. Maybe fewer than stars.

[![Stars](/images/stars.jpg "See that really bright one near the top? That one corresponds to the first 'Hello World' program ever written.")](https://en.wikipedia.org/wiki/Star#/media/File:Starsinthesky.jpg)
> Stars. We've written fewer programs than there are. Maybe we'll have written more some day.

The hard part of programming and the most important part is knowing what program to type.

To know what to type, a programmer needs to:

* Identify a problem worth solving.

* Identify the inputs and outputs.

* Identify exact steps to perform the computation that solves the problem.

The first two steps often involve a great deal of communication with people having the problems ("users").
Programmers initially do not understand the needs of the users or their problems well enough to write a program to
solve them. Even if the programmer is the user, there are usually many details of the problem that need to be
worked out.

Consider a system allowing online registration for a library card. What information should the user
provide? Does the library need to verify the user's address? If so, how do they do this? Should the user upload
a picture of mail or receive a confirmation code by mail? The required program varies significantly, and there
is rarely a single obvious best approach.

Once the problem is identified, there are often complications in the details of how to solve it. Sure, we want
a web search engine. But how do we search billions of webpages in under one second? The details are [complicated](https://www.google.com/search/howsearchworks/).

Humans often do not respond well to underspecified problems. They do the wrong things, don't do enough, and don't
always clarify.

Computers do not respond at all to underspecified problems.

Programmers with an underspecified problem must specify all details of the problem to the computer. To do this in a way
that solves the problem well, they need to understand all details of the inputs, outputs, and solution.

The traditional way this is broken down is:

* Requirements gathering - figuring out the inputs, outputs, and how they should relate to each other.

* Design - figuring out the steps to some detail, but not in a way the computer can understand yet.

* Implementing - writing the program.

* Testing - verifying the written program meets requirements.

A lot of all of these is needed for larger projects, which can take place over years or decades.

The additional work around the writing of the program is why so there are so many names for programmers beyond programmers: software engineers, software developers,
software architects, and the like often perform very similar work. But whatever title you prefer (even if it's code monkey) and however you define it, all the tasks above
are necessary to create a functioning program. Splitting the work across people sounds good in theory, but
it requires even better communication between people working on each part to pull off. It is inevitable that the whoever
works on a later stage above will uncover problems in the assumptions of the people working at earler stages, and
they need to work together to rectify the problems.
It's very much not a linear process.

[![Code monkey](/images/monkey.jpg "It was... sweet.")](https://en.wikipedia.org/wiki/File:Saimiri_sciureus-1_Luc_Viatour.jpg)

> [Code M. Monkey](https://en.wikipedia.org/wiki/Code_monkey), taking a bite of programming for the first time. C. 2005

### Programs are not alone

The example from earlier had five lines of code without comments:

```ruby
def calculate_sales_tax_and_total(order_total_before_tax, sales_tax_rate)
  sales_tax = order_total_before_tax * sales_tax_rate
  order_total = order_total_before_tax + sales_tax
  [sales_tax, order_total]
end
```

This is for something as simple as calculating sales tax. Not all the lines are that interesting, and lines of code is an imperfect metric.
But consider that Windows XP had 50 million lines of code to give a rough idea of the complexity that exists.
Any typo in all 50 million lines could produce a bug, but, more importantly, different programmers could have different ideas about
the problem. What should a negative sales tax rate do? The code above would grant a discount to the customer, which is almost
certainly a bug. It would be better not to give a result at all.

In the larger scale, there are:

* Billions of users

* Billions of computers

* Millions of computer programs

* Hundreds of programs running in the background on your computer at any given time

* Billions of basic instructions (like those in the example above) running each second on many computers

* Bllions of numbers in RAM and many more in long-term storage per computer

Programs deal not only with numbers, but with strings - text that is encoded as a series of numbers. I/O is not to and from memory
but to and from several peripheral devices all at the same time, and the internet. There are tens to hundreds of computers in the path
between your computer and other computers on the internet, each running many programs of their own.
There are specialized processors to speed up tasks like graphics processing and machine learning.

It is exceedingly rare to have a single self-contained program. Nearly all programs need to interact with other programs.
Programs called drivers read to/from monitors, mice, keyboards, and the internet. Operating systems like Windows, Mac OS X, or GNU/Linux
handle which programs are running on the processor at any given time, which have access to which part of memory, the keyboard, or the screen.
Programs communicate with other programs in many ways. Your web browser downloads programs from the internet and runs them.

Even within a single program, it is rare for all code to be written by one person. Code, like hardware, has interfaces. These are the software
analog of electronic interfaces like USB or HDMI. For example, given:

```c++
Number Find(Text corpus, Text word);
```

This is an interface (in the C++ language) for a function that finds the place where a word appears inside some text. For example:

```
corpus: "A surprise to be sure, but a welcome one."
word: "welcome"
Output: 29
```

The 29th spot (letter, punctuation, or space) is the start of the word "welcome".

An interface specifies the inputs, outputs, and how they relate to each other. Sound familiar? Identifying a good interface is
usually the first step in implementing a program or any major part of a program.

An implementation can be implemented in many different ways, so long as the inputs, outputs, and behavior are the same for each implementation.
Behavior is fairly general. One implementation of the interface above would be:

```c++
Number Find(Text corpus, Text word) {
  return 42;
}
```

This program returns 42 regardless of the inputs. This is terrible! The inputs and ouputs all have the right data types
(text inputs, and a number output), but the behavior is not right in any reasonable interpretation.
This is what is meant by behavior (or 'conventions') in an interface.

It's common to call an interface an API. Programmers like acronyms. It stands for Application Programmable Interface.
Originally, it had a narrower meaning, but nowadays any interface might be called an API and vice versa. The AP in API is meaningless.

APIs are how programs on a computer coordinate, how they communicate with the operating system, and how computers coordinate over the internet.
They let programs communicate without worrying about all the details of the work - the caller of an API only cares about results.

Even within a single program, code is usually organized into APIs to make it easier to understand how the many detailed computations being performed
relate to each other. One program may also include another program inside itself, calling the other program's APIs as if they were its own. Programs
designed to be included in this way are called libraries.

Graphical operating systems usually provide libraries to work with files, display windows, play sounds, receive mouse input, and more. Early operating systems (and still some day)
operated in a command line - where the only input and outputs were streams of text - a program would read text from the screen and print text to it.

[![DOS](/images/dos.png "Contrary to popular belief, not all command-line interfaces are DOS. In fact, zsh in alacritty on Arch Linux is a far cry from DOS. Too far away to be heard, maybe.")](https://en.wikipedia.org/wiki/File:PC_DOS_1.10_screenshot.png)

APIs are the glue that connect pieces of a program, libraries, computers, and larger systems.
They serve as a convenient bridge between having to specify each and every step a computer must take, and needing to specify only some technical details
about the inputs and outputs.

APIs range in specificity from something very generic like the above (there are only so many reasonable interfaces you can write for finding text in a string)
to something extremely specific - like an API to draw a window with a form on the screen (there are a great deal of reasonable ways to do this).

When testing that a program works, the only thing that must be tested is the behavior specified by the API (for example, that `Find` returns the right spot inside the text)
rather than the steps the program takes to achieve this. This allows flexibility: perhaps a faster way to find a word in some text might be found later, which
could then replace the implementation.

### The End

Hopefully this helped you understand better the process of programming and how software works.

If you want to learn to program:

* You don't need any background. Many programs involve no math beyond basic arithmetic.

* Try to find something that sounds fun. It's much easier to sink time into learning something you enjoy.

* It's okay to fail. Even professional programmers make **a lot** of mistakes and had just as much trouble learning the basics.
  When programming, you need to get used to constantly seeing error messages and using their information to figure out what went
  wrong.

* You don't need to pay anyone to teach you. There is so, so much free content available online. If you want to work with others,
  there are many online communities and free hackathons (coding events). Focus on learning over cerifications, to start.
  If you have questions, search for answers (or ask them on [Stack Overflow](https://stackoverflow.com) you can't find any).
  This includes the question of where to find programming tutorials.

* Don't worry too much about languages. Many people will tell you conflicting things about the "best" language to start with.
  There is no objective best, just pick one and get started learning.

* Watching and reading are not enough. You need to program in order to learn.

* Have other people look at your code. Send it to friends, or maybe [Stack Exchange Code Review](https://codereview.stackexchange.com).
  They will have all sorts of tips and tricks to make your life easier, but most importantly they will help you write
  code that is easy for others to read.

You don't even need that much time to try it out. Set aside a few hours and try a tutorial online. If you like it, great.
If not, set it down and maybe pick it up again in a few months or years. It gets easier every time.

