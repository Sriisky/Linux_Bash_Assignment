#!/bin/bash
#BASH menu script that has 6 options:
#Option 1 = List files
#Option 2 = Show free disk space
#Option 3 = Show system path
#Option 4 = Display command history
#Option 5 = Backup files
#Option 6 = Exit
#making bash script exe from anywhere
export PATH=$PATH:/home/sara
server_name=$(hostname)
#Option 1
function list_files() {
echo ""
for entry in "$search_dir"/*
do
echo "$entry"
done
echo ""
}
#Option2
function disk_space() {
echo ""
df -h
echo ""
}
#option3
function sys_path() {
echo ""
echo "$PATH"
echo ""
}
#option4
function com_history() {
echo ""
HISTFILE=~/.bash_history
set -o history
history | tail
echo ""
}
#option5
function backup_files() {
echo ""
echo "Please enter a directory to be backed up"
read input
echo $input
echo "Now backing up the files from $input"
cp -R $input BackupFolder/$input
echo"Your files have been successfully backed up"
echo ""
}
function all_checks() {
list_files
disk_space
sys_path
com_history
backup_files
}
# Color Variables
green='\e[32m'
blue='\e[34m'
clear='\e[0m'
# Color Functions
ColorGreen(){
echo -ne $green$1$clear
}
ColorBlue(){
echo -ne $blue$1$clear
}
#menu that gets displayed
menu(){
echo -ne "
*Bash Commands*
$(ColorGreen '1)') List files
$(ColorGreen '2)') Show free disk space
$(ColorGreen '3)') Show system path
$(ColorGreen '4)') Display command history
$(ColorGreen '5)') Backup files
$(ColorGreen '6)') Exit
$(ColorBlue 'Choose an option:') "
read a
case $a in
1) list_files ; menu ;;
2) disk_space ; menu ;;
3) sys_path ; menu ;;
4) com_history ; menu ;;
5) backup_files ; menu ;;
6) exit 0 ;;
*) echo -e $red"Wrong option."$clear; WrongCommand;;
esac
}
# Call the menu function
menu
