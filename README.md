# rsync-for-android

Transfer files over USB at the speed of lightning with rsync (needs Termux).



## Overview

Transfer files to and from your Android device much faster than over MTP (the default) or even ADB pull/push using rsync.

## Why?

Quite simply put, `libmtp` and `adb` provide terrible performance. Windows' implementation of MTP is better but it still keeps overwriting files unnecessarily and can't detect changes.

We need a better solution. Luckily there's already `rsync` which gives us delta-compression. Only problem is that it's a client-server program, needing an `rsync` server running on the phone.

For copying a large number of files like a Music library or Photo gallery, `rsync` provides massive performance gains especially when only a few files have changed.

## Requirements

1. Termux app installed and initialised (run at least once)
2. ADB command in $PATH
3. USB debugging enabled on your phone
4. An rsync client on your PC ([GRsync](http://www.opbyte.it/grsync/) recommended for GUI)

## Usage

1. Run `adb devices` to ensure that your phone shows up in the list. Authorize on the phone if necessary.

2. Run the script with `./start-rsync-android`. This will perform the one-time-setup (if necessary) and forward the port 8873 on your phone to localhost:8873, enabling you to access your phone's rsync server at localhost:8873.

## Example
Backup all your photos to your Backup HDD:

 ```bash
rsync -avPh --info=progress2 rsync://localhost:8873/sdcard/DCIM /media/Backup/Phone/DCIM
 ```
