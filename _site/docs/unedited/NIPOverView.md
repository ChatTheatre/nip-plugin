%META:TOPICINFO{author=\"kallea\" date=\"1089309873\" format=\"1.0\"
version=\"1.5\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>General overview of the system\</FONT\>

**Briefly, what is it?** \<font style=\"font-size: 8pt;\"\>(Related:
[Happy Birthday, NIP](NIPHappyBirthdayNip))\</font\>

**NIP** is an NPC system written entirely in Merry. Its biggest
\"feature\" is the signal/hook implementation, which is responsible for
everything **non-reaction/witness-based**, that is \-- anything
spontaneous. Any unprovoked thinking that occcurs in the mind of the NPC
takes place using the sig/hook system.

Apart from the sig/hooks, the NIP controls and handles implementation,
modification, creation and maintenance of new and old NPC\'s with a set
of setprop-triggers.

You can thus create an NPC entirely through woe, and then just summon
and start it once it\'s finished, for what it\'s worth.

Creating an NPC from scratch is fairly simple. Just build some object of
some sort (like a cat or mouse, or a bartender or a rollerblading
monkey), and call the one command **+nip \"set Woe:for:the:object\"**
and it\'s done!

Of course, now you have to chuck in all the libs and such that your NPC
requires.

\<br\> **What Can It Do, And More Importantly \-- What Can\'t It Do?**

It can do basically anything. No, really, it can. It\'s just a matter of
adding whatever you need if it\'s not there already, and tada, you have
it.

It is more of a shell than a system. It provides the tool to create and
expand in whichever direction you desire, and is as flexible as you make
it.

**Want a courier?** Sure thing. In fact, it\'s a top priority and if not
finished already, it should be soon.\<br\> **.. servants?** Some
already-made. More to come. Check out and try making your own\<br\> **..
an animal?** Special efforts will be put into this area in time. Not a
top priority, but it\'s up there with the rest.\<br\> **.. enemies?**
Definitely.\<br\> **.. a specific servant who every evening steps out of
their house, walks through the setting and lights all the torches?** Of
course. Scheduled events, on the list.\<br\> .. etc.

**What you can\'t do** is really based on yourself and fellow staffers
in your game. The system is exclusively merry, and it can initially be
tricky to learn how to make signals and hooks within. It currently
doesn\'t have very much \"pre-made\" stuff, and it\'s mostly a matter of
how gracious the coders in neighbouring games are, whether they share
their libs or not.

However, I (Kalle) and hopefully others will continuously add new
features and libs, and are open to requests and suggestions, and are
even more open to aid you in making or learning this stuff yourself.

\<br\> **A little more specific, how does it work?**

The system is roughly divided into three separate parts,

\* libraries \* signals \* hooks

**Libraries** are the most \"general\" of them all, and contain
react/witness-scripts etc. \<br\> Apart from this, they contain a set of
\"system properties\" that explain properties to be set, hooks/signals
to implement, and so on.\<br\> *A library may contain a signal and/or a
hook, but hooks may not contain libraries or signals, and signals may
not contain libraries or hooks.*

**Signals** are the smallest objects, with the least settings. They
simply have a name and a priority, which later on determines in which
order any scripts that are **attached** to it will be executed.

**Hooks** are simply a set of scripts named a certain way
(lib:hook:signal) so as to connect with the various available signals.

For instance, a hook may contain scripts for signals that **may** be
implemented; if the signal is enabled in the NPC when the hook is
loaded, the script will be added accordingly. If not, the script will be
ignored.

For instance, the **eating** hook has a reference to the **MOOD** signal
(lib:eating:mood) which will set the mood of the NPC to \"hungry\" if
its fat reserves are low enough. This script would be totally redudant
to execute if the NPC did not have the MOOD signal, neh?

Same with the **sleeping** hook.

  ------------ --------------------
  \*           **SIGNALS**
  **HOOKS**    DELAY
  anger        
  eating       
  emoting      
  freemoting   
  happiness    
  mood         lib:mood:delay
  musician     
  sadness      
  sleeping     lib:sleeping:delay
  ------------ --------------------

Listed in the above chart are the currently existing hooks and signals,
and how they are connected to each other. As you may have noted in the
\'mood\' hook\'s connection with the \'MOOD\' signal, there are two
scripts, **lib:mood:mood-exec** and **lib:mood:mood-init**. The **init**
scripts are always executed first in the loop, and **exec** scripts are
executed right before **post** scripts (lib:hook:signal-post).

**Script execution order:** \* By signal priority \*
lib:\*:*signal*-**init** \* lib:\*:*signal*-**pre** \* lib:\*:*signal*
\* lib:\*:*signal*-**exec** \* lib:\*:*signal*-**post**

\-- Main.KalleAlm - 01 Jun 2003
