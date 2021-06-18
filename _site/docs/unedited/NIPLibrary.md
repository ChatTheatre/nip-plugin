%META:TOPICINFO{author=\"kallea\" date=\"1054582200\" format=\"1.0\"
version=\"1.1\"}% %META:TOPICPARENT{name=\"NIPSystemReference\"}%
\<style\> b { font-size: 12pt; color: \#000000; font-weight: bold; } A {
text-decoration: none; font-size: 11pt; color: \#0000ff; } .title {
font-size: 20pt; font-weight: bold; color: \#000000; } \</style\>

\<FONT CLASS=\"title\"\>What is a library?\</FONT\>\<br\> *A.k.a.
\"What\'s the difference between libraries and signals/hooks?\"*

**A library** (in NIP) is a single object, describing a certain feature
of an NPC, such as \"anger\", \"eating\", \"musician\", \"courier\",
\"guard\", \"emoting\", etc. by defining a number of properties and
containing (optionally) a set of merry scripts.

More specifically, a library may (optionally) contain any or all of the
following properties:

  ------------------ ---------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------
  **PROPERTY**       **DESCRIPTION**                                                                    **EXAMPLE**
  dependency:needs   I need these libraries/signals/and-or-hooks loaded before I\'ll let you load me    ({ \<Lib:NIP:signals:MOOD\> })
  done:message       Emit this to everyone who loads this library                                       \"Congratulations. You just added the library \'foo\' to the NPC. Remember to put down the toilet seat when you\'re done.\"
  init:hooks         Array of hooks to add with the library                                             ({ \"eating\" })
  init:merry         Array of merry scripts in this object to inherit                                   ({ \"react:smile-iob\", \"lib:my:thing\" })
  init:signals       Add/modify these signals to these priorities\*                                     (\[ 100:\"MOOD\" \])
  init:properties    Create these properties with these values if the properties do not already exist   (\[ \"nip:trait:foo\":\"bar\", \"nip:pi\":3.14 \])
  ------------------ ---------------------------------------------------------------------------------- -----------------------------------------------------------------------------------------------------------------------------

\* Read the signal reference for further information on signals. Also
note that the init:signals property is usually reserved for actual
signals, and the init:signals property won\'t load a signal, just set
the signal and/or priority for it.

\<br\> **What is the difference between \...**

**\... a library and a signal?** The signals are basically just a series
of identifiers, each with an individual priority setting which
determines in which order the signals are triggered.

A signal is usually embedded into a library, but is still called a
\"signal\". Read [What is a signal?](NIPSignal) for further information
how this works.

**\... a library and a hook?** A hook is a group of scripts named in a
certain way so that the system will find them. Each hook may contain
scripts that are linked to any possible signal and these will be
loaded/unloaded automatically by the system depending on the loaded
signals in the NPC. Read [What is a hook?](NIPHooks) for further
information.

\-- Main.KalleAlm - 02 Jun 2003
