%META:TOPICINFO{author=\"kallea\" date=\"1138644304\" format=\"1.0\"
version=\"1.8\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPStyle]{.twiki-macro .INCLUDE}

\<font class=\"title\"\>Tutorial: NPC Auto-descriptions using
spawn-traits\</font\>

[Spawn-traits](NIPLibRefSpawnTraits) is one of the most recent additions
to the NPC system (as of 29 Nov 2003). It\'s a very simple and
straightforward feature, with only one internal script.

What\'s tricky about it, however, are the settings required to properly
make use of it.

The settings are contained in a single property, **nip:spawn:traits**.
This property is a mapping, where each key represents a property-name.
Each corresponding value is a string array with each and every possible
alternative value for the property. For example,

      ([ "appearance:eye:color" : ({ "green", "emerald", "brown", "blue" }) ])

In the above case (provided the property \'nip:spawn:traits\' was set to
the above), whenever a spawn of the NPC was made, the property
\"appearance:eye:color\" would be set to \"green\", \"emerald\",
\"brown\" or \"blue\", at random.

      ([ "appearance:eye:color" : ({ "green"; "emerald", "brown"; "blue" }),
          "appearance:eye:type" : ({ "sad", "squinty", "narrow", "bright"; "shallow", "deep" }),
          "appearance:fur:color" : ({ "brown", "black", "brown-striped"; "black-striped" }) ])
    -etc-

To use these appearance traits properly, doing the above is not enough.
We also need to use SAM-tags to describe the NPC dynamically. In the
above case, I would set the eye/eyes details to the following:

    brief    = $(this.appearance:eye:type) $(this.appearance:eye:color) eyes
    look      = A pair of eyes, $(this.appearance:eye:color) and $(this.appearance:eye:type).
    examine  = A pair of $(this.appearance:eye:type) $(this.appearance:eye:color) eyes.

By using \$(this.propertyname) I am directly referring to the value of a
property in the NPC itself. Thus, if I set appearance:eye:type to
\"bright\" and appearance:eye:color to \"green\" in my NPC above, doing
a look on its eyes would return \"A pair of eyes, green and bright.\"
and an examine would give me \"A pair of bright green eyes.\"

At this point, we have enough info to go on and put this system into an
NPC.

Now, we can do this several ways. One way is to sit down and think up
the various variable traits that this particular NPC should have.
Another way is to make a static version of the NPC first and then
replace the static parts with dynamic parts as we find them. There is no
good or bad, or right or wrong. The latter would take longer time as
there\'s an extra step of making a static version first, while the first
requires are more thoughtful approach. In this case, I\'m going to use
the first.

So, I make an NPC. I make a dog, of unknown origin, which means I have a
lot of features I can put in. I can make its coat spotted or striped, or
stained. I can give it up to three coat colors, and I can make it
long-haired or short-haired, curly or straight. I can give it blue eyes
or green or brown, short nose, long nose, thin nose, triangular ears,
floppy ears, big ears, small ears, long tail, furry tail, big paws, long
legs, robust legs, etc etc etc etc. The possibilities are practically
endless.

But I start out by defining the various parts of my dog that I want
\"alterable\" (or \"dynamic\"):

     - ears
        - size, shape
     - nose
        - shape
     - tail
        - length, type
     - legs
        - length, type
     - coat
        - type, color, alternate colors
     - hair
        - length, type
     - paws
        - type
     - eyes
        - color, type
     - head
        - size, type
     - dog (prime)
        - size

Now I have a bunch of variable traits for my dog that will make each
spawned copy of it seem very unique to anyone who gives it a good look.
It\'s necessary to map each of these \"traits\" to a property-name now,
as I will refer to them from the description of the dog later on. I am
personally going to use the \"appearance\" property namespace for each
trait, but feel free to use whatever you want:

     - ears
        - size           = appearance:ear:size
        - shape         = appearance:ear:shape
     - nose
        - shape         = appearance:nose:shape
     - tail
        - length          = appearance:tail:length
        - type           = appearance:tail:type
     - legs
        - length          = appearance:leg:length
        - type           = appearance:leg:type
     - coat
        - type           = appearance:coat:type
        - color         = appearance:coat:color
        - alt colors     = appearance:coat:altcolor
     - hair
        - length          = appearance:hair:length
        - type           = appearance:hair:type
     - paws
        - type           = appearance:paw:type
     - eyes
        - color         = appearance:eye:color
        - type           = appearance:eye:type
     - head
        - size           = appearance:head:size
        - type           = appearance:head:type
     - dog (prime)
        - size           = appearance:dog:size

Now, before I start coming up with the various values for each trait,
I\'m making my dog. I\'m not going to be too detailed on the creation of
it, but I\'m going to tell you the things I do that are affected by
this.

First off, I\'m making the following details on my dog:

     - default (prime)
     - ear
     - ears
     - nose
     - tail
     - leg
     - legs
     - coat
     - fur
     - paw
     - paws
     - eye
     - eyes
     - head
     - face
     - body

For the default detail, I\'m setting the following descriptions:

      brief = $(this.appearance:dog:size) $(this.appearance:coat:color) dog
      look  = A $(this.appearance:dog:size) dog with $(this.appearance:coat:color) and $(this.appearance:coat:altcolor) coat. 

Next, I\'m making the ears. These are two separate details, \"ear\" and
\"ears\". For ear,

      brief = $(this.appearance:ear:size) $(this.appearance:ear:shape) ear
      look  = The $(this.appearance:ear:size) $(this.appearance:ear:shape) ear of a $(this.appearance:dog:size) dog.

And for ears,

      brief = $(this.appearance:ear:size) $(this.appearance:ear:shape) ears
      look  = A pair of $(this.appearance:ear:size) $(this.appearance:ear:shape) ears.

The nose,

      brief = $(this.appearance:nose:shape) nose
      look  = The $(this.appearance:nose:shape) nose of a $(this.appearance:dog:size) dog.

Tail,

      brief = $(this.appearance:tail:length) $(this.appearance:tail:type) tail
      look  = The $(this.appearance:tail:length) $(this.appearance:tail:type) tail of a $(this.appearance:dog:size) dog.

The legs are similar to the ears. I make a leg, and a legs, detail.

Leg,

      brief = $(this.appearance:leg:length) $(this.appearance:leg:type) leg
      look  = One of four $(this.appearance:leg:length) $(this.appearance:leg:type) legs, {?when | $(this.base:stance) | 3 |all of which are comfortably tucked beneath the $(this.appearance:dog:size) dog's body. | 4 |currently sat upon. | * |supporting the $(this.appearance:dog:size) dog's body. }

Legs,

      brief = $(this.appearance:leg:length) $(this.appearance:leg:type) legs
      look  = Four $(this.appearance:leg:length) $(this.appearance:leg:type) legs, {?when | $(this.base:stance) | 3 |all of which are comfortably tucked beneath the $(this.appearance:dog:size) dog's body. | 4 |currently sat upon. | * |supporting the $(this.appearance:dog:size) dog's body. }

Paw,

      brief = $(this.appearance:paw:type) paw
      look  = One of four $(this.appearance:paw:type) paws.

Paws,

      brief = $(this.appearance:paw:type) paws
      look  = The $(this.appearance:paw:type) paws of a $(this.appearance:dog:size) dog.

Eye,

      brief = $(this.appearance:eye:type) $(this.appearance:eye:color) eye
      look  = One of two $(this.appearance:eye:type) $(this.appearance:eye:color) eyes.

Eyes,

      brief = $(this.appearance:eye:type) $(this.appearance:eye:color) eyes
      look  = A pair of eyes, $(this.appearance:eye:color) and $(this.appearance:eye:type).

Head,

      brief = $(this.appearance:head:size) $(this.appearance:head:type) head
      look  = A $(this.appearance:dog:size) dog's $(this.appearance:head:size) $(this.appearance:head:type) head, framed by a pair of $(this.appearance:ear:size) $(this.appearance:ear:shape) ears.

At this point, we have a few more descriptive details left. Namely
\'coat\', \'fur\', \'body\' and \'face\'. We\'re going to include the
other details in the description of these in some appropriate way.

Coat,

      brief = $(this.appearance:coat:color) coat
      look  = The $(this.appearance:dog:size) dog's $(this.appearance:hair:length) and $(this.appearance:hair:type) coat is $(this.appearance:coat:color) with $(this.appearance:coat:type) $(this.appearance:coat:altcolor).

Fur,

      brief = $(this.appearance:coat:color) fur
      look  = The $(this.appearance:hair:length) $(this.appearance:hair:type) fur is $(this.appearance:coat:color) with $(this.appearance:coat:type) $(this.appearance:coat:altcolor).

Body,

      brief = $(this.appearance:dog:size) body
      look  = The $(this.appearance:dog:size) dog's body, with four $(this.appearance:leg:type) legs, one $(this.appearance:tail:type) tail and $(this.appearance:head:size) head.

Face,

      brief = face
      look  = The $(this.appearance:dog:size) dog's face, with $(this.appearance:eye:type) $(this.appearance:eye:color) eyes, and a $(this.appearance:nose:shape) nose.

And we\'re finally done describing the thing. Now we need to come up
with various values for each of the traits we used in the above.

     - ears
        - size           = small, large
        - shape         = floppy, triangular, straight, dangling
     - nose
        - shape         = long, short, stumpy, wrinkled, smooth
     - tail
        - length          = long, short
        - type           = fluffy, straight
     - legs
        - length          = long, short
        - type           = robust, elegant, sinewy, muscular
     - coat
        - type           = spotted, stained, striped
        - color         = dark-brown, light-brown, brown, black, white, golden, red, grey, light-grey, dark-grey
        - alt colors     = dark-brown, light-brown, brown, black, white, golden, red, grey, light-grey, dark-grey
     - hair
        - length          = long, short, trimmed, wild
        - type           = wavy, curly, straight
     - paws
        - type           = big, small, heavy, thick
     - eyes
        - color         = brown, dark-brown, light-brown, green, emerald, blue, dark-blue, light-blue, yellow, golden
        - type           = sharp, bright, shallow, deep, dull, sad, mourning, playful, happy, calm
     - head
        - size           = large, small
        - type           = round, stretched, even, uneven, smooth
     - dog (prime)
        - size           = small, medium-sized, large

Now, we have a body, we\'ve set it up with a bunch of details, and
we\'ve decided on the spawn traits we want. Now we need to turn the dog
into an NIP NPC before we can actually put these into it!

I\'ve named my dog \"Examples:complete:NIP:dog\" (on S7 only).

    > +nip "set Examples:complete:NIP:dog"
    WELCOME TO THE 'NIP' CNPC SYSTEM!

    Hold one moment while the core library is set up in &lt;Examples:complete:NIP:dog> ...
    --> Implementing base.
    --> Adding base libraries.
    --> Inserting system signals.
    --> Setting revision according to current system state.
    Done!

    > +summon Examples:complete:NIP:dog
    A dog arrives.

    > +setp dog "add spawn-traits"
    Setting 'add' in &lt;Examples:complete:NIP:dog>;
    - from: nil
    - to: "spawn-traits"
    Attempting to add library ...
    The spawn-traits library has been loaded. This will look for the mapping "nip:spawn:traits", which 
    could look like this: ([ "appearance:color" : ({ "blue", "green", "red" }), "something:else" : ({ 1,
     2, 3 }) ]) -- in this case, the property "appearance:color" would be set to either "blue", "green" 
    or "red" in the object, and the property "something:else" would be either 1, 2 or 3. This is good to
     make on-the-fly variations of CNPC's at spawn-time.
    &lt;Lib:NIP:lib:spawn-traits> loaded successfully.

Now, we simply have to bunch all the traits we had above, together into
one big ass property. This:\<pre\> - ears - size (appearance:ear:size) =
small, large \</pre\> turns into \<pre\>(\[ \"appearance:ear:size\" : ({
\"small\", \"large\" }) \])\</pre\>

And so on, until we have this:\<pre\> (\[ \"appearance:ear:size\" : ({
\"small\", \"large\" }), \"appearance:ear:shape\" : ({ \"floppy\",
\"triangular\", \"straight\", \"dangling\" }), \"appearance:nose:shape\"
: ({ \"long\", \"short\", \"stumpy\", \"wrinkled\", \"smooth\" }),
\"appearance:tail:length\" : ({ \"long\", \"short\" }),
\"appearance:tail:type\" : ({ \"fluffy\", \"straight\" }),
\"appearance:leg:length\" : ({ \"long\", \"short\" }),
\"appearance:leg:type\" : ({ \"robust\", \"elegant\", \"sinewy\",
\"muscular\" }), \"appearance:coat:type\" : ({ \"spotted\", \"stained\",
\"striped\" }), \"appearance:coat:color\" : ({ \"dark-brown\",
\"light-brown\", \"brown\", \"black\", \"white\", \"golden\", \"red\",
\"grey\", \"light-grey\", \"dark-grey\" }), \"appearance:coat:altcolor\"
: ({ \"dark-brown\", \"light-brown\", \"brown\", \"black\", \"white\",
\"golden\", \"red\", \"grey\", \"light-grey\", \"dark-grey\" }),
\"appearance:hair:length\" : ({ \"long\", \"short\", \"trimmed\",
\"wild\" }), \"appearance:hair:type\" : ({ \"wavy\", \"curly\",
\"straight\" }), \"appearance:paw:type\" : ({ \"big\", \"small\",
\"heavy\", \"thick\" }), \"appearance:eye:color\" : ({ \"brown\",
\"dark-brown\", \"light-brown\", \"green\", \"emerald\", \"blue\",
\"dark-blue\", \"light-blue\", \"yellow\", \"golden\" }),
\"appearance:eye:type\" : ({ \"sharp\", \"bright\", \"shallow\",
\"deep\", \"dull\", \"sad\", \"mourning\", \"playful\", \"happy\",
\"calm\" }), \"appearance:head:size\" : ({ \"large\", \"small\" }),
\"appearance:head:type\" : ({ \"round\", \"stretched\", \"even\",
\"uneven\", \"smooth\" }), \"appearance:dog:size\" : ({ \"small\",
\"medium-sized\", \"large\" }) \])\</pre\>

So, we \...\<pre\> \> +setp dog \"nip:spawn:traits (\[
\"appearance:ear:size\" : ({ \"small\", \"large\" }),
\"appearance:ear:shape\" : ({ \"floppy\", \"triangular\", \"straight\",
\"dangling\" }), \"appearance:nose:shape\" : ({ \"long\", \"short\",
\"stumpy\", \"wrinkled\", \"smooth\" }), \"appearance:tail:length\" : ({
\"long\", \"short\" }), \"appearance:tail:type\" : ({ \"fluffy\",
\"straight\" }), \"appearance:leg:length\" : ({ \"long\", \"short\" }),
\"appearance:leg:type\" : ({ \"robust\", \"elegant\", \"sinewy\",
\"muscular\" }), \"appearance:coat:type\" : ({ \"spotted\", \"stained\",
\"striped\" }), \"appearance:coat:color\" : ({ \"dark-brown\",
\"light-brown\", \"brown\", \"black\", \"white\", \"golden\", \"red\",
\"grey\", \"light-grey\", \"dark-grey\" }), \"appearance:coat:altcolor\"
: ({ \"dark-brown\", \"light-brown\", \"brown\", \"black\", \"white\",
\"golden\", \"red\", \"grey\", \"light-grey\", \"dark-grey\" }),
\"appearance:hair:length\" : ({ \"long\", \"short\", \"trimmed\",
\"wild\" }), \"appearance:hair:type\" : ({ \"wavy\", \"curly\",
\"straight\" }), \"appearance:paw:type\" : ({ \"big\", \"small\",
\"heavy\", \"thick\" }), \"appearance:eye:color\" : ({ \"brown\",
\"dark-brown\", \"light-brown\", \"green\", \"emerald\", \"blue\",
\"dark-blue\", \"light-blue\", \"yellow\", \"golden\" }),
\"appearance:eye:type\" : ({ \"sharp\", \"bright\", \"shallow\",
\"deep\", \"dull\", \"sad\", \"mourning\", \"playful\", \"happy\",
\"calm\" }), \"appearance:head:size\" : ({ \"large\", \"small\" }),
\"appearance:head:type\" : ({ \"round\", \"stretched\", \"even\",
\"uneven\", \"smooth\" }), \"appearance:dog:size\" : ({ \"small\",
\"medium-sized\", \"large\" }) \])\</pre\>

And that\'s it! Quite intimidating little command that last one, but it
shouldn\'t be too difficult to get the grip of it if you know the
what\'s.

\-- Main.KalleAlm - 29 Nov 2003

Once you\'ve added spawn traits to your CNPC, you will probably want
those adjectives to show up on the details of them.

\<font color=red\>Update: the information below is deprecated; inherit
Lib:NIP:EXT/setprop-post:appearance instead of adding a script manually.
The script below has been added to the main NIP distribution. HOWEVER,
read below the greyed out part, as there is still stuff relevant to get
things working, **the nip:trait:appearance:adjectives part, in
particular!** \--Kalle, Jan 29, 2006.\</font\>

\<font color=grey\> The first thing you need to do is set up a script
that will add the adjectives to the detail. You can do this in the CNPC
object itself, or a CNPC parent object. If you are using spawn-traits
for numerous CNPCs, I would suggest setting it in the parent to save
yourself some work.

Type +tool merry edit %Woename:Of:CNPC setprop-post:appearance

In that editor, you\'ll write out the following script:

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-\--

    /* 
      D=Add/remove appearance traits to details. 
    */

    int i, sz;

    if( this."nip:trait:appearance:names" )
      $props = this."nip:trait:appearance:names"[$(hook-property)];
    if( this."nip:trait:appearance:adjectives" )
      $adjec = this."nip:trait:appearance:adjectives"[$(hook-property)];

    if( !$props )
      $props = ({ });
    if( !$adjec )
      $adjec = ({ });

    if( typeof( $props ) != T_ARRAY )
      $props = ({ $props });
    if( typeof( $adjec ) != T_ARRAY )
      $adjec = ({ $adjec });

    sz = sizeof( $props ) > sizeof( $adjec ) ? sizeof( $props ) : sizeof( $adjec );

    if( $(hook-oldvalue) )
    {
      $o = explode( $(hook-oldvalue), " " );
      $os = sizeof( $o );
    }
    if( $(hook-value) )
    {
      $n = explode( $(hook-value), " " );
      $ns = sizeof( $n );
    }

    for( i = 0; i < sz; i++ ) {
      if( i < sizeof( $props )) {
         if( $(hook-oldvalue) )
            for( $x = 0; $x < $os; $x++ )
              Set( this, "details:" + $props[i] + ":sname:" + $o[$x], nil );
         if( $(hook-value) )
            for( $x = 0; $x < $ns; $x++ )
              Set( this, "details:" + $props[i] + ":sname:" + $n[$x],<br> TRUE );
      }
      if( i < sizeof( $adjec )) {
         if( $(hook-oldvalue) )
            for( $x = 0; $x < $os; $x++ )
              Set( this, "details:" + $adjec[i] + ":adjective:" + $o[$x], nil );
         if( $(hook-value) )
            for( $x = 0; $x < $ns; $x++ )
              Set( this, "details:" + $adjec[i] + ":adjective:" + $n[$x], TRUE );
      }
    }

\-\-\-\-\-\-\-\-\-\-\-\-\-\-\-- \</font\>

The next thing you need to do is set up in the CNPC object itself (not a
parent) the following property:\<br\>
nip:trait:appearance:adjectives\<br\> which is what deems which details
in the CNPC get which adjectives.

So say you have a SAM tag in the default detail
\$(this.appearance:eyecolor), you want to set (\[
\"appearance:eyecolor\":({ \"default\" }) \])

Using a goldfish CNPC I coded up, this is an example:

+setp fish \"nip:trait:appearance:adjectives (\[
\"appearance:body:shape\":({ \"body\" }), \"appearance:cheek:size\":({
\"cheeks\" }), \"appearance:cheek:type\":({ \"cheeks\" }),
\"appearance:fin:length\":({ \"fins\" }), \"appearance:<fish:color>\":({
\"default\", \"body\", \"fins\", \"head\", \"scales\" }),
\"appearance:<fish:shine>\":({ \"default\" }),
\"appearance:gravel:color\":({ \"bowl\", \"gravel\" }),
\"appearance:water:type\":({ \"bowl\", \"water\" }) \])

You\'ll notice I have SAM tags for fish color in the following details:
default, body, fins, head, and scales. So the adjectives will be set in
each of those details.

And that\'s it!

\-- Main.AnneWarren - 11 Aug 2004
