%META:TOPICINFO{author=\"kallea\" date=\"1151917980\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>Behavior philosophy\</font\>

[]{.twiki-macro .TOC}

## Introduction

This is mostly philosophical, but contains some bits about why we chose
to go the route we went when implementing the relations system. As an
added bonus, there\'s some history in here as well.

### Elmer

In 2002, I spent a summer writing up Elmer, an NPC in Marrach. The major
accomplishment with the dog was the fact he would **react** to what
people did. Not only would he react, but he would **alter his feelings
towards** people based on how they treated him. This has lead to endless
amounts of opportunity for roleplay, where people have intentionally
made Elmer dislike or like them in order to assist them in portraying
their characters. This may sound a little overexponated, but I don\'t
think I\'ve ever gotten as much praise in my life, as I did for that old
mutt, so he deserves the credit, even if I may not.

Elmer\'s relationship system was a simple map of adverbs and verbs and
relationships numbered from 1 to 7, where each number represented one
of: loved, trusted, friendly, neutral, unfriendly, distrusted, hated.
Additionally, the system had a numeric value that represented a
person\'s position within the current relationship. So when a person did
something good, Elmer bumped their numeric relationship up one point. If
the numeric relationship exceeded a certain amount, Elmer upped their
\"real\" relationship one step, which actually affected his way of
looking at them and which orders he allowed them to give him, and so on.

At some point in there, I had a vision where NPC\'s, items, and
characters would interact with each other, seamlessly, using a protocol
of some kind. The protocol would for instance prompt players with things
such as \"Do you want to \...\" and it would, seamlessly, prompt NPC\'s
with the same kind of questions, that were answered via relayed
callbacks in the NPC. NPC\'s would be able to \"tell\" other NPC\'s
things and the other NPC\'s would be able to respond in whatever fashion
was the most appropriate at the time\...

This system I named \"NIP\", which stood for \"NPC Interaction
Protocol\". The end result was something almost completely different
from what I initially wanted to make, but we are slowly moving toward
that vision. And the reason for this longwinded yap can be found in the
next section.

### The NPC Interaction Protocol

NIP was in some shape finished and ready to be used around 2003.
Immediately, I was asked for the ability to make NPC\'s react to actions
in the same manner that Elmer does; that is, if somebody frowns at the
nipper, the nipper should react to that, and if someone smiles at the
nipper, it should react to THAT. This was obviously a very important
system that many a person wanted to use and found missing in NIP, and
simultaneously, I tried to wrap my head around how to make such a system
implementation that didn\'t involve having the coders sit and do what I
did with Elmer, which was:

    - adverb "happily"  modifies: r+ = 1.2, t+ = 1.2, r- = 0.8, t- = 0.8
    - adverb "hatefully" modifies: r+ = 0.5, t+ = 0.5, r- = 1.4, t- = 1.4 [only-negative]
    - adverb ...

And:

    - verb "smile" is: ranged, positive, strength 5
    - verb "kick"  is: touching, negative, strength 20
    - verb "kiss"  is: touching, positive, strength 20
    - verb ...

As you most likely realize, the above is insanity, and only the most
devoted relations builder would stand writing something like that in an
accurate, complete fashion. Thus, a system had to be developed which did
NOT force the builders to write up rules for each individual verb and
adverb, but still allowed them to define complex rules that did not make
every nipper react the same way to the same verb/adverb combination.
Enter Azrael, Death, Quo, Sahra, Sol, Willow, and \"the relations
project.\"

## The relations project

The relations project is an ongoing project where volunteers from the
various games help out to define generic, subjective rules for verbs and
adverbs. The verbs and adverbs are flagged with various qualities that
represent specific characteristics of the individual verbs or adverbs.
This was necessary in order to allow relation builders to create rules
that were not restricted by the subjectivity of the \"judge\" for the
particular verb or adverb. Each verb or adverb could be one extreme or
the other, or neutral, indicating that the verb did not possess a
quality that met either of the two extremes. An example is \"serious,
neutral, or playful.\" An action can be serious, but it cannot be
playful at the same time. However, an action can be neither serious nor
playful, and this is what neutral represents.

The qualities, their opposites and their corresponding synonyms are as
follows:

  Quality        Opposite       Synonyms
  -------------- -------------- -------------------------------------------------------------
  Serious        Playful        Humorlessness, importance, severity, will, determination.
  Playful        Serious        Irreverence, amusement, satisfaction, happiness, mischief.
  Rough          Gentle         Meanness, violence, brutality, force.
  Gentle         Rough          Forgiveness, compassion, kindness, cultivation.
  Personal       Distant        Closeness, similarity.
  Distant        Personal       Dissent, difference, atypicalness.
  Respect        Disrespect     Mannerly, recognizing, respectful, courtesy, complimentary.
  Disrespect     Respect        Arrogance, forwardness, gall, rudeness.
  Well-meaning   Ill-meaning    Benevolence, friendship, unselfishness, geniality.
  Ill-meaning    Well-meaning   Meanness, spitefulness, hostility, aversion.
  Animalistic    Social         Mannerless, barbaric, odd.
  Social         Animalistic    Refined, mannerly, civil.

Some of these definitions turned out to be slightly problematic. For
example the \"personal/distant\" definition seemed almost tied with the
\"respectful/disrespectful\" definition, in that anything that was
personal, was disrespectful; anything that was distant, was respectful.
We came to realize that personal should mean closeness in the sense that
you know somebody; but not that they necessarily were a friend. I might
be close to my arch nemesis, but I still loathe him/her/it. This is the
closeness that personal indicates.

Adverbs and verbs were naturally handled slightly differently. Verbs
were given bases, e.g. \"the verb smile is well-meaning.\" Adverbs were
given modifiers, e.g. \"the adverb hatefully modifies an action towards
being ill-meaning.\" This resulted in \"smiling\" on its own being
\"well-meaning\", but \"smiling hatefully\" being \"neutral\".

The obvious benefit of going this route is the fact that as time goes
on, the system will be improved as the volunteers refine and add new
verbs/adverbs to the system. Right now, there are 104 verbs and 62
adverbs \"known\" to the system, and this list will keep on growing,
especially as people begin to use the system in their games.

So how would the above flagging be used in an NPC?

## The relations rules editor

\<img src=\"%ATTACHURLPATH%/rre.png\" alt=\"rre.png\" /\>

The above screenshot is from the relations rules editor. As you see,
there is a table with green \"YES\" and red \"NO\" cells, describing the
current rules prerequisites. The table is updated when the prerequisites
are changed, letting you know which verb/adverb combinations will
trigger this particular rule. So for example, in this case, if you annoy
the NPC caringly, the NPC will consider your action friendly, despite
the fact you\'re annoying it. If you annoy it bouncily, animalistically,
etc. the NPC will not interpret the action in the same way. There are
some oddities in there, such as the fact \"acknowledge hatefully\" will
actually make the NPC think you\'re being a-positive, but this can be
explained by the fact that this rule is for close friends of the NPC.
They\'ve already earned their friendship by being nice, so chances are
their \"hatefulness\" is a joke.

Relations rules take some getting used to but I\'ve found them an
extremely powerful way of defining how an NPC should react to various
non-verbal actions, like kicks and punches, licks and kisses, and so on.

\-- Main.KalleAlm - 30 Jun 2006

%META:FILEATTACHMENT{name=\"rre.png\" attr=\"\" comment=\"\"
date=\"1151917803\" path=\"rre.png\" size=\"196667\" user=\"kallea\"
version=\"1.1\"}%
