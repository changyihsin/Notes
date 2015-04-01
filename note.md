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
