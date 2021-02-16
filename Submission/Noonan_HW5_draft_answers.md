## Gillian Noonan
## HW 5 Challenge and Discussion Questions: Recharge Me


## **Challenge:**
A flopy code is provided to you that recreates the 3D homogeneous box model with constant head boundary conditions.  The aquifer is now defined as unconfined - it was confined for the BoxModel simulations and the recharge package has been added.  You will use this to explore the impact of recharge into an unconfined aquifer.  

### Model Description
Initial conditions:
- Homogeneous medium.  
- Unconfined aquifer, recharge package added.
- Well is located at [0,10,15] - well not pumping
- Recharge rate is 0.
- Left and right constant head boundaries = 20, 10

You need to modify the model to:
  - Reduce boundary heads to 15 and 5.  
  - Add recharge at a constant rate of 1e-4 m/day over the entire top boundary.  
  - Model a system with zero recharge except for a farm located in [6:10, 6:10] - in python terms.  Recharge beneath the farm is 1e-4 m/day due to excess irrigation.  
  - Start the well pumping at a rate of 8 m3/day.  


---------------------------------------------------------
------------------------------------------------------------
### Noonan - Notes

*Lecture Notes:*

*Notes on Recharge with MODFLOW*
  >   - unconfined aquifer conditions are what makes sense for recharge (convertible cells in MODFLOW - convert between confined and unconfined on the fly)
  - Change head to 15 and 5
    - slope will be the same: gradient same, K same, same flow through system. However - aquifer thickness is 10.  Second case will have an unsaturated zone.  
    - Gradient on right needs to be steeper to account for flow, so gradient becomes curved across the model instead of constant decrease.
  - In the two cases of 20, 10 and 15, 5: K is same, gradient is decreased, so flow must also be decreased.  Transmissivity is changing because saturated thickness is changing.
  - Non-linear problem: we don't know what the head distribution is until we know the saturated thickness.  But we don't know the head distribution until we know the saturated thickness.  All we know is it will be a curve.  Complicated because part of aquifer is confined, other part is unconfined.   The top portion will be linear because it's still confined, then becomes non-linear at water table, where slope continually increases to boundary because thickness is continually decreasing.  Rate of decrease depends on head needed to establish the steady-state flow.
  - Recharge is flux of water across the water table.  Recharge = P-ET (for steady state).  

*For model with confined and unconfined zones:*
  >- Equipotential surface at water table, where head is zero, acts as no-flow boundary.  For MODFLOW to handle it, it converts the cell (thickness of layer to closest layer thickness dependent on water table elevation (for unconfined aquifer).   
  -  It's a Non-linear problem: Don't know water level until solve flow problem, don't know how to solve flow problem until we know what the thickness is.  Have to guess water table elevation, solve flow problem for that distribution of transmissivities.   Check do we end up with head distribution that we assumed to start with?  If no, adjust head and solve again until head distribution gives us the transmissivity that, coupled with that head distribution or gradient, ends up in steady state flow conditions.

Think in terms of how will changes affect model:
> recharge: why does it look different?  If i add recharge, what's going to happen?

Recharge in the form of excess irrigation from a farm (square area in middle of domain) -
> look in plan view and try to understand where recharge is going.  Draw which areas might be contaminated from farm.

Recharge effect on head -
  >- reduced gradient on left (less water in ) -  increased gradient on right (more water out), ponded water so saturated thickness is higher.  
  - size of curve depends on how much water is being added. Enough water can even change direction of gradient (push out both sides)
----------------------------------
-------------------------------------

### Noonan - Challenge Response

***1) For the initial boundary head values and pumping and recharge rates, compare the head versus x distance - along a transect from the middle of one constant head boundary to the other - to the results for the BoxModel.  Now reduce the boundary heads to 15 and 5.  Compare this result and explain any observed differences.  The overall gradient is the same, as is the K of the medium ... is the flow the same for both boundary conditions?  Why or why not?***
> Answer: For initial boundary head values and pumping and recharge rates, the starting well is zero pumping and recharge is 0 - in this way, it equals the basic homogeneous box model simply with constant head values of 20 on the left and 10 on the right.

> After reducing the heads to 15 and 5 and comparing the plots (see below), the noticeable difference is that the 15,5 plot shows some curving towards the right side of the plot - the gradient is no longer linear.  

> In the two cases of 20, 10 and 15, 5: K is same, gradient is decreased, so flow must also be decreased.  Transmissivity is changing because saturated thickness is changing.  Aquifer thickness is 10.  So, the second case (15,5) will have an unsaturated zone.  Flow only takes place through the saturated part of aquifer.  Aquifer thickness is cut in half - so transmissivity is also halved.  On the right hand side, it's harder for water to flow through, but the same amount needs to flow through to maintain steady state conditions.  Therefore, the gradient on right needs to be steeper to account for flow, but still needs to meet point 15 on left and 5 on right for constant head conditions. thus, the gradient becomes curved across the model instead of constant decrease like in the 20,10 condition.


constant head boundary of 20, 10
![](assets/Noonan_HW5_draft_answers-2b8cfc6c.png)

constant head boundary of 15,5
![](assets/Noonan_HW5_draft_answers-c7af994f.png)


***2) Now add recharge at a constant rate of 1e-4 m/day over the entire top boundary.  Explain the head transect and boundary flows.  Is flow in this system 2D or 3D?  Is it represented as 2D or 3D?  Explain what you mean by your answers.***
> Answer:   Adding water across the entire top boundary is reflected in the head gradient plot as reduced gradient on left (less water in) and increased gradient on right (more water out) in order to maintain the steady state and constant head boundary conditions.  

> The flow in this system is 2D because now we have water flowing down and across the profile, however, I believe per lecture that MODFLOW represents this as 1D flow per cell, as it converts the cell, based on the thickness of the nearest saturated zone, simply to 1D flow at an elevation representing the water table?

![](assets/Noonan_HW5_draft_answers-3dfd15c8.png)

***3) Now model a system with zero recharge except for a farm located in [6:10, 6:10] - in python terms.  Recharge beneath the farm is 1e-4 m/day due to excess irrigation.  First, calculate the annual excess irrigation, in meters, that has been applied to the farm.  Second, assuming that the crop is cotton, it is located in southern Arizona, and cotton is grown all year (for simplicity), calculate the total irrigation rate on the farm that would be associated with this amount of excess irrigation.  Finally, identify the area within the domain that might be subject to contamination if the recharge water was somehow tainted.***
> Answer:  Annual excess irrigation per year in meters = 1e-4 m excess irrigation/day x 365 day/yr = .0365m/yr

> If crop is cotton, and grown in AZ, total irrigation rate on farm would be found via the relationship:
 >> Total irrigation + total rainfall - cotton plant uptake - evaporation = excess recharge

> To identify the area within the domain that may be affected by contamination, one should follow the flow lines out of the irrigation zone.  The below plot highlights the potentially affected zone.

![](assets/Noonan_HW5_draft_answers-93dabdd5.png)

***4) Lastly, start the well pumping at a rate of 8 m3/day.  Using one color, identify the capture zone of the well.  Using a second color, show the area that might be contaminated by the irrigated farm fields.  Comment on the impact of the well on the pattern of potential contamination.***
> Answer:  The plot below shows again the potentially impacted zone from irrigation on the farm, and the flow lines going to the well that is pumping at a rate of 8m3/day.   It can be seen that the two shapes overlap, indicating potential contamination in the well from the agricultural field excess recharge.  The flow lines can be seen bending toward the well, indicating that it may pull some of the contaminated water that would have traveled further to the right.   In this way, it could act as a reducing factor to overall subsurface contamination.

![](assets/Noonan_HW5_draft_answers-7b729318.png)
--------------------------------------

### Discussion Points
**In addition to The Challenge, start thinking about the following ideas:**

How can MODFLOW, which does not model unsaturated flow, represent an unconfined aquifer?
> Initial Thoughts:  With a type 2 boundary at the top of the water table??  Like a flux through?

What do you think would happen (in MODFLOW) if you pumped an unconfined aquifer so hard that the water level dropped below the bottom of the aquifer?  Explain this from the point of view of what is happening in the model ... then think about what would happen in real life!
> Initial Thoughts: These are hard questions, whoa.  In MODFLOW, if the water level dropped below the bottom of the aquifer, wouldn't that be zero flow?  like no water available to pump??  So it would look like pumping a dry unit perhaps, whatever that looks like?  I'm not sure i really understand conceptually here what is happening when pumping an unconfined aquifer actually results in the water dropping below the bottom of the aquifer, how is that even physically possible?

How will the steady state capture zone of a model with recharge differ from that in the same model without recharge?
> Initial Thoughts:  The capture zone of a model with recharge vs a model without recharge - well, firstly, the model with recharge has more water available to capture, so there will be less effect on the outflow balance?  But overall, the size of the capture zone should not change since it is dependent on the pumping rate and not the available water supply??

What is recharge?  What does it mean to define recharge for a MODFLOW model?  How is it related to defining ET and precipitation?  Where, exactly, is the top boundary of the model?
> Initial Thoughts:  Recharge is flux of water across the water table.  Defining recharge for a MODFLOW model means adding a rate and area of distribution for this additional flow coming from the top of the model.  Recharge is related to ET and precipitation (P) by the fact that Recharge = P-ET (for steady state).  The top boundary of the model is at the top of the uppermost layers of cells in your model domain?
