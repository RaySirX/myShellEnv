# Manifesto.... 
## - don't be an admin/programmer princess, relying on gui's and tools to do your job
## - visual editors are like flavors of the week, providing marginal productivity improvements over last weeks
## - stick with the bare bones (omg! I can't code cuz VisualCode/eclipse/fav gui editor... is missing)
## - Learn VI as a backup
## - rock the command line
## - same goes for (zsh) shells.  good to know but unnecessary to a basher
#
#install-oh-my-zsh
- WSL - mojibake - https://superuser.com/questions/1108443/utf8-characters-in-windows-10-bash-terminal

- 

# AMD graphics - amdcpu-install

[how to install amdgpu on popos] https://www.reddit.com/r/pop_os/comments/r6ljb8/howto_installing_amdgpupro_on_pop_os/?onetap_auto=true

Problem 1) Pop!_OS not valid install target "Unsupported OS: /etc/os-release ID 'pop' "
The issue as of now is that amdgpu-install doesn't recognize pop as a valid installation candidate. Solution is to add pop as a valid target in the amdgpu-install script.

Solution: Change line 241 to include `| pop` Pop!_OS will then be seen as a valid installation target

which amdgpu-install //will return location of scripts
//using editor of choice, change 241 to include logical 'or' pop
| pop

Problem 3) DPKG error kernel package not supported
```

ERROR (dkms apport): kernel package linux-headers-5.15.5-76051505-generic is not supported Error! Bad return status for module build on kernel: 5.15.5-76051505-generic (amd64) Consult /var/lib/dkms/amdgpu/5.11.32-1337797/build/make.log for more information. dpkg: error processing package amdgpu-dkms (--configure): installed amdgpu-dkms package post-installation script subprocess returned error exit status 10 Errors were encountered while processing: amdgpu-dkms E: Sub-process /usr/bin/dpkg returned an error code (1)

```

Solution: DKMS isn't needed, we're better off using the in kernel module already provided.

amdgpu-install --no-dkms

Problem 4 Can't install amdgpu drivers on Ubuntu 22.04 LTS due to unmet dependency on xorg-video-abi-24
The issue can be fixed by manually editing file /etc/apt/sources.list.d/amdgpu.list (workaround taken from https://askubuntu.com/a/1419033)
Instead of
deb https://repo.radeon.com/amdgpu/22.20/ubuntu focal main
Should be
deb https://repo.radeon.com/amdgpu/22.20/ubuntu jammy main
