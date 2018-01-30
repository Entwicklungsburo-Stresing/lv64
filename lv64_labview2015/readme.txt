 labview examples
these examples shows how to read a camera.


LoopselFF
implements a very constant measure loop outside labview
reads a complete block of nos scans
during block read, the thread is highest 
We recommend this example as starting point for own applications.
Call the SetupDMA vi only once with the max. RAM you will ever need.
As this takes a while, you should use smaller sub buffers by using parts of this big buffer
and should not allocate new buffers again.

usage:
after read the slider can select the scan which is displayed
first hit run, then hit arm/clear and then read.
For a new block of scans press stop then arm and then read again.


About
can read the registers of the PCIE board.
should not deliver zeros or 0xFF






Before calling any sub VIs, Init-> InitDrv + InitBrd  must have been called, 
otherwise an Error message appears! Wrap your call as shown in about.vi





