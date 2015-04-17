
 - First, flash Nexus 5 binaries for Android 5.1 (LMY47D) as the base image
	 - a. download 5.1 (LMY47D) image for "Nexus 5" from https://developers.google.com/android/nexus/images
	 - b. follow [3] to unlock your N5
	 - c. You can see your Nexus 5 at "FASTBOOT MODE", then use flash-all.sh located in hammerhead-lrx47d folder uncompressed at step 1-a to install Android 5.1.
        $ ./flash-all.sh

 - Follow MDN [1] to build your N5 local build. Please be noted that when you run "./config.sh", you need to use "nexus-5-l" as the device name. After building FxOS successfully, you need to run flash.sh to your N5 at fastboot mode.

 - If you has flashed your N5 to Firefox OS v2.2, you can download Gaia+Gecko from [2] when you want to get a updated Firefox OS v2.2.

 - [1] MDN Build steps: https://developer.mozilla.org/en-US/Firefox_OS/Building_and_installing_Firefox_O/Firefox_OS_build_process_summary
 - [2] Mozilla FTP for the lastest v2.2 Gaia+Gecko: http://ftp.mozilla.org/pub/mozilla.org/b2g/nightly/latest-mozilla-b2g37_v2_2-nexus-5-l-eng/
 - [3] How to unlock your N5:
	 - Go to "Settings"->"About phone", then tap "Build number" 6 times to enter developer mode
	 - Go to "Settings"->"Developer options", enable "USB debugging"
	 - Unlock OEM:
		 - $ adb reboot bootloader
		 - $ fastboot oem unlock
