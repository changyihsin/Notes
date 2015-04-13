 - packaged/hosted application
	 - packaged app - A packaged app is an Open Web App that has all of its resources (HTML, CSS, JavaScript, app manifest, and so on) contained in a zip file, instead of having its resources on a Web server. 
		 - easy to review
		 - easy to distribute without investing in a server infrastructure
	 - hosted application - A hosted app is an Open Web App that has all of its resources (HTML, CSS, JavaScript, app manifest and so on) stored on a Web server
 - Same origin 
	 - These are different origins
		 - http://example.com
		 - http://example.com:8080 (different port)   
		 - https://example.com (different protocol)
		 - http://www.example.com
		 - http://myapp.example.com (subdomain)
	 - These are same origins 
		 - http://Example.com:80
		 - http://example.com
 - Why?
	 - If the app manifest were not hosted at the same origin as the app itself, there would be nothing to prevent third parties from making apps directly out of content hosted at your origin
	 - third parties could create an app manifest using your branding that would trick users into installing an app that was a facade for stealing passwords or other improper behavior
	 - The origin restriction is on content (HTML pages) only. Images and other embedded resources can be located elsewhere (for example, on a content delivery network), except for the app's icon, which must be served from the app's origin.
 - Web App Sandbox
	 - Each app runs in as a separate sandbox
		 - This means that if the user has two apps installed, App A and App B, these apps will have a completely different set of cookies, different local data, and different permissions. This even applies if both of these apps open an iframe that points to the same origin. i.e. if both App A and App B open an iframe pointing to "http://www.mozilla.org", they will both render the website, however the website will be fetched and rendered with different cookies in the two apps. A result of this is that if the user logs in to, for example, Facebook while using App A, this in no way affects App B's ability to interact with the user's account on Facebook. The login cookie that Facebook sets when the user logs in using App A is only available in App A. If App B opens an iframe to Facebook, the cookie wouldn't be there and so when App B opens Facebook, it receives the Facebook login page rather than the user's account.
 - Apps can't open each other 
	 - This means that apps can't open other apps by using iframes. If App A creates an iframe with the src set to the URL of App B, this won't actually open App B in the iframe. It will simply open the website located at that URL. It will not use any of App B's cookies and so it will behave no differently than if App B wasn't installed on the user's device.
 - Sandboxed Permissions
	 - In the same way that web site data is sandboxed per app, so is permission data. If App A loads a page from http://maps.google.com and that page requests to use geolocation and the user says "yes, and remember this decision for all times", this only means that http://maps.google.com has access to geolocation within App A. If App B then opens http://maps.google.com, that page won't have access to geolocation unless the user grants that permission again.
 - Browser API Sandbox
	 - To additionally secure applications that open a large set of URLs, such as browsers, we have added a browserContent flag. The browserContent flag allows each app to have not one, but two sandboxes: one for the app itself, and one for any "web content" that it opens.For example:
Say that the MyBrowser app is loaded from the https://mybrowser.com domain. This is the domain the scripts and resources are loaded within. The scripts and resources belong to this domain. Now, if a page in this app creates an "iframe mozbrowser", a different sandbox is created and used for this "iframe", which is different from the sandbox used by the app. So for example if this "iframe" is navigated to https://mybrowser.com, it will result in different cookies being used inside the "iframe mozbrowser". Likewise, the contents inside the "iframe mozbrowser" will see different IndexedDB and localStorage databases from the ones opened by the app.


Web App Types 
<table>
<thead>
  <tr>
   <th scope="col">Type</th>
   <th scope="col">Delivery</th>
   <th scope="col">Permission Model</th>
   <th scope="col">Installation</th>
   <th scope="col">Updates</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Web</td>
   <td>Hosted or Packaged</td>
   <td>Less sensitive permissions, which are not dangerous to expose to unvalidated web content.</td>
   <td>Installed from anywhere</td>
   <td>Can be updated transparently to user or explicitly via a marketplace, depending on where the app was installed from, and the delivery mechanism.</td>
  </tr>
  <tr>
   <td>Privileged</td>
   <td>Packaged &amp; Signed</td>
   <td>Privileged APIs requiring validation and authentication of the app.</td>
   <td>Installed from a trusted marketplace</td>
   <td>Updated via a trusted marketplace, user prompted to approve download and installation of updates.</td>
  </tr>
  <tr>
   <td>Internal</td>
   <td>Packaged</td>
   <td>Powerful and dangerous APIs not available to third-party apps.</td>
   <td>Pre-installed on the device</td>
   <td>Updated only as part of system level updates.</td>
  </tr>
 </tbody>
</table>

 - Package format
	 - be a ZIP fIle with application.manifest at the root of container. 
 - Content Security Policy
	 - a mechanism web applications can use to mitigate a broad class of content injection vulnerabilities, such as cross-site scripting (XSS). Content Security Policy is a declarative policy that lets the authors (or server administrators) of a web application inform the client about the sources from which the application expects to load resources. It's defined in app manifest. 

 - FFOS App Security overview
 - Trusted and Untrusted Apps
<table>
 <thead>
  <tr>
   <th style="width: 82px;">
    <p>Type</p>
   </th>
   <th style="width: 102px;">
    <p>Trust Level</p>
   </th>
   <th style="width: 447px;">
    <p>Description</p>
   </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td style="width: 82px;">
    <p>Certified</p>
   </td>
   <td style="width: 102px;">
    <p>Highly Trusted</p>
   </td>
   <td style="width: 447px;">
    <p>System apps that have been approved by the Operator or OEM (due to risk of device corruption or risk to critical functionality). System apps and services only; not intended for third-party applications.<br>
     This designation is reserved for just a small number of critical applications. Examples: SMS, Bluetooth, camera, system clock, telephony, and the default dialer (to ensure that emergency services are always accessible).</p>
   </td>
  </tr>
  <tr>
   <td style="width: 82px;">
    <p>Privileged</p>
   </td>
   <td style="width: 102px;">
    <p>Trusted</p>
   </td>
   <td style="width: 447px;">
    <p>Third-party apps that have been reviewed, approved, and digitally signed by an authorized Marketplace.</p>
   </td>
  </tr>
  <tr>
   <td style="width: 82px;">
    <p>Web (everything else)</p>
   </td>
   <td style="width: 102px;">
    <p>Untrusted</p>
   </td>
   <td style="width: 447px;">
    <p>Regular web content. Includes both installed apps (stored on the mobile phone) and hosted apps (stored remotely, with only an app manifest stored on the mobile phone). The manifest for hosted apps can be obtained through a Marketplace.</p>
   </td>
  </tr>
 </tbody>
</table>

 - App Manifest
 - App installation, update, uninstall
 - Service Worker 

 - Runtime and Security Model for Web Applications
	 - It describes how an application is defined through an application manifest, and how it can be installed, updated and packaged. It also specifies how such an application can be put into the background, be put back in the foreground or woken up. Finally, the document describes the security model for such applications. This includes the permission model and the different security rules that would apply.

 - Service Worker and Shared Worker

New security model
==================
 

 - QA
	 - What is sensitive APIs?
	 - Current update/installation/uninstallation mechanism 
	 - Current security model
	 - What are cookie jars for current apps?

 - Goal
	 - Enable exposing "sensitive APIs" to 3rd party developers.
	 - Use the same update and security model for gaia and for 3rd party content. 
	 - Don't require content which uses "senstivie APIs" to be installed. Users should be able to simply browse to it. 
	 - ***Don't have separate cookie jars for separate apps. At least for normal content which doesn't use "sensitive APIs".***  
	 - ***Ensure that content which uses "sensitive APIs" always runs in a separate process. Enforce in the parent process that only these separate processes can trigger "sensitive APIs". I.e. hacking a child process should not permit access to more sensitive APIs.*** 
	 - ***Enable content which uses "sensitive APIs" to have normal http(s) URLs such that they can use OAuth providers like facebook.*** 
	 -  ***Enable content which uses "sensitive APIs" to use service workers.*** 
 - Issues
	 - Signing
		 - Should we allow other forms manual review of each app? Can the marketplace "review a developer" and give the developer access to automatic signing? 
		 - Is there a reason to restrict signed packages to only be hosted on the marketplace? 
		 - Should we enable the marketplace to host signed packages for developers which doesn't want to run a web server?
		 - Decide on exact signature format 
 
	 - Verifying signatures
		 - https://website.com/RSSReader2000/package.pak!//index.html
		 - The part before the "!//" is the URL to the package itself. The part after the "!//" is the resource path inside the package. 
		 - Loading signed content does not require an installation to happen, Simply navigating to a URL.
		 - Before serving any resources from the package to the rest of Gecko, the network layer will first wait for the signatures to be loaded from the package. It will also verify that the resource that is currently being loaded is covered by, and matches, the signature. 
		 - Should we require that the signature-files live at the start of the package. That way we'd always have the signature available before the file contents covered by the signature. 
		 - We should likely cache which resources in the package that we've checked the signature of, so that we don't have to recheck if a resource is loaded multiple times. 
		 - Another thing that needs to be done before any content is served by the network layer is to look in the manifest and populate the nsIPermissionManager database with any permissions enumerated in the manifest. After having checked that the manifest properly matches the signature of course. 

	 - CSP
		 - We need to make sure that it can't load scripts from outside of the signed package
		 - The plan is to use the CSP code to accomplish this
		 - We'll also need to extend it to enable it to enforce loads to happen "from same package", rather than just "from same origin".
		 - Does CSP allow putting limits on where serviceworkers can be loaded from? We need to restrict ServiceWorkers scopes as well as script-urls to be from inside the package. 
		 - We also can't allow signed content to be opened in an "iframe", other than by pages from the same signed package.
		 - However it's also because we want to always open signed content in a separate OS process, and currently gecko does not support out-of-process plain "iframe"s
		 - Hopefully this is a restriction we can eventually relax, for example by allowing pages in a signed package to opt in to being iframe-able. But this will require out-of-process "iframe"s and so will have to wait. 
		 
	 - Process isolation
		 - In order to ensure that only signed content can access the APIs that it has been signed for, we want to always use separate child processes to run such content. 
		 - This means that when a user navigates from an unsigned page to a signed page, that we need to switch which process render the pages. Right now this can only be done by creating a new "iframe mozbrowser"
		 -  We need to figure out how to make navigation work. This will likely require very tricky "iframe mozbrowser" work. We also need to change security checks that currently are done in the parent process. Currently many of them are heavily based on app-ids and installed apps. This may need to be changed.
		 - We need to figure out if changes are needed to the security checks of sensitive APIs.  
	 - Installing/uninstalling and updating
		 - if the package still exists in our http cache when the user revisits a signed page, but the cache headers indicate that the content needs to be updated, we do a normal GET request to see if a new version needs to be downloaded.
		 - If a new version of the package is being sent, we follow the same behavior as when visiting a package for the first time. I.e. we need to reverify signatures as well as update any permissions in the nsIPermissionManager database. 
		 - we want to avoid having to download a whole package if just part of it has changed.
			 - the server to respond to the GET request for an updated package with just a "diff" of what's changed between the previous and current version.
			 - gecko indicate that it supports a new type of content encoding as well as send the etag of the current package file
			 - The server can then look at the etag and if it has (or can generate) a diff between the clients version and the latest version, it can respond with a special content-encoding as well as the package diff. 
			 - Gecko can then use the diff to patch the existing package. 
		 - Decide on details of diff mechanism and format
		 - Decide on how to verify signatures when a diff is downloaded. Also decide if we can verify signatures incrementally or not. 

	 - Service Workers
		 - In order to make service workers work with the package update logic we should couple package update with service worker update.
		 - When the ServiceWorker spec require the browser to check or download update, the ServiceWorker script, we instead update the full signed package.
		 - "automatic" ServiceWorker update check
			 - when the user visit a page which uses the ServiceWorker
			 - when the ServiceWorkerRegistration.update() function is called
		 - How do we enable the newly installing serviceworker to load content from the new package version, even though the previous package version is the one pinned in the cache. 
		 - Does CSP allow putting limits on where serviceworkers can be loaded from? We need to restrict ServiceWorkers scopes as well as script-urls to be from inside the package. 
	 - Origins and cookie jars
		 - we should stop always using different cookie jars for different apps
		 - In particular normal unsigned content should always use the same cookie jar no matter which app it belongs to, I.e. login to facebook 
		 - Signed packages will get their own cookie jars. So a signed package will not share cookies, IndexedDB data, etc with unsigned content from the same domain
		 - Do requests from a signed package to unsigned content use the package's cookie jar? Or the normal cookie jar. I.e. if a signed package does an XHR request to a normal website, does that use the website's cookies
		 - Figure out how to give signed content its own cookie jar. 
			 - One potential solution here is to remove our close tie between cookie jar and appid. 
			 - Another possible solution would be to make the various APIs use the full package path instead of the domain as key. 
		 - What happens if unsigned content does an XHR request to a URL inside a signed package. There doesn't seem to be any security issues involved in allowing that. 
		 - Does this mean that the *cookies* used for signed content is the same as the cookies used for unsigned content? I.e. that only IDB/localStorage/permissions are separate for signed content. That seems to be the case if network requests to normal websites from signed content uses the normal cookie jar. What does document.cookies return? Should we make it return null? 
		 - One potential solution here is to do security checks in the parent only to protect the storage data and permissions of the signed content. And make sure to flag the principals used for documents loaded from signed packages as belonging to the appropriate package. But for anything related to network, just treat signed content like normal content belonging to the normal cookie jar. 
		 - Would it be simpler to make signed content use an entirely separate cookie jar. Including for XHR requests and "iframe"s to content outside of the signed package? That might allow us to use a more generic cookie jar feature.
		 - Figure out exactly what field to use to indicate which signed package a principal belongs to
	 
 - Reference
	 - Security Model - https://developer.mozilla.org/en-US/Firefox_OS/Security/Security_model
	 - Runtime and Security Model for Web Applications - http://www.w3.org/TR/runtime/
	 - 
