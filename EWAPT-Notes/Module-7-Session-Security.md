[TOC]

### Weaknesses of the Session Identifier



* Web application  use login page  and keep track User Session
  * So, that user don't login each time when visit to web application
* HTTP is a stateless protocol, so web application use
  * libraries, cookies to keep track of the user session
* ![image-20210219171441488](images/image-20210219171441488.png)
* ![image-20210219171607775](images/image-20210219171607775.png)
* ![image-20210219171637039](images/image-20210219171637039.png)
* ![image-20210219171656618](images/image-20210219171656618.png)
* ![image-20210219171827594](images/image-20210219171827594.png)





---



### Session Hijacking



* It is the **exploitation of a valid session assigned to a user**

* The attacker can get the victim’s session identifier using a few different methods, though typically an XSS is used

  * ```
    NOTE:
    
    
    If the session identifier is weakly generated, the attacker might be able to brute-force the Session ID
    ```

* ![image-20210219172130025](images/image-20210219172130025.png)

* ![image-20210219172159626](images/image-20210219172159626.png)







* ### Session Hijacking via XSS

  * Session Hijacking is only **one**  of the many possibilities of a successful XSS exploit.

  * ![image-20210219172345646](images/image-20210219172345646.png)

  * ### Example

    * Suppose we got XSS on a target - **elsfooradio.site.**  on  Comment Field
    * ![image-20210219172529675](images/image-20210219172529675.png)
    * ![image-20210219172606861](images/image-20210219172606861.png)

  * ### Preventing Session Hijacking via XSS

    * ![image-20210219172738697](images/image-20210219172738697.png)
    * ![image-20210219172813524](images/image-20210219172813524.png)
    * ![image-20210219172829681](images/image-20210219172829681.png)
    * ![image-20210219172943491](images/image-20210219172943491.png)
    * ![image-20210219173021800](images/image-20210219173021800.png)
    * ![image-20210219173050254](images/image-20210219173050254.png)
    * ![image-20210219173132352](images/image-20210219173132352.png)





* ### Session Hijacking via Packet Sniffing

  * This attack requires the attacker to be able to sniff the HTTP Traffic of the victim
    * unlikely to happen for a remote attacker
    * but it is feasible on a local network if both the attacker and victim are present
  * If HTTP traffic is encrypted through **IPSEC** or **SSL** , the session token will be harder (if not possible) to obtain
  * ![image-20210219173827673](images/image-20210219173827673.png)
  * ![image-20210219173858370](images/image-20210219173858370.png)





* ### Session Hijacking via Access to the Web Server

  * Session data is stored in either the **web server's file system** or **in memory**
  * If an attacker obtains full access to the web server, the attacker can steal the session data of  all users 
    * not *just* the session identifiers
  * ![image-20210219174209292](images/image-20210219174209292.png)
  * ![image-20210219174234391](images/image-20210219174234391.png)
  * ![image-20210219174356174](images/image-20210219174356174.png)
  * ![image-20210219174435899](images/image-20210219174435899.png)







---



### Session Fixation



* Session fixation is a session hijacking attack where,  the attacker **fixates** a **sessionID** and forces the victim to use it (after the user logs in).
* The attack can be divided into two phases:
  1. The attacker obtains a valid sessionID
  2. The attacker forces the victim to use this sessionID to establish a personal session with the web server
* Attacker not interested in **~~stealing the sessionID~~**  , instead attacker creates one of its own and forces the victim to use it
* ![image-20210219175042991](images/image-20210219175042991.png)
* ![image-20210219175103075](images/image-20210219175103075.png)
* ![image-20210219175223200](images/image-20210219175223200.png)
* ![image-20210219175248649](images/image-20210219175248649.png)
* ![image-20210219175320397](images/image-20210219175320397.png)
* ![image-20210219175340250](images/image-20210219175340250.png)





* ![image-20210219175404884](images/image-20210219175404884.png)
* ![image-20210219175433554](images/image-20210219175433554.png)
* ![image-20210219175456369](images/image-20210219175456369.png)
* ![image-20210219175526741](images/image-20210219175526741.png)
* ![image-20210219175629611](images/image-20210219175629611.png)



* ![image-20210219175703931](images/image-20210219175703931.png)
* Best technique to defend application from Session Fixation attacks is to generate a **new** *sessionID* after any authenticated operation is performed.
* Most of the time, however, it is sufficient to destroy and re-generate a new session upon successful login.
* Server-side scripting languages provide different libraries and built-in functions to manage sessions.
* ![image-20210219175841716](images/image-20210219175841716.png)
* ![image-20210219175937738](images/image-20210219175937738.png)
* ![image-20210219182028609](images/image-20210219182028609.png)
* ![image-20210219182108914](images/image-20210219182108914.png)







---





### Cross Site Request Forgeries [CSRF]





* CSRF exploits  a feature of internet browsing, instead of a specific vulnerability

* CSRF  is a vulnerability where a third-party web application is able to perform an action on the user's behalf

* It is based on the fact that web applications can send requests to other web applications, without showing the response.

* ### Example

  * ![image-20210219182545222](images/image-20210219182545222.png)
  * ![image-20210219182626607](images/image-20210219182626607.png)
  * ![image-20210219182706575](images/image-20210219182706575.png)
  * ![image-20210219182729752](images/image-20210219182729752.png)
  * ![image-20210219182745915](images/image-20210219182745915.png)





* ![image-20210219182811587](images/image-20210219182811587.png)
* All requests to a web application that do not implement an Anti-CSRF mechanism are automatically vulnerable.
* When a web application stores session information in cookies, these cookies are sent with every request to that web application 
  * (same-origin policy applies).
* This may sound odd, but storing session tokens in cookies enables CSRF exploitability 
  * (while, of course, storing session tokens into URLs enable other kind of exploits).
* **Tokens** & **Captchas** are the most commonly used *protection* mechanism





* ![image-20210219183005983](images/image-20210219183005983.png)



* In 2005, we had to consider using Joomla as a CMS for Hacker's Center and retiring our old, hand-coded ASP-based CMS
* The first thing we realized when we took it for a drive was the presence of multiple CSRF vulnerabilities.
* The worst of them allowed us to have a super administrator, with an open session on his Joomla backend, uploading arbitrary files, post articles or even deface his own website.
* If only we could manage to force him into visiting a web page  containing the exploit payload...
* ![image-20210219183223654](images/image-20210219183223654.png)
* ![image-20210219183246404](images/image-20210219183246404.png)
* ![image-20210219183308302](images/image-20210219183308302.png)
* ![image-20210219183328711](images/image-20210219183328711.png)
* ![image-20210219183404439](images/image-20210219183404439.png)
* ![image-20210219183433319](images/image-20210219183433319.png)
* ![image-20210219183453943](images/image-20210219183453943.png)
* ![image-20210219183506264](images/image-20210219183506264.png)





* ![image-20210219183529565](images/image-20210219183529565.png)



* Most common protection mechanism against CSRF exploit is -> **token**
  * Token -> a nonce (which is a number used once and discarded)  and makes part of the request required to perform a given action unpredictable for an attacker
  * This token can be implemented as an **MD5 hash** (or stronger) of some randomly-generated string
* ![image-20210219183819818](images/image-20210219183819818.png)
* ![image-20210219183842233](images/image-20210219183842233.png)
* ![image-20210219183916646](images/image-20210219183916646.png)



* An attacker able to force the victim to request the forged URL, has  to provide a valid token.
* Two conditions may occur:
  *  The victim has not visited the page and, as such, has no token set in session variables at all
  * The victim has visited the page and has a token
* ![image-20210219184030248](images/image-20210219184030248.png)
* ![image-20210219184042734](images/image-20210219184042734.png)
  * ![image-20210219184106062](images/image-20210219184106062.png)
* ![image-20210219184127157](images/image-20210219184127157.png)







---



