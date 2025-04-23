# dystopia_asmfixes
Repository where i put fixes for Dystopia made by directly modifying the server's library code.
Install by renaming the file so it replaces the original file, backup the original in case there is a problem and do not use on your client, as i do not know what VAC does with modified client library files.
Fixes are made for the "Callisto update" dystopia build.(Dystopia devs worked on The Callisto Protocol, and the latest update to the game followed weeks after its release.)
Files are : 
server_srvJIP.so : Fix for RestorePlayerTo(part of FinishLagCompensation) executing a failsafe possibly meant for debug build if the lag compensated player is inside a forcefield or another player.(result is you get teleported to where you were on someone else's computer in certain cases)
server_srv_JIP2.so : see above + attempted fix for SPROP_COORD prediction lag bug, achieved by forcing flags int to have SPROP_COORD flag masked out and SPROP_COORD always set even if bits isn't 32.
serverJIP.dll : server_srvJIP.so but for windows
