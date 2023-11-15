# closestreamlines
A tool for closing streamlines obtained by integration over a vector field

Work in progress. The code is now quite stable and robust.

The tool builds closed streamlines if possible from pairs of forward and backward streamlines obtained by integration over a vector field.

It is assumed that the streamlines should loop on themselves or remain open, i.e., in principle they should not be spiraling. A sufficient (but not necessary) condition is that the divergence of the field is null, as it is for example for 2D flows of incompressible fluids or for magnetic fields in a symmetry plane.

If the flow has streamlines that do not loop on themselves, like for instance in a slice of a vortex with out-of-plane components, the method will likely close the streamlines even if these should not be closed.

The quality of the result depends upon the quality of the integration. Both matplotlib's and pyvista's integrators are very good but they should be used with a sufficient resolution for optimal results. The integrators also have some control parameters that may need to be adjusted for the target applications.

There are many ways to distort (bend) the streamlines in order to compensate for the integration drift so that they accurately loop over themselves. The choices made here were done so that the method remains both simple and robust. It is probably possible to do better but the difference will be very small in the general case. In practice, the difference between drift compensation methods are likely to be visible only in the presence of singularities and, even in this case, they can be minimized by choosing a higher vector field resolution. Regarding the distortion (bending) of the streamlines, it is more likely to correct integration errors than to add noise to the result.

## Main procedures:
`closestreamlines.py` : procedures for processing the streamlines, including unpacking them from matplotlib or pyvista objects.

## Examples:
The three examples below illustrate how to use the tool for visualizing the streamlines of a magnetic field in the symmetry plane of a cuboid magnet. This case is a difficult one because it includes first order and second order singularities, i.e., abrupt change in the direction of the magnetic field on some boundaries of the magnet and streamlines degenerated to a single point at some points of the surface of the magnet. The proposed method works quite well for both type of singularities.

`matplotlib_magpylib_example.ipynb` : example with streamlines obtained with matplotlib.

`pyvista_magpylib_high_res.ipynb` : example with streamlines obtained with pyvista with integration at high resolution.

`pyvista_magpylib_low_res.ipynb` : example with streamlines obtained with pyvista with integration at low resolution. The streamlines are distorted and not regularly spaced but this comes from the fact that the streamline integration is done at a low resolution and the method for closing the streamlines does not fail.

You may try the `verbose=1` option to see some information about how the functioning of the method.

## To do: 
Examples without magpylib dependency.


Credit: this work partially builds upon [a first implementation shared by Alexandre Boisselet](https://github.com/magpylib/magpylib/issues/678#issuecomment-1806533202).
