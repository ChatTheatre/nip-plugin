%META:TOPICINFO{author=\"kallea\" date=\"1054662957\" format=\"1.0\"
version=\"1.2\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { font-size: 12pt; color: \#000000; font-weight: bold; } A {
text-decoration: none; font-size: 11pt; color: \#0000ff; } .title {
font-size: 20pt; font-weight: bold; color: \#000000; } \</style\>

\<FONT CLASS=\"title\"\>What is a signal?\</FONT\>

**A signal** (in NIP) contains two things: \* a name (signal identifier)
\* a priority value

These are the current base signals loaded into every default system:

  ------------ -------------- ------------------------------------------------------------ -------------------------------
  **SIGNAL**   **PRIORITY**   **DESCRIPTION**                                              **LOCATION**
  DECIDE       1000           Decide if NPC should act, and what it should do              Lib:NIP:base:signals:DECIDE
  DELAY        10             Determine (and perform) the pause between each \"thought\"   Lib:NIP:base:signals:DELAY
  INTERNAL     500            Perform any/all internal operations                          Lib:NIP:base:signals:INTERNAL
  ------------ -------------- ------------------------------------------------------------ -------------------------------

Now, as you can see in the descriptions above, the signals each are
responsible for a certain section of the NPC. New signals may be added
(see Lib:NIP:signals:MOOD for example), signals may at any time be
modified or removed entirely, all at the whim of the creator.

Signals are usually embedded into libraries which take care of the
add/delete signal aspects. Usually (but not necessarily), signals also
load a hook, by tradition one with the same name (except in all
lowercase letters \-- signal \"DELAY\" for example, loads hook
\"delay\", etc).

Signals are not physical objects. The libraries which add signals are
usually called \'signals\' for sake of clarification.

Here is a snippet from the documentation in which the manual addition of
signals is described:

    ---
      Syntax:        +setp [target] "signal &lt;SIGNAL-ID> [&lt;SIGNAL-PRIORITY>]" 
                         If SIGNAL-PRIORITY is not set, the signal  
                         in question will be REMOVED. 
     
      Example:      +setp dog "signal DELAY 1" (add) 
                         +setp cat "signal BARK" (delete) 
    ---

Signals cooperate closely with hooks. In fact, one couldn\'t work
without the other. While the signals simply specify the order of
execution, the hooks contain all the code.

For example, in the \'eating\' library (which contains the \'eating\'
hook), the following hook scripts reside:

    ---
    lib:eating:decide    Dependant on the DECIDE signal
    lib:eating:internal  Dependant on the INTERNAL signal
    lib:eating:mood     Dependant on the MOOD signal
    ---

As the DECIDE and INTERNAL signals are default, we can safely presume
that both the lib:eating:decide script, and the lib:eating:internal
script will be executed each time the system performs its loop.

But how do we determine in which order they are called?

As we previously said, each signal is set up of an identifier and a
priority. \<br\> Whenever the signal/hook set up is changed, the system
automatically performs the signal/hook path calculation, which sets up
an array of scripts to keep looping through. In the above case, the
signal/hook path would look like this:

\* 1: lib:eating:internal *(INTERNAL, priority 500)* \* 2:
lib:eating:decide *(DECIDE, priority 1000)*

But wait! There was that third script, lib:eating:mood, too. Let\'s look
at that signal:

  ------------ -------------- ----------------------------------- ----------------------
  **SIGNAL**   **PRIORITY**   **DESCRIPTION**                     **LOCATION**
  MOOD         100            Ensure the NPC mood is up to date   Lib:NIP:signals:MOOD
  ------------ -------------- ----------------------------------- ----------------------

Okay, the priority for MOOD is 100, which would turn the
signal/hook-path into:

\* 1: lib:eating:mood *(MOOD, priority 100)* \* 2: lib:eating:internal
*(INTERNAL, priority 500)* \* 3: lib:eating:decide *(DECIDE, priority
1000)*

If the MOOD signal is present, the lib:eating:mood script will be
executed (of course, providing the \'eating\' hook is present as well).
But if the MOOD signal isn\'t there, the lib:eating:mood script won\'t
even be loaded into the NPC. \<br\> This is all dealt with automatically
by the system.

\"So,\" you ask, \"What\'s it **good** for?\"\<br\> Well, first off,
it\'s incredibly dynamic. You can practically go in and modify each and
every little part of the system without having to re-write bunches of
code. It\'s also proven very efficient, and although the amount of
scripts is higher than in the average object, the structure and layout
is usually much cleaner and easier to supervise.\<BR\> Once the concept
of signals and hooks is clear, it\'s easy to set up, configure and
customize an NPC. To turn a lifeless object into a fully functional NPC
that eats, sleeps, emotes, free-emotes (free emits), keeps track of a
bunch of moods (happiness, sadness, anger, hunger, sleepiness), takes
about 5 minutes (whereas 4 minutes and 30 seconds goes into creating the
behavior database):

    ---
    > +summon Marrach:Coders:kalle:battle-axe
    A battle axe arrives.
    > +nip 'set Marrach:Coders:kalle:battle-axe
    WELCOME TO THE 'NIP' CNPC SYSTEM!

    Hold one moment while the core library is set up in &lt;Marrach:Coders:kalle:battle-axe> ...
    --> Implementing base.
    --> Adding base libraries.
    --> Inserting system signals.
    Done!
    > +setp axe "add offers
    > +setp axe "add eating
    > +setp axe "add sleeping
    > +setp axe "add MOOD
    > +setp axe "add happiness
    > +setp axe "add anger
    > +setp axe "add sadness
    > +setp axe "add emoting
    > +setp axe "add freemoting
    ---

The NPC now has all the features mentioned above. The operation took
about 20 seconds. [Click here](NIPHowRecord) to see how to record
behavior.

\-- Main.KalleAlm - 02 Jun 2003
