# Postprocess RAMSES outputs

Here I store some snipet of code that I have found useful in the past:

## Loops in batch
Here is an example of loops in batch:

```for i in {1..188}; do cp output_00$i/info_00$i.txt info ; done ;```

## Generating random points on a sphere
Naive implementation to generate points on a sphere may lead to wrong results (eg. https://mathworld.wolfram.com/SpherePointPicking.html). Here is my implementation to generate ``npart`` point of a unit 3-sphere in Mathematica:
```
npart = 10;
tab = ParallelTable[0, {i, npart + 1}, {j, 3}];
For[i = 1, i < npart + 2, i++,
 r = Random[Real, {0, 1}];
 cth = Random[Real, {-1, 1}];
 sth = Sqrt[1 - cth^2];
 \[Phi] = Random[Real, {0, 2 \[Pi]}];
 tab[[i, 1 + Mod[i, 3]]] = r*sth*Cos[\[Phi]];
 tab[[i, 1 + Mod[i + 1, 3]]] = r*sth*Sin[\[Phi]];
 tab[[i, 1 + Mod[i + 2, 3]]] = r*cth;
 ]
```
