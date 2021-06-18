%META:TOPICINFO{author=\"alexl\" date=\"1126618740\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<h1\>How to set an NPC up for basic communication\</h1\>

This document contains information on how to set the
[communicate](NIPLibRefCommunicate) library up, including information
about how to define its communications data.

\<div style=\'margin: 10px; border: dashed \#000000 1px; background:
\#eeeeff;\'\> **NOTE:** A [new tool](NIPToolComm) is available which in
more than a few ways makes this document slightly obsolete. It **is**
still a useful read to understand the underlying logics of the
communications system in NIP, but it is no longer required to comprehend
it in full. For more information about the tool in question, go to the
[+NIP tool spec: comm](NIPToolComm) page.\</div\>

This isn\'t entirely trivial. In particular, you need to have a somewhat
nice grasp on how properties in the SkotOS system work. (What is an
array? How do you write an array? What is a multi-dimensional array? See
[Properties and values](Properties and values) f.f.i.)

Now that I\'ve scared you away, let\'s proceed with how to set up an NPC
for communication.

[]{.twiki-macro .TOC}

[Todd Nilson delves into teaching how to apply the Nip Comm
Libraries](UntidyLogWellsNipTutoriual)

[Tidy Version](TidyVerstionWellsTutorial)

------------------------------------------------------------------------

## What do you mean, exactly, by \"communication\"?

That\'s a good question. Look at this example:

------------------------------------------------------------------------

\> smile at janet \"Hi, Janet.\" You smile at Officer Janet, \"Hi,
Janet.\"

Officer Janet raises her eyebrow at you, \"What do you want?\"

------------------------------------------------------------------------

A fascinating scene, but part from that, it is a perfect example of
communication. Summarized, it is: \"a system used by NPC\'s to parse
through sentences and decide which reaction, if any, to give.\"

So how **does** Janet know what to reply when I say \"Hi, Janet.\"? It
may sound like a question best suited for a 5 year old, but it\'s
actually not that simple to figure out.

Let\'s look a little closer at how NIP figures this out further down.
Still with me? You rock.

------------------------------------------------------------------------

## Dissecting Miss Janet

Janet has graciously offered herself up for dissection \-- no, Janet,
lie still .. could someone tighten the gag, please? Thank you.. \-- so
we will cut her up and take a peek inside. It\'s going to be a little
messy but nothing a hot shower can\'t fix.

### Janet herself

Firstly, Janet has the NIP library [communicate](NIPLibRefCommunicate).
If you\'re trying this out (by applying the examples given on a test NPC
in your work area in-game), you should be sure to add this library
before continuing on.

Secondly, there is a separate PropertyContainer which I call
`"Kalle:NIP:comm:janet"`. This is referred to as Janet\'s
\"communications data object\", or \"comm db\". In Janet\'s body, the
property \"nip:trait:communicate:db\" points at this object.

Nothing odd there, I hope.

### The \"comm db\"

In the \"comm db\", we have a few properties along with some behavior
data.

    "family:greetings" = ({ ({ "hello", "hi", "yo" }) })

It\'s okay if you don\'t get this just yet. If you can sort of guess at
what it does, then that\'s good.

    "nip:families" = ({ "greetings" })

This is easier. It\'s a simple list (array) of families\... whatever
those are.

### Families

Before we continue, I need to tell you what I mean by \"families.\" A
family, in this case, is a construct of word combinations which are used
to determine whether or not a particular sentence is corresponding to a
particular reaction.

An example of a family is this, translated into English: \"If someone
says something to me, where their sentence contains one of the words
HELLO, HI or YO, do \...\"

Each family has a one-word name (which may contain hyphens and
underscores), for example \"how-are-you\" or \"greetings\".

Coincidentally, the aforementioned example would become:\<verbatim\>({
({ \"hello\", \"hi\", \"yo\" }) })\</verbatim\>and if we gave it the
family name \"greetings\", we would have\<verbatim\>\"family:greetings\"
= ({ ({ \"hello\", \"hi\", \"yo\" }) })\</verbatim\>

Still leaves a lot to explain, though. So let\'s take a deep breath and
take a look at\...

------------------------------------------------------------------------

### Communication logics

It would be impossible, or at least gravely impractical \-- not to
mention lag-causing \-- for an NPC to parse through every sentence
spoken, analyze it, and make sophisticated attempts at figuring out what
it means. Lots and lots of attempts to do this have been made since the
early 20th century and are still made today. So far, noone has
successfully managed to make a computer \"talk\" like a human being and
understand a human language. In the SkotOS environment, even attempting
to do this kind of thing would be suicidal. But there are ways to make
it appear as if the computer or NPC understands.

A sentence is a group of words thrown together.

\"I hate you,\" is a perfectly valid sentence,

As is \"Did you know that, yesterday, a friend of mine saw that guy from
that show which everybody is so damned obsessed about?\"

The first sentence is very much \"to the point.\" It\'s easy to parse
through some form of system and come up with a fitting response. The
latter is worse, though, since it contains a bunch of words and some, or
most, of them are practically useless.

The first step in figuring out what someone is saying is to consider
which possible IMPORTANT word combinations there can be to say it. \*
(I) hate you. \* (I) dislike you. \* You suck. \* You are (an) idiot. \*
You are stupid.

Those five (and I\'m sure many others) are ways of saying that you hate,
or at least strongly dislike, somebody. The words in parentheses are
unimportant words. Taking those out, we get: \* hate you \* dislike you
\* you suck \* you are idiot \* you are stupid

We now see that there are three \"types\" of sentences in there. 1 (X)
you 2 you (X) 3 you are (X)

\... which means we can actually group those 5 sentences into 3 entries,
like this: 1 you suck 2 hate/dislike you 3 you are idiot/stupid

With me? Okay, because now we\'re going to do some magic stuff with
these things to make NIP understand what they mean.

The communicate library uses a particular logic using multi-dimensional
arrays where each dimension is either an \"and-dimension\" or an
\"or-dimension\". Let\'s look at a couple of examples of how this is
written.

The first dimension is an \"and-dimension\", which means ALL of the
words listed must exist in the sentence for it to be valid: \* NIP:
`({ "hi", "there" })` \* English: hi there \* Logic: hi AND there

The second dimension is an \"or-dimension\", so AT LEAST ONE of the
words listed must exist in the sentence: \* NIP:
`({ ({ "hi", "hello" }) })` \* English: hi/hello \* Logic: hi OR hello

The third dimension is, just like the first, an \"and-dimension\": \*
NIP: `({ ({ ({ "hi", "there" }) }) })` \* English: hi there \* Logic: hi
AND there

The fourth is an \"or-dimension\", fifth is AND, sixth is OR, and so on,
but you know? If you start poking around in the sixth, you\'re in
deeeeeeeeeeeeeeeep waters. You\'ll at the most land on the 3rd or 4th.

Let\'s go back to the example we were working on \-- the hate one, that
is. So, as we said, we now have 3 entries: 1 you suck 2 hate/dislike you
3 you are idiot/stupid

Turning the 1st entry into logic, we get this: \* Logic: you AND suck

It\'s fairly straight-forward. Turning that into a NIP communication
array, we get: \* NIP: ({ \"you\", \"suck\" })

Nothing much to be said there. It\'s all in the first dimension of the
array, and the first dimension is a so called \"and\" dimension.

Turning the 2nd entry into logic, we get this: \* Logic: (hate OR
dislike) AND you

Uh-oh, what\'s with the parentheses? If you\'ve ever written a program
or script, you should know what it does. If you\'ve been poking into
mathematics past the more basic levels, you should also know what it
means. \* (1+2)\*3 = 9 \* 1+2\*3 = 7

Why? Because multiplication takes precedence over addition. In the first
case, 1+2 is done first, then the resulting 3 is multiplied by 3. 3\*3 =
9. In the second case, 2\*3 is done first, then the resulting 6 is added
to the 1. 1+6 = 7. Using parentheses, we can define a precedence that
differs from the natural precedence of mathematics.

Similarly, we are able, and in a lot of cases required, to define a
precedence in communication logics. The logical expression \"hate OR
dislike AND you\" is ambiguous. Do we mean \"hate, or dislike and you\"?
Or do we mean \"hate or dislike, and you\"? There is a difference there,
believe it or not.

In the NIP communicate library, we express parentheses by expanding into
the next dimension. \* Logic: (hate OR dislike) AND you \* NIP: ({ ({
\"hate\", \"dislike\" }), \"you\" })

Remember what we said before? First dimension is an \"and\" dimension,
second dimension is an \"or\" dimension?

Let\'s take the 3rd and final entry \-- \"you are idiot/stupid\" \-- and
turn it into logic. \* Logic: you AND are AND (idiot OR stupid)

This is basically the same deal as \#2 but we have one additional word
and the parenthesized words are at the end, instead of the beginning: \*
Logic: you AND are AND (idiot OR stupid) \* NIP: ({ \"you\", \"are\", ({
\"idiot\", \"stupid\" }) })

Still with me? Amazing! We\'re almost there, promise!

Up until this point, we\'ve only dealt with one sentence type logics.
However, most of the time, this isn\'t enough. Jumping away from the
current example for a sec, let\'s take greeting someone as an example.
\* Hi! \* Hello! \* Yo! \* Good day/morn/morning/eve/aft/afternoon!

These sentences all mean the exact same thing, which should be given the
exact same type of response. But they\'re constructed differently! We
have two sentence types: \* (X)! \* Good (X)!

Saying \"Good hi\" would probably be silly. Saying \"Hi day\" would
probably be silly too. Let\'s quickly turn these two into logics and NIP
structures: \* Type: (X)! \* Logic: hi OR hello OR yo \* NIP: ({ ({
\"hi\", \"hello\", \"yo\" }) })

\* Type: Good (X)! \* Logic: good AND (day OR morn OR morning OR eve OR
aft OR afternoon) \* NIP: ({ \"good\", ({ \"day\", \"morn\",
\"morning\", \"eve\", \"aft\", \"afternoon\" }) })

There is, hopefully, nothing too surprising in those two. The surprise
comes now (maybe):

We want to put these two together into one single logic. How do we do
that? \* Type: (X)! or Good (X)! \* Logic: (hi OR hello OR yo) OR (good
AND (day OR morn OR morning OR eve OR aft OR afternoon)) \* NIP: ({ ({
\"hi\", \"hello\", \"yo\", ({ \"good\", ({ \"day\", \"morn\",
\"morning\", \"eve\", \"aft\", \"afternoon\" }) }) }) })

Well, that may look hairy, but it\'s really not. All I did was extend
the logic to be each sentence type parenthesized on its own with OR in
between. The trickiest part is, honestly, the matching of the ({ })\'s.
There are a lot of them in there, aren\'t there\...?

So let\'s try that on our previous example. We had: \* Sentence \#1: You
suck! \* Logic: you AND suck \* ({ \"you\", \"suck\" })

\* Sentence \#2: (I) hate/dislike you. \* Logic: (hate OR dislike) AND
you \* NIP: ({ ({ \"hate\", \"dislike\" }), \"you\" })

\* Sentence \#3: You are (an) idiot/stupid. \* Logic: you AND are AND
(idiot OR stupid) \* NIP: ({ \"you\", \"are\", ({ \"idiot\", \"stupid\"
}) })

Thus, we get: \* Logic: (you AND suck) OR ((hate OR dislike) AND you) OR
(you AND are AND (idiot OR stupid)) \* NIP: ({ ({ ({ \"you\", \"suck\"
}), ({ ({ \"hate\", \"dislike\" }), \"you\" }), ({ \"you\", \"are\", ({
\"idiot\", \"stupid\" }) }) }) })

Can you nest your way through that? That one\'s\... pretty big. Let\'s
dissect it for the sake of:

  part                    dimension   and/or   comment
  ----------------------- ----------- -------- ------------------------------------------------------------------------------------------------------------------------
  ({                      1           AND      Initial mode is \"AND\", always.
  ({                      2           OR       
  ({                      3           AND      Since we want \"you AND suck\", we need to actually hop into the 3rd dimension right away
  \"you\", \"suck\"       3                    you AND suck
  })                      2           OR       Back down to the OR level. So far, we\'ve done (you AND suck), and now we want to start on ((hate OR dislike) AND you)
  ,                       2                    (you AND suck) or \...
  ({                      3           AND      
  ({                      4           OR       hate *OR* dislike, remember?
  \"hate\", \"dislike\"   4                    hate OR dislike
  }),                     3           AND      hate/dislike, AND \...
  \"you\"                 3                    
  })                      2           OR       Back down to OR level again. We\'ve got two out of three done so far. Go us!
  ,                       2                    (you AND suck) OR ((hate OR dislike) AND you) OR \...
  ({                      3           AND      
  \"you\", \"are\",       3                    you AND are AND \...?
  ({                      4           OR       
  \"idiot\", \"stupid\"   4                    idiot OR stupid
  })                      3           AND      
  })                      2           OR       
  })                      1           AND      
  })                      0           n/a      End.

------------------------------------------------------------------------

### Families, again

Okay, that was a little long, but never fear, it\'s the messiest it\'ll
get.

We\'re back at families, though. A family is, as you may have guessed,
an identifier which points to a communicative logical construct, like
what we played with just a moment ago. In Janet\'s comm db, we
had:\<verbatim\>\"family:greetings\" = ({ ({ \"hello\", \"hi\", \"yo\"
}) })\</verbatim\>Which is equal to the sentence type \"(X)\", or,
\"Hello/hi/yo\". It also responds to \"\<whatever\> (X)\", \"(X)
\<whatever\>\", \"\<whatever\> (X) \<something else ever\>\" and
\"\<whatever\> (part of X) \<something else ever\> (other part of X)
*and so on and so forth*\".

In short, any sentence which contains the words listed will be
considered an appropriate target for this particular family. What next?
In Janet\'s case, it\'s simply recorded behavior. Some lustful builder
has already recorded behavior for Officer Janet, in **the comm db
object.**

When recording behavior, you usually choose an object and a
mood/situation. When doing so for families, you prefix the
mood/situation with the family name.

In this case, the family name is \"greetings\". The mood name for
\"catch \'em all\" is \"db\" (since we don\'t want to go into \"how
would Janet respond to \'Hi\' if she\'s angry or sad or hungry etc.\").

Putting the family name and the mood name together we thus get:
\"greetings:db\" which we would then use when we recorded behavior, as
such:\<verbatim\>+nip \"record start Kalle:NIP:comm:janet
greetings:db\"\</verbatim\>

\... but since someone\'s done this for us already, we don\'t have to do
that.

I will soon put in examples on what else can be done using families and
communication. For now, this should provide you with the basics, and the
tricky part. I will attempt to write up a tool that can be used to
convert to and from \"English\" structures, like \"(hi OR hello) AND
there\" into a NIP structure. More info on this later, but don\'t hold
your breath on this one. It might take awhile.

\-- Main.KalleAlm - 24 Apr 2005
