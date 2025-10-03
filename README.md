# TinyTitan-redux
An attempt to get tinytitan working in a nicer way

This repo contains submodules pointing to other parts of the TinyTitan system, as well as tooling used to get the system running.
 
## Current Functionality
- None

## Target Functionality
### Phase One
- Able to compile everything, and run on a pi 1 running legacy pios (old enough to work with TinySetup upstream)

### Phase Two
- Able to compile everything, and run on a pi 1(?) running current pios (trixie)

### General wishlist
- For all pis except 1: Deployment via imaging.
- Access to an "outside" network via vlans.
- Maybe netboot on pi3+s, or at least image over the network on older ones.
- RAUC?

## Notes
### Operating Environment - Upstream
The below is a description of the result of the installation instructions.

#### All nodes
* Rasbian ?ver?
* Packages added from main repos:
   - vim
   - mpich2
   - xboxdrv
   - libglew-dev
   - sshpass
   - libav-tools
* Hostname is 'piX' where 'X' is the node number. (hosts and hostname, as well as pubkey comments)
* Network is statically configured with 192.168.3.(100+X)/24, gw .1
* DNS is not configured.

#### After pi_post_setup.sh
* Hostsfile templated with pi1..piN hostnames at addresses from above on pi1 only
* ssh pubkeys (if they existed) from pi1..N copied into local authorized keys, then distributed to all nodes.
* GPU memory set to 128m on pi1 only.
* system reboots

#### manual tasks
Create ~pi/pi_mpihostsfile
Install a "workload" (probably compiled externally?)
Get some kind of autostart
(SPH contains controller configs that can work with a script in the TinySetup repo to start when the guide button is pressed; this relies on xboxdrv being setup by the rc.local in this repo, but this is not installed by said scripts)