How to operate the cameras with LabVIEW

Usage:
After run you can set the boards and some other params in the right upper frame.
Then press "Initialize"

The camera can perform a specific number of samples in a block-wise fashion.
The number of samples per block (nos) and the number of total blocks (nob)
are defined in the lower left box of the conrol front panel.

After this values have been entered, the "alloc mem" button must be pressed,
before the first measurement can be started. Each time these parameters are
changed, the amount of allocated memory must be updated as well bz pressing this button.

A single run can be started by clicking the "start" button in the lower right
box of the panel. A single run cycles through all the blocks and performes as
many samples per block as previously being specified.

The exposure time can be modified in the STIMER box or if external trigger is used, be sure not 
to exceed the 51kHz frontier.

The measurement can also be done continuously after activating the correspondig
switch in the same box. Additionaly you can use "fast continuous mode", it sets nob to 1 and optimize nos.
The measurement can be stopped by pressing ESC. Now the last blocks can be examined 
by moving the sliders.

To terminate the program you must use the "exit here" button, in order to stop
the cam control program and its background processes propperly.
If you use the labviews exit, the driver will not be closed properly!
That will lead to additional error messages.

After a single run or during a measurement, the two sliders can be used to
browse through the blocks and the samples.


About
can read the registers of the PCIE board.
Is intended for testing the driver install and should not deliver zeros or 0xFF


Before calling any sub VIs, Init-> InitDrv + InitBrd  must have been called, 
otherwise an Error message appears! Wrap your call as shown in the about.vi example.







