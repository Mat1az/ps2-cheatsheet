# PS2 HDD Internal - POPSTARTER
Guide to Setting Up POPSTARTER on PS2 with an Internal HDD (PS2 FAT or PS2 7000x IDE Hardmod)

## Directory Structure
 - **__.POPS**:
   - .VCD Files
   > SLUS.XX.Example Game.VCD
 - **__common/POPS**: 
   - VCD Folders
   - POPS.ELF
   - IOPRP252.IMG
   - CHEATS.TXT
 - **+OPL/APPS**:
   - .ELF Files
   > SLUS.XX.Example Game.ELF
 - **+OPL**:
   - conf_apps.cfg

## config_apps.cfg
 > Example Game=pfs0:/APPS/SLUS.XX.Example Game.ELF

## Some Bash Scripts
 > Generate **empty folders** & **.ELF files** for all .VCD files in the current directory (you need popstarter.elf)
 ```bash
 #!/bin/bash

 for file in *.vcd; do
   base_name="${file%.*}"
   elf_file="$base_name.elf"
   dir_name="$base_name"
   cp popstarter.elf "$elf_file"
   mkdir "$dir_name"
 done
 ```
 > Generate **config_apps.cfg** from all .VCD files in the current directory
 ```bash
 #!/bin/bash

 apps_file="conf_apps.cfg"

 # Remove the list file if it already exists
 rm -f "$apps_file"

 for file in *.ELF; do
   base_name="${file}"
   game_name=${base_name%.*}
   game_name=${game_name##*.}
   echo "$game_name=pfs0:/APPS/$base_name" >> "$apps_file"
 done
 ```
