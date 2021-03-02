![image-20210221215142129](images/image-20210221215142129.png)

---



[TOC]



### XML Documents and Databases





> XML -> E*X*tensible *M*arkup *L*anguage -> v 1.0 -> a markup language (such as HTML) -> designed to **describe data** and *not* to **display data**

> XML Documents -> often used as databases.

> Data can be read and written through -> **queries** and the XML database looks just like an XML document



> ![image-20210222075234367](images/image-20210222075234367.png)
>
> 
>
> 
>
> 
>
> > ```
> > <?xml version="1.0" encoding="ISO-8859-1"?>
> > ```
> >
> > This is **XML Declaration** - Although not required but if it exists, it must be the first line in the document
> >
> > 
> >
> > **XML Declaration** -> defines the current version number -> 1.0  + the encoding type
>
> 
>
> 
>
> > ```
> > <users>
> > ...
> > </users>
> > ```
> >
> >
> > This line describes the root **element**  of the document.
> >
> > XML elements -> defines the structure of the document and identify named section of information
> >
> >
> > Elements -> form a document Tree => in above example **<users>** is the parent of all other elements
> >
> >
> > Note => all elements must have a closing tag and must be properly nested
>
> 
>
> ![image-20210222084158002](images/image-20210222084158002.png)
>
> 
>
> 
>
> > ```
> > <user id=’1’>
> > ...
> > ```
> >
> > 
> >
> > This line describes a child element. 
> >
> > Similar to HTML tag, elements  can have  attributes (**name="value"**), which are useful in defining properties of elements
> >
> > Attributes must be **quoted** and can only appear in start tags
> >
> >
> > Example -> **user** element has attribute named **id** with its value set to **1**
>
> 
>
> > ```
> > <username>jason</username>
> > ```
> >
> > 
> >
> > This element  is  child node for the element **user**.  -> This element  contains text -> this text can be consider value of the element
> >
> > If we consider a database structure , **jason** would be the text contained in the table **user**  with **id=1**
>
> 
>
> > ```
> > <!-- Comment -->
> > ```
> >
> > Similarly to HTML, XML documents can define and contain **comments**
> >
> >
> > a **comment** is defined as any type of content that is not intended for the XML parsers.







---



### XPATH





* XPATH -> **XML Path Language**
* XPATH -> is a standard language used to query and navigate XML documents.
* Latest Version -> 3.0
* XPATH -> makes use of path expressions to select nodes from an XML document
* ![image-20210222085131499](images/image-20210222085131499.png)
* ![image-20210222085210217](images/image-20210222085210217.png)
  * ![image-20210222085246844](images/image-20210222085246844.png)
  * ![image-20210222085411833](images/image-20210222085411833.png)
  * ![image-20210222085512495](images/image-20210222085512495.png)
  * ![image-20210222085556568](images/image-20210222085556568.png)
  * ![image-20210222085630247](images/image-20210222085630247.png)
  * ![image-20210222085658196](images/image-20210222085658196.png)
  * ![image-20210222085741107](images/image-20210222085741107.png)







* ![image-20210222085926255](images/image-20210222085926255.png)

* In SQL, we able to insert a comment expression into a query

* > ![image-20210222090016592](images/image-20210222090016592.png)
  >
  > 
  >
  > SQL Query to match credential against the database (login operation)
  >
  >
  > ![image-20210222090125323](images/image-20210222090125323.png)
  >
  > 

  

* Unlike SQL, the XPath language does not permit comment expressions.

* The attacker must provide a specific payload to bypass a Boolean operator present in the query.

* Unlike SQL,  XPath is a case-sensitive language

  * Therefore, this means that the keywords of the language must be specified exactly as they have been declared in the language specs.

* ![image-20210222090440799](images/image-20210222090440799.png)







---



### Detecting XPATH Injection





* First step =>  check  whether the web application is susceptible to **XPath Injection**

  * => Web Application make use of an XML database for data storage and querying

* Detection Process is same as in SQL Injection

  * Discover each web application parameter and send specific input data (probes) to check whether it is vulnerable or not

* ![image-20210222090811777](images/image-20210222090811777.png)

* ### EXAMPLE

  * Suppose a vulnerable web application called -> **CountryInfo**

  * This web application accepts a parameter **countryID** and uses it to query an XML document through XPath queries

  * ![image-20210222090950538](images/image-20210222090950538.png)

  * ![image-20210222091059810](images/image-20210222091059810.png)

  * ![image-20210222091130919](images/image-20210222091130919.png)

  * ![image-20210222091205537](images/image-20210222091205537.png)

    

    

    

  * ![image-20210222091323666](images/image-20210222091323666.png)

  * In a blind injection, the attacker will try to trigger two conditions: **TRUE** and **FALSE**

  * The **TRUE** condition will be determined by an injection payload forcing an always TRUE statement, like **1=1**

  * The **FALSE**  payload => **1=2** => and web application output will be **different**  when use this **FALSE** condition payload

  * Similarly to SQL Injection, if the web application is vulnerable, it will react differently and return two different outputs.

  * ![image-20210222091801578](images/image-20210222091801578.png)

  * The web application hides the errors but, this does not mean that it is not vulnerable.

  * ![image-20210222091849581](images/image-20210222091849581.png)

  * ![image-20210222091925528](images/image-20210222091925528.png)

  * ![image-20210222092007382](images/image-20210222092007382.png)

  * ![image-20210222092035651](images/image-20210222092035651.png)

    * > In this payload, **999999** is most likely missing **countryID** in the database and **1=1** is a Boolean expression that is always **TRUE**

    * ![image-20210222092210600](images/image-20210222092210600.png)

  * ![image-20210222092308956](images/image-20210222092308956.png)
* ![image-20210222092342765](images/image-20210222092342765.png)
  

  

  
  * ![image-20210222092428582](images/image-20210222092428582.png)
  * ![image-20210222092543470](images/image-20210222092543470.png)
  * ![image-20210222093159499](images/image-20210222093159499.png)
  * ![image-20210222093218753](images/image-20210222093218753.png)
  * ![image-20210222093305128](images/image-20210222093305128.png)
  * ![image-20210222093321486](images/image-20210222093321486.png)
  
  
  
    
  

---



### Exploitation



> With this process, the attacker takes advantage of the vulnerability to access restricted data

> Attacker can exploits the vulnerability to perform actions such as:
>
> 
>
> * **Bypassing Authentication**
> * **Extracting the XML document structure and contents**





* ![image-20210222093604378](images/image-20210222093604378.png)
* ![image-20210222093633248](images/image-20210222093633248.png)
* ![image-20210222093700010](images/image-20210222093700010.png)
* ![image-20210222093724539](images/image-20210222093724539.png)
* ![image-20210222093816937](images/image-20210222093816937.png)
* ![image-20210222093854811](images/image-20210222093854811.png)
* ![image-20210222093939706](images/image-20210222093939706.png)
* ![image-20210222094013884](images/image-20210222094013884.png)
* ![image-20210222094103484](images/image-20210222094103484.png)











* ![image-20210222094141701](images/image-20210222094141701.png)

* The attacker’s main goal is to extract all the XML document data; this operation is identical to dumping a database during a SQL injection

* In an SQL Database -> **schemas**, **tables** and **columns**

* In XML Document -> **nodes**, **attributes**, and **values**

* So, attacker's GOAL -> get all the -> **nodes**,**attributes** and **values** of the XML Document that is being used as a database.

* ![image-20210222094415932](images/image-20210222094415932.png)

* As the attacker, we do not know the *structure of the XML* document, but we need to find it out

* ![image-20210222094552312](images/image-20210222094552312.png)

* First, attacker needs to *detect* which input data *satisfies* the **TRUE** and the **FALSE** conditions.

  * For example,  considering the password as the injectable parameter, the input data satisfying the 2 conditions would be :
    * ![image-20210222094748854](images/image-20210222094748854.png)

* ![image-20210222094858143](images/image-20210222094858143.png)

* ![image-20210222094938987](images/image-20210222094938987.png)

* Suppose that in our example the identifier of the root node is **users**

* The attacker will perform multiple XPath queries to find all the identifier’s characters.

* Note that each time the condition is true, it means that the character used is correct and we can then go on with the next character

* ![image-20210222095351010](images/image-20210222095351010.png)

* ![image-20210222095417398](images/image-20210222095417398.png)

* So, by trying such above payloads, we can get - **users** - root node

* ![image-20210222095508068](images/image-20210222095508068.png)

* ![image-20210222095536239](images/image-20210222095536239.png)

* ![image-20210222095628455](images/image-20210222095628455.png)

* ![image-20210222095646227](images/image-20210222095646227.png)

* ![image-20210222095706414](images/image-20210222095706414.png)

* We know the following XML document structure:

  * ```
    <users>
    	<user>
    		...
    	</user>
    </users>
    ```

* ![image-20210222095811447](images/image-20210222095811447.png)

* Suppose, got all the node identifiers of the XML Document

  * Example -> identifiers of the nodes:  **users, user, username, password**
  * and how they appear in the hierarchy

* Now, after this we need to get the content of a node like a username record

* We can access the username using the XPAth Query =>

  * ```
    /users/user[position()==$i]/username
    ```

  * Where **$i** is a numerical placeholder ( that could iterate to discover every username in the system)

* ![image-20210222100237241](images/image-20210222100237241.png)

* ![image-20210222100252232](images/image-20210222100252232.png)

* ![image-20210222100325153](images/image-20210222100325153.png)





---



### Best Defending Techniques



> The best way to protect against XPath injection is to filter all input data



![image-20210222100420834](images/image-20210222100420834.png)



![image-20210222100445627](images/image-20210222100445627.png)





![image-20210222100522978](images/image-20210222100522978.png)







---





