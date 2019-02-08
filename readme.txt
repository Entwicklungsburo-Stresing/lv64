Howto operate the cameras with LabVIEW

Usage:
The camera can perform a specific number of samples in a block-wise fashion.
The number of samples per block (nos) and the number of total blocks (nob)
are defined in the lower left box of the conrol front panel.

After this values have been entered, the "alloc mem" button must be pressed,
before the first measurement can be started. Each time these parameters are
changed, the amount of allocated memory must be updated as well.

A single run can be started by clicking the "start" button in the lower right
box of the panel. A single run cycles through all the blocks and performes as
many samples per block as previously being specified.

The exposure time can be modified in the same box and should not be much lower
than 0,125 ms. 

The measurement can also be done continuously after activating the correspondig
switch in the same box. The measurement can be aborted by pressing ESC.

Before LabVIEW can be terminated, the "exit here" button must be pressed in
order to stop the cam control program and its background processes propperly.

After a single run or during a measurement, the two sliders can be used to
browse through the blocks and the samples.


About
can read the registers of the PCIE board.
should not deliver zeros or 0xFF






Before calling any sub VIs, Init-> InitDrv + InitBrd  must have been called, 
otherwise an Error message appears! Wrap your call as shown in about.vi





