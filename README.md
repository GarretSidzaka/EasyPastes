# EasyPastes
These are a collection of small shell scripts converted to .sh format for download.  Also the original one-liners are also included in the readme.

CPU Stress
`read -p "Please enter the number of minutes for test >" MINTEST && [[ $MINTEST == ?(-)+([0-9]) ]]; NCPU="$(grep -c ^processor /proc/cpuinfo)";  ((endtime=$(date +%s) + ($MINTEST*60))); NCPU=$((NCPU-1)); for ((i=1; i<=$NCPU; i++)); do while (($(date +%s) < $endtime)); do : ; done & done`

Nukedisk **Caution: Use with care!**
`parted -l | grep "Disk /dev" && echo "Enter disk name like /dev/sdc" && read -r NAMEDISK && echo "WARNING DISK WILL GET NUKED!" && read -p "Press [Enter] key to start NUKE or cntl-c to quit!" && SEEKAMOUNT=$(blockdev --getsize $NAMEDISK) && DISKSPOT=$(expr $SEEKAMOUNT - 4096) && echo "Killing the front of the drive" && dd if=/dev/urandom of=$NAMEDISK bs=512 count=4096 && echo "Now the back" && dd if=/dev/urandom of=$NAMEDISK bs=512 count=4096 seek=$DISKSPOT && echo "The drive is now a wreck, mission accomplished!" && read -p "Press Enter to create a label for the device, or ctrl-c to quit" && parted $NAMEDISK mklabel msdos && read -p "Label created, press Enter to quit" && exit`

Finalorder
`OURHOST=$(hostname) && OURMEM="$(cat /proc/meminfo | grep Mem)" && OURDISK="$(fdisk -l | grep sd)" && OURCPU="$(cat /proc/cpuinfo | grep 'model name' | uniq)" && OURVER="$(cat /etc/*-release | head -n 3)" && OURBOARD="$(cat /sys/devices/virtual/dmi/id/board_{vendor,name,version})" && OURBREAK="$(printf '%0.s-' {0..60};)" && OURIPS="$(ip addr show | grep 'inet ' | awk '{print $2}')" && OURRESOLV="$(cat /etc/resolv.conf | grep nameserver | awk '{print $2}')" && clear && printf "\\nMetadata Verification Check for: " && echo "$OURHOST" && printf "\\nThis System's Motherboard:\\n" && echo "$OURBREAK" && echo "$OURBOARD" && printf "\\nThis System's Memory:\\n" && echo "$OURBREAK" && echo "$OURMEM" && printf "\\nThis System's Disks:\\n" && echo "$OURBREAK" && echo "$OURDISK" && printf "\\nThis System's Processor:\\n" && echo "$OURBREAK" && echo "$OURCPU" && printf "\\nThis System's Network Settings:\\n" && echo "$OURBREAK" && printf "\\nIP Addresses:\\n" && echo "$OURIPS" && printf "\\nResolvers:\\n" && echo "$OURRESOLV" && printf "\\nThis System's Linux:\\n" && echo "$OURBREAK" && echo "$OURVER"`


