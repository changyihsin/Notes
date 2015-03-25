## NFC Workshop 2015/03/16 ~03/20 ##
## **Contribution for Webcast**  ##
 - Webcast is a function implemented in Fx0. KDDI would like to contribute webcast to mozilla code base. 
	 - The architecture of webcast is uploaded in bug 1143996 https://bug1143996.bugzilla.mozilla.org/attachment.cgi?id=8579793
	 
 - Webcast provides the other way to share contents, current status for content sharing between difference devices in FFOS are
	 - Use mozActivity to share content via
		 - Bluetooth API, for certificated app only 
		 - MozNFCPeer.sendFile(), for certificated app only. It's on top of Bluetooth API. 
		 - via application, like E-mail
	 - We should provide better user experiences in sharing, especially for large files or content
		 - Some ideas  
			 - WiFi Direct APIs, for certificated app only
				 - WiFi or WiFi direct APIs can be used to establish layer 2 connection between devices. 
					 - Need to use mozTCPSocket APIs in web content to sharing. 
					 - Or can we use http server ? We can use WebSocket and XMLHttpRequest APIs if http server is available.  
						 - http://showcase.kddi.com/csc/works/view/25
				 - How about using webRTC
					 - https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel
 
 - Questions and action items
	- What's mozilla's opinion about webcast sharing (tap to sharing using NFC). Do we want to merge this function to our code base?
	- Do we like to put the web server into FFOS framework?
		 - In the form of library or 
		 - Running in the system by default
			 - Any security concert?
			 - What if URL is hacked? 
			 - Can others device access to web server? 
			 - Can we limit the access by ip/mac filter?
			 - Why don't we use https?
	 - Ux decision for sharing content between devices? 
		 - We can use mozActivity, and implement the sharing in certificated app. Advantage is that related APIs, such as Bluetooth, WiFi direct and NFC can be certificated as they are now. 
		 - Expose WiFi Direct, Bluetooth or NFC APIs to privileged, and application developers need to use these APIs to share content. 
			 - Reference bug - https://bugzilla.mozilla.org/show_bug.cgi?id=1042851#c8
			 - P2P discussion - http://goo.gl/vZQM0X
			 - Bug 1082453 - B2G NFC: discuss MozNFCPeer.sendFile
			 - Bug 1042851 - (b2g-nfc-privilege) (meta) [NFC] Make NFC APIs 

	- Related developers effort
			 - UX 
			 - Gaia (Reviewer)
			 - Gecko(Technical discussion)
				 - Henry
				 - Yoshi
				 - Dimi 
				 - Vincent

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
 - David Huseby is asking about using secure element as key store, not sure if it is possible to use SD secure men 
 - https://w3c.github.io/webappsec/specs/credentialmanagement/
 - Firefox account in NFC 
 - SD secure element 
 - KDDI AU payment card
	 - Web money 
 - Need hardware devices for test purpose
	 - embedded secure element 
	 - SD secure element 



## Web NFC in W3C ##

 - W3C spec provided by intel
	 - http://w3c.github.io/web-nfc/index.html
 - Paul will help to driver standardize W3C. 

