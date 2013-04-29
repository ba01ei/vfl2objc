Summary
=======

vfl2objc is a tool to convert VFL (Visual Formatting Language) based UI layout to native objective C code.


Usage
=====

First set it up by running:
    sudo setup.rb

Then restart Xcode. Click Xcode->services from top menu, you should be able to see vfl-file

To start a new VFL based code block, enter something like below in the right place in your code:

   UIView* superview = someView;
   // --- VFL
   /*
     |-10-[someElement]-10-|
     V:|-5-[someElement(100)]
    */
   // VFL ---

(Note: the first line and the last line are important.)

And then click vfl-file from the service menu. And the VFL block you entered will expand to a full code block.

Each time after editing something in the VFL section, also run the vfl-file service, so the code will get updated.


Rules
=====

|-5-[A(100)] means that element A is 5 points from the left edge of its container, and it's 100 points wide. And A has flexible right margin.

V:|-10-[B(50)] means that element B is 10 points from the top edge and is 50 points tall. (V means vertical). And B has flexible bottom margin.

|-5-[C]-5-| means that C has flexible width, and it's 5 points to the left edge and 5 points to the right edge.

V:[D]| means that D is touching the bottom edge, and have a flexible top margin, and D's height should be set beyond the VFL based block (either before or after)

|-5-[E]-5-[F(50)]-5-[G(>0)]-5-| means that E has a fixed width set outside the VFL block, F has a fixed width of 50 points, G has a flexible width

[H(100)] means that H is 100 points wide, and it's position and autoresizing mask is unknown, so you need to set them beyond the VFL block.


The rule of thumb is that there can be 1 and only 1 flexible element in 1 dimension, e.g.

|-5-[A(100)]-5-| is wrong because when the superview width is not 110 there will be a conflict.

|-5-[A(>0)]-5-[B(>0)]-5-| is wrong because it is unclear on how to assign the widths for A and B.



