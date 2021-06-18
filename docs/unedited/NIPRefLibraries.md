%META:TOPICINFO{author=\"kallea\" date=\"1151925491\" format=\"1.0\"
version=\"1.7\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
[NIPRefStyle]{.twiki-macro .INCLUDE}

\<FONT CLASS=\"title\"\>Why, Yes I am God.\</FONT\>\<br\> *A.k.a. \"How
to create your own NPC library\"*

[NIPRefLibrariesTOC]{.twiki-macro .INCLUDE}

This document is intended for the coding audience, familiar with
Skotos\' Merry, and familiar with the basics on how the NPC system
behaves and works. The information provided herein will presume that
this is the case.

\...

**How to create a library \-- thoughts to think**

\* **What is my library specifically going to do?**\<BR\> A library
should usually be a tiny matter. It should usually do one single thing,
and should in most cases take up to a page of code, not too much more
than that. \* A good idea is \"*My NPC horse needs to be mountable. So
I\'m making a lib for that.*\" \* while a bad idea is \"*My NPC horse
needs some stuff like whinnying and mounting so I\'m gonna do that.*\"

Restrict yourself to one specific issue and concentrate on that.
Separate the different features into different libraries.

\* **Where do I start planning this?**\<BR\> You\'re encouraged (but not
required) to fetch the [template](NIPTempTodo) from the [NIP System
Reference](NIPSystemReference) page and add it to the todo list there.
That\'s one way to \"think it out\".\<BR\> Some thoughts to consider,
though: \* Are there any libs or features I can make use of? \* Will I
make one/several hooks for this lib?

-   If so, which signals will my hook append to?
-   Will I even make a whole new signal for the lib? \* How \'heavy\'
    will this lib be? Is it going to lag the game into unrecognition
    when a few NPC\'s use it, or is it going to work for one, fifty, one
    hundred NPC\'s?

Those few pointers said, let\'s go on and step through the actual
process from idea to conclusion:

[Click here to read on.](NIPRefLibraries1.1)

\-- Main.KalleAlm - 03 Jun 2003
