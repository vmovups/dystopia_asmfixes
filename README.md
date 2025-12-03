# dystopia_asmfixes
Repository where i put fixes for Dystopia made by directly modifying the server's library code.

Install by renaming the file so it replaces the original file, backup the original in case there is a problem and do not use on your client, as i do not know what VAC does with modified client library files.

Fixes are made for the "Callisto update" dystopia build.(Dystopia devs worked on The Callisto Protocol, and the latest update to the game followed weeks after its release.)

Recommended files are server_srvJIP_MPROUNDSNOW(or server_srv-collisionfix-stats-rounds.so) and the engine_srv_JIP_128UPDATERATE ones

Thanks to bauxite too, for helping finding the rollback bug with a purpose made test map for reliably triggering it and making me aware of the 128 tickrate bug, also helping testing weapon TTK and tickrate relation

Recommended tickrate is 128, due to the nature of the floating point logic used for time using 100 tickrate while seemingly the best(most weapons have integer multiples of 10ms time between each bullet fired) the TTK of fast firing weapons actually becomes intermittently worse over the course of the first 20+ minutes of map gameplay before becoming just worse overall, using 128tickrate provides stable weapon TTK that is close to what Puny Human intended, guarantees that time passes in increments of 0.0078125 seconds(instead of random 0.0100xxxx ~0.0099...) and reduces latency of non-lag compensated actions(cyberspace hacking, shooting spiders, boltgun firing etc...)

Files and their descriptions : 

server_srvJIP.so : Fix for RestorePlayerTo(part of FinishLagCompensation) executing a failsafe possibly meant for debug build if the lag compensated player is inside a forcefield or another player.(result is you get teleported to where you were on someone else's computer in certain cases)

server_srv_JIP2.so : see above + attempted fix for SendPropVector SPROP_COORD prediction lag bug, achieved by forcing flags int to have SPROP_COORD flag masked out and SPROP_NOSCALE always set even if bits isn't 32.(update: does not work, ignore this one safely)

server_srvJIP_MPROUNDSNOW : same as JIP(rollback fix) with another patch making successful mp_rounds votes apply now instead of at round end. Meant to be used with https://github.com/bauxiteDYS/SM-DYS-Round-Info (the mp_rounds fix should be harmless if you do not use the plugin on your server)

server_srv-collisionfix-stats-rounds.so : server_srvJIP_MPROUNDSNOW but bauxite included the hex edit to redirect stats to CartesianBear's stats server directly too, this way you do not need to modify the hosts file.

engine_srv_JIP_128UPDATERATE : Fix a bug in Source 2013 engine that makes the server cap clients' updaterate and cmdrate at 100 when the server tickrate is above 101, the patch makes the server force the client to always use 128 no matter what to prevent netcode-bound network "stuttering".(ticks where no data is sent or received inconsistently due to engine rate capping logic)

serverJIP.dll : server_srvJIP.so but for windows
