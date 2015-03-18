## **Contribution for Webcast**  ##
 - Initial a discussion on b2g mail list channel about merging webcast to FFOS.
	 - What's mozilla's opinion about webcast sharing (tap to sharing using NFC). 
	 - There is a slides and some demo videos to explain web cast. 
		 - put the link here.
		 - Related developers effort
			 - UX 
				 - Juwei 
			 - Gaia (Reviewer)
				 - Tim
				 - gmarty 
			 - Gecko(Technical discussion)
				 - Henry
				 - Yoshi
				 - Dimi 
				 - Vincent

 - Current status for content sharing between difference devices.
	 - We can use mozActivity to share content using
		 - Bluetooth API, certificated app only 
		 - MozNFCPeer.sendFile(), NFC API on top of bluetooth API, certificated app only. 
		 - via E-mail
	 - Can we do more, and provide better user experiences.
		 - WiFi Direct APIs, certificated app only
			 - can be used to established layer 2 WiFi connection, and get the ip address between two or more devices. 
			 - Need to use mozTCPSocket APIs in web content to sharing. 
				 - https://developer.mozilla.org/en-US/docs/Web/API/TCPSocket
			 - Or we can use http server. 
				 - http://showcase.kddi.com/csc/works/view/25
			 - How about using webRTC
				 - https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel
			 - or XMLHttpRequest
				 - https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
				 - 
 - Create meta bugs and break them down to individual bugs to contribute web cast done by KDDI. 
	 - Bug 1143996. 
	 
 - Discussion items:
	 - What's mozilla's opinion about webcast sharing?
	 - UX decision for sharing content between devices. 
		 - Use mozActivity, API can be certificated as they are now. 
		 - Expose WiFi Direct, Bluetooth or NFC APIs to privileged APP, and app developers need to use these APIs to sharing content. 
	 - Can we put the web server on FFOS framework?
		 - In the form of library or 
		 - Running in the system by default
			 - What if url is hacked? 
			 - Can others people access to web server ? 
			 - Maybe use mac filter?
			 - Why not use https?
	 - use mozActivity or privileged APIs for content sharing ? 
	 - P2P discussion - http://goo.gl/vZQM0X
 - Reference bugs
	 - Bug 1082453 - B2G NFC: discuss MozNFCPeer.sendFile
	 - Bug 1042851 - (b2g-nfc-privilege) (meta) [NFC] Make NFC APIs available to privileged webapps
		 - https://bugzilla.mozilla.org/show_bug.cgi?id=1042851#c8

 ## **Open web hardware** ##
 - GPIO APIs for open web hardware project
	 - https://bugzilla.mozilla.org/show_bug.cgi?id=1087955
 - The open hardware project is funded by mozilla Japan.  
	 - http://en.mozillafactory.org/about
 - RaspberryPi on Firefox OS
	 - Bug 1001404 - (fxos-rpi) [meta] FxOS on RaspberryPi (RPi)
 - They have plan to mass production the CHIRIMEN in Kickstarter.
 - Discussion group in Facebook 	 
	 - https://www.facebook.com/groups/305208196333685/?pnref=lhc
 - Arm is provided a Embedded OS for IOT using web technology.
	 -  https://mbed.org/ 
 - low level WebAPI discussion 
	 - https://groups.google.com/forum/#!topic/mozilla.dev.webapi/t4Xh2EH0rIo

## Secure Element ##

 - We have secure element APIs landed in 2.2. These APIs are preference off for certificated app only at the moment. After access control enforcer bug (Bug 884594)  is landed, we would like to expose these APIs to privileged app. Then what? What the use cases or user story using secure element APIs?
	 -  Payment 
	 -  Store user credential information in secure element. 
	 -  ...
 - The problem is application developers should know more technical details about the specification and allow them to do the payment or read/write to secure element. Can we eliminate the gap to make application developers's life easier? 
 - So the questions are 
	 - More use cases others then controlled by operators?
	 - Simplify the technical gaps to allow developers to use secure element. 

