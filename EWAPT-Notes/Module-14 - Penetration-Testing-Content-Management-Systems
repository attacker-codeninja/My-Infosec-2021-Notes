![image-20210222100656982](images/image-20210222100656982.png)

---



[TOC]



### Introduction



> CMS -> Content Management System => Example => Joomla & Drupal & Wordpress



![image-20210222100937914](images/image-20210222100937914.png)





> The standard methodology for assessing CMS web applications 
>
>  	-> follows a path of first **identifying** the *CMS vendor* and *version*.



> After got *vendor* and *version*,  then focus on -> to identifying vulnerabilities within the particular CMS version

> Like -> Are there any publicly known vulnerabilities related to the specific version ?



> Next **step** => do information gathering about the various **components** of the CMS application

> This includes => 
>
> * plugins,  
> * extensions,  
> * enumerating user accounts,  
> * web server settings,  
> * misconfigurations  and 
> * common files related to the CMS which might reveal configuration settings

 

> After  Information Gathering phase => Next Step => Exploitation Phase => to exploit any vulnerabilities discovered through information gathering.

> If **in-scope** => can do brute-force CMS using user accounts we enumerated





> **METHODOLOGY =>**
>
> 
>
>
> ![image-20210222101859102](images/image-20210222101859102.png)







---



### Wordpress



* Wordpres is Most widely-deployed CMS and is developed based on the PHP programming language
* Backend Database is commonly **MySQL** and  this is important to know for pentester
* Wordpress can be used as 
  *  range from simple blogs, to complex fully-functional Content Management systems to even being the complete underlying code-base for many websites due to the fact that it is easy to deploy, and relatively easy to maintain
* Wordpress allows for the quick inclusion of modular **3rd-party**  plugins for easy-to-implement functionality for a number of different purposes.
* Wordpress is easy to implement CMS
* **DOWNFALL**
  * wordpress is open-source
  * Wordpress allows 3rd-party development of its core, plugins and other utilities
  * So, it can be known to introduce vulnerabilities throughout its development life cycle





> ![image-20210222102527467](images/image-20210222102527467.png)





> Gather information about the web application as much as possible 



* Step 1 => Use Tool -> **WPSCAN**

  * ![ ](images/image-20210222102654594.png)

  * WPScan can also conduct Bruteforce dictionary attacks against a WordPress login page

  * Command => **wpscan --url http://fooblog.site**

    * > --url parameter => to determine the WordPress Version installed and some other information about the installation including PHP version, potential vulnerabilities, and interesting files, such as robots.txt files which could contain interesting directory or file references.

    * ![image-20210222155222574](images/image-20210222155222574.png)

  * Command => # wpscan --url http://fooblog.site **--enumerate u**

    * > --enumerate u => Its use for enumerating users
      >
      > ![image-20210222155327980](images/image-20210222155327980.png)

  * ### WordPress “Manual” User Enumeration (User Dictionary Method)

    * Each blog post -> will have an "Author" listed
    * ![image-20210222155836293](images/image-20210222155836293.png)
    * If user does not exist in **author directory** then we can get  404 error like =>
      * ![image-20210222155936479](images/image-20210222155936479.png)
    * But for using valid user from **author directory** we can get 301 =>
      * ![image-20210222160031058](images/image-20210222160031058.png)
    * And by this HTTP Response *difference*  we can use to our advantage to enumerate users.
    * ![image-20210222160515711](images/image-20210222160515711.png)
    * ![image-20210222160533434](images/image-20210222160533434.png)
      * So, we can see 2 users we got using this brute-force technique

    

    

    

  * ### WordPress “Manual” User Enumeration (Brute Force Method)

      

      * ![image-20210222160649469](images/image-20210222160649469.png)
      * ![image-20210222160718474](images/image-20210222160718474.png)
      * ![image-20210222160933339](images/image-20210222160933339.png)
  
  * After enumerate Users ,  we can use WPSCAN's built in brute-force option to get access to the *Administrative Interface*
  
  * Next, we can use WPScan option for -> **Enumerating Plugins**
  
    * We need to find all the installed plugins within a wordpress installlation
  
    * Before start -> run WPScan with **--update** parameter =>  This will make sure WPScan has its latest signatures database.
  
      * > wpscan --update
  
  * Another important WPScan parameter need to use is => **--user-agent**
  
    * The default WPScan user-agent is well known, and will likely flag Intrusion Detection Systems or Web Application Firewalls.
    * a well-known web browser user-agent will help with evading some basic defenses.
  
  * ### Enumerating Plugins
  
    * In order to enumerate plugins, we can use the “--enumerate” parameter, along with the “p” value, as follows.
  
    * > wpscan --url http://fooblog.site --enumerate p
  
    * ![image-20210222162044257](images/image-20210222162044257.png)
  
    * ![image-20210222162109657](images/image-20210222162109657.png)
  
    * ![image-20210222162421409](images/image-20210222162421409.png)





* ### Step 2 => Tool => Plecost

  * https://github.com/iniqua/plecost

  * Excellent tool for Enumerating **Plugins**

  * Require -> **plugins wordlist**

  * By default comes with several lists of its own

  * ```
    Command =>
    
    # plecost -i /usr/share/plecost/wp_plugin_list.txt http://fooblog.site
    ```

  * ![image-20210222162727632](images/image-20210222162727632.png)





* ### Step 3 => NMap NSE Scripts

  * Useful Nmap NSE Scripts =>
    * **http-wordpress-brute**
    * **http-wordpress-users**
    * **http-wordpress-enum**
  * ![image-20210222163112244](images/image-20210222163112244.png)
  * So, we can use Nmap NSE Scripts for various purposes like =>
    * enumerating users
    * enumerating plugins
    * and brute-forcing a wordpress application





* ### Step 4 => Directory Indexing/Listing

  * Sometimes, small **misconfigurations** can also lead us to a trove of information in regard to what plugins might be installed and other information we might find useful.
  * When **Directory Indexing or Directory Listing**  is *enabled* on a web server, 
    * then it allows us  to view the contents of a directory in a folder/file-list type structure.
  * How to know is Directory Listing enabled or not ?
    * By browsing to a known directory => **wp-content** directory
    *  This directory contains most of the WordPress content related to themes, plugins, languages, etc.
    * ![image-20210222163713279](images/image-20210222163713279.png)
  * ![image-20210222163736326](images/image-20210222163736326.png)
  * ![image-20210222170520410](images/image-20210222170520410.png)
    * ![image-20210222170556805](images/image-20210222170556805.png)
  * ![image-20210222170751802](images/image-20210222170751802.png)
  * ![image-20210222170823165](images/image-20210222170823165.png)
  * Using tool **Nikto** or **WPScan** => with default configurations => confirm Directory Indexing 
    * But , this is NOISY, and will generate alerts
    * So, we should opt for manual identification of misconfigurations where possible, using just a web browser





* ### Step 5 => Wordpress Exploitation

  * After gather information like version, vulnerable plugins, users and other vulnerabilities either in the core or in plugins etc  next  step is Exploitation Phase

  * ### 1. Brute Force Attacks

    * Bruteforce attacks most popular way to gain access to the administrative interface

    * Once admin access has been obtained,  attacker will get full contol over *plugins*,*users*,*configuration settings* and more

    * Attacker then can deliver **malicious content to visiting users, or users of the blog in general.**

    * This type of access can also lead to code execution on the underlying operating system

    * ![image-20210222171832927](images/image-20210222171832927.png)

    * ![image-20210222171919312](images/image-20210222171919312.png)

    * Default administrator user of a WordPress installation is => **admin** and worth to try

    * This “default” user makes it a prime target for Bruteforce attacks

    * ![image-20210222172113875](images/image-20210222172113875.png)

    * ![image-20210222172132874](images/image-20210222172132874.png)

    * If we lucky, then can get the desire result else not

    * ![image-20210222172203802](images/image-20210222172203802.png)

    * ![image-20210222172226114](images/image-20210222172226114.png)

      

      

      

      

    * NOTE => other then Wordpress there are plenty of tools for same purpose => 

      * https://github.com/search?o=desc&q=wordpress+bruteforce&s=&type=Repositories

      

      

      

      

    * ![image-20210222172411808](images/image-20210222172411808.png)

    * https://github.com/atarantini/wpbf

    * This is another good tool  bruteforce WordPress login page

    * ![image-20210222172459322](images/image-20210222172459322.png)

    * ![image-20210222172534330](images/image-20210222172534330.png)

    * ![image-20210222172604000](images/image-20210222172604000.png)

    * ![image-20210222172634681](images/image-20210222172634681.png)

    * ![image-20210222172653902](images/image-20210222172653902.png)

    * ![image-20210222173743378](images/image-20210222173743378.png)

    * ![image-20210222173903335](images/image-20210222173903335.png)

    * ![image-20210222174032742](images/image-20210222174032742.png)

    * ![image-20210222174049979](images/image-20210222174049979.png)

      

      

      

    * A general rule of thumb when using tools, is to understand their inner-workings.

    * Making small modifications to existing code can go a long way in regards to staying under the radar in some cases

    

    

    

    

    

  * ### 2. Attacking Plugins

    * We must know that many WordPress vulnerabilities => because of 3rd-Party Plugins

    *  ![image-20210222174436386](images/image-20210222174436386.png)

      * Vulnerable Plugin => https://wordpress.org/plugins/404-to-301/

      * This vulnerability do both -> hook an **administrator's browser** and code execution on OS of the Web Server hosting Wordpress

      * ![image-20210222174655693](images/image-20210222174655693.png)

      * ![image-20210222174719994](images/image-20210222174719994.png)

      * First as Information Gathering => try to run wpscan to enumerate this plugin 

        ```
        # wpscan --url http://fooblog.site --enumerate p
        ```

      * ![image-20210222174826245](images/image-20210222174826245.png)

      * Once got this **404-to-301** plugin and its version then Google about this Vulnerable Version

      * This particular version, 2.3.0, is known to be vulnerable to an **unauthenticated,** *Stored XSS* within the administrator control panel of the plugin.

      * ![image-20210222175011604](images/image-20210222175011604.png)

      * From above image we can see a interesting field => User-Agent

      * It's mean The application logs the **User-Agent** of the *client browser* requesting the non-existent page, and stores it for the Administrator to review at a later date , along with the page that was requested.

      * So, an attacker can **forge the User-Agent**  field of attacker's request Using BurpSuite

      * This vulnerable plugin fail to  sanitize the input being received by the client browser.

      * So, attacker can use XSS Payload => in User-Agent header => and it will trigger an alert popup, as soon as the administrator views the plugins’ 404 logs control panel:

        * ![image-20210222175528906](images/image-20210222175528906.png)

      * Testing =>

        * ![image-20210222175554683](images/image-20210222175554683.png)
        * Here, first we try to visit with **NONEXISTENTURL**  URL and then also provide XSS Payload in **User-Agent** Header
        * Once click on **GO** button then we can see following result
          * ![image-20210222175705887](images/image-20210222175705887.png)
        * This confirms the plugin has redirected our request to a non- existent page (/NONEXISTENTURL in this example)
        * Now, Once an administrator of the WordPress site visits the plugins’ control panel, they would get an alert popup with “/xss/” in the popup
        * ![image-20210222175813305](images/image-20210222175813305.png)

      * Now, to exploit such Basic XSS to advance using tool => **BEEF** exploitation framework to serve up a malicious “hook” via an <iframe> tag.

      * This would give us access to the administrators’ web browser, and potentially their machine.

    * ![image-20210222181729707](images/image-20210222181729707.png)

    * ![image-20210222181800698](images/image-20210222181800698.png)

    * ![image-20210222181827475](images/image-20210222181827475.png)

    * From there, we can conduct a myriad of different attacks to deliver payloads using BeEF’s built in commands.

    * Beside this BEEF exploit vector, there is  another even better attack vector to compromise the web server through this vulnerable plugin.

      * ![image-20210222182153980](images/image-20210222182153980.png)

    * ![image-20210222182228479](images/image-20210222182228479.png)

    * ### Testing in Action

      * ![image-20210222182327913](images/image-20210222182327913.png)
      * ![image-20210222182344710](images/image-20210222182344710.png)
      * ![image-20210222182358862](images/image-20210222182358862.png)
      * ![image-20210222182416697](images/image-20210222182416697.png)
      * ![image-20210222182422528](images/image-20210222182422528.png)
      * Keep in mind, that this particular attack is valid for most plugins that contain stored XSS vulnerabilities so long as we make some minor modifications to the Metasploit module.
      * ![image-20210222182541335](images/image-20210222182541335.png)
      * ![image-20210222182606570](images/image-20210222182606570.png)
      * ![image-20210222182704665](images/image-20210222182704665.png)
      * Lines 77 to 109 are responsible for making the changes to the “footer.php” page, and inserts the PHP meterpreter payload.
      * ![image-20210222182744553](images/image-20210222182744553.png)

      

      

      

      

    * ![image-20210222182930430](images/image-20210222182930430.png)

    * Once an attacker has gained access to a WordPress installation as an administrator, it becomes trivial to use plugins as a method to achieve persistence.

    * In the case with the previous exploit, the “footer.php” was modified to include malicious code.

    * This can be considered as leveraging the WordPress “Core” to execute our own malicious code, due to the fact we’re simply embedding our own malicious code into a pre-existing PHP file.

    * ![image-20210222183357925](images/image-20210222183357925.png)

    * ### WPForce

      * https://github.com/n00py/WPForce
      * A tool or scripts to upload PHP shells to a WordPress installation and works by first bruteforcing administrator credentials, and using that access to upload its own built-in shells, which results in a simple command shell on the target web server.
      * WPForce is comprised of several components we can use to achieve our goal of server compromise.
      * ![image-20210222183633566](images/image-20210222183633566.png)
      * ![image-20210222183702213](images/image-20210222183702213.png)
      * ![image-20210222184012750](images/image-20210222184012750.png)
      * ![image-20210222184048098](images/image-20210222184048098.png)
      * **add_admin.js** script => will add *an administrator user* to the WordPress installation => then we can use this user for  accessing the interface.
      * ![image-20210222184302008](images/image-20210222184302008.png)
      * ![image-20210222184411219](images/image-20210222184411219.png)
      * ![image-20210222184445451](images/image-20210222184445451.png)
      * ![image-20210222184507670](images/image-20210222184507670.png)
      * ![image-20210222184527608](images/image-20210222184527608.png)
      * ![image-20210222184719542](images/image-20210222184719542.png)
      * ![image-20210222184741569](images/image-20210222184741569.png)
      * ![image-20210222184758477](images/image-20210222184758477.png)
      * ![image-20210222184824127](images/image-20210222184824127.png)
      * Using **Meterpreter** 
        * ![image-20210222184921283](images/image-20210222184921283.png)
        * ![image-20210222185145524](images/image-20210222185145524.png)
        * ![image-20210222185209868](images/image-20210222185209868.png)
      * So, **WPFORCE** is an  excellent tool for maintaining persistence to a server hosting WordPress, and for Post-Exploitation.

    

    

    

    

---



### Joomla



* JOOMLA -> another very popular CMS, similar to Wordpress
* easy-to-use and manage web interface when it comes to content  creation
* Joomla is also Open-Source and written in PHP allows to easily add functionality to a site via what are known as “Extensions” or “Components”.
* Similar to Wordpress vulnerabilities are often a result of
  * poorly coded components, and sometimes, issues also arise from within the Core of the application itself.







![image-20210222185612693](images/image-20210222185612693.png)





![image-20210222185637189](images/image-20210222185637189.png)





> Having a good idea of the specific version an application is running helps us identify any known vulnerabilities within a particular application



* Most recent versions of Joomla contain a **joomla.xml** file within the **“/administrator/manifests/files” directory**
  * it is readable without authenticating to the application.
* ![image-20210222185904635](images/image-20210222185904635.png)
* So, to obtain Joomla Version  either **manually browse the above URL** or
  * **use the curl and grep commands to pull the version from the joomla.xml** file with a regular expression, in the event you need to quickly script the process for querying multiple hosts
  * ![image-20210222190030986](images/image-20210222190030986.png)







* ![image-20210222190250225](images/image-20210222190250225.png)
* OR can  use “grep” command for the “X-Powered-By” string
  * ![image-20210222190426438](images/image-20210222190426438.png)
* OR can use BurpSuite
  * ![image-20210222190527020](images/image-20210222190527020.png)





* ### Tool =>  Joomscan

  * https://github.com/rezasp/joomscan
  * Joomscan will automate the process of 
    * identifying the Joomla version
    * any vulnerabilities in the Core
    * locating the Administrator Login Page
    * and a number of checkes we can find useful
  * Command => joomscan -u http://joomla.site
  * Output example  for =>  joomla version and location of the admin page and a number of potentially critical vulnerabilities
    * ![image-20210222191114330](images/image-20210222191114330.png)
    * ![image-20210222191117863](images/image-20210222191117863.png)

* ### Tool => Joomla Scan

  * https://github.com/drego85/JoomlaScan
  * Command => python joomlascan.py -u http://joomla.site/joomla
  * ![image-20210222191831103](images/image-20210222191831103.png)

* ### **Extensions**

  * main Joomla components is **Extensions** within Joomla
  * Extensions are also sometimes referred to as “Components”.
  * Extensions are essentially “Plugins”, similar to WordPress, and can be downloaded, and quickly installed into a Joomla site from within the Joomla Administrator interface.
  * ![image-20210222192000725](images/image-20210222192000725.png)
  * And similar to WordPress, extensions often introduce vulnerabilities into a Joomla installation.
  * Using Joomla Scan Tool, we can enumerate many of the extensions installed on a Joomla site which uses a built in “**comptotestdb.txt**” file
    * which is essentially  a database of well-known components and extensions.
  * ![image-20210222192314435](images/image-20210222192314435.png)
  * Components found with the **com_<component-name>** naming format and can be accessed via a URL, and are specified with the **"option"** parameter like =>
    * ![image-20210222192457208](images/image-20210222192457208.png)
  * Unfortunately, there is no “easy” way to enumerate every single extension or component within a Joomla installation ( without having an administrator account)
    * and discovery  require a database or file of known extension names
  * ![image-20210222192657117](images/image-20210222192657117.png)
    * this will give us a  good starting point in regard to which extensions or components  to look for
    * ![image-20210222192754987](images/image-20210222192754987.png)
    *  save above result to **comptotestdb.txt** file to use with **joomla scan tool**  for additional extension or component checks.
    * ![image-20210222193035651](images/image-20210222193035651.png)
  * Metasploit also contains several auxiliary modules to **enumerate plugins/extensions.**
    * Joomla plugin module => https://www.rapid7.com/db/modules/auxiliary/scanner/http/joomla_plugins
    * ![image-20210222193148706](images/image-20210222193148706.png)
    * ![image-20210222193207503](images/image-20210222193207503.png)









* ### **Content Discovery**

  * Tool can be use to do Content Discovery => **dirsearch** and many others
  * It will discover  directories and files,  can give some useful  or sensitive file or directory
  * Command => **./dirsearch.py -u http://joomla.site/joomla -e php -x403**
  * ![image-20210222193545832](images/image-20210222193545832.png)
  * Also **robots.txt** can be use to give directories that might contain useful information
    * ![image-20210222193646651](images/image-20210222193646651.png)
  * Also keep in mind that, sometime an administrator will create backups of a site while rolling out a new version, and might leave critical files on the webserver that pertain to a sites’ initial configuration.
  * Even in **robots.txt**  file,  sometimes browsing to those disallowed directories can lead to things like
    * backups of the Joomla “configuration.php”
    * or other critical files
    * which can reveal credentials to the database for example.
    * ![image-20210223080737595](images/image-20210223080737595.png)
  * Even Burp suite featue **Spider**  can also be useful in revealing things we might miss through manual identification of content:
    * ![image-20210223080836169](images/image-20210223080836169.png)
  * **"phpinfo"** files => also helpful in identifying how the web server is configured , and what options are enabled in regard to the PHP configuration
    * ![image-20210223080935530](images/image-20210223080935530.png)
    * ![image-20210223080941272](images/image-20210223080941272.png)
  * Another thing to check is if the Administrator login page is publicly accessible
    * The “Administrator” interface can usually be found with the **/administrator directory in the sites’ web root**
    * and we can do  dictionary attacks against this page
    * ![image-20210223081116182](images/image-20210223081116182.png)











![image-20210223081215073](images/image-20210223081215073.png)







![image-20210223081240627](images/image-20210223081240627.png)



* This phase entails 
  * dictionary-based bruteforce attacks against the administrator panel,
  * identification of vulnerabilities within the Joomla Core
  * and exploitation of any vulnerable extensions





![image-20210223081422856](images/image-20210223081422856.png)





* With Wordpress,  enumerating users having many methods to determine user like from authors from blog posts and other contet

* But with Joomla,  This is not the case,  Instead

  * we must rely on **guesswork** when it comes to trying to bruteforce users and admin accounts
  * This is because when first installing Joomla website, the admin is required to define the username the installer like to  use for the account
  * This way it will makes it harder to do dictionary-based bruteforce attack against the administrator interface
  * So that leaves us with a lower success rate in actually obtaining access to the administrator interface.

* So, we need to do start from the some **common administrator username** that might be in use, such as **"admin"** , which is seen frequently to be the case with Joomla installs.

* Once do this step with admin username, we can use several tools to help in bruteforcing the admin panel.

* ### Tool => JoomBrute

  * https://github.com/0rbz/JoomBrute

  * ![image-20210223082040987](images/image-20210223082040987.png)

  * Usage =>

    * require 3 parameters
      * URL to the administrator panel, 
      * a username
      * a wordlist for passwords

  * Command =>

    * ```
      python JoomBrute.py --url http://joomla.site/joomla/administrator --username admin
      --wordlist /usr/share/wordlists/rockyou.txt
      ```

  * **-ua** option => to define User-Agent also available in this tool

    * By default User-Agent => **JoomBrute/1.0**
    * Recommended changing this to something more common

  * ![image-20210223082338782](images/image-20210223082338782.png)









![image-20210223082420927](images/image-20210223082420927.png)





* Joomla or CMS Vulnerabilities history showing  that many vulnerabilities  arise in its CORE because of open-source

* This vulnerabilities arise because of failure to escape or filter certain characters from user-supplied input.

* This often leads to SQL Injection and Cross Site Scripting vulnerabilities among other types of vulnerabilities.

* ### 1. CVE-2015-7857 (com_contenthistory SQL Injection)

  * https://www.cvedetails.com/cve/CVE-2015-7857/

  * It  affects Joomla versions from 3.2 up to 3.4.4

  * This vulnerability found in the Joomla Core component -> **com_contenthistory**

  * This vulnerability when exploited, and depending on the server configuration , usually leads to access to an affected server as the **www-data user.**

  * Research - https://www.trustwave.com/Resources/SpiderLabs-Blog/Joomla-SQL-Injection-Vulnerability-Exploit-Results-in-Full-Administrative-Access/?page=1&year=0&month=0

  * ![image-20210223090540530](images/image-20210223090540530.png)

  * ![image-20210223090728042](images/image-20210223090728042.png)

  * This ultimately results in being able to extract information from the database that should typically only be accessible to the admin user

  * This finding allows us to extract information from an unauthenticated perspective.

  * ![image-20210223090841510](images/image-20210223090841510.png)

  * ![image-20210223090910790](images/image-20210223090910790.png)

  * These type of errors most of the time indicate that we may be able to potentially craft a query that will return some useful information.

  * ![image-20210223091118850](images/image-20210223091118850.png)

  * Note that our value **1** comes after the MySQL **"SELECT"** statement

  * It indicates that we might be able to craft a more specific SELECT statement, which could result in getting information from a specific table.

  * Use SQLMAP =>

    * ```
      sqlmap -u
      "http://joomla.site/joomla/index.php?option=com_contenthistory&view=history&list[select]=1"
      ```

    * ![image-20210223091249517](images/image-20210223091249517.png)

    * So, **option** parameter is vulnerable

  * ![image-20210223091445113](images/image-20210223091445113.png)

  * Ans so on we can use sqlmap to gather more informations like, Tables, Users, Columns and DUMP them or even can get SHELL using **--os-shell**

  * Even can use **METASPLOIT**

    * ![image-20210223091712361](images/image-20210223091712361.png)
    * ![image-20210223091730221](images/image-20210223091730221.png)
    * This particular exploit will only work if an administrator is currently logged into the application, as it needs to extract an existing session Token. If that’s the case, then we can easily get a shell. like above

  

  

  

  

* ### 2. CVE-2016-8869 (Joomla Registration Privilege Escalation)

  * http://cve.circl.lu/cve/CVE-2016-8870
  * This CVE allows remote attackers to create administrative accounts, even when user registration is disabled
  * This vul affects => Joomla version up to  3.4.4
  * This vul is chain of => *file extension whitelist bypass vulnerability*  **to** *ultimately obtain command execution on the underlying operating system.*
  * With a default Joomla installation, users are restricted 
    * from being able to upload media file types that contain the “<?php” string, or extensions of types .php and .phtml.
  * But researcher discovered that
    * **“<?=“**  => was allowed within files, and
    * file types with extension => **.pht** also allowed
    * So, combination of => **<?=**  and **.pht** => result in command execution
  * Exploit Script => Joomra => https://github.com/XiphosResearch/exploits/tree/master/Joomraa
    * to create an administrator user within a vulnerable Joomla installation
  * ![image-20210223092617739](images/image-20210223092617739.png)
  * ![image-20210223092639109](images/image-20210223092639109.png)
  * ![image-20210223092644169](images/image-20210223092644169.png)
  * ![image-20210223092912375](images/image-20210223092912375.png)
  * ![image-20210223092931971](images/image-20210223092931971.png)
  * ![image-20210223092954160](images/image-20210223092954160.png)
  * ![image-20210223093013894](images/image-20210223093013894.png)
  * ![image-20210223093035913](images/image-20210223093035913.png)
  * ![image-20210223093114431](images/image-20210223093114431.png)
  * ![image-20210223093246990](images/image-20210223093246990.png)
  * So, we can get a shell on the system





---



