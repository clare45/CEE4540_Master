# Deriving $Q(t)$ for a Tank with a Valve

This document contains the derivation of the flow through a tank-with-a-valve over time, $Q(t)$. Our reference will be a simple hypochlorinator, shown in the following image. In the image, a hypochlorite solution is slowly dripping and mixing with piped source water, thereby disinfecting it. The valve is almost closed to make sure that the hypochlorite solution drips instead of flows. At the end of this document is an image which shows the variables in the final equation.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flow%20Control%20and%20Measurement/Images/drip_hypochlorinator.jpg?raw=true" width=400></center>

This derivation begins by finding two equations for flow, $Q$, through the hypochlorinator and setting them equal to each other. First, the rate of change of the volume of hypochlorite solution in the tank is equivalent to the flow out of the hypochlorinator. Since the volume of hypochlorite solution in the tank is equal to the tank's cross-sectional area times it height, we get the following equation:

$$Q =  - \frac{d\rlap{-}V}{dt} = - \frac{{A_{Tank}}dh}{dt}$$

Such that:  

$\frac{d\rlap{-}V}{dt}$ = rate of change in volume of solution in the tank  
$\frac{dh}{dt}$ = rate of change in height of water (hypochlorite solution) level with time  

Our other equation for flow is the head loss equation. Since major losses are negligible for a short pipe-low flow rate system, we only need to consider minor losses. The only real minor loss in this system occurs in the almost-closed valve that is dripping the hypochlorite solution. However, we will also use the head loss trick. Therefore, the total driving head of the system $h$ is equal to the minor losses:

$$h = h_e = \left( \sum K_e \right) \frac{Q^2}{2gA_{Valve}^2}$$

Bear in mind that this is the second form of the minor loss equation as described in [this previous derivation](https://github.com/AguaClara/CEE4540_DC/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flow%20Control%20and%20Measurement/Images/Derivation_minor_loss_equation.md "Minor loss equation derivation"). Rearranging the minor loss equation to solve for $Q$, it looks like this:

$$Q = A_{Valve} \sqrt{\frac{2 h_e g}{\sum K_e}}$$  



Now we can set both equations for $Q$ equal to each other and move them both to one side:

$$A_{Tank} \frac{dh}{dt} + A_{Valve} \sqrt{\frac{2gh}{\sum K_e}} = 0$$


From here, calculus and equation substitution dominate the derivation. Separating the variables of the equation immediately above, we get the following integral:

$$\frac{ -A_{Tank}}{{A_{Valve}} \sqrt{\frac{2g}{\sum K_e}} }   \int \limits_{h_0}^h \frac{dh}{\sqrt h} = \int \limits_0^t {dt}$$

Which, when integrated, yields:

$$\frac{ -A_{Tank}}{A_{Valve} \sqrt{ \frac{2g}{\sum K_e}} } \cdot 2 \left( \sqrt{h} - \sqrt{h_0} \right) = t$$

And solved for $\sqrt{h}$ returns:

$$\sqrt h  = \sqrt{h_0} - t \frac{A_{Valve}}{2 A_{tank}} \sqrt {\frac{2g}{\sum K_e}}$$

At this point, the steps and equation substitutions may begin to seem unintuitive. Do not worry if you do not understand why _exactly_ a particular substitution is occurring. Since we determined above that $h_e = h$, our equation above for $\sqrt{h}$ is also an equation for $\sqrt{h_e}$. As such, we will plug the equation above back into the minor loss equation solved for $Q$ from above, $Q = A_{Valve} \sqrt{\frac{2 h_e g}{\sum K_e}}$, to produce:

$$Q = A_{Valve} \sqrt{\frac{2g}{\sum K_e}} \left( \sqrt{h_0}  - t \frac{A_{Valve}}{2 A_{tank}} \sqrt{\frac{2g}{\sum K_e}} \right)$$

Now we can focus on getting rid of the variables $A_{Valve}$, $\sum K_e$, and $A_{tank}$. By using the minor loss equation once more, we can remove both $A_{Valve}$ and $\sum K_e$. Consider the initial state of the system, when the hypochlorinator is set up and starts dropping its first few drops of hypochlorite solution into the water. The initial flow rate, $Q_0$, and elevation difference between the water level and the valve, $h_0$, can be input into the minor loss equation, which can then be solved for $A_{Valve}$:

$$ A_{Valve} = \frac{Q_{0}}{ \sqrt{ \frac{2 h_0 g}{\sum K_e}} }$$

Plugging this equation for $A_{Valve}$ into the equation for $Q$ just above, we get the following two equations, in which the second equation is a simplified version of the first:

$$Q = Q_0 \frac{1}{\sqrt{h_0}} \left( \sqrt{h_0} - \frac{Q_0 t}{2 A_{Tank} \sqrt{h_0}} \right)$$

$$\frac{Q}{Q_0} = 1 - \frac{t Q_0}{2 A_{Tank} h_0}$$

This next step will eliminate $A_{Tank}$. However, it requires some clever manipulation that has a tendency to cause some confusion. We will define a new parameter, $t_{Design}$, which represents the time it would take to empty the tank _**if the initial flow rate through the valve, $Q_0$, stays constant in time**_. Of course, the flow $Q$ through the valve does not stay constant in time, which is why this derivation document exists. But imagining this hypothetical $t_{Design}$ parameter allows us to form the following equation:

$$ Q_0 t_{Design} = A_{Tank} h_{Tank}$$

This equation describes draining all the hypochlorite solution from the tank. The volume of the solution, $A_{Tank} h_{Tank}$, is drained in $t_{Design}$. Rearranged, the equation becomes:

$$ \frac{Q_0}{A_{Tank}} = \frac{h_{Tank}}{t_{Design}}$$

Such that:  
$h_{Tank}$ = elevation of water level in the tank with reference to tank bottom at the initial state, $t = 0$

Here lies another common source of confusion. $h_{Tank}$ is not the same as $h_{0}$. $h_{Tank}$ is the height of water level in the tank with reference to the tank bottom. $h_{0}$ is the water level in the tank with reference to the valve. Therefore, $h_{0} \geq h_{Tank}$ is true if the valve is located at or below the bottom of the tank. If the tank is elevated far above the valve, then the $h_{0} > > h_{Tank}$. If the valve is at the same elevation as the bottom of the tank, then $h_{0} = h_{Tank}$. Please refer to the following image to clarify $h_{0}$ and $h_{Tank}$. Also note that both $h_{Tank}$ and $h_{0}$ are not variables, they are constants which are defined by the initial state of the hypochlorinator, when the solution just begins to flow.

<center><img src="https://github.com/AguaClara/CEE4540_Master/blob/master/AguaClara%20Water%20Treatment%20Plant%20Design/Flow%20Control%20and%20Measurement/Images/hypochlorinator_variable_explanation.jpg?raw=true" width=550></center>


Finally, our fabricated equivalence, $\frac{Q_0}{A_{Tank}} = \frac{h_{Tank}}{t_{Design}}$ can be plugged into $\frac{Q}{Q_0} = 1 - \frac{t Q_0}{2 A_{Tank} h_0}$ to create the highly useful equation for flow rate as a function of time for a drip hypochlorinator:

$$\color{purple}{
\frac{Q}{Q_0} = 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0}
}$$

Which can be slightly rearranged to yield:

$$\color{purple}{
Q(t) = Q_0 \left( 1 - \frac{1}{2} \frac{t}{t_{Design}} \frac{h_{Tank}}{h_0} \right)
}$$

Such that:  
$Q = Q(t)$ = flow of hypochlorite through valve at time $t$  
$t$ = elapsed time  
$t_{Design}$ = time it would take for tank to empty *if* flow stayed constant at $Q_0$, which it does not  
$h_{Tank}$ = elevation of water level with reference to tank bottom  
$h_0$ = elevation of water level with reference to the valve  

"How does this 'tank with a valve' scenario differ from the 'hole in a bucket' scenario?" some might ask. If you are interested, you may go through the derivation on your own using the orifice equation instead of the minor loss equation for the first step. If you do so you'll find that the equation remains almost the same, the only difference being that the $\frac{h_{Tank}}{h_0}$ term drops out for an orifice, as $h_{Tank} = h_0$. The big difference in the systems lies with the flexibility of having a valve. It can be tightened or loosened to change the flow rate, whereas changing the size of an orifice multiple times in a row is not recommended and is usually irreversible.
