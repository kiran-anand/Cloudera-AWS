S3_DataCopy.sh 
Script to copy data to and from Amazon S3. This script can be used to automate backing up and restore of data present in the instance store (ephemeral) disks in AWS EC2 instances. 

Command: S3_DataCopy.sh <option (backup/restore) FS-list-provided (optional parameter - y/n -> default 'n')>
eg - S3_DataCopy.sh backup y

Prerequisites: The user executing the script should have the following.
1) AWS CLI installed in the local machine executing the script.
2) Setup AWS CLI environment variables in ~/.aws directory - If not include those in the script.
3) The user executing should be able to run AWS CLI executable "aws".
4) Write access to the Present Working Directory ($PWD) as well as S3 bucket.
5) Choose one of the options for executing the script as listed below.
  5a) If FS-list-provided is set to 'y', file fs_list.txt (predefined list of filesystems) is present in $PWD. Use of this option is preferred.
  5b) If FS-list-provided is not set to 'y', the file fs_list.txt will be generated by the script.
Dependency: fs_list.txt file if the argument FS-list-provided is set to 'y' -> option 5a is chosen.

If option 5a is chosen, all filesystems to be backed-up/restored should be provided in fs_list.txt -
Each filesystem within fs_list.txt should be separated by newline character
#cat fs_list.txt
/data01
/data02
/data03

If option 5b is chosen, the fs_list.txt will be generated by the script -
All disks within the instance except the one used for root mount (/) will be considered as ephemeral

Currently the S3 bucket and directories are provided as variables within the script that can be edited.