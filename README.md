# Brett: Bidirectional recurssive encoder from transformer time-dependent

If $T_1(\cdot), ..., T_L(\cdot)$ denote the output from one layer of stacked transformer structure (encoders or decoders), we have
```math
T_l(x) = f_l(A_l(x)+x)
```
