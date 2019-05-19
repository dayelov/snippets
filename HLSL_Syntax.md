
## Loop  
`[Attribute] do { Statement Block; } while( Conditional );` 
- Execute a series of statements continuously until the conditional expression fails. For statement.  Iteratively executes a series of statements, based on the evaluation of the conditional expression.    

`[Attribute] while ( Conditional ) { Statement Block; }` 
- while  
## Conditioning
`[Attribute] if ( Conditional ) { Statement Block; }`  

```hlsl
Particles.NormalizedAge < 0.333 ? float4(1,0.1,0.1,1) : Particles.NormalizedAge < 0.575 ? float4(0.1,1,0.1,1) : float4(0.1,0.1,1,1)
```
```hlsl
Particles.Position.z > Emitter.InitialPosition.z - Emitter.ZOffset ? Particles.Position : float3(Particles.Position.x, Particles.Position.y, Emitter.InitialPosition.z -Emitter.ZOffset)
```


## Switch
`[Attribute] switch( Selector ) { case 0 : { StatementBlock; } break; case 1 : { StatementBlock; } break; case n : { StatementBlock; } break; default : { StatementBlock; } break;` Switch  


### Var

```hlsl 

float4 color;
float fVar = 3.1f;

int iVar[3];

int iVar[3] = {1,2,3};

uniform float4 position : SV_POSITION; 
const float4 lightDirection = {0,0,1};
```