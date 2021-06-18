%META:TOPICINFO{author=\"kallea\" date=\"1092252000\" format=\"1.0\"
version=\"1.3\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>Setting up a scene.\</FONT\>

\[*Also check out the [Recording class](NIPClassRecording) for a
thorough documentation on the aspect of behavior.*\]

**Introduction:**

With the new conditional behavior system in place, it\'s time to tackle
the concept of how to make a CNPC behave in various situations.

We\'ve already covered how to record for when a CNPC is hungry or
sleepy, or happy, sad, etc. but those are basic matters. What if we want
to set up how a guard acts when someone of low rank wants to enter a
room he\'s not allowed to enter?

Or what if a high-ranked person wishes to enter a room he\'s allowed to
enter? Immediately, we can think of a few emotes here. Bowing deeply to
the latter. Snorting unamusedly at the first.

What if we want to record how a cat interacts with someone it\'s fond
of? Or someone it despises?

In this tutorial we\'re going to set up a few scenes to get to know how
this particular part of the system works.

**The servant and the rat.**

So, we\'ve decided to write up the behavior for a servant who sees a
rat. Relatively easy, and straight forward.

In this scene, there are really only one external subject, the rat. Then
we of course have the standard, always-available, here and me/any
bodypart of mine.

**The first thing we\'re going to do** is to find some appropriate
object that will serve as the rat in the scene. To be simple and
accurate, I\'ve decided to +spawn a copy of NPC:child:rat/black

    StoryCoder Kalle's black rat arrives.
    You drop a black rat.

There we go. Now, due to this scene\'s simplicity, I can set it up now.

Before I do, however, some things need to be explained.

Like, every subject in the scene has a symbolic name. Right off, the
room I\'m in has the symbolic name \"here\". That\'s always there. I
have the symbolic name \"me\". Any details of mine have the symbolic
names \"me:detailname\", so my arm would be \"me:arm\".

When we set up a scene, we add external symbolic names to various things
in our immediate presence. In our case, we\'re going to give the rat the
symbolic name \"beast\". This is by our own choice, we could just as
well call it \"rat\" or \"animal\" or \"furrything\". I will explain the
reason for why this is the way it is shortly.

**To set it up,** I use the +nip command\'s \'scene\' function. This
function is fairly simple and straight-forward. I +nip at something and
evoke \"scene symbolic name\".

As I said before, I decided to give the rat the name \"beast\". Thus, I
do:

    > +nip rat "scene beast"
    Scene role (beast) set to a black rat.

And I\'m done. Trying not to repeat myself in other documents (namely,
the how to for recording behavior), I\'m going to swiftly step through
setting up the behavior database for the servant.

**WOE** \* I clone Core:PropertyContainer \* I give the cloned copy the
name <Data:NIP:behavior:servants:beast>

Now that I\'ve created the woe object, there\'s something I need to
cover before I start recording.

In this particular case, the -mood- I use is actually not a real mood.
It\'s some appropriate name for the situation in question. In this case,
I\'m going to call the mood \"BEAST\". It\'s not a real mood, and won\'t
ever be added to the array of moods in the NPC itself. It\'s something
that will be triggered through other means. More about that later.

\* I type in \<PRE\>+nip \"record start
<Data:NIP:behavior:servants:beast> BEAST\"\</PRE\>

And I\'m done. Now I can interact with the rat and it will be recorded
appropriately. So I do this swiftly:

    ---
    > squeak at rat "!Eeep!"
    You squeak at a black rat, "!Eeep!"
    [STO:1]

    > grimace disgusted at rat "!Someone take it away!!"
    You grimace disgustedly at a black rat, "!Someone take it away!!"
    [STO:2]
    ---

That\'s enough to prove my point. Now, I\'ve got a servant set up for
this, as the process on how to do this is fairly well covered in other
areas. But here\'s a quick \"set up 1-2-3\" in case you\'re unsure. I\'m
using the \'emoting\' library.

\* +nip \"set woename-for-npc\" \* +setp NPC \"add emoting\"

Now, I want to make a little script that checks if any rats are in my
immediate vicinity. If I find a rat, I trigger the \"beast\" behavior.
I\'m going to call this script lib:beast:decide and put it in a new
library, which I set up and call Marrach:NIP:lib:beast

\* Clone Core:PropertyContainer \* Rename to Yourtheatre:NIP:lib:beast

    --- <B>merry:lib:beast:decide</B> in <B>Marrach:NIP:lib:beast</B> ---
    /*

        D=Rat-squeak sig-hook script.

    */

    /* We need an object, and an object array for the room. */
    object env, *inv;

    /* And an integer for the check. */
    int i; 

    env = this."base:environment"; /* We need the room itself. */
    inv = env."base:inventory"; /* And the room's 'inventory'. */

    /* Step through each item in the room's inventory, */
    for( i = 0; i < sizeof( inv ); i++ )

      /* And check the room to see if we find any rats. */
      if( inv[i]."base:volition" && 
            arr_to_set( 
              Get( inv[i], "details:"+NRefDetail(inv[i])+":snames" )
            )["rat"] ) {

         /* We found a rat! */
         $beast = inv[i];

         Call( this, "handler:emoting:parse", $db: ${Data:NIP:behavior:servants:beast}, $mood: "BEAST" );

      }
    ---

That might seem a bit confusing. That\'s okay, though. Let\'s look at a
few segments of the above that are important:

    --- <B>the IF case</B> ---
      if( inv[i]."base:volition" && 
            arr_to_set( 
              Get( inv[i], "details:"+NRefDetail(inv[i])+":snames" )
    ---

We make two checks there.

\* Does the object have volition? This is somewhat important, as we\'re
taking a little risk here. After all, we don\'t want the servant to
start squeaking at \... a rat-fur hooded cloak, if someone would be
silly enough to give it the sname \'rat\'.

The second check is a little tricky. If you look at for instance
yourself, and check the property **details:default:snames**, you will
see that it\'s an array of names, for instance ({ \"kalle\", \"dot\",
\"ser\", \"man\", \"pc\", \"person\", \"human\", \"male\", \"being\",
\"mammal\", \"primate\" }).

The arr_to_set() call turns the above into (\[ \"being\":1, \"dot\":1,
\"human\":1, \"kalle\":1, \"male\":1, \"mammal\":1, \"man\":1, \"pc\":1,
\"person\":1, \"primate\":1, \"ser\":1 \]).

And thus, we can check if the arr_to_set()\[\"rat\"\] is TRUE. If it is,
the sname \"rat\" is in the snames.

    --- <B>the $beast thing</B> ---
         /* We found a rat! */
         $beast = inv[i];
    ---

Now, if you recall earlier, we called the rat in the scene \"beast\".
Now, similarily, we must set the property \$beast to the rat object when
we use the behavior. **The symbolic name we choose in the scene will be
referred to through \$symbol in the system.**

In our example above, we made the script lib:beast:decide. This is a
signal hook name, and as such we must state that we\'re adding a new
hook to the system. The hook in question is \'beast\' as defined.

So, we simply do:

\* +setp \"Marrach:NIP:lib:beast init:hooks ({ \"beast\" })\"

Now, as I said, we already have our servant with us in the room. So
we\'re going to add the new library we made (Marrach:NIP:lib:beast) to
the servant.

\* +setp servant \"add beast\"

As we statically call the behavior database from within the script (bad
call, but for simplicity\'s sake we\'ll let that one slide), we don\'t
have to do anything else.

Except start the NPC up.

\* +nip servant \"live\"

And watch her freak out (as our rat is still in the room).

\-- Main.KalleAlm - 15 Jun 2003

*Any parts of this confusing? Uncomprehensive? Stupid? Plain out wrong?
Feel free to \<A
HREF=\"[mailto:kalle\@marrach.skotos.net](mailto:kalle@marrach.skotos.net)\"\>poke
me\</A\>. I\'ll probably listen. ;)*

For more, brief examples, move on to [page 2](NIPTutorialSceneryII).
