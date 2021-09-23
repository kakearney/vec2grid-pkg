## vec2grid.m Documentation
[![View vec2grid on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://www.mathworks.com/matlabcentral/fileexchange/21617-vec2grid)

This is a simple utility to rearrange a list of data points into an ndgrid-style grid.  It allows the original data points to be listed in any order, and allows for missing grid points (which become NaNs in the final grid).

**Note:** In order to support higher dimensional data, I opted to return data in ndgrid format rather than meshgrid format.  This means output will often need to be transposed to be used with plotting functions like surf, pcolor, etc.

### Syntax

```
[xg, yg] = vec2grid(x1, x2, ..., y);
[xg, yg] = vec2grid(xy);
[xg1, xg2, ... yg] = vec2grid(...);
```

### Example

Let's assume we have a list of 2D data points, with a corresponding vector of z-data for each x-y point.  The data points are stored in random order, and a few points are missing from the full grid.

```matlab
[x,y] = ndgrid(1:4,1:5);
z = (1:numel(x))';

order = randperm(numel(x), numel(x)-3)';
x = x(order); y = y(order); z = z(order);

[x y z]
```
```
ans =

     1     3     9
     3     5    19
     4     3    12
     3     3    11
     2     2     6
     2     4    14
     4     5    20
     1     5    17
     2     3    10
     2     5    18
     4     2     8
     3     2     7
     3     4    15
     2     1     2
     1     1     1
     1     4    13
     3     1     3
```

We use vec2grid to return the data to a gridded format.  

```matlab
[xg,yg,zg] = vec2grid([x y z])
```
```
xg =

     1
     2
     3
     4


yg =

     1
     2
     3
     4
     5


zg =

     1   NaN     9    13    17
     2     6    10    14    18
     3     7    11    15    19
   NaN     8    12   NaN    20
```




