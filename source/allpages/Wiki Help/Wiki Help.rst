*********
Wiki Help
*********
On the left column you see the source text with markup, and on the right column, the output once saved.

-=Maketoc=-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}{maketoc}{CODE}
--- ~hs~ ---
{maketoc}{SPLIT}

-=Title bar=-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}-=A titlebar=-{CODE}
--- ~hs~ ---
-=A titlebar=-{SPLIT}

-=Headings from level 1 to n=-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}!h1 heading
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Proin consequat libero. Phasellus porta diam id justo. In eget neque ut metus aliquet bibendum. Curabitur lacinia aliquam sem. Praesent aliquam. Morbi quis tellus. Vestibulum nec neque commodo metus sagittis ullamcorper. Maecenas turpis. Mauris quis leo. Maecenas id felis. Nulla nec nibh. Morbi facilisis. Cras in ipsum a felis ornare dapibus.{CODE}
--- ~hs~ ---
!h1 heading
Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Proin consequat libero. Phasellus porta diam id justo. In eget neque ut metus aliquet bibendum. Curabitur lacinia aliquam sem. Praesent aliquam. Morbi quis tellus. Vestibulum nec neque commodo metus sagittis ullamcorper. Maecenas turpis. Mauris quis leo. Maecenas id felis. Nulla nec nibh. Morbi facilisis. Cras in ipsum a felis ornare dapibus.{SPLIT}

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}!!h2 heading
Nullam mi. Praesent vehicula consectetuer tortor. Mauris venenatis leo at metus. Ut sit amet enim. Aenean tortor orci, hendrerit a, eleifend quis, pharetra eu, felis.{CODE}
--- ~hs~ ---
!!h2 heading
Nullam mi. Praesent vehicula consectetuer tortor. Mauris venenatis leo at metus. Ut sit amet enim. Aenean tortor orci, hendrerit a, eleifend quis, pharetra eu, felis.{SPLIT}

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}!!!h3 heading
Vestibulum dignissim. Praesent non magna id ipsum iaculis pharetra. Nam tristique vestibulum felis. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Fusce eget nisi. Nullam quis nisi.{CODE}
--- ~hs~ ---
!!!h3 heading
Vestibulum dignissim. Praesent non magna id ipsum iaculis pharetra. Nam tristique vestibulum felis. Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Fusce eget nisi. Nullam quis nisi.{SPLIT}

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}!!!!h4 heading
Cras euismod lectus vel metus. Praesent gravida. Nunc molestie mattis justo. Curabitur ornare, felis et vulputate dapibus, leo est condimentum enim, blandit ultrices orci mauris at eros. Pellentesque eu arcu eu massa mattis rhoncus. Ut volutpat mi in ligula. Pellentesque vitae tellus quis nibh feugiat ornare. Nullam arcu. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.{CODE}
--- ~hs~ ---
!!!!h4 heading
Cras euismod lectus vel metus. Praesent gravida. Nunc molestie mattis justo. Curabitur ornare, felis et vulputate dapibus, leo est condimentum enim, blandit ultrices orci mauris at eros. Pellentesque eu arcu eu massa mattis rhoncus. Ut volutpat mi in ligula. Pellentesque vitae tellus quis nibh feugiat ornare. Nullam arcu. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.{SPLIT}

-=Autonumbering in headings=-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}!!# Introduction
Bla bla...

!!# Methodology
Bla bla...

!!!# Laboratory work
Bla bla...

!!!# Statistical analyses
Bla bla...

!!# Results
Bla bla...

!!# Discussion
Bla bla...
{CODE}
--- ~hs~ ---
!!# Introduction
Bla bla...

!!# Methodology
Bla bla...

!!!# Laboratory work
Bla bla...

!!!# Statistical analyses
Bla bla...

!!# Results
Bla bla...

!!# Discussion
Bla bla...{SPLIT}

-= Lists =-

::__Unordered list__::{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}*An __unordered__ list item
**A subitem
And some text
*Another item
. . . and more text . . .
*Item 3
. . . and some more text, to illustrate the line spacing.{CODE}
--- ~hs~ ---
*An __unordered__ list item
**A subitem
And some text
*Another item
. . . and more text . . .
*Item 3
. . . and some more text, to illustrate the line spacing.{SPLIT}


::__Ordered list__::{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}#An __ordered__ list item
##A subitem
+ And some text not breaking the numbering
#Another item
and more text (breaking the correlative numbering)
#Item 3
. . . and some more text, to illustrate the line spacing.{CODE}
--- ~hs~ ---
#An __ordered__ list item
##A subitem
+ And some text not breaking the numbering
#Another item
and more text (breaking the correlative numbering)
#Item 3
. . . and some more text, to illustrate the line spacing.{SPLIT}

-= Tables =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}A table:
||Row One, Column One|Row One, Column Two
Row Two, Column One|Row Two, Column Two||{CODE}
--- ~hs~ ---
A table:
||Row One, Column One|Row One, Column Two
Row Two, Column One|Row Two, Column Two||{SPLIT}

-= Boxes =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}^A box^{CODE}
--- ~hs~ ---
^A box^{SPLIT}

-= Links =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}An [http://tikiwiki.org|external link|nocache]{CODE}
--- ~hs~ ---
An [http://tikiwiki.org|external link|nocache]{SPLIT}

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}An ((OldHomePage|internal link)) {CODE}
--- ~hs~ ---
An ((OldHomePage|internal link)) {SPLIT}


-= PLUGINS: Img =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}{img src=http://profiles.tikiwiki.org/img/tiki/tikilogo.png align=center }{CODE}
--- ~hs~ ---
{img src=http://profiles.tikiwiki.org/img/tiki/tikilogo.png align=center }{SPLIT}

-= PLUGINS: Quote =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}Quote plugin:
{QUOTE()}
Just what do you think you're doing, Dave?

--HAL, in 2001: A Space Odyssey (1968)
{QUOTE}{CODE}
--- ~hs~ ---
Quote plugin:
{QUOTE()}
Just what do you think you're doing, Dave?

--HAL, in 2001: A Space Odyssey (1968)
{QUOTE}{SPLIT}

-= PLUGINS: Code =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}Code plugin:
{CODE(wrap=&gt;1)}
{Hello World in Pascal}

program HelloWorld(output);
begin
  WriteLn('Hello World!');
end.
{CODE}{CODE}
--- ~hs~ ---
Code plugin:
{CODE(wrap=&gt;1)}
{Hello World in Pascal}

program HelloWorld(output);
begin
  WriteLn('Hello World!');
end.
{CODE}{SPLIT}

-= PLUGINS: Fancytable =-

{SPLIT(fixedsize=&gt;n,colsize=&gt;48%|4%|48%)}{CODE(wrap=&gt;1)}FANCYTABLE plugin:
{FANCYTABLE(head=&gt;head one~|~head two~|~head three)}cell one~|~cell two~|~cell three
r2 c1~|~ r2 c2~|~ r3 c2{FANCYTABLE}{CODE}
--- ~hs~ ---
FANCYTABLE plugin:
{FANCYTABLE(head=&gt;head one~|~head two~|~head three)}cell one~|~cell two~|~cell three
r2 c1~|~ r2 c2~|~ r3 c2{FANCYTABLE}{SPLIT}

