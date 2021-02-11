First - I love the completeness of your Challenge answers ... it really helps
me to see what you know and where you are still fuzzy.  Fantastic!  100%!!

The oval drawdown is tricky.  Think of it this way.  The flow in a homogeneous
medium is coming predominantly from the direction with the highest gradient.
In this case, this 'stretches' the cone such that it is steeper toward the
constant head boundary and flatter toward the no flow boundary.  But, this
effect becomes more pronounced as you approach the boundary.  So, right by
the well, the drawdown is still circular.  Is that better?

As for flipping the axes .. you don't want to flip them for the plots that use
the built-in flopy plotting utilities ... these have been flipped.  It is only
for plots that you make using matplotlib or similar that you have to remember
that the MODFLOW row naming convention is flipped from that in python.  Good?

Remember also that TOTAL flow in equals TOTAL flow out.  So, flow in through
the left boundary equals flow out through the right PLUS the flow out through
the well!

Great job on testing your intution, too!  The funky diamond is actually just
showing you that the model failed to converge.  It is a plot of garbage
results :)
