# Why-your-First-Layer-breaks-free
Some REASONS why your First layer loses adhesion and breaks free

This is mainly about PLA, but you can "extrapolate" concepts and temps etc to other filaments.

"Z_HEIGHT"
===========================================================================================================
The most common reason is the "Z_HEIGHT" - rather than just say Z_Offset.... because Z_Offset is just ONE
way they tune where Z=0 physically is.

Z_Offset.  That is a setting that tells the system how much HIGHER the Nozzle Tip is compared to what the
hardware height measurement system told the system eas an "End Stop".
eg  As the printhead is lowered down, there is a hardware function to tell the system when to stop heading
downwards, seeing going any lower would (could) hit the print bed.
This End Stop is pretty well ALWAYS higher than the true contact point.  That is so it wil stop BEFORE
ever hitting the bed!

To print successfully, you need to know when the nozzle tip is RIGHT ON the bed. Ideally you want Z=0 to
be right at that nozzle to bed contact point.  Then you rise to the First layer Height, say 0.2mm to print
that First Layer.
Adhesion needs that extruded filament to "squish" at least some amount, so that it has "pushed" filament 
into the bed at least a BIT. So whilst you "say" you want a 0.2mm layer height, it might begin at 0.18mm
height really, to give that 0.02mm squish amount.

So, the End Stop value - whether from Micro Switches, or a probe etc - is some value. Maybe that is 3.2mm
above the Nozzle tip to bed contact point. So you need to have some OFFSET to add to your End Stop value
so you can arrive at the true contact point.
In that above exmaple/number.... 3.2mm.... you would need an Offset of 3.2mm - which a system might
require that to be a negative number, or they might "know" that the positive value given is to be
subtracted.  But anyway, they need to know that OFFSET value.
This is what the Z_Offset is !
But note that an Offset could be given in some other ways also!  Z_Offset exists, but it does not HAVE
to be used!  You could set Z_Offset=0, thus no correction for that End Stop difference, but an Offset
is entered into the SLICER instead. Z=0 is now still up 3.2mm higher, but all G-Code is offset with
-3.2mm and thus still corrects for it in the end!
But the NORMAL way to correct the offset is to use the Z_Offset.... so I advise always using that!

Now you have a Z=0 point that is truly where the nozzle tip contacts the bed.....
But beds are rarely LEVEL all over!  The point you checked the Z_Height, and then set the Z_Offset to
correct for, is ONLY valid at that single point! The bed is almost certainly 'wavy'... undulating
heights.  And this is why Bed Leveling/Meshing was created...

The system can test and record a Height Map of the bed. Well, that is IF you have Bed Leveling hardware,
such as a Probe of some kind!  You could still MANUALLY test and record a Bed Mesh (grid of positions)
to save and have the system use that, but that is quite tedious!  But 3D printer users had to do that
if they had no probve setup! These days almost every printer has a probe of some kind on it!

So you do a Bed Mesh (creation) and then all the wavy, undulations, are known., and the Z_Offset will
have another value offset that, to match the Bed Mesh recording. Thus the nozzle tip wil now TRACK the
bed height and then it will "always" be printing at Z="X" height (eg 0.18mm for Layer one)

So you might now see that setting the Z_Offset to a CORRECT value is critical. But also a Bed Mesh is
critical.
Also, for the Z_Offset you will almost certainly need to tune/tweak that when you WATCH a print test
doing that First Layer. So that it truly is printing with the optimal "squish" amount. Plus printing some
test piece will shows it is TRACKING the Bed Mesh well.

Many printers can do an excellent Bed Mesh - highly accurate. Some not so accurate, thus SOME areas
might not have optimal adhesion, and clean first layers/lines, and could need manual editing of indivual
Bed Mesh grid points to fix those up - or maybe re-running a Bed Mesh could do it better next time.

You almost always begin printing in the bed centre area. But if you do multiple objects, some will begin
elsewhere. And IF they are in a 'poor' Bed Mesh area, then that object could break free!

So this is ONE case of where and why an object might break free. Whilst "90%" of your other printing
never fail like that..,,,
You need to do test prints that check ALL of the bed... and then fix the problem areas, with that
manual tuning of gris points, or re-run the Bed Mesh and test that again.


HEATING
========================================================================================================
Extruded plastic is HOT.  It is also "sticky" when hot. This means it can/will stick to the bed when it
is laid down into it. And even a bit more so if it was "squaished" into the bed - which is what we
covered above.

But it is extruded at 200degC region..... and will cool down to the bed temperature region.
If the bed is COLD, the plastic will go full hardened and have virtually ZERO "stickiness". Then the 
adhesion level will go to zero (or neaer that) also!  So you want a heated bed!
For PLA it seems best is from 45degC to 60degC.  The range/variation can tie in with what true temp
the bed is at, versus the reported value(!), or what material the bed surface has, or even the SHAPE
of the object - more to do with what First Layer surface area it has.
An object with a small surface area might need HIGHER heat on the bed.  Or might HAVE to have a Brim,
or a Raft, so that it has a larger surface area on the bed then.


"GLUE" and Tape
========================================================================================================
There are various glues (glue sticks, liquids etc) that you can use to COAT the bed so that object then
stick much better - if not extremely well! In "end result" these can be excellent!!  But in MESS, and
needs to clean up, they can be painful!
The ideal printing system needs ZERO user effort, and ZERO clean up! LOL
So there are bed SURFACES that provide that solution!!  Though none get it 100% perfect/reliable. Thus
glue/tape might still ne a required option....



COOLING
========================================================================================================
We ewere worried about HEATING the bed before -and heating is a critical need - if you do not use glue/tape!
But when printing it is best if the extruded plastic is COOLED, and often FAST, to give the cripest and most
accurate printing "lines" - thus final object surface, and dimension etc.
But cooling is the ENEMY of ADHESION !!

So the bed is heated......
The extruded plastic needs to be cool(er).....
We can't do BOTH!!......

The printhead will have a "parts cooling fan", to cool the extruded plastic as soon as it hits the prior
plastic layer. the plastic will meld/melt into the lower layer before it coools enough, so that is fine,
but if you are on Layer TWO then the cooling will also be cooling down Layer ONE - which is the layer we
NEED to be warm/soft and giving adhesion to the bed!

The Bed is warm/hot.... so that helps....

What we do is DON'T COOL the object until a few layers have been laid down - so that by then the parts
cooling fan will HOPEFULLY not cool Layer ONE anymore.

So this is a source of adhesion LOSS. If the parts cooling fan is used on too low a layer.
For a small object it matters more!  Wait for MORE layers first!  Except maybe it has slopes or
overhangs on the first layers, which need good, quick, cooling, so they do not droop/sag. Well, you
can't win all battles!! You will need to COMPROMISE - maybe TEST - to see what cooling setup works best
for THAT object.

There are also, more and more common, non-printhead mounted Parts Cooling Fans, that can blow a ton of
air over the printed object! Again, cooling that first layer down too much to continue to adhere!
And, again, you will have to TEST how to control those fans in a workable manner for any given object
you print!

I think this COOLING aspect is one of the biggest cause that users OVERLOOK in finding the reason why
their objects keep losing adhesion!!!!
Yes, the Z_Offset is CRITICAL.... but most people know that, and can set it up well.  Maybe not always
truly optimal, but still "very well". But FEW users think enough about the COOLING problem!


In The End
========================================================================================================
1) Get the Z_Offset optimal !!!
2) Use a GOOD print bed surface!  PEI etc plates, or glass, or "Ultrabase" etc
3) Use Bed HEAT
4) Cooling - I think it is best to use appropriate, ADEQUATE, cooling so that your object print quality
   is best. And if that cooling amount means adhesion is lacking, THEN use a gluestick etc. It is likely
   it only occurs on smaller objects anyway.
   But also, you might just be using TOO MUCH cooling - more than truly required, and causing that loss
   of adhesion unecessarily!




