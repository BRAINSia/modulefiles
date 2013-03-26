modulefiles
================

Repository for all the Modules 'modulefiles' specific to the SINAPSE lab

Modules is installed in /usr/local/Modules and the modulefiles repository is in /ipldev/sharedopt/modulefiles

To build Modules for OSX:
`CC=/usr/bin/clang; CPP=/usr/bin/clang++; \
./configue --with-module-path=/ipldev/sharedopt/modulefiles \
           --prefix=/ipldev/sharedopt/Modules \
           --exec-prefix=/ipldev/sharedopt/Modules/Darwin_i386 \
           --enable-logging \
           --with-log-dir=/tmp/modules \
           --with-tcl=/ipldev/sharedopt/tools/tcl/8.5.12/... #(directory containing tclConfig.sh)`
`make`
`make install`
            
To set up the correct aliases for Modules:
`ln -s /usr/local/Modules/${VERSION} /usr/local/Modules/default`
# Setup the Module shell-commands:
 (Note: modify these folders to have certain modules loaded automatically for every user )
`cp ./etc/csh.modules /etc/`
`cp ./etc/profile.modules /etc/`

# Set up skeleton files:
If you have no skeleton files:
`cp ./etc/skel /etc/skel`
`rm /etc/skel/*.in` (Note: also remove and CSV files/directories)
Else: (you have the minimum set .cshrc, .login, .kshenv, .profile)
`env HOME=/etc/skel /usr/local/Modules/default/bin/add.modules`
Inspect and remove old file (/etc/skel/*.old)

# Modify the users 'dot' files
For each user:
`/usr/local/Modules/default/bin/add.modules`
For more information, see the Modules INSTALL file...

INSTALLING PACKAGES
===================
When installing a non-CMake project "foo" with version "0.0.1":
`cd /ipldev/sharedopt/pkg/foo/0.0.1`
`module load modules; mkroot -m`  # Creates bin/, sbin/, man/, lib/, etc.
`cd /ipldev/sharedopt/src/foo/0.0.1`
`./configure --prefix=/ipldev/sharedopt/pkg/foo/0.0.1`
`make`
`make install`
`cd /ipldev/sharedopt/pkg/foo/0.0.1`
`mkroot -c` # Deletes empty directories from 'mkroot -m'


