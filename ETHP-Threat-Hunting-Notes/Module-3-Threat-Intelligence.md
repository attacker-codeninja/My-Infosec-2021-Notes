---
typora-copy-images-to: images
---

![image-20210301171616787](images/image-20210301171616787.png)

---



* **“Threat Intelligence is data on threats.”**
* For data to become intelligence, it has to be *processed, analyzed, and become actionable*
* The data will include context,not just indicators
* Intelligence may contain 
  * more than IP Addresses
  * File Hashes
  * etc
* It may contain TTPs => advice on how to stop their attack
* This type of hunter is relying on the information of **known** threats
* **SIEM =>** Security Information and Event Management solution
  * Centralized collection point where all logs (firewall,network, application,event etc)  are collected
    * so that Security Analyst can analyze them in once place, instead of logging into various consoles to view log data.
  * The logs can also contain external data.
* We need to gather  internal data using a SIEM  before start looking for threat intel externally





---





![image-20210301172435356](images/image-20210301172435356.png)





* Several trusted third-parties collect and gather cyber intel data and release **Threat Intelligence reports**
* These reports cover
  * malicious activity that was observed and explain specific threat actors associated with that activity.
* As a hunter, we need to read these reports
* ![image-20210301172606907](images/image-20210301172606907.png)
* For **FireEye** => Reports can be found in 
  * https://www.fireeye.com/current-threats/threat-intelligence-reports.html
  * These reports focus on intelligence regarding threat actors => APT28 and threat groups => FIN6
    * https://www.fireeye.com/current-threats/apt-groups/rpt-apt28.html
    * https://www.fireeye.com/solutions/financial-services/rpt-fin6.html
  * Naming convention for Financial Threats known as => **FIN** groups
  * **FIN6** => a cybercrime group that steals credit card and sells it in underground markets
    * They target PoS (Point of Sale) systems in the retail and hospitality sectors.
    * FIN6 group is also known as **G0037** under **MITRE's** naming convention
  * Annual report from FireEye => called **M-Trends**
    * https://www.fireeye.com/current-threats/annual-threat-report/mtrends.html
  * ![image-20210301173655469](images/image-20210301173655469.png)
  * ![image-20210301173739792](images/image-20210301173739792.png)
  * FireEye also publishes threat intelligence reports by industry
* Many researcher publish new research reports on emerging threats, often containing IOCs
  * Example => 
    * https://unit42.paloaltonetworks.com/unit42-nexuslogger-new-cloud-based-keylogger-enters-market/
    * https://unit42.paloaltonetworks.com/
* ![image-20210301174040180](images/image-20210301174040180.png)
* ![image-20210301174115706](images/image-20210301174115706.png)
* ![image-20210301174144175](images/image-20210301174144175.png)





---





![image-20210301174213388](images/image-20210301174213388.png)





![image-20210301174239567](images/image-20210301174239567.png)





* ![image-20210301174352998](images/image-20210301174352998.png)
* ![image-20210301174412470](images/image-20210301174412470.png)





![image-20210301174449650](images/image-20210301174449650.png)



* ![image-20210301174543081](images/image-20210301174543081.png)





![image-20210301174603610](images/image-20210301174603610.png)



* ![image-20210301174635336](images/image-20210301174635336.png)





> ### 4. Threat Connect



* Similar to OTX
* ![image-20210301174740525](images/image-20210301174740525.png)





> ### 5. MISP



* MISP => Malware Information Sharing Platform
* ![image-20210301174838850](images/image-20210301174838850.png)





---





![image-20210301174909264](images/image-20210301174909264.png)





![image-20210301174926776](images/image-20210301174926776.png)





* ![image-20210301175007335](images/image-20210301175007335.png)
* ![image-20210301175045246](images/image-20210301175045246.png)
* ![image-20210301175111437](images/image-20210301175111437.png)
* We use => **IOC Editor** tool
* It provides an interface for managing data and manipulating the logical structures of IOCs.
* IOCs => are XML documents that help security professionals capture diverse information about threats, including
  * attributes of malicious files, characteristics of registry changes, and artifacts in memory
* Tool => https://www.fireeye.com/services/freeware/ioc-editor.html
* Another Tool => **Redline**
  * ![image-20210301175346427](images/image-20210301175346427.png)
  * https://www.fireeye.com/services/freeware/redline.html
* Another Tool => **YARA**
  * It helping malware researchers to identify and classify malware samples
  * we can create descriptions of malware families based on textual or binary patterns
  * https://virustotal.github.io/yara/





---





