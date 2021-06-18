%META:TOPICINFO{author=\"kallea\" date=\"1054586536\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { font-size: 12pt; color: \#000000; font-weight: bold; } A {
text-decoration: none; font-size: 11pt; color: \#0000ff; } .title {
font-size: 20pt; font-weight: bold; color: \#000000; } \</style\>

\<FONT CLASS=\"title\"\>What is a hook?\</FONT\>

**Hooks** (in NIP) are packages of scripts attached to a specific
[signal](NIPSignal) which are executed continuously from a loop called
**the heartbeat thread**.

Each hook may contain script references to any possible signal. The
scripts will only be called if the specific signal exists, all handled
internally by the heartbeat thread.

To explain this better, I\'m going to describe how a hook, \'eating\',
works by looking at pieces of the code and explaining what it does
(apologies if the code is out-of-date, please let me know if so is the
case):

    --- <B>Lib:NIP:lib:eating/lib:eating:decide</B> ---
    object *inv, food;
    float relative_hunger;
    int i;

    /* First off, are we awake? */
    if( this."npc:state" == "asleep" ) return nil;

    /* Awake we are. So, how hungry are we relatively speaking? Where 1 is full and 0 is starving (backwards, I know). */

    relative_hunger = Flt( this."npc:energy" ) / Flt( this."nip:trait:eating:grammes" );

    if( (this."npc:eating" && relative_hunger < 1.0) || relative_hunger < 0.5 ){
      /* Okay, we wouldn't say no to a cookie and/or we're currently eating something. */
      food = this."npc:eating";
      if( food && food."base:environment" != this ) this."npc:eating" = food = nil;
      if( !food ){
         /* Scan our inventory to see if we have anything edible. */
         inv = this."base:inventory";
         for( i = 0; i < sizeof( inv ); i++ )
            if( !inv[i]."base:edible" ) inv[i] = nil;
         inv -= ({ nil });

         if( sizeof( inv )){
            /* It appears we have something edible in our possession. Grab one thing at random. */
            food = inv[random( sizeof( inv ))];
         }
      }
      if( food )
         if( !random( 1+Int( relative_hunger * 25.0 ))){
            Act( this, "eat", $what: ({ food }) );
            this."npc:eating" = food;
            return $SIG_DONE;
         } else return nil;

    }

    if( relative_hunger < 0.3 && !random( 1+Int( relative_hunger * 30.0 ))){ 
      /* Uh-oh. We're very hungry. Anything in the room to gnaw on? */

      /* Fetch our environment's inventory. */
      inv = this."base:environment"."base:inventory";

      for( i = 0; i < sizeof( inv ); i++ )
         if( !inv[i]."base:edible" ) inv[i] = nil;
      inv -= ({ nil });

      if( sizeof( inv )){
         /* It appears there's food in the environment. Try to grab it! */
         food = inv[random( sizeof( inv ))];

         Act( this, "take", $what: ({ food }) );
         return $SIG_DONE;
      }
    }
    ---

Possibly one of the biggest hook-scripts currently, the eating/DECIDE
hook/signal script checks if the NPC is hungry enough to do something
about it, ranging from checking its inventory (\"got food in my
hands?\") to checking its environment (\"any food in the room?\"). If it
decides to act, it will do so and return a certain signal that declares
that the rest of the signal should be ignored (see [signal
streams](NIPSignalStreams) for more information on the subject.

    --- <B>Lib:NIP:lib:eating/lib:eating:internal</B> ---
    int energy;

    energy = Int( this."npc:energy" );
    energy -= Int( (this."base:intrinsicmass" * (float) $NPC_PAUSE)/40.0 );
    if( energy < 0 ) energy = 0;
    this."npc:energy" = energy;
    ---

The eating/INTERNAL hook/signal script simply increases the NPC\'s
hunger (or more correctly, decreases the NPC\'s fat reserves), thus
making it hungrier as time passes.

    --- <B>Lib:NIP:lib:eating/lib:eating:mood</B> ---
    float relative_hunger;
    int i;

    /* First off, are we awake? */
    if( this."npc:state" == "asleep" ) return nil;

    /* Awake we are. How hungry are we? (0 = starving, 1 = full) */
    relative_hunger = Flt( this."npc:energy" ) / Flt( this."nip:trait:eating:grammes" );

    /* Are we hungry enough to be "hungry"? */
    if( relative_hunger < 0.4 )
      /* Yep. Strengthen the HUNGRY mood a bit. */
      this."nip:moodvals"["HUNGRY"] += Int(( 0.5 - relative_hunger ) * 150.0 );
    ---

The eating/MOOD hook/signal script will, if the MOOD signal is present,
make the mood, HUNGRY, relative to the NPC\'s hunger, thus automatically
making it possible for the NPC to be \"hungry\".

\-- Main.KalleAlm - 02 Jun 2003
