FIFO examples
these examples shows how to read 2 cameras parallel.
here a special flag for compiling the DLL is needed:
_HWCH2  TRUE  (in ESLSCDLL.h)
use this special compiled DLL for the example 
-> is saved here in the board.vis subfolder


GETFFCam(2)
starts PCI board timer and looks in a loop for data in the fifo by testing FFValid.
if so it starts reading this to main ram. 
Simplest version for not time critical apps.
is not able to reach high linerates (like 1kHz) as the display of data needs too much time.
!can not be faster then tread + tdisplay!
to get higher line rates display must be avoided like:
LoopSelFF displays later
RingGetCam2 displays not every scan.
also shown here is the setup for DAT (delay after trigger) if set to external trigger.
DAT can be monitored with a scope at the trig out plug of the PCI board (uses SetTOREG).



RingGetcam(2)
shows how to read (2) cameras parallel with a background thread.
The main read thread reads the FIFO data to main Ram. This part is executed in higher priority.
The display thread runs with normal priority and displays one of the last scans, 
which was copied by the main thread to an additional display buffer if it was requested by Flag FetchActLine
This Flag must be set once by calling DLLStartFetchRingBuf to start the cycle. 
With a 2nd Flag: DispBufValid both threads are syncronized. These Flags are global in the DLL (BOARD.C).

In the call of SRingStartThread the priority is set to 15 - thats standard max. priority.
For high speed cameras and heavy computing systems this value could be set to a max. val. of 31(timecritical).
In that case one core is exclusively used, but in case of a bug it never returns (cold reset needed).

this example uses just one memory array for both lines(length=1 line) with data sorted as: 
word array CHA
word array CHB
resort of hardware data is done in BOARD.C -> CallIORead
resort of arrays is done in the read loop of labview. 

also implemented is a ring buffer of size RingBufDepth=50
Could be used much bigger if needed. Here it is used for demonstration only.
in fact this function uses the ReadRingBlock function (RingBlockSel) with start=stop=0
-> copy only the actual line to user buffer



LoopselFF
implements a very constant measure loop outside labview
reads a complete block of nos scans
during block read, the thread is highest 
(important only for single core systems: should run modal and disable mouse).
if needed: set _PS2KEYBOARD TRUE and recompile DLL
we recommend this example as starting point for own applications.

usage:
after read the slider can select the scan which is displayed
first hit run, then hit arm/clear and then read.
For a new block of scans press stop then arm and then read again.


RingBlockSel(2)
same as RingGetCam, but a block of scans is copied, not only one.
the background thread is collecting data all the time.
the call of ReadRingBlock copies a block of 
start up to stop around the calling time stamp to the user buffer
if start,stop is <0 it is in the past, if >0 it is in the future
in future means the thread is waiting until all data is collected
and copies all data after that to the user buffer.

usage: 
if stop fetch is pushed, the data is copied once to user buffer and the slider can walk trough the buffer
if stop fetch is not pushed, the user buffer data is overwritten in 50ms (timer vi) 



for more infos and comments, please have a look to the DLL sources ESLSCDLL

!!!!
Before calling any sub VIs, Init-> InitDrv + InitBrd  must have been called, 
otherwise an Error message appears! Wrap your call as shown in about.vi





