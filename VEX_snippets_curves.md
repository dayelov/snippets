# Curve/Spline

Gradient along curve:
```cpp
float ValueAlongSpline = @ptnum/(@numpt-1.0);
```
Curve on Ramp:
```cpp
float gradient = @ptnum/(@numpt-1.0); 
@Cd.y = chramp('colorRamp', gradient);  
```
measure:
```cpp
vector2 uv4 = set(f@curveu, 0);
uv4 = primuvconvert("op:../curve1", uv4, 0, chi("mode"));
f@curveu = uv4.x;
```

 convert | arg; | value
--- | --- | ---
real > unit |          0  |  0.11..   
real > unitlen |       1  |  0.9..
real > len |          2 |  15..
unit > real  |         3  |  9
unit > unitlen  |      4  | 0-1
unit > len    |        5  | dl! // 33 
unitlen > real  |      6  |  9
unitlen > unit  |       7  | 0-1
unitlen > len  |       8  | dl! // 33
len > real   |        9  |  0.06
len > unit    |        10  |  0.07
len > unitlen |      11  |  0.033


**Shape Polywire with ramp for combined curves**
```
// Create Primitive Wrangle before polywire, use @width as Wire Radius
// Get array of points in each curve (primitive)
i[]@primPts = primpoints(0, @primnum);

// For each point in current curve
foreach (int i; int currentPoint; @primPts){
    float ramp_index = fit(i, 0, len(@primPts)-1, 0,1);
    f@widthPrim = chramp("shape", ramp_index)/20;
    setpointattrib(0, "width", currentPoint, @widthPrim, "set"); 
    }
 ```

**Fade noise on curves with ramp**
```
// Requires uvtexture SOP in "Pts and Columns" mode before this wrangle

// Define UI controls
float remap_uv = chramp('remap_uv', @uv.x);
float power = chf('Noise_Power');
float freq = chf('Noise_Frequency');

// Create noise
vector noiseXYZ = noise(@P*freq);
// Modify noise values
vector displace = fit(noiseXYZ, 0,1, -1, 1)*power*remap_uv;
// Apply modified noise to a points position
@P += displace;
// Visualize fade ramp on curve
@Cd = remap_uv;
```

### Gradient on Curve
```
@gradient = @ptnum/(@numpt-1.0);
@ramponcurve = chramp('ColorRamp', gradient);  // map it to ramp
```

### Carve Curve
```cpp
float max = chf("max"); // like carve u parm
float min = chf("min"); // like carve v parm
vector uv;     
int primnum = @primnum;
float d = xyzdist(0, @P, primnum, uv);
@P = primuv(0, "P", primnum, set(fit01(uv.x,min,max), 0.0, 0.0));
```
```cpp
float animDur       = f@perimeter * 400.0;

float n             = fit( noise( v@P * 22.0 ), 0.2, 0.8, 0.0, 1.0 );
float offset        = fit01( lerp( n, rand( @primnum ), 0.35 ), 0.0, 15.0 );
float animPer       = fit( @Time - offset, 0.0, animDur, 0.0, 1.0 );

int primPts[]       = primpoints( 0, @primnum );
foreach( int pt; primPts )
{
    float u         = point( 0, "curveu", pt );
    if( u > animPer ){
        removepoint( 0, pt );
    }
}

if( animPer > 0.0 ){
    vector pos      = primuv( 0, "P", @primnum, set( animPer, 0.0, 0.0 ) );
    int newPt       = addpoint( 0, pos );
    addvertex( 0, @primnum, newPt );
}
```

### Delete last point
```cpp
@ptnum == `npoints(0)-1` //group the last point on curve
@ptnum == @numpt-1 // group the last point on curve
@ptnum%(@numpt-1)==0  //1st AND last point at the same time

0-`npoints(opinputpath(“.”,0))-2` // selects all points but the last. //
0 `npoints(0)-1` // select first and last point
/*to delete last point
- Delete By Pattern: $N
- Delete By Expression: $PT==$NPT-1
- Delete By Range: change Start to: $N*/


// Scale 10 times first and last points
if ((@ptnum == 0) || (@ptnum == (@numpt-1))) f@pscale = 10; 
else f@pscale = 1;
// Scale 10 times first and last points, short form    
f@pscale = (@ptnum == 0) || @ptnum ==(@numpt-1) ? 10 : 1;

# create Groupexpreesion SOP
neighbourcount(0, @ptnum) == 2

```