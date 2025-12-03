# dystopia_asmfixes
Repository where i put fixes for Dystopia made by directly modifying the server's library code.

Install by renaming the file so it replaces the original file, backup the original in case there is a problem and do not use on your client, as i do not know what VAC does with modified client library files.

Fixes are made for the "Callisto update" dystopia build.(Dystopia devs worked on The Callisto Protocol, and the latest update to the game followed weeks after its release.)
Recommended files are server_srvJIP and the engine_srv_JIP_128UPDATERATE ones

Files are : 

server_srvJIP.so : Fix for RestorePlayerTo(part of FinishLagCompensation) executing a failsafe possibly meant for debug build if the lag compensated player is inside a forcefield or another player.(result is you get teleported to where you were on someone else's computer in certain cases)

server_srv_JIP2.so : see above + attempted fix for SendPropVector SPROP_COORD prediction lag bug, achieved by forcing flags int to have SPROP_COORD flag masked out and SPROP_NOSCALE always set even if bits isn't 32.(update: does not work, ignore this one safely)

server_srvJIP_MPROUNDSNOW : same as JIP(rollback fix) with another patch making successful mp_rounds votes apply now instead of at round end. Meant to be used with https://github.com/bauxiteDYS/SM-DYS-Round-Info

engine_srv_JIP_128UPDATERATE : Fix a bug in Source 2013 engine that makes the server cap clients' updaterate and cmdrate at 100 when the server tickrate is above 101, the patch makes the server force the client to always use 128 no matter what to prevent netcode-bound network "stuttering"(ticks where no data is sent or received inconsistently due to engine rate capping logic)

serverJIP.dll : server_srvJIP.so but for windows
