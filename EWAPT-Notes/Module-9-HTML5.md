![image-20210219204045539](images/image-20210219204045539.png)



---



[TOC]



### CORS [Cross Origin Resource Sharing]



* ![image-20210219204236558](images/image-20210219204236558.png)
* The **Same Origin Policy [SOP]**  is a policy implemented by browsers to 
  * prevent interactions between resources of different origin.
* CSS Stylesheets, images and scripts are loaded without checking the SOP
* The Same Origin Policy is consulted when **cross-site HTTP requests**  are initiated by client-side scripts
* Example
  * Browsers check the SOP when performing AJAX requests.
* ![image-20210219204549824](images/image-20210219204549824.png)
* Although SOP is necessary for many reasons, it becomes very restrictive when two entities hosted on different domains **need to establish** some kind of interaction.
* Two different origins cannot interact one with each other even if they have mutual trust.



* ![image-20210219204813745](images/image-20210219204813745.png)
* Within the Flash security model, a method to bypass the same origin policy has already been developed.
* ![image-20210219204846242](images/image-20210219204846242.png)
* ![image-20210219204924221](images/image-20210219204924221.png)





* ![image-20210219205001692](images/image-20210219205001692.png)
* **CORS** is a mechanism that enables **client-side cross-origin requests**.
* Document describes how the browser and the web server must cimmunicate one with each other to *bypass* the **SOP**
* It als explains which HTTP headers must be used to do so.
  * These HTTP headers are not part of the HTTP/1.1 standard.
  * They are called **Control Access Headers** 
* ![image-20210219205333659](images/image-20210219205333659.png)
* ![image-20210219205424003](images/image-20210219205424003.png)
* According to [http://caniuse.com/] , currently, CORS is supported by all browsers except Opera Mini.







![image-20210219205606000](images/image-20210219205606000.png)



* JavaScript Code to perform a cross-origin AJAX request

  * ```
    function crossOriginXHRGet(){
    var xmlhttpr = new XMLHttpRequest();
    var url = 'http://originb.ori/page.html'; <- 
    	xmlhttpr.open('GET', url, true);
    	xmlhttpr.onreadystatechange = handler;
    	xmlhttpr.send(body);
    	}
    ```

  * Suppose **crossOriginXHRGet** function defined into the page at the URL **http://origina.ori/index.html**

* The Ajax request is cross-origin because the requester origin is different from the target origin:

  * Requester origin: http://origin**a**.ori
  * Target origin: http://origin**b**.ori

* Abiding by SOP, the function handler cannot use JavaScript to read the page contents at

  *  http://origin**b**.ori/page.html.

* This kind of access to a resource is possible only if the HTTP CORS headers are used and set properly.

* First, we need to know the different types of cross-origin requests that a browser can send.

* Depending upon the request type, the exchanged headers will vary. They are :

  * Simple Rrequests
  * Preflight Requests
  * Requests with credentials

* ![image-20210219210306425](images/image-20210219210306425.png)

* ![image-20210219210347215](images/image-20210219210347215.png)

  * ![image-20210219210428597](images/image-20210219210428597.png)
  * ![image-20210219210458775](images/image-20210219210458775.png)
  * ![image-20210219210517414](images/image-20210219210517414.png)
  * ![image-20210219210543626](images/image-20210219210543626.png)
  * ![image-20210219210613450](images/image-20210219210613450.png)
  * ![image-20210219210715221](images/image-20210219210715221.png)
  * ![image-20210219210734722](images/image-20210219210734722.png)
  * ![image-20210220073947029](images/image-20210220073947029.png)
  * ![image-20210220074041575](images/image-20210220074041575.png)
  * ![image-20210220074155978](images/image-20210220074155978.png)
  * ![image-20210220074235839](images/image-20210220074235839.png)
  
* ![image-20210220074421884](images/image-20210220074421884.png)

* ![image-20210220074731841](images/image-20210220074731841.png)







* ![image-20210220074932255](images/image-20210220074932255.png)

* Access control headers dictate how the browser has to treat cross origin requests.

* Headers :

  * Access-Control-Allow Origin
  * Access-Control-Allow-Credentials
  * Access-Control-Allow-Headers
  * Access-Control-Allow-Methods
  * Access-Control-Max-Age
  * Access-Control-Expose-Headers
  * Origin
  * Access-Control-Request-Method
  * Access-Control-Request-Header

* ### 1. Header => Access-Control-Allow-Origin

  * **Access-Control-Allow-Origin** is the most important HTTP response header

  * It's set by target origin to allow access from a specific requester origin

  * Format => 

    * ```
      Access-Control-Allow-Origin: <allowedOrigin>
      ```

  * Example

    * ![image-20210220083446112](images/image-20210220083446112.png)
    * ![image-20210220083515711](images/image-20210220083515711.png)

  * The target origin can specify a **wildcard (*).**

    * This would permit external scripts hosted on any site to access resources from the target origin.

  * Example

    * ![image-20210220083719374](images/image-20210220083719374.png)

  * A typical security issue occurs when an origin containing sensitive documents can be accessed by all origins.

  * This would permit an attacker to steal all information contained in the origin simply by getting the victim to visit a crafted website  under his control.

  

  

  

* ### 2. Header => Access-Control-Allow-Credentials

  * The **ACAO [Access-Control-Allow-Credentials** HTTP response header sent by the target origin to the requester indicates that the actual request can be made with credentials

  * By default -> the requester origin (requester's browser) does not send credentials to the target origin

  * ![image-20210220084234984](images/image-20210220084234984.png)

  * ### Example

    * ![image-20210220084354234](images/image-20210220084354234.png)
    * ![image-20210220084417006](images/image-20210220084417006.png)
    * ![image-20210220084456943](images/image-20210220084456943.png)
    * ![image-20210220084530805](images/image-20210220084530805.png)

  * For security reasons, a target origin cannot specify that  **a resource is both accessible by any other origin and that it accepts credentials**

  * ![image-20210220084657562](images/image-20210220084657562.png)





* ### 3. Header => Access-Control-Allow-Headers

  * The **Access-Control-Allow-Headers** HTTP response header is sent by the target origin to the requester during preflight request.
  * It indicates which non-standard HTTP headers can be sent in the actual request
  * ![image-20210220085929591](images/image-20210220085929591.png)
  * ![image-20210220090032414](images/image-20210220090032414.png)





* ### 4. Header => Access-Control-Max-Age

  * The **Access-Control-Max-Age** HTTP response header is sent by the target origin to the requester during preflight request.
  * It indicates how long the results of a preflight request can be cached.
  * ![image-20210220103612680](images/image-20210220103612680.png)



* ### 5. Header => Access-Control-Expose-Headers

  * The **Access-Control-Expose-Headers**  HTTP response header sent by the target origin to the requester indicates which headers can be accessed by the browser
  * ![image-20210220103823313](images/image-20210220103823313.png)





* ### 6. Header => Origin

  * A cross-origin request includes an extra HTTP header named **Origin**
  * This header is always sent and contains the origin (protocol, domain name, and port) of the request
  * Although it is always sent, it is useless for the authorization protocol.





* ### 7. Header => Access-Control-Request-Method

  * The **Access-Control-Request-Method** HTTP request header is sent by the requester origin during preflight requests.
  * It is sent within the **OPTIONS**  request and specifies what method the requester is going to use during the actual request.
  * ![image-20210220105800718](images/image-20210220105800718.png)
  * The browser will analyze the  **Access-Control-Allow-Methods** HTTP response header to check whether the method is considered safe or not.





* ### 8. Header => Access-Control-Request-Headers

  * The **Access-Control-Request-Headers** HTTP request header is sent by the requester origin during preflight requests.
  * It is sent with **OPTIONS** request and specifies which non-standard headers the requester is going to use during the actual request
  * ![image-20210220110055824](images/image-20210220110055824.png)
  * ![image-20210220110112236](images/image-20210220110112236.png)





---



### Cross Windows Messaging





> HTML5 allows *iframes, frames, popups and the current window* to communicate one with each other regardless of the same origin policy, by using  a mechanism as **Cross Window Messaging**



> So, Cross Window Messaging =>  realted to => **iframes,frames,popups and current window** => to communicate with each other => with keep in mind about *SOP*



> When using this feature, two windows that have some kind of **relationship** can exchange messages.





* ### Relationship between Windows

  * Typical **relationships** between two windows are:
    * A main window including an iframe
    * A main window including some HTML code that generates a popup
  * A window or a tab in our browser cannot interact with other windows unless they have a relationship.

* ### Sending Messages

  * A window can send messages to another window by using the **postMessage** API call
  * The sender window **(hosted at http://domain1.com)**  will run some code similar to the following.
    * ![image-20210220111018150](images/image-20210220111018150.png)

* ### Receiving Messages

  * Analogously, a window is allowed to receive messages from another window if a handler, related to the message event, has been installed.
  * ![image-20210220111212611](images/image-20210220111212611.png)

* ### Security Issues

  * Security Issues occurs when the receiver window does not check the origin of the sender when receiving a message

  * With this poor configuration,  the receiver window could interact with any sender regardless of whether it is trusted or not.

  * ![image-20210220111358598](images/image-20210220111358598.png)

  * ![image-20210220111425472](images/image-20210220111425472.png)

  * ![image-20210220111511857](images/image-20210220111511857.png)

    

    

    

    

    

  * ### Cross Domain XSS

    * ![image-20210220111720906](images/image-20210220111720906.png)









----



### Web Storage



> HTML5 allows websites to **store data locally** in the browser.

> This is done by accessing  the **localStorage**  and the **sessionStorage**  objects via JavaScript.



> The concept of persistent data in the browser environment could mistakenly lead us to associate this type of storage with cookies.



![image-20210220112100170](images/image-20210220112100170.png)





![image-20210220112232002](images/image-20210220112232002.png)





* ### Local Storage

  * Local storage is a **persistent** JavaScript object used as local repository.
  * ![image-20210220112353028](images/image-20210220112353028.png)
  * ![image-20210220112509133](images/image-20210220112509133.png)





* ### Session Storage

  * ![image-20210220112631785](images/image-20210220112631785.png)
  * ![image-20210220112717752](images/image-20210220112717752.png)
  * ![image-20210220112801014](images/image-20210220112801014.png)







![image-20210220112852412](images/image-20210220112852412.png)







* Local storage can be accessed via JavaScript through the **localStorage object.**

* Web developers do not need to manage this storage directly, but they can add and remove elements using the web storage API.

* ### Adding an Item

  * We can **add** an item to **localStorage**  by using the  **setItem** API call by providing a key and a value for inserted element
  * ![image-20210220113043441](images/image-20210220113043441.png)
  * So ,  setItem = Add Item = with key and value pair

* ### Retrieving an Item

  * To **retrieve** an item from the **localStorage**,  we can use thee **getItem** API call => specifying the key of the element we want to retrieve
  * ![image-20210220113414825](images/image-20210220113414825.png)

* ### Removing an Item

  * To **remove** an item from the **localStorage**, we can use **removeItem** API Call
  * ![image-20210220113523716](images/image-20210220113523716.png)

* ### Removing all Items

  * To **clear** the **localStorage** content,  we can use **clear** API Call. => All items in the **localStorage** will be deleted
  * ![image-20210220113639652](images/image-20210220113639652.png)











![image-20210220113725967](images/image-20210220113725967.png)





* Session storage can be accessed via JavaScript through the  **sessionStorage** object
* Web Developers can manage the **sessionStorage** via the same API interface of the **localStorage**:
  * setItem
  * getItem
  * removeItem
  * clear







* ### Security Issues

  * ![image-20210220114011196](images/image-20210220114011196.png)

  * ![image-20210220114029955](images/image-20210220114029955.png)

    

    

    

  * ![image-20210220114110459](images/image-20210220114110459.png)

  * ![image-20210220114133336](images/image-20210220114133336.png)





---



### Web Sockets





![image-20210220114341787](images/image-20210220114341787.png)





> During the evolution of the web, the need for low latency and high throughput applications such as social network chats emerged.



> In past, these applications were relying on polling done by means of standard HTTP Requests



> This method had a huge overhead on the network and added latency issues.



> To overcome these limitations, **W3C** group make new protocol to meet real-time web application needs => **WebSockets**



![image-20210220180018169](images/image-20210220180018169.png)





* ### WebSocket Benefits

  * ![image-20210220180137557](images/image-20210220180137557.png)





* ### WebSocket API

  * ![image-20210220180332709](images/image-20210220180332709.png)
  * ![image-20210220180424075](images/image-20210220180424075.png)







* ![image-20210220180447362](images/image-20210220180447362.png)
* **WebSockets** do not create security pitfalls per se, as much as HTTP does not pose security issues
* What they carry from a domain to another one is a completely different thing.
* If developers **do not sanitize**  the content of the message exchanged  via **WebSockets**, could permit be used to perform a variety of attack such as **XSS, localStorage stealing, SQLi and more depending on the specific web application**









---



### Sandboxed Frames



> ![image-20210220180813850](images/image-20210220180813850.png)
>
> 
>
>
> Security issues which fixed with HTML5 





* ### 1. Redirection

  * A classic issue occurs when a website hosts 3rd-party contents through **iframes**

  * Despite **SOP** , the *location* property  of each document is always *writable* (location is an exception to the SOP)

    * this could be dangerous for the website which includes an iframe
    * ![image-20210220181126124](images/image-20210220181126124.png)

  * ### Examples

    * ![image-20210220181207015](images/image-20210220181207015.png)
    * ![image-20210220181257335](images/image-20210220181257335.png)
    * ![image-20210220181337997](images/image-20210220181337997.png)

  * ### Prevention

    * Install  a special event (**onbeforeunload**) in the main document hosting the iframes
    * The event  will be triggered when the attacker's iframe tries to change the parent document location property
    * By using this technique, the main document can only inform the  visitor that the page is being changed.
      * ![image-20210220181633481](images/image-20210220181633481.png)
    * This is not a real solution
      * however, it is a way to inform the visitor that someone is trying to redirect him.
      * It actually does not even block the redirection







* ### 2. Accessing the Parent Document from the Iframe

  * If the **main document** and the **iframe** are *located* on the **same origin**, they can access each other
  * The **iframe** document could *change* the contents of the **main document**, using the same technique used by the  *defacement-via-XSS* attack family
  * ![image-20210220182014619](images/image-20210220182014619.png)
  * This could be dangerous in the presence of multiple vulnerabilities.
  * For example, in a scenario where:
    * the attacker succeeds in exploiting a persistent XSS in the **vulnerable.html** page
    * the **vulnerable.html** page is included through an iframe into  the **index.html** page
  * ![image-20210220182152143](images/image-20210220182152143.png)
  * ![image-20210220182232475](images/image-20210220182232475.png)
  * ![image-20210220182258866](images/image-20210220182258866.png)
  * Before  HTML5, the main document was not able to prevent **iframe** from running *JavaScript*









![image-20210220182418252](images/image-20210220182418252.png)





> The **sandbox** attribute  is a new attribute of the element *iframe*



> It has been introduced by the HTML5  specs and it enables ->  **restrictions on iframe contents.**



![image-20210220182538729](images/image-20210220182538729.png)





![image-20210220182615613](images/image-20210220182615613.png)







---

