
POPs: Vex based solver


# Properties
```md
- OBJECT 
- PRE-SOLVE
- SOURCE 
```

#### OBJECT Input  
- popobject  

#### PRE-SOLVE Input    
- pop vop  

#### SOURCE Input    
(birth/birth from attribute)
- fireworks  
- popattract (to point or geometry)  
- popdrag  
- popvop // sam mozesz zrobic force, np ( vel +=  noise)  
  
- popcurveforce // podpinasz krzywa i leci  
- popcolision (stick/ bounce)  
- popgroup  
- popforce // jakies noizy Old thing   

## POP SOLVER:  
(behavior on collisions)

## Multi Solver
multisolver is for pops (and rigid body)

## POP FLUIDS:  
popfluid PBD fluid make intersection in pops (node from white water) (h17 core of new water solver in future maby with vellum). 
```
Constrain Iteration -  20 
Constrain Stiffness - 100 (stay toghether )
Viscosity - higher value to sticky durfaces 
Tensile Strengh - keep distance between particles 0.01 - larger make
```

## SOURCE
(source obj) debricesource // for RBD ingeret vel
(source obj) fluidfource // volume source from point