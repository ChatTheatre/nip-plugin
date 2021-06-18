%META:TOPICINFO{author=\"kallea\" date=\"1084984202\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<h1\>Tutorial: Hack\'N\'Slash game\</h1\>

So you want to make a mindless text-based DOOM game? Sure, why not.
Let\'s go through how to do this, step by step. Well, almost. You\'re
going to have to come up with some type of combat system yourself, but
the automated NPC stuff will be ready for you here.

This tutorial is going to flat out presume that your combat system is a
timing-based, imperative-controlled system - like duelling in Marrach.
If it is, for example, based on a turn-based combat system or similar,
this won\'t get you \"all the way.\" It might prove helpful, though, who
knows?

This tutorial is divided into the following segments:

[]{.twiki-macro .TOC}

------------------------------------------------------------------------

## Before We Begin

Before we start, here\'s a checklist of things you\'ll need to 1) have,
or 2) make, before you continue.

\* A body of some sort for your NPC. \* Any kind of weapons required to
fight. \* **A functional combat system**

To keep things simple, I\'m going to presume from here on that you\'ve
made two **verbs** for your combat system \-- punch and rest \-- and
that you\'ve made a \"thug\" NPC which will try to punch anyone he
encounters off their socks. The thug will check the property
\"combat:health\", and if it drops below 50, he\'s going to rest more
often than he punches. If it\'s above 50, he\'s going to punch more
often than he rests.

Our \"punch\" command has a \"time setting\" of 2 seconds. This means if
we perform a punch, we will see \"You are too busy with something
else.\" if we try to do anything during the following 2 seconds. Our
\"rest\" command has a time setting of 1 second, during which we\'ll be
extra vulnerable, etc. All this is hypothetical and in the combat system
I\'m not going to write here. However, these facts are important to keep
track of later on, when we start creating the maps.

------------------------------------------------------------------------

## 1. Adding the appropriate libraries to the NPC.

Initially, we only really need one library \--
[fighting](NIPLibRefFighting).

Later on, we might want to fancify things a bit, but let\'s keep things
simple for now.

------------------------------------------------------------------------

## 2. Setting the properties in our thug NPC by hand.

While not the best nor most productive solution on the planet, setting
the properties by hand is quite educational, and will give you some
understanding on how the fighting system works. It\'s very simple, but
it looks overwhelming at first.

### 2.1. The imperative map.

The first and most important property is
`nip:trait:fighting:imperative_map`. It contains a mapping with each
possible combat action, pointing to each possible next combat action for
that action. which in turn points to an integer representation of how
likely it is that the NPC should perform that particular action. Sounds
confusing? It\'s not. Look at this:

    ([ "punch" : ([ "rest"  : 100 ]),
        "rest"  : ([ "punch" : 100 ]) ])

According to the above setup, the NPC will enter the fight and, say,
begin with a punch. After punching, the NPC will look at the \"punch\"
map (`([ "rest" : 100 ])`) and see what to do next. Since it only has
one viable alternative there, we can say with 100% certainty that the
NPC will perform a \'rest\' after performing a \'punch\'.

The next time, the NPC will scan the \"rest\" map
(`([ "punch" : 100 ])`), because the last action was a \"rest\". This
will go on until the combat is ended. (More about initiating/ending
combat later on.)

As you can see, the behavior of our friend the thug will be dreadfully
predictable. He\'ll punch, then rest, then punch, then rest, then punch,
etc. While we can\'t do that much with a 2-verb combat system, we can
still make things a tad more interesting there. Let\'s revamp the
`nip:trait:fighting:imperative_map` property once more before we
continue looking at the rest of the properties:

    ([ "punch" : ([ "rest"  : 60,
                         "punch" : 40 ]),
        "rest"  : ([ "punch" : 60,
                         "rest"  : 40 ]) ])

In the above scenario, there\'s going to be a lot more unpredictability
in which the choosing of the command to perform is made. There is a 60%
chance that the thug will, after punching, perform a rest, and a 40%
chance that he will perform another punch. As you probably realize, this
property can turn into a monster quickly, but once you understand the
basics behind it, it\'s really not that big a deal. Let\'s move on.

### 2.2. The delay map.

The next property is `nip:trait:fighting:delay_map`. This map handles
the time between each action, for each action. Recall me saying that the
punch took 2 seconds to perform, and the rest took 1? This is where we
feed this knowledge to the fighting system.

    ([ "punch" : ({ 2.1, 3.0 }),
        "rest"  : ({ 1.1, 2.0 }) ])

The above says, in English: \"Each time I perform a \"punch,\" I should
wait between 2.1 second and 3.0 seconds before my next action, and each
time I perform a \"rest,\" I should wait between 1.1 second and 2.0
seconds, before my next action.\"

Now, before you go putting ({ 0.01, 0.02 }), you should know that these
values heavily affect the server performance. If you set these too low,
enough amount of NPC\'s are going to cause serious system lag, and your
game will be unplayable. Especially in a setting where timing is of
essence. I recommend ({ 0.1, 0.5 }) as being the absolute lowest.

Also take into consideration that these values in a way define how
\"good\" the NPC is. How fast the NPC is at acting. If you deliberately
set these values to slower than what the system will accept, the NPC
will be generally regarded as weaker/less skilled. This is a classical
way, commonly used in games to simulate varyingly difficult NPC\'s.

### 2.3. The condition map.

At this point, we\'ve almost gotten all the way to a fully functional
NPC combat system, actually. Not too difficult yet, is it? There\'s one
thing missing though - the link between the NPC\'s behavior and the
NPC\'s state.

Take for example an NPC with a grave wound. He or she would probably
fight less offensive and try to keep their breath by resting more than
an NPC who just skipped out of bed, having swallowed his last
mustard-smeared baguette.

In order to do this, we need to come up with some appropriate property
for our combat system. A property that tells us how wounded we are.
Let\'s say there is an integer value, `trait:wound-count`, which is set
to between `0` and `4`, where `4` equals `death` and `0` equals
`unwounded`.

Now, let\'s say that the middle-ground for this is 2. Below 2, and
we\'re considered relatively \"healthy,\" and we can slack on the
resting and be more aggressive. Above 2 and we\'re in a grave state and
need to rest more.

So, how on earth do we do this?

The condition map, `nip:trait:fighting:condition_map`, is a semi-complex
mapping which consists of a number of settings, each in order to create
any number of rules for any number of properties. The syntax for the
condition map is as follows:\<verbatim\>(\[ \"\<property in NPC\>\" : ({
\<middle\>, \<effect\>, ({ \<positive affected actions\> }), ({
\<negative affected actions\> }) \])\</verbatim\>

\* `<property in NPC>` - This is the name of a numeric property that we
grab from the nipper each time. \* `<middle>` - This is the \"middle\"
value. The middle value is subtracted from the property taken from the
NPC to determine whether the property is negative or positively
affecting the NPC. If the resulting value
(`<property from NPC> - <middle>`) is less than zero, the negative
affected actions list is modified and the positive affected actions list
is untouched. If the resulting value is more than zero, the positive
affected actions list is modified and the negative list is untouched. \*
`<effect>` - The resulting value is multiplied by the effect to receive
the final value which in turn is added to each and every action listed
in the appropriate actions list, **if these actions are also available
in the imperative map**.

Enough confusing ourselves. Here\'s an example:

    ([ "trait:wound-count" : ({ 2, 10.0, "rest", "punch" }) ])

In the above example, we\'re grabbing `trait:wound-count` from the
nipper. We subtract 2 from that. If the nipper is unwounded, that means
we\'ll get -2. That\'s negative, which means \"punch\" will be affected.
We multiply that with the effect - 2 \* 10 = 20. And now we add 20 to
\"punch\".

If the NPC has a grave wound (`trait:wound-count` set to `3`), we would
subtract 2 from 3 - and get 1. 1 is positive, which means \"rest\"
should receive a bonus. 1 \* 10 = 10, thus rest receives a +10 bonus.

The `<middle>` value can be used to determine how aggressive our thug
is. By setting the middle value higher, we will have a higher threshold
before we start going into \'rest\' mode. By setting it lower, we will
easier go into \"rest\" mode as soon as we\'re wounded.

At this point, we\'re done with the properties. Now it\'s time to go
into the whole aspect of \"initiating a fight\".

------------------------------------------------------------------------

## 3. Initiating and resolving a fight.

There are about as many solutions to initiating a fight as there are
fighting systems out there.

In our simple combat system, Harry types \"fight Lucy\", and Lucy
responds by typing \"fight Harry.\" When both have done so, each
participant (Harry and Lucy) acts \"combat/start\", which in Merry would
look something like:\<verbatim\> Act( \$actor, \"combat/start\" ); Act(
\$opponent, \"combat/start\" );\</verbatim\>

When a fight ends, for whatever reason, be that A wounds B, or A kills
B, or B surrenders, etc., each participant acts \"combat/stop\" to
signal the end of the fight, which in Merry would look something
like:\<verbatim\> Act( \$actor, \"combat/stop\" ); Act( \$opponent,
\"combat/stop\" );\</verbatim\>

Now, we can pretty much presume the following: \*
`merry:react:fight-(role)` can be used as a trigger for **challenges
upon the NPC** \* `merry:act:combat/stop` can be used as a trigger for
**current fight has ended** \* `merry:act:combat/start` can be used as a
trigger for **new fight began/opponent accepted our challenge**

To keep things simple, we\'re going to restrict ourselves to being
challenged and accepting challenges. We won\'t go into the whole ordeal
of detecting targets and such.

And we\'ll still keep to the whole matter of consent, which might not be
desired, in the end.

### 3.1. Detecting a challenge placed upon us.

Our thug must be able to detect when someone tries to attack him.
Luckily for him (and us), we\'ve already figured out that
`merry:react:fight-(role)` is the appropriate signal for detecting this
(where `(role)` is e.g. \"who\", depending on how the fight verb is set
up).

Since this system will not include weapons and such, the script that
handles the initiating will be very simple.

    --- merry:react:fight-who in Thug NPC ---
    /*

      D=We're challenged! And we'll gladly accept!

    */

    /*
     * Let the action fall through.
     * It's important that we have TRUE set
     * as the second argument to the $delay()
     * call below. Otherwise, the fight command
     * will not go through in full.
     */
    $delay(2+random(2),TRUE);

    /*
     * Challenge back.
     */
    Act( this, "fight", $who: $actor );

    /*
     * Hand over control to the fighting system.
     */
    ::core_fight_init();
    -----------------

That\'s it for the initializing of fights. Possibly, you might want to
make the NPC grab and wield a sword or a machine gun or whatever he/she
might be using.

### 3.2. Detecting the end of a fight.

Equally lucky are we that we already at this point know about
`merry:act:combat/stop` being the signal triggered when a fight ends. So
we simply do\...

    --- merry:act:combat/stop in Thug NPC ---
    /*

      D=Fight is over. Stop fighting.

    */

    /*
     * Immediately (no delaying) signal to the 
     * fighting thread that it should abort.
     */
    ::core_fight_done();

    /*
     * Then simply return TRUE.
     */
    return TRUE;
    ---------------

------------------------------------------------------------------------

## 4. Try it.

If you actually got this far, congratulations. I know it\'s not easy to
go through all that nonsense without once seeing results on the way.
It\'s unfortunately not that easy to see the results without getting
this far, which we\'ve managed to do now. So cheers to us.

Firstly, unsummon your thug and +spawn a copy of him. Enable the copy,
if that will do anything at all, and then try to fight him. If all went
well, he will accept your challenge and proceed to beat the snot out of
you. If not, make use of the error logs. They\'re fascinatingly helpful.

\-- Main.KalleAlm - 09 May 2004
