%META:TOPICINFO{author=\"kallea\" date=\"1069693680\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>Tutorial: Predator and prey
(cat\'n\'rat).\</font\>

*This tutorial describes how to create two NPC\'s and set them up as
predator, and prey. I am going to presume that you are well versed with
how to create and set up NPC\'s in general, and will mainly focus on the
aspect of the predator/prey features. However, if you follow the
instructions step-by-step and do as I do, you will end up with the
correct results, regardless.*

The first thing I\'m going to ask you to do is to set two NPC\'s up. My
suggestion is a cat and a rat, but it\'s up to you what you choose in
the end (snake/mouse, lion/gazette, wolf/rabbit, whatever). Set these up
as NPC\'s and place them both in the same room (summon, don\'t spawn).

[]{.twiki-macro .TOC depth="4"}

------------------------------------------------------------------------

# Set npc:master in the prey NPC.

The first thing I\'m going to ask you to do is to target the PREY NPC
(the mouse/gazette/rabbit/whatever) with the following command:

    > +setp [target] "npc:master 1"

This will make any predators that see this object disregard it
immediately, as it is a \"master\" copy, and we don\'t want those
destroyed or eaten.

------------------------------------------------------------------------

# The predator, basic.

The predator NPC is the hunter. It\'s the NPC that will eventually track
down and (attempt to) turn prey NPC\'s into a juicy dinner. We\'re going
to start by defining the predator NPC.

## Adding a bunch of libraries.

We\'re going to hardcore-like add a few libraries to the predator. In
this tutorial, we\'re going to use emotes (behavior) and eating \-- and,
of course, the predator library.

From here on, I\'m going to refer to the **predator** as \'cat\'.

    > +setp cat "add emoting"
    > +setp cat "add offers"
    > +setp cat "add eating"
    > +setp cat "add predator"

You should be getting a bunch of output after each command. I\'ve chosen
to not print this information out, here.

------------------------------------------------------------------------

## Look over what we\'ve got now.

Let\'s take a look at the values we have gathered up at this point:

    > +stat cat "property:export:nip:*"
    -- Properties (export:nip:*)--
    Property: export:nip:offer:scripts = ({ "handler:offer:eating" })
    <b>Property: export:nip:stats:agility = 10
    Property: export:nip:stats:offense = 10</b>
    Property: export:nip:trait:eating:accepts = ([ "base:edible":1, "nip:food":1 ])
    Property: export:nip:trait:eating:burn = 300
    Property: export:nip:trait:eating:grammes = 2000
    Property: export:nip:trait:emoting:frequency = 10
    <b>Property: export:nip:trait:predator:prey = ({ "prey" })
    Property: export:nip:trait:predator:scavenger = 0</b>

Bold entries are settings that relate to the predator library. We\'ll
eventually change most of those.

\* \"nip:stats:agility\" determines how agile the predator is \*
\"nip:stats:offense\" determines how skillful the predator is in
attacking \* \"nip:trait:predator:prey\" is a list of the various prey
types this NPC would consider valid targets \*
\"nip:trait:predator:scavenger\" is a flag which decides whether or not
the NPC is a scavenger. If unset (default), the NPC will ONLY eat food
it killed itself.

We\'re leaving these be for now, and turn our attention over to the prey
NPC.

------------------------------------------------------------------------

# The prey, basic.

The prey is the hunted. It is the food for the predators of the world.
We could leave it at that, if it wasn\'t for the fact we\'re actually
going to tackle simulating the prey, and include support for it to
\"look dead\" among other things.

From here on, I will refer to \'the prey\' as \"rat\".

## Adding a bunch of libraries.

Once more, we\'re going to simply toss in a few libs in the NPC without
giving them much thought. The rat\'s going to have emoting, and of
course prey.

    > +setp rat "add emoting"
    > +setp rat "add prey"

You should be getting a bunch of output after each command. I\'ve chosen
to not print this information out, here.

------------------------------------------------------------------------

## Looking over the values we\'ve got.

Let\'s take a peek at the rat\'s values now as well.

    > +stat rat "property:export:nip:*"
    -- Properties (export:nip:*)--
    <b>Property: export:nip:start = ({ "handler:start:prey" })
    Property: export:nip:stats:agility = 10
    Property: export:nip:stats:defense = 10</b>
    Property: export:nip:trait:emoting:frequency = 10
    <b>Property: export:nip:trait:prey:type = ({ "prey" })</b>

Bold values indicate properties that are related to the \'prey\'
library;

\* nip:start is a relatively undocumented wrapper, which contains a list
of scripts to execute when a copy of the NPC is spawned. We may safely
disregard what this further means for now. \* nip:stats:agility defines
how agile the NPC is \* nip:stats:defense defines how skillful the NPC
is at fending off attacking predators \* nip:trait:prey:type contains a
list of the prey\'s type(s). We\'re going to look into this a little
more in a moment.

------------------------------------------------------------------------

# Seeing the result.

Unsummon both your NPC\'s and spawn a copy of each. (Don\'t forget to
\"drop\" them, since they probably end up in your hands.)

After doing so, enable the cat.

    > +nip cat "live"

Now go grab a sandwich and a beer. When you come back you should see
something like this:

    A brown rat dies from its wounds.

    A black cat takes the corpse of a brown rat.

    A black cat takes a bite of the corpse of a brown rat.

    A black cat takes a bite of the corpse of a brown rat.

    A black cat takes a bite of the corpse of a brown rat.

    A black cat finishes eating.

But it\'s probably gonna be more like a spammage of \"\[predator\] takes
a bite of the corpse of \[prey\]\", neverending. Remember that each bite
taken is 0.015 mass. Which means if you set an NPC up with e.g. 0.2 mass
(which is relatively tiny), it\'s going to take 14 bites to eat it all.
For a large animal, this isn\'t odd at all. For smaller beasts, it may
be ridiculous that a cat takes fourteen bites of a mouse.

Slay the predator (and the rat, if it\'s not eaten by now) and summon
the two master objects again.

## Tweaking the values.

Things are working now, but we need to tweak those values we looked at
earlier. For instance, there is **no** message whatsoever when the rat
manages to escape an attack. And there is only the \"*A brown rat dies
from its wounds.*\" message to indicate that the brown rat was ever
attacked.

These two types of messages are handled through behavior data objects.
If you don\'t know what these are, you may want to [check into the \"how
to record behavior\" how-to](NIPHowRecord) as well as the [scenery
tutorial](NIPTutorialScenery).

To make this useful for you I\'m going to use my name as the name of the
behavior objects. I\'m simply going to name them
<Data:tutorial:kalle:predator> and <Data:tutorial:kalle:prey>.

### The predator behavior

The first one is going to contain predator specific data. The predator
behavior currently contains only one \"situation\" (or \"mood\"),
**KILL**.

This situation is when the predator kills its prey. So let\'s record a
few \'killing\' actions.

Start by creating the data object for the predator. Name it
<Data:tutorial:yourname:predator>.

    > +cobj propcontainer "Data:tutorial:kalle:predator"
    OK.

The next thing you wanna do is posses the predator.

    > +possess cat
    You inhabit a black cat.

Now we need to set the rat up as our target. This is explained in detail
in the [scenery tutorial](NIPTutorialScenery).

    > +nip rat "scene prey"
    Scene role (prey) set to a brown rat.

Finally, before we start emoting, we need to enable recording in the
<Data:tutorial:yourname:predator> object, for the situation KILL.

    > +nip "record start Data:tutorial:kalle:predator KILL"
    Begun recording for mood/condition 'KILL' in <Kalle:tutorial:cat>. When you are done, type: +nip "record stop"

Now we emote a few attacking moves. To make our moves actually go
through, start by +forcing the rat to \"consent allow all\"

    > +force rat "consent allow all"
    Forcing a brown rat to: consent allow all
    Consent list for a brown rat has been modified.

    > suddenly pounce on rat "!
    You approach a brown rat.

    You suddenly pounce on a brown rat, "!"
    [STO:1]

    > swiftly break rat's neck "!
    You swiftly break a neck, "!"
    [STO:2]

    > bite rat's head predatoril "!
    You bite a head predatorily, "!"
    [STO:3]

    > swing my claw at rat suddenl "!
    You swing your claws at a brown rat suddenly, "!"
    [STO:4]

    > +nip "record stop"
    Stopped recording in <Kalle:tutorial:cat>.

    > +nip "scene --"
    Scene deleted.

Feel free to go on if you wish. Four is more than enough to prove my
point, however.

The two last commands unloads the recorded (important) and removes the
scene set up (not equally important, but a good thing to do,
nonetheless).

------------------------------------------------------------------------

### The target (prey) behavior

Now we\'re going to record for the prey. We\'re going to record for when
the prey manages to evade the predator\'s attack.

    > +cobj propcontainer "Data:tutorial:kalle:prey"
    OK.

    > +possess rat
    You inhabit a brown rat.

In the predator recording, we set the rat up as the role \"prey\". In
this case, we\'re going to set the **cat** up as the \"**predator**\".
These roles are specifically required and used in the predator/prey
feature, and must be named exactly so.

    > +nip cat "scene predator"
    Scene role (predator) set to a black cat.

Previously, we started recording in the <Data:tutorial:kalle:predator>
object, for the situation \"KILL\". Now, we\'re going to record in
<Data:tutorial:kalle>:**prey** for the situation \"**EVADE**\":

    > +nip "record start Data:tutorial:kalle:prey EVADE"
    Begun recording for mood/condition 'EVADE' in <Kalle:tutorial:rat>. When you are done, type: +nip "record stop"

And we record. I am +forcing the cat to \"consent allow all\" just in
case.

    > +force cat "consent allow all
    Forcing a black cat to: consent allow all
    Consent list for a black cat has been modified.

    > hysterically run from cat "!
    You hysterically run from a black cat, "!"
    [STO:1]

    > squeakil scamper around cat "!
    You squeakily scamper around a black cat, "!"
    [STO:2]

    > fearfull run from cat's paws "!
    You fearfully run from a black cat's paws, "!"
    [STO:3]

    > jump over cat's paws evasive "!
    You jump over a black cat's paws evasively, "!"
    [STO:4]

    > +nip "record stop"
    Stopped recording in <Kalle:tutorial:rat>.
    > +nip "scene --
    Scene deleted.

    > +possess kalle
    You inhabit Kalle.

Again, feel free to continue. Four is more than enough.

------------------------------------------------------------------------

### Set up the behavior properties.

We\'ve recorded for both the rat and the cat, but so far we haven\'t set
them up to use the stuff we recorded. This is simple.

    > +setp cat "nip:behavior:predator <Data:tutorial:kalle:predator>"
    > +setp rat "nip:behavior:prey <Data:tutorial:kalle:prey>"

And we\'re done.

------------------------------------------------------------------------

## Taking another look at things.

Unsummon the NPC\'s again, and spawn a copy of each into your
environment.

Now, unfortunately, you need to consent these fellows manually. A fix to
this will hopefully come to life at some point. For now, do:

    +force cat "consent allow all"
    +force rat "consent allow all"

Now enable the cat.

    > +nip cat "live"

And grab another beer.

Note that the amount of time you need to wait is directly related to the
amount of things in the room. The more stuff, the longer wait. This is
because the predator will grab random stuff continuously, and if
whatever it found is valid prey, it will attack. This is the only
\"randomizer\" the predator goes by.

Depending on how fast a drinker you are, the size of your beer, and the
amount of things in your environment, about half a bottle later you
should see something similar to the following (depending on randomness
and what you actually recorded previously):

    A black cat moves from the gate to the living room to a brown rat.

    A black cat swiftly breaks a brown rat's neck.

    A brown rat dies from its wounds.

    A black cat takes the corpse of a brown rat.

Or, if the rat \"wins\" the initial attack, you should see something
like:

    A brown rat hysterically runs from a black cat.

    A brown rat moves from the gate to the living room to a black cat.

    A brown rat squeakily scampers around a black cat.

    A black cat moves from the gate to the living room to a brown rat.

    A black cat swings her claws at a brown rat suddenly.

    A brown rat dies from its wounds.

    A black cat takes the corpse of a brown rat.

# Note about prey types.

As we said earlier, the predator has:

    Property: export:nip:trait:predator:prey = ({ "prey" })

And the prey has:

    Property: export:nip:trait:prey:type = ({ "prey" })

These two properties coordinate in a way that requires a brief example.

\* A cat would look at a rat as prey. \* A cat would also look at a
mouse as prey. \* A cat would in fact probably regard a squirrel as
prey. \* A cat would probably regard a bunny as prey. \* But, a cat
wouldn\'t consider a gazette as prey.

Now, if we look at it the other way:

\* A rat is an animal, a small rodent. \* A mouse is an animal, a small
rodent. \* A squirrel is an animal, a small rodent. \* A bunny is an
animal, a small mammal. \* A gazette is a medium-sized animal.

Here we see a bunch of \"classes\" for animals. We\'ve listed: rat,
small, rodent, mouse, squirrel, bunny, mammal, gazette, medium-sized.

If we chose to use these classes, then the cat predator object would
*probably* have the following property:

    nip:trait:predator:prey = ({ "rat", "small", "rodent", "mouse", "squirrel", "bunny", "mammal" })

A rat prey, would probably have this:

    nip:trait:prey:type = ({ "small", "rodent", "rat" })

A bunny prey, would probably have this:

    nip:trait:prey:type = ({ "small", "mammal", "bunny" })

A gazette would have:

    nip:trait:prey:type = ({ "gazette", "medium-sized" })

Now, the trick comes where the cat finds prey in the wilderness. If the
cat found a bunny (small, mammal, bunny), the check would go: \* Do we
have \"small\" listed in our predator:prey list? Yes. \* Do we have
\"mammal\" listed? Yes. \* Do we have \"bunny\" listed? Yes.

Valid target, then.

But, if the cat found a gazette (gazette, medium-sized), the check would
go: \* Do we have \"gazette\" listed in our predator:prey list? No.

Invalid target.

------------------------------------------------------------------------

# Conclusion

The NPC\'s currently solve consent issues by moving the predator into
proximity with the prey right before the attack. This is a hack, but it
works, and it is a work-around for the consent-issues earlier.

The predator and the prey NPC both have some values you can tweak around
to make things better. Take a peek at the [todo:
predator](NIPTodoPredator), as well as the
[predator](NIPLibRefPredator)- and [prey](NIPLibRefPrey)-library
reference pages for details on each of these properties.

\-- Main.KalleAlm - 20 Nov 2003
