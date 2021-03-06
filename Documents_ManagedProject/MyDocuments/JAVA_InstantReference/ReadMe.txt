






########################################## USEFUL HINTS ############################################################


Useful JAVA reference sites:
===========================================
http://www.javaknowledge.info/jstl-1-1-simple-insert-update-delete-example/
https://www.youtube.com/watch?v=eaAqwTdUAAo (Durga software solutions)

https://netbeans.org/kb/docs/web/mysql-webapp.html
https://netbeans.org/kb/docs/web/mysql-webapp.html#view-connection-pool
https://netbeans.org/kb/docs/ide/git.html

https://netbeans.org/project_downloads/samples/Samples/JavaEE/ecommerce/ 		(Affable Bean Project snapshots loation)

https://www.youtube.com/watch?v=TTbj_x3yiLE						(Openshift tutorial)  

-----------------------------------------------------------------------------------------------------------








Web hosting sites:
=========================================
https://www.openshift.com
http://cloudbees.com
http://www.serversfree.com/
http://3owl.com/
https://cloud.google.com/appengine/
Cloud Foundry 
heroku
---------------------------------------------------------------------------------------------













Netbeans shortcuts
====================
ctrl + Shift + I 					-> imports all the necessary packages for the class
Right click anywhere in the coding page > insert code 	-> it will give you many options to insert different type of readymade code
--------------------------------------------------------------------------------------------------------------------------------------------











Java Application set up and structure
==========================================
1. Add JDK bin folder to the PATH
		set path C:\Program Files\Java\jdk1.8.0_111\bin 			(all the JAVA compile time command softwares (JDK) are in this folder)

2. Add the library folder to the CLASSPATH
		set classpath C:\Program Files\Java\jre1.8.0_131\lib 			(all the jar files, usesd at run time (JRE) are present in this folder)

3. Add the required JAR files to the Project library					(for example add "log4j-1.2.17.jar" to the Java application Project's library)
 
 				In case of web application, 
				put the required JARs in the server's library folder 	(c:/programfiles/glassfish/domains/domain1/lib)

4. Import the required libraries(present in the JAR) in the JAVA application		(Ex:- "import import org.apache.log4j.Logger;" )

5. Use the library's class in the Program						(Ex:- "Logger" class  )	
				
6. Instantiate the class and use the method of the class in the Java application 	(Ex:- The class's getLogger() method returns an object ->used for loggings)







How to import libraries in JAVA / JSP
===============================================

Import libraries in JAVA
---------------------------
1. The library classes are usually bundled in a JAR file

2. You have to first Add the JAR file to the project Library, 

3. Then in the Java Program, you have to import the required JAR file-class with proper hierarchy, so that the your Java program can recognize the JAR file-class(es) 

						Example Code:-
							import org.apache.log4j.Logger;

4. Now your Java Program recognizes the Logger class of the LOG4J JAR file (log4j-1.2.17.jar)

5. Then you can instantiate the Logger class 

						Example Code:-
							Logger logger = Logger.getLogger(ControllerServletInvokingEJBSessionBean.class );

6. Then you can use the Logger class's properties / methods through that instance ("logger")

						Example Code:-
							logger.info()

Import libraries in JSP
---------------------------

1. Similarly, in JSP you can use external librariesby using <%@taglib> 	-> stands for "tag library"

						
2. You have to import the required libraries ("core" and "sql")  to use their utilities in the JSP program
							
						Example Code:-
							<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
							<%@taglib prefix="sql" uri="http://java.sun.com/jsp/jstl/sql"%>


3. Here you are importing the core library and instantiating it to a reference "c"
	you are importing the sql  library and instantiating it to a reference "sql"


4. Then you can use the core library's  properties / methods through the instance "<c:XXX ---- />"

						Example Code:-
							<c:forEach var="customer" items="${customerDetails}">    
            							
                						<c:out value="${customer.custName}" /> 
            
        						</c:forEach>
	
	you can use the sql  library's  properties / methods through the instance "<sql:XXX --- />"
						Example Code:-
							<sql:update var="customerInsertResult" dataSource="jdbc/myTestDataSource">
                						INSERT INTO customer (cust_name, cust_address, cust_email)
                						<%VALUES ("${param.txt_Name}", "${param.txt_Addr}", "${param.txt_Email}")%>               
            						</sql:update>
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------
  







How to capture the user inputs in the servlet or JSP
=============================================================
The user input can be passed through query string or query parameter or form submit or init-param setting in web.xml or context parameter setting for the application
		
		query String Example1 :-
			
				http://localhost:8080/customer.jsp?"Sambit"

		query parameter Example1 :-
				http://localhost:8080/customer.jsp?custName=Sambit&custAddress=Pune
		
		Form-submit example :-

				<input type= text name = "custName">


		init-param setting in web.xml
				
				</servlet>

					<servlet name="Myservlet">
					<servlet class="MyServlet.class">
					<init-param>
						<param name="custName" >
						<param value="Sambit">
					</init-param
				
				</servlet>
	
		parameter set in servlet context

				getServletContext().setAttribute("customerDetails",customerFacade.findAll()); 
	
 
In Servlet:
------------									
		request.getQueryString()

				or

		request.getParameter("custName")

				or 

		getInitParameter().getAttribute("custName")		->The init parameter can be set in "web.xml" for a particular servlet

				or 

		getContextParameter().getAttribute("customerDetails")	->The context parameter can be set for the entrire application across multiple servlets
		


In JSP
--------					
			
		<%= request.getParameter("custName")%> 

				or

		<%=pageContext.request.queryString%> 
		


In JSP (with core / sql tag library)
-------------------------------------

		<c:set var="custName" value="${param.custName}" />  

				or

		<c:set var="custName" value="${initParam.custName}" />
				
				or

		<c:set var="custName" value="${customerDetails}" />

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------			










How to use if or Choose...when in JSP core tag
====================================================

Logic to be implemented:- 

	 If customer name is submitted as user input, then Print the customer name, 
	 Else, Ask the user to provide customer name



If condition
------------

	<c:if test="${!empty param.custName}">

            		<c:out value="${param.custName}" /> 
        
	</c:if>

	<c:otherwise>
		
    			Please provide the customer name </br>	

        </c:otherwise>


Choose .. When
--------------

	<c-rt:choose>

        	<c-rt:when test="${!empty param.custName}">

    			Welcome <c-rt:out value="${param.custName}" />. 

        	</c-rt:when>

        	<c-rt:otherwise>
		
    			Please provide your name </br>	

        	</c-rt:otherwise>

	</c-rt:choose>

coditional checking
----------------------
	<c:if test="${!empty customerEdited}">     		(Checking non empty variable)

 	<c:if test="${customerEdited.equals('yes')}">		(checking the variable's string value)

	<c:if test="${customerID == 1}">			(checking the variable's integer value)

	<c:if test="${numberOfStudents >= 40}">			(comparing the variable's integer value)




----------------------------------------------------------------------------------------------------------------------------------------------------------------------














What is EJB and How it Works
=============================

1. First, the users input some data through a Form (index.html) or in a URL query string and submits to the Servlet for processing.

2. The servlet captures the user inputs through request.getParameter("<userInputName>"), processes the inputs and sends response to the client (browser)

3. If there is any business logic to be processed, then then servlet uses the EJB session bean to perform the business logic by invoking its services/methods 

4. Examples of EJB session bean to add two numbers accepted as user inputs
   -----------------------------------------------------------------------------
	AddNumbers.java 
		- contains the private attributes (relevant to the user Inputs-> i.e first Number, second number)
		- has public constructor 
		- jas getter-setter method for all the attributes
		- has a method "addNumbers()" to implement business logic (->add two numbers and assign the result to another attribute)
		

	
5. In the servlet class, Inject the EJB container 
								Code:-
									@EJB           

 			 Instantiate the EJB bean   
								Code:-
									AddNumbers addObj; 			
							
7. Now the Servlet can use the EJB bean object("addObj") to invoke the required method "addNumbers()" for addition of two numbers 					

8. For that, you have to first set relevant EJB bean attributes with the respective FORM inputs (already captured by servlet) through setter  method.

9. The servlet can fetch the add result(stored in a EJB bean attribute) through getter method and  print it to browser screen.	 

	Note:-
		Here, instead of EJB bean, We could have created a simple bean "AddNumbers" and instantiated it in normal way like 
		-> AddNumbers addObj = new AddNumbers()
		and used its method "addNumbers()" in the servlet. it would still work.
				
		But the issue will arise when we come across a  distributed system. 
				(where, the servlet might be in a server situated at one location and the simple bean might be in a machine at different location)
				In this scenario, the servlet can't recognize the simple bean "AddNumbers.java".
				So we have to handle this issue by creating EJB bean.
				Since the EJB bean is created inside the EJB container, it can be accessed from a servlet (irrespective of its machine location) 	

10. System requirements:
	You need the ejb jar file ("javax.ejb-3.1.2.2.jar") to be added to the Project library
 	But in our case, the Glassfish server (which is already installed), contains the ejb libraries. So no need to separately add the ejb jar file to the project.

11. In the servlet class, you have to import the ejb APIs to avail the functionality of EJB(Enterprise Java Beans)

								Code:- 
									import javax.ejb.*;


Example of EJB session bean to handle database operation (fetch/insert/update/delete data from the Database table)
--------------------------------------------------------------------------------------------------------------------

CustomerFacade.java
		- inherits the abstract class - "AbstractFacade.java", which actually performs all the database operations using the JPA functionalities
    		
		- operates on the database table "customer" through the entity bean - "Customer.java" 

		- Sine the entity bean is created in the Persistent Provider(JPA),      		
		  the session bean has to inject the Persistence Unit to use the functionalities of "EntityManager" component of JPA, which reads the ORM meta data for 													  an entity and performs persistence operations on the database 
			
			Inject the Persistence Unit 
       								Code:- 		
									@PersistenceContext(unitName = "<ProjectName>_PU")
			
			Instantiate the EntityManager component of JPA
								
								Code:- 
									private EntityManager em; 

		- since the session beans extends an abstracts class "AbstractFacade.java", so it has to implement the abstract method "getEntityManager()" of the 		  parent class by overriding it and it has to return an EntityManager object ("em")
									
								Code:- 
									@Override
    									protected EntityManager getEntityManager() {
        									return em;
    									}

			

		- The EJB session bean doesn't have its own methods. 
		  It inherits the database operation methods (create()/edit()/remove()/find()/findAll()....)  from its Parent Class("AbstractFacade.java")
		  
		- To convey the parent class that it wants findAll() operation on the "Customer" entity bean,
	 	   the session bean invokes the constructor of the parent abstract class inside its own constructor 
				    and pass the entity bean (Customer.class) as an argument 
				    so that the parent class's constructor will set the value of its own attribure "entityClass" as Customer.class
								
								Code:-	
									public CustomerFacade() {
        									super(Customer.class);
    									}
		
			
			
AbstractFacade.java
		- The Abstract class contains:
			- a private attribute "entityClass" which is of type Class<T>
								
								Code:-
									private Class<T> entityClass;
			
			- a constructor which sets the value of its attribute "entityClass" as its argument value.
												
								Code:-
									public AbstractFacade(Class<T> entityClass) {
        									this.entityClass = entityClass;
    									}

								So when it is invoked inside the constructor of the session bean through super(Customer.class), 
								it sets value of its attribute "entityClass" as "Customer.class"

			- an abstract method "getEntityManager()" which has a "EntityManager" return type 

			- the methods(create()/edit()/remove()/find()/findAll()....) which use the "getEntityManager()" to perform various database operation
			  

			- For example, the above basic database operation methods are implemented like this:

								Code:-
									//select all records from the table
									public List<T> findAll() {
        										cq = getEntityManager().getCriteriaBuilder().createQuery();
        										cq.select(cq.from(entityClass));
        										return getEntityManager().createQuery(cq).getResultList();
									}

									//Add a new record
									public void create(T entity) {
        										getEntityManager().persist(entity);
    									}
									
									//Modify an existing record
    									public void edit(T entity) {
        										getEntityManager().merge(entity);
    									}
									
									//delete a record
    									public void remove(T entity) {
        										getEntityManager().remove(getEntityManager().merge(entity));
    									}

			- since the "getEntityManager()" abstract method is of type "EntityManager",  			   hence  "getEntityManager()" method automatically gets access to the EntityManager class's methods such as 
													- createQuery() / persist() / merge() / remove() ...... 
			

	
		- The Abstract class has to import the Persistence APIs to avail the functionality of JPA
								Code:-	
									import javax.persistence.*;
									import javax.persistence.EntityManager;
	



In the servlet class, 
		Sine the session bean is created in the EJB container,     		
		  the servlet has to inject the EJB container to use the functionalities of EJB 
			
			Inject the EJB container 
								Code:- 
									@EJB           

 			Instantiate the EJB bean   
								Code:-
									CustomerFacade customerFacade;	

		Now the Servlet can use the EJB session bean object("customerFacade") 
								to invoke the required method "findAll()" for retrieving all the records from the customer table
								and assign the return value to a application-scoped variable which can be used later for display
								
								Code:-
									getServletContext().setAttribute("customerDetails",customerFacade.findAll());
			

		
		
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------









How to create a WAR file from the Web application
===================================================
NetBeans IDE > Right click your project > Click "Clean and Build" 
The war file "<Project name>.war" will be created under the "dist" folder of your app
This war file is ready for deployment.

OR
If it is a maven - web application Project, 
Right click the project > Custom > Goals > Type "install"  
The war file "<Project name>.war" will be created under the "target" folder of your app
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------










How to deploy Web application in a remote server:
=================================================						
Create a Web application in local development environment (using netbeans)
Access the webapplication developed in Glassfish application server of local machine through URL:
				http://localhost:8080/WebApplicationProject1
Create the WAR/EAR file in your local development environment (using Netbeans ID) - "WebApplicationProject1.WAR"
Put the WAR/EAR file in the remote server (using SSH)

Open the Glassfish Application server admin console in the remote server (http://<IP address of the remote server>:4848)
Deploy web application > select the WAR/EAR file ("WebApplicationProject1.WAR") to deploy
Finish
The Web application will now run (hosted) in the remote server.
Access the Web applicaion through the URL:
				http://<IP address of the remote server>:8080/WebApplicationProject1
--------------------------------------------------------------------------------------------------------------------------------------------------------------		













Serialization and Externalization
====================================
if a class implements Serializable interface, it will serialize (write an object to an output stream) all the variables in the object 

Unlike Serializable interface, Externalizable interface is not a marker interface and it provides two methods - "writeExternal" and "readExternal"
In case of Externalization, you have to explicitly mention what fields or variables you want to serialize 
Ex:- 	When you write the "Car" object to the OutputStream, the "writeExternal" method is called and the data is persisted. 
	when you read the "Car" object from the ObjectInputStream, "readExternal" method is called and the object (its state) is retrieved.
--------------------------------------------------------------------------------------------------------------------------------------------------------------			







What are the differet Java Persistence Providers (JPA)
=======================================================

JPA  provides Data Persisitence in a distributed application (Persisting the entity beans to the Database)

The followings are some of the Persistence Providers :

1) ECLIPSELINK

	Download the following JAR files
			
				org.eclipse.persistence.jpa.jpql_2.5.2.v20140319-9ad6abd.jar		(Provides Java Persisitence solution through the APIs)

				org.eclipse.persistence.jpa.modelgen_2.5.2.v20140319-9ad6abd.jar	(Provides Java Persisitence solution through the APIs)	

				javax.persistence_2.1.0.v201304241213.jar				(Provides Java Persisitence solution through the APIs)

	Add the above jars to the Project's library (lib folder)
	
			D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\<ProjectName>\lib

	Note:- 
	The NetBeans IDE already has ECLIPSELINK integrated with it. So you dont need to download or put the JARs in the lib folder


2) HIBERNATE JPA











How to produce server logs for the appication on Run Time
=================================================================

The followings are some of the logging solutions, available which can be used for creating customized server logs to keep a track on the application's execution.

1) ECLIPSELINK

2) LOG4J & LOG4JDBC

3) APACHE-COMMON-LOGGING


    


1) ECLIPSELINK (Provides SERVER-logs during APPLICATION RUNTIME and writes to a LOG FILE or CONSOLE or a DATABASE TABLE)
   _______________________________________________________________________________________________________________________________________________________________

   Implement eclipselink in a Java / Web Application
   -------------------------------------------------
   1. Download the following JAR file:
				
				eclipselink.jar		->(Provides loggings solution )

   2. Add the above jars to the Project's library (lib folder)
	
			D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\<ProjectName>\lib
	
	Note:- 
	The NetBeans IDE already has ECLIPSELINK integrated with it. So you dont need to download or put the JARs in the lib folder

   3. All the Persistence  and logging related configuration details are provided in an xml file - persistence.xml

	persistence.xml :
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
	
	<persistence version="2.1" xmlns="http://xmlns.jcp.org/xml/ns/persistence" 
				   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 										   				   xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/persistence http://xmlns.jcp.org/xml/ns/persistence/persistence_2_1.xsd">

  		<persistence-unit name="<ProjectName>_PU" transaction-type="JTA">

			<provider>org.eclipse.persistence.jpa.PersistenceProvider</provider>
    
			<jta-data-source>jdbc/myTestDataSource</jta-data-source>
    
    			<exclude-unlisted-classes>false</exclude-unlisted-classes>
    		
			<properties>
      				<property name="eclipselink.logging.level" value="FINEST"/>
    			</properties>

  		</persistence-unit>

	</persistence>

	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

	Note:-
	Other logging solutions such as "Log4J" and "Apache common logging" can be also integrated with EclipseLink by

		1. Implementing your own SessionLog

		2. Configuring the use of your SessionLog

	


2) LOG4J and LOG4JDBC - (Provides server logs  during APPLICATION RUNTIME and writes to a LOG FILE or CONSOLE or a DATABASE TABLE)
   ______________________________________________________________________________________________________________________________________________________________

   Implement Log4J in a Java application
   --------------------------------------
   1. Download the following JAR files:
				log4j-1.2.17.jar 	(provides all types of logs except sql logs)

				log4jdbc-1.2.jar  	(provides sql logs)

				slf4j-api-1.7.5.jar	(supporting JAR for log4jdbc)

				slf4j-log4j12-1.7.5.jar (supporting JAR for log4jdbc)
   
	Note:- 
		If there is no Database operations involved, then you need only the LOG4J JAR file (log4j-1.2.17.jar ) to provide the application logs
	  	If there is database operation involved, then you also need the LOG4JDBC JAR files (log4jdbc-1.2.jar, slf4j-api-1.7.5.jar, slf4j-log4j12-1.7.5.jar )

   2. Add the above jars to the Project's librarry
	
	NetBeans IDE - Right Click the Project > Properties > libraries > ADD JAR > select required JAR file(s) > OK

	Now the JAR files will appear in the
		NetBeans IDE <project tab> / <project name> / libraries 
	
	
   3. Create "log4j.properties" file 
	Right click source > new > other > properties file > select the folder 
		"D:\Sambit\NetBeansProjects\JavaApplications_Repository\<JavaApplicationProject Name>"					
	
   The properties file will be added to the Project

   4. All the configurations regarding logging must be declared in the properties file "log4j.properties" or in an XML mile "log4j.xml"

	There are five different levels of logging: ALL / DEBUG / INFO / WARN / ERROR / FATAL

	Note:- If the <logging level> is set as "DEBUG", then the logs of all levels ("DEBUG" level or higher than DEBUG) will be written to the log file / console.
	       If the <logging level> is set as "INFO", then the logs of all levels ("INFO" level or higher than INFO) will be written to the log file / console.

	log4j.properties (Log4J configuration file) :
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
	#The Logger gathers the logs, then gets it to the appender and then the appender prints out the information to a LOG FILE or CONSOLE or a DATABASE TABLE


	#Root Logger option
	#log4j.rootLogger=<logging level>, <Appender1>, <Appender1>, <Appender1>, .....

		or

	#log4j.logger.<appname>logger=<logging level>, <Appender1>, <Appender1>, <Appender1>, .....

	

	log4j.rootLogger=DEBUG, fileOut, fileErrorOut, consoleOut, dbTableOut
										#DEBUG is the logging level (This will produce logs- "DEBUG" level or higher)
										#fileOut  - the name of the appender used for writing the logs to a FILE
										#fileErrorOut - the appender used for writing only the ERROR logs to a FILE 
										#consoleOut   - the appender used for writing the logs to CONSOLE
										#dbTableOut   - the appender used for writing the logs to a DATABASE TABLE
										#sqlConsoleOut- the appender used for writing SQL logs to CONSOLE
							
 

	#fileOut Appender writes all types of logging level(DEBUG, INFO, WARN, ERROR, FATAL) informations to a LOG FILE

	log4j.appender.file=org.apache.log4j.RollingFileAppender 					(defines the type of the appender, here it is a Rolling File)
	log4j.appender.file.File=D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<ProjectName>.log	(defines the path of the appender)
	log4j.appender.file.MaxFileSize=10MB								(defines the maximum size of the appender)
	log4j.appender.file.MaxBackupIndex=10								(Archive log files -maximum number of backup files)
	log4j.appender.file.layout=org.apache.log4j.PatternLayout					(defines the layout of the appender)
	log4j.appender.file.layout.ConversionPattern=%d{yyyy-MM-dd} %5p [%t] (%F:%L) - %m%n		(defines the layout pattern-<file name>, <line no.>, <time>.. )


	#fileErrorOut Appender writes only the ERROR information to a LOG FILE

	log4j.appender.fileErrorOut=org.apache.log4j.RollingFileAppender 				(defines the type of the appender, here it is a Rolling File)
	log4j.appender.fileErrorOut.threshhold=ERROR							(makes the loggings restricted to only Error level)
	log4j.appender.fileErrorOut.File=D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<ProjectName>Error.log	(defines the path of the appender)
	log4j.appender.fileErrorOut.MaxFileSize=10MB							(defines the maximum size of the appender)
	log4j.appender.fileErrorOut.MaxBackupIndex=10							(Archive log files -maximum number of backup files)
	log4j.appender.fileErrorOut.layout=org.apache.log4j.PatternLayout				(defines the layout of the appender)
	log4j.appender.fileErrorOut.layout.ConversionPattern=%d{yyyy-MM-dd} %5p [%t] (%F:%L) - %m%n	(defines the layout pattern-<file name>, <line no.>, <time>.. )



	#### consoleOut Appender writes all types of logging level(DEBUG, INFO, WARN, ERROR, FATAL) informations to CONSOLE

	log4j.appender.consoleOut=org.apache.log4j.ConsoleAppender					(defines the type of the appender, here it is console)
	log4j.appender.consoleOut.layout=org.apache.log4j.PatternLayout					(defines the layout of the appender)
	log4j.appender.consoleOut.layout.ConversionPattern=%d{yyyy-MM-dd} %-5p [%t] (%F:%L) - %m%n	(defines the layout pattern-<file name>, <line no.>, <time>.. )



	#### dbTableOut Appender writes the error-log to a DATABASE TABLE (You have to create a "LOGS" table in tha "mytestschema" database)
	
	log4j.appender.dbTableOut=org.apache.log4j.jdbc.JDBCAppender					(defines the type of the appender, here it is a Database Table)
	log4j.appender.dbTableOut.URL=jdbc:mysql://localhost:3306/mytestschema				(defines the database name)
	log4j.appender.dbTableOut.driver=com.mysql.jdbc.Driver						(defines the database driver)					
	log4j.appender.dbTableOut.user=root								(defines the user credential to access the Database)
	log4j.appender.dbTableOut.password=nbuser							(defines the password)
	log4j.appender.dbTableOut.sql=INSERT INTO LOGS VALUES ('%x', now() ,'%C','%p','%m')		(defines the fields in the LOGS table)
	log4j.appender.dbTableOut.layout=org.apache.log4j.PatternLayout					(defines the layout pattern-<file name>, <line no.>, <time>.. )
	

	#### set the log4jdbc properties

	log4j.logger.jdbc.sqlonly=DEBUG,LOg4JDBC 	
	log4j.logger.jdbc.sqltiming=DEBUG,LOg4JDBC	
	log4j.logger.jdbc.audit=OFF
	log4j.logger.jdbc.resultset=ERROR,LOg4JDBC 	
	log4j.logger.jdbc.connection=ERROR,LOg4JDBC 	
	log4j.logger.jdbc.resultsettable=ON

	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

   



	log4j.xml (Log4J configuration file) :
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
	
	<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
		
		<logger name="dev">
			<level value="info"/>
		</logger>
		
		<logger name="org.apache.log4j">
			<level value="debug"/>
		</logger>
		
		<logger name="org.eclipse.persistence">
			<level value="debug"/>
		</logger>
		
		
		<root>
			<level value="debug"/>
			<appender-ref ref="fileOut"/>
			<appender-ref ref="fileErrorOut"/>
			<appender-ref ref="consoleOut"/>
			<appender-ref ref="dbTableOut"/>
		</root>

		<appender name="fileOut" class="org.apache.log4j.RollingFileAppender">
			<param name="File" value="D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<ProjectName>.log"/>
			<param name="MaxFileSize" value="10000KB"/>
			<param name="MaxBackupIndex" value="5"/>
			<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%d{yyyy-MM-dd} %p [%t] - %m%n"/>
			</layout>
		</appender>

		<appender name="fileErrorOut" class="org.apache.log4j.RollingFileAppender">
			<param name="File" value="D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<ProjectName>_Error.log"/>
			<param name="MaxFileSize" value="10000KB"/>
			<param name="MaxBackupIndex" value="5"/>
			<param name="Threshold" value="error"/>
			<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%d{yyyy-MM-dd} %p [%t] - %m%n"/>
			</layout>
		</appender>

		<appender name="consoleOut" class="org.apache.log4j.ConsoleAppender">
			<param name="Threshold" value="debug"/>
			<layout class="org.apache.log4j.PatternLayout">
			<param name="ConversionPattern" value="%d{yyyy-MM-dd} %p [%t] - %m%n"/>
			</layout>
		</appender>
	

	</log4j:configuration>

	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%



   5. If database operations are involved in the application, then log4jdbc will provide the sql logs
		
			change the JDBC driver and JDBC connection string throughout the project.
		
			com.mysql.jdbc.Driver 			to 		net.sf.log4jdbc.DriverSpy 
			jdbc:mysql://localhost:3306/test 	to 		jdbc:log4jdbc:mysql://localhost:3306/mytestschema


   6. Import the Logger and PropertyConfigurator in the application class
			
			Code:- 
				import org.apache.log4j.Logger;
				import org.apache.log4j.PropertyConfigurator;
	
   7. Create a logger object inside the class:
			
			Code:- 
				final static Logger logger = Logger.getLogger(<classname>.class);

   8. Inside the the main() method, configure the properties file

			Code:- 
				PropertyConfigurator.configure("log4j.properties");

   9. Inside the main() method, Use the logger object to print specific information to the log file

			Code:- 
				logger.info("successful");

   10. If you think a particular job execution may give error at run time, then you can put that part in the try block and catch the error through logger.error
			Code :- 
				try{
                   
                    			new ReadFromFile("D:/myTestFile.txt");     // a file is being read by invoking the constructor of the class "ReadFromFile"
                		}
				catch(Exception e){
                    			logger.error("Error while Reading from the File"+e.getMessage());	// Error is captured and printed to the log file
                		}

   11. Run the application

	A log file "<ProjectName>.log"      will be created under the folder D:\Sambit\NetBeansProjects\SERVER_LOGS_UsingLog4J
	A log file "<ProjectName>Error.log" will be created under the folder D:\Sambit\NetBeansProjects\SERVER_LOGS_UsingLog4J 


	

   Implement Log4J in a Web Application
   ----------------------------------------
   1. Download the following JAR files:
				log4j-1.2.17.jar 
				log4jdbc-1.2.jar  
				slf4j-api-1.7.5.jar
				slf4j-log4j12-1.7.5.jar
   
	Note:- 
		If there is no Database operations involved, then you need only the LOG4J JAR file (log4j-1.2.17.jar ) to provide the application logs
	  	If there is database operation involved, then you also need the LOG4JDBC JAR files (log4jdbc-1.2.jar, slf4j-api-1.7.5.jar, slf4j-log4j12-1.7.5.jar )

   2. Add the following jars to the Project's librarry
	
	NetBeans IDE - Right Click the Project > Properties > libraries > ADD JAR > select required JAR file(s) > OK

	Now the JAR files will appear in the
		NetBeans IDE <project tab> / <project name> / libraries 
	
	and also appear in the folder
		D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\WebAppProject6_ControllerServlet_WithDBConnection_UsingEJB-Transaction\build\web\WEB-INF\lib

	Also put the jar files in the glassfish library folder-
							C:\Program Files\glassfish-4.1\glassfish\domains\domain1\lib\
			
   3. Create "log4j.properties" file 
	Right click source > new > other > properties file > select the folder 
		
		"D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\<WebApplicationProject Name>\web\WEB-INF" 			

	The properties file will be added to the Project


   4. All the configurations regarding logging must be declared in the properties file "log4j.properties" or in an XML mile "log4j.xml"
	
	There are five different levels of logging: ALL / DEBUG / INFO / WARN / ERROR / FATAL

	Note:- If the <logging level> is set as "DEBUG", then the logs of all levels ("DEBUG" level or higher than DEBUG) will be written to the log file / console.
	       If the <logging level> is set as "INFO", then the logs of all levels ("INFO" level or higher than INFO) will be written to the log file / console.

	log4j.properties:
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
	#The Logger gathers the logs, then gets it to the appender and then the appender prints out the information to a LOG FILE or CONSOLE or a DATABASE TABLE


	#Root Logger option
	#log4j.rootLogger=<logging level>, <Appender1>, <Appender1>, <Appender1>, .....
	#log4j.logger.<appname>logger=logging level>, <Appender1>, <Appender1>, <Appender1>, .....

	log4j.rootLogger=DEBUG, fileOut, fileErrorOut, consoleOut, dbTableOut
										#DEBUG is the logging level (This will produce logs- "DEBUG" level or higher)
										#fileOut  - the name of the appender used for writing the logs to a FILE
										#fileErrorOut - the appender used for writing only the ERROR logs to a FILE 
										#consoleOut   - the appender used for writing the logs to CONSOLE
										#dbTableOut   - the appender used for writing the logs to a DATABASE TABLE
										#sqlConsoleOut- the appender used for writing SQL logs to CONSOLE
	#### set the log4jdbc properties

	log4j.logger.jdbc.sqlonly=DEBUG,LOg4JDBC 	
	log4j.logger.jdbc.sqltiming=DEBUG,LOg4JDBC	
	log4j.logger.jdbc.audit=OFF
	log4j.logger.jdbc.resultset=ERROR,LOg4JDBC 	
	log4j.logger.jdbc.connection=ERROR,LOg4JDBC 	
	log4j.logger.jdbc.resultsettable=ON
	#-Dlog4jdbc.debug.stack.prefix=myservetpackage							(defines from what level you want to capture the SQL execution)
											
 

	#fileOut Appender writes all types of logging level(DEBUG, INFO, WARN, ERROR, FATAL) informations to a LOG FILE

	log4j.appender.file=org.apache.log4j.RollingFileAppender 					(defines the type of the appender, here it is a Rolling File)
	log4j.appender.file.File=D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<appName>.log	(defines the path of the appender)
	log4j.appender.file.MaxFileSize=10MB								(defines the maximum size of the appender)
	log4j.appender.file.MaxBackupIndex=10								(Archive log files -maximum number of backup files)
	log4j.appender.file.layout=org.apache.log4j.PatternLayout					(defines the layout of the appender)
	log4j.appender.file.layout.ConversionPattern=%d{yyyy-MM-dd} %5p [%t] (%F:%L) - %m%n		(defines the layout pattern-<file name>, <line no.>, <time>.. )


	#fileErrorOut Appender writes only the ERROR information to a log file

	log4j.appender.fileErrorOut=org.apache.log4j.RollingFileAppender 				(defines the type of the appender, here it is a Rolling File)
	log4j.appender.fileErrorOut.threshhold=ERROR							(makes the loggings restricted to only Error level)
	log4j.appender.fileErrorOut.File=D:\\Sambit\\NetBeansProjects\\SERVER_LOGS_UsingLog4J\\<appName>Error.log	(defines the path of the appender)
	log4j.appender.fileErrorOut.MaxFileSize=10MB							(defines the maximum size of the appender)
	log4j.appender.fileErrorOut.MaxBackupIndex=10							(Archive log files -maximum number of backup files)
	log4j.appender.fileErrorOut.layout=org.apache.log4j.PatternLayout				(defines the layout of the appender)
	log4j.appender.fileErrorOut.layout.ConversionPattern=%d{yyyy-MM-dd} %5p [%t] (%F:%L) - %m%n	(defines the layout pattern-<file name>, <line no.>, <time>.. )



	#### consoleOut Appender writes all types of logging level(DEBUG, INFO, WARN, ERROR, FATAL) informations to CONSOLE

	log4j.appender.consoleOut=org.apache.log4j.ConsoleAppender					(defines the type of the appender, here it is console)
	log4j.appender.consoleOut.layout=org.apache.log4j.PatternLayout					(defines the layout of the appender)
	log4j.appender.consoleOut.layout.ConversionPattern=%d{yyyy-MM-dd} %-5p [%t] (%F:%L) - %m%n	(defines the layout pattern-<file name>, <line no.>, <time>.. )



	#### dbTableOut Appender writes the error-log to a DATABASE TABLE (You have to create a "LOGS" table in tha "mytestschema" database)
	
	log4j.appender.dbTableOut=org.apache.log4j.jdbc.JDBCAppender					(defines the type of the appender, here it is a Database Table)
	log4j.appender.dbTableOut.URL=jdbc:mysql://localhost:3306/mytestschema				(defines the database name)
	log4j.appender.dbTableOut.driver=com.mysql.jdbc.Driver						(defines the database driver)					
	log4j.appender.dbTableOut.user=root								(defines the user credential to access the Database)
	log4j.appender.dbTableOut.password=nbuser							(defines the password)
	log4j.appender.dbTableOut.sql=INSERT INTO LOGS VALUES ('%x', now() ,'%C','%p','%m')		(defines the fields in the LOGS table)
	log4j.appender.dbTableOut.layout=org.apache.log4j.PatternLayout					(defines the layout pattern-<file name>, <line no.>, <time>.. )
	%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

   5. If database operations are involved in the application, then changes the JDBC driver and JDBC connection string wherever it is mentioned.
		
			com.mysql.jdbc.Driver 			to 		net.sf.log4jdbc.DriverSpy 
			jdbc:mysql://localhost:3306/test 	to 		jdbc:log4jdbc:mysql://localhost:3306/mytestschema

   6. Import the Logger and PropertyConfigurator in the servlet class
			Code:- 
				import org.apache.log4j.Logger;
				import org.apache.log4j.PropertyConfigurator;
	
   7. Create a logger object inside the servlet class- 

			final static Logger logger = Logger.getLogger(<classname>.class);

   8. In the web.xml, Define how the servlet will locate properties file 

			Code:-
				<servlet>
        				<servlet-name>HelloWebServlet</servlet-name>
        				<servlet-class>myServletPackage.HelloWebServlet</servlet-class>
        					<init-param>
            						<param-name>log4j-init-file</param-name>
            						<param-value>WEB-INF/log4j.properties</param-value>
        					</init-param>
    				</servlet>

	
   9. Configure the properties file in the Servlet's init() or doGet() or doPost() depending on the requirement:

		PropertyConfigurator.configure(<dynamic path of the properties file>); 
		
		
		Note:- The build process will copy the properties file from <project directory>\Web\WEB-INF to  <project directory>\build\web\WEB-INF
			So in the servlet, the path of the properties file must be
			D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\WebAppProject3_SimpleServlet_WithDBConnection_UsingJDBC-SQLQuery\build\web\WEB-INF\
																		       log4j.properties	
		Replace <path of the properties file> with (prefixPath + initFilePath) 

			prefixPath =  getServletContext().getRealPath("/");    
									       (D:\Sambit\NetBeansProjects\JavaWebApplication_Repository										   					\WebAppProject3_SimpleServlet_WithDBConnection_UsingJDBC-SQLQuery\build\web\)
	        	
			initFilePath = getInitParameter("log4j-init-file");  //refers"web.xml", picks corresponding value of "<param-name>log4j-init-file</param-name>"
									       (WEB-INF/log4j.properties) 
		

   10. Inside the doGet() / doPost() method, Use the logger object to print specific information to the log file
			Example Code:-
				logger.info("the passed query string customer name = "+ customer_name);
            			logger.debug("query string to print out:"+ customer_name);


   11. If you think a particular job execution may give error at run time, then you can put that part in the try block and catch the error through logger.error
			Example Code :- 
				try{
                   
                    			rs = ps.executeQuery();   ;     // JDBC query executed through the PreparedStatement and assigned to a Resultset object
                		}
				catch(SQLException sqle){
                    			logger.error("Error while executing query"+sqle.getMessage());	// Error is captured and printed to the log file
                		}

   12. Run the application
	
	A log file "<Project name>.log"  will be created under the folder D:\Sambit\NetBeansProjectsLOG4J\SERVER_LOGS_UsingLog4J
	A log file "<Project name>Error.log" will be created under the folder D:\Sambit\NetBeansProjectsLOG4J\SERVER_LOGS_UsingLog4J 
-----------------------------------------------------------------------------------------------------------------------------------------------------------------













Creating Maven Projects in NetBeans
======================================
Maven projet is based on a Project Object Model("pom.xml") which contains information about the project and configuration details/dependencies used by Maven to build the project.
if the project uses any external functionality (Ex:- JunitTest), You dont have to separately download the dependency jar files (Junit.jar).
Maven takes care of downloading the necessary dependency files and the dependency is automatically added in the "pom.xml".
				Code :-
					<dependencies>
        					<dependency>
            						<groupId>junit</groupId>
            						<artifactId>junit</artifactId>
            						<version>4.10</version>
            						<scope>test</scope>
        					</dependency>
    					</dependencies>

Maven will package the application to JAR (if it is a Java Application project)
				   to WAR (if it is a Java Web Application project)
				Code :-
					<packaging>jar</packaging>
						or
					<packaging>war</packaging>


1. File > New Project > Maven > Java Application
				Project Name:-		Maven-JavaApplicationProject1		
				Project Location :-	D:\Sambit\NetBeansProjects\MavenProjects_Repository\JavaApplicationProjects 	
				Project Folder :-	D:\Sambit\NetBeansProjects\MavenProjects_Repository\JavaApplicationProjects\Maven-JavaApplicationProject1
				Artifact ID :-		Maven-JavaApplicationProject1  (same as project name)
				Group ID :-		com.sambit		
				version :-		1.0-SNAPSHOT 	("1.0-SNAPSHOT" for development stage. it will be "1.0" for Production-release stage)
				Package :- 		com.sambit.maven.mytestPackage

2. Add a Student class ("Student.java") file to the project 
3. Run the File(Project) -> Right click the project > Run

	OR

   Complile the Project -> Right click the project > Custom > Goals > Type "compile"
				While compiling the project, maven will first download all the dependencies declared in the "pom.xml" file and then build the project.
	
	OR

   Create a JAR file out of the project -> Right click the project > Custom > Goals > Type "install"  (It will create a JAR file in the "target" folder)
										
	OR
	
   Create a Junit Test for the Project -> Right click the project > new > others > unit test > JUnit Test
				Test Class name :- 	StudentTest
				package name :- 	com.sambit.maven.mytestPackageForJUnitTest
			
				A test class(StudentTest.java) will be created under the Test Packages- com.sambit.maven.mytestPackageForJUnitTest
				You will see there is a new dependency declaration for the JUnitTest added in he "pom.xml" file 
				(maven automatically downloads the respective jar file- "Junit-4.10.jar")
--------------------------------------------------------------------------------------------------------------------------------------------------------------		















Github commands
=============================

Steps to remove directory from githun repository
----------------------------------------------------
git rm -r --cached FolderName
git commit -m "Removed folder from repository"
git push origin master
















Managing Projects (file versioning) in GITHUB 
=============================================================


Creating a Repository in Github and cloning the repository to local computer (folder)
-------------------------------------------------------------------------------------
1. Open Gibhub  https://github.com (mynamesahu / sks1234)
2. Create a repository "JavaWebApplication_Repository" in Github (Add ReadMe file)
3. Clone the repository to local folder
 				In NetBeans IDE-> Team > Remote > Clone > 
								Git Repository Location: https://github.com/mynamesahu/JavaWebApplication_Repository.git
								    (Open the repository in Github page  > Click the "Clone/Download" button > copy the URL ans paste)
								usename - mynamesahu
								password - sks1234
								Destination Folder - D:\Sambit\NetBeansProjects\JavaWebApplication_Repository
								Select remote branches - "Master"
								Destination Parent Directory - D:\Sambit\NetBeansProjects\
								Clone Name - JavaWebApplication_Repository
				> Clone completed
				  A new folder "JavaWebApplication_Repository" is created under D:\Sambit\NetBeansProjects\

4. Creating a Project under the Repository (locally using NetBeans IDE)

								
				> Dialogbox - Do you want to create an IDE project from the cloned sources?
				> Click "Create Project"
					Project Name - WebAppProject7
					Project Location - D:\Sambit\NetBeansProjects\JavaWebApplication_Repository
					Project Folder - D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\WebAppProject7
				  A new Project "WebAppProject7" appears under the Project tab of NetBeans IDE
				  A new folder "WebAppProject7" is created under the folder - D:\Sambit\NetBeansProjects\JavaWebApplication_Repository
						
							

5. Create any File(s) under the Project (locally using NetBeans IDE)

				> Create a JSP file - "employeeDetails.jsp" in the Project "WebAppProject7"
					



6. Commit the changes to the Files(Add file/Modify File and Delete file) in Local folder

				> commit the changes (add/modify a file-"employeeDetails.jsp") by right clicking the project > Git > Commit



7. Push the changes to the remote github repository


				> Push the changes(add/modify a file-"employeeDetails.jsp") by right clicking the project > Git > remote > push 
																	remote name: origin
																        branch name: master
				> Verify the Github Page now
				  A new Project "WebAppProject7" will appear under the repository "JavaWebApplication_Repository"
				  A new file "employeeDetails.jsp" will appear under the Project "WebAppProject7"							    

Creating a New Project in an existing Github repository
------------------------------------------------------------

1. Create a Netbeans Project under a folder D:\Sambit\
	NetBeans IDE > New > Project > web app project > Project Name : TestWebAppProject

2. The Project is created under  D:\Sambit\TestWebAppProject

3. Now Move the TestWebAppProject folder to D:\Sambit\NetBeansProjects\JavaWebApplication_Repository

4. NetBeans IDE -> 
	Right click the Project > commit
	Right click the Project > remote > push 
					   (Specify the Git repository location : https://github.com/mynamesahu/JavaWebApplication_Repository.git)

5. The new Project is now added to the existing "JavaWebApplication_Repository" repository




Making an already existing Netbeans project as a Github repository project
---------------------------------------------------------------------------

If there is a project already existing in Netbeans (D:\Sambit\NetBeansProjects\WebAppProject1) and not in Github repository, 
You can push the Project to the Github repository by following steps:

Move the existing folder D:\Sambit\NetBeansProjects\WebAppProject1 to some other location (D:\WebAppProject1) 
The project will disappear from the NetBeans Project Tab.



1. Open Gibhub  https://github.com (mynamesahu / sks1234)
2. Create a repository "JavaWebApplication_Repository" in Github (Add ReadMe file)
3. Clone the repository to local folder
 				In NetBeans IDE-> Team > Remote > Clone > 
								Git Repository Location: https://github.com/mynamesahu/JavaWebApplication_Repository.git
								    (Open the repository in Github page  > Click the "Clone/Download" button > copy the URL ans paste)
								usename - mynamesahu
								password - sks1234
								Destination Folder - D:\Sambit\NetBeansProjects\JavaWebApplication_Repository
								Select remote branches - "Master"
								Destination Parent Directory - D:\Sambit\NetBeansProjects\
								Clone Name - JavaWebApplication_Repository
				> Clone completed
				  A new folder "JavaWebApplication_Repository" is created under D:\Sambit\NetBeansProjects\

4. Now move the existing Project from (D:\WebAppProject1) 
  			to the newly created folder (D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\WebAppProject1)


5. Open the Project in NetBeans

			NetBeans IDE -> File > "Open Project" 
				> Browse to the folder "D:\Sambit\NetBeansProjects\JavaWebApplication_Repository\WebAppProject1"
				> Select the Project
				> Open the Project

				 A new Project "WebAppProject1" appears under the Project tab of NetBeans IDE


6. Commit the new project in Local folder

				> right clicking the project > Git > Commit



7. Push the project to the remote github repository

				> right clicking the project > Git > remote > push
				> Verify the Github Page now
				A new Project "WebAppProject1" will appear under the repository "JavaWebApplication_Repository"
											    

Checking out a File :-
--------------------------
If more than one person are working on the same file, then the file should be checked out first by one person.
Once the file is checkout, it will be locked => others can't work on that file
After the work on the file is completed, the file must be checked in 
Then commit the changes (add/modify file) to the local repository
Then Push the changes to the remote GITHUB repository
----------------------------------------------------------------------------------------------------------------------------------------------------------------------
















How to push your Git repository to an external server
======================================================
<To be written>











HOW TO CONFIGURE MYSQL DATABASE SERVER and CREATE A DATABASE INSTANCE / SCHEMA
=================================================================================
1. Create a Web Application Project in NetBeans IDE
		Project folder path - C:\Sambit\NetBeansProject\<ProjectName>

2. Install MySQL Server

		Download MySQL server ZIP file
		Unzip the ZIP file to a folder 
						D:\Sambit\NetBeansProjects\MySQL

		Add the mysql commands to your PATH (environment variable)
						
						set Path  D:\Sambit\NetBeansProjects\MySQL\bin\
3. Check if the MySQL Server is Running
	
	
	Open a command-line prompt window:

		C:\>mysqld			(start server) 
	
		C:\> mysqladmin ping
			 
		    output:- mysqld is alive	(server is running)



		C:\> mysqladmin shutdown	(shut down the server)


	Change the "root" account Password

		C:\> mysql -u root
		mysql> UPDATE mysql.user SET Password = PASSWORD('nbuser') WHERE User = 'root';
 		mysql> FLUSH PRIVILEGES;


		
										
4. Register MySQL server in NetBeans IDE

		NetBeans IDE -> services Tab -> Right click Databases > Register MySQL Server >

		MySQL server properties window opens
		
		Set the Basic Properties:
		
					host name : 		localhost
					port number:		3306
					Admin user name:	root
					Admin password:		nbuser
		
		MYSQL server is now registered in the NetBeans IDE.
		
		Note:-
		The Glassfish application server requires an appropriate driver to enable communication between your Java program and the the MySQL database. 
		So You need to download the MySQl server driver (jar file -"mysql-connector-java-5.1.41-bin.jar") and put in the Glassfish server library (lib folder)

		The good is, the NetBenas IDE already contains the MySQL(Connector/J) driver, so you do not need to download it. 
		
		You need to just Enable JDBC driver deployment in the Glassfish server settings, so that the driver will be automatically deployed to GlassFish server.

			NetBens IDE -> Services Tab -> Servers -> 
							Right Click GlassfisgServer 4.1 > Properties > Enable JDBC Driver Deployment

5. Configure the NetBeans IDE to START / STOP the MySQL server 

		NetBeans IDE -> services Tab -> Databases > Right Click MySQL server > Properties
		
		MySQL server properties window opens
		
		Set the Admin Properties:
					
					Path/URL to Admin Tool : D:\Sambit\NetBeansProjects\MySQL\bin\mysqladmin.exe
					Path to start command:	 D:\Sambit\NetBeansProjects\MySQL\bin\mysqld.exe
					Path to stop command:	 D:\Sambit\NetBeansProjects\MySQL\bin\mysqladmin.exe
								 					(Arguments : -u root -p nbuser shutdown)

6. Create a Database Instance
		
		Right click the MySQL Server node > Create Database.

				New Database Name : 	mytestschema
				Grant Full Access To : 	root@localhost 		(=>root account on the localhost host has full access the "mytestschema" database)
 
		A new database instance "mytestschema" is created under a link 
							jdbc:mysql://localhost:3306/mytestschema [root on Default schema]
		

					You can create tables under this database instance

						mytestschema > Right click Tables > Create Table
		
		Note:-
			"mytestschema" database is created in the MySQL server which runs on 		port 3306 of localhost
			"myTestPool" Connectionpool is created in the Glassfish server which runs on 	port 4848 of local host
					
			So you have to provide "root user" credentials to the connection pool so that the glassfish server can access the "mytestschema" database. 


		
	Alternatively, You can create database schema using MySQL Work bench (which is a GUI based tool to create tables and ERD diagram and generate DDL script)	
		

Creating Database schema using MySQL Work bench
--------------------------------------------------------

1. Open MySQL Work bench 

		Download MySQL workbench 
		Install MySQL workbench

2. Create a schema - "mytestschema"
	
		File > New Model > Click the plus(+) icon located to the upper right corner 
		Name of schema - mytestschema
		collation -	utf8-utf8_unicode_ci
		Save to a file under C:\Sambit\NetBeansProject\<ProjectName>\mytestschema.mwb
		Schema is created.
 		
		"mytestschema" will automatically get created under MYSQL server


3. Open an empty ERD Diagram canvas in the schema

		Click Model > Create Diagram from Catalog Objects.

		A new EER Diagram opens displaying an empty canvas. 


4. create entities in the ERD diagram (relation between the entities)

		Click the New Table icon located in the left margin > select the mytestschema from the dropdown box > hover your mouse onto the canvas > click again. 

		A new entity displays on the canvas 

		In the catalog tree, the new table will appear under mytestschema \ table1 (default table name)

		
		Double Click the table > 

		The entity editor opens

		Specify the followings :
					Name: 		customer		(name of the entity)
					Engine: 	InnoDB			(The InnoDB engine provides foreign key support) 
					Comments: 	xxxxxxx

		Save the changes
				File > save Model

 		In the catalog tree, the table will be modified to mytestschema \ customer 
		
		The newly created entity is now "customer"


5. Create Properties for the entity

		Now that you've added entity to the canvas, you need to specify their properties (columns in a database table).

		
		In the Table editor ->  Double Click the first row below propery headings  > Add following details for the first property of "student" enity:

					Column Name- 		stud_id
					Data Type- 		INT
					Checkbox select:  	PK		   NN		UN		AI  			
							      (Primary Key)  	(Not Null)   (Unsigned)	    (Auto Increment) 
											   
										
					 
					Double Click the second row  > Add following details for the second property of the "student" entity:

					Column Name- 		stud_name
					Data Type- 		VARCHAR
					Checkbox select:  	NN 

					
					Double Click the third row  > Add following details for the third property of the "student" entity:

					Column Name- 		stud_address
					Data Type- 		VARCHAR
					Checkbox select:  	NN 

					
					Double Click the fourth row  > Add following details for the fourth property of the "student" entity:

					Column Name- 		stud_DOB
					Data Type- 		DATE
					Checkbox select:  	NN 

					and so on ......

		Close the Table Editor window to view the table clearly on the canvas

		To resize the table for  all columns to be visible on the canvas
					choose Arrange > Reset Object Size 

 
		To view the Table indexes
					Click the Indexes row  

		Save the changes.

6. Repeat steps 4 and 5 for creating each new entity and their peoperties


7. Generate DDL script by forward Engineering
	
		File > Export > Forward Engineer SQL CREATE Scipt (Ctrl+Shift+G) > 
							Output SQL script file path : 	D:\Sambit\NetBeansProjects\<ProjectName>\
							file name 	       	    :	mytestschema_DDLscript.sql 


			      > Next

			      > In the SQL Object Export Filter window, select checkbox for "Export My SQL Table Objects" 

			      > Finish

		The DDL script is created 
				C:\Sambit\NetBeansProjects\<ProjectName>\mytestschema_DDLscript.sql 


8. Create a Database schema on MySQL Database from the ERD (by running the DDL script)


	Run the DDL script in the MY SQL Database server

		NetBeans IDE -> Services Tab -> MySQL server > Right click any existing schema > connect

						The link jdbc:mysql://localhost:3306/<any existing schema name> [root on Default schema] appears

						Right click the link > Execute command > copy the content of the DDL script and paste in the script execution window
						
						> Run SQL
		
		"mytestschema" will be created under MySQL server
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------








Adding the database driver's JAR file to the server:-
======================================================
Adding the database driver's JAR file is vital to enable the glassfish application server to communicate with your database. 

The NetBeans IDE's server management is able to detect (at the time of deployment) whether the JAR file has been added to the application server or not.
If not, it does so automatically ( by enabling JDBC Driver Deployment option)
1. Choose Tools > Servers to open the Servers manager. 
2. Select the GlassFish server in the left pane.
3. In the main pane, select the Enable JDBC Driver Deployment option. 
If the option is enabled, it initiates a check to determine whether any drivers are required for the server's deployed applications. 
In the case of MySQL, if the driver is required and it is missing, the NetBeans IDE's bundled driver (C:\Program Files\NetBeans 8.0.2\ide\modules\ext\)is deployed to the appropriate location(library folder-C:\Program Files\glassfish-4.1\glassfish\domains\domain1\lib\) on the Glassfish server.


Alternatively, You can manually add the JDBC driver to the Glassfish application server.
1. Find the JAR file(mysql-connector-java-5.1.41-bin.jar) in the DB driver's installation directory OR download the file from 													"http:/dev.mysql.com/downloads/connector/j"
2. Then Copy the JAR file into the library folder of Glassfish application server -> C:\Program Files\glassfish-4.1\glassfish\domains\domain1\lib\

-------------------------------------------------------------------------------------------------------------------------------------------------------












Setting up Data Source and Connection Pool for a Database
=============================================================

***************************************
Through Glassfish Server Console:
***************************************

You can set up the Data-source and Connection-Pool for a database directly within the GlassFish server Admin Console (http://localhost:4848).

Console Page > Resources > JDBC > JDBC Connection Pools
			Create a new connection-pool ("myTestPool")  

				Resource Type - 	 "javax.sql.ConnectionPool DataSource"
				Data Source Class Name - "com.mysql.jdbc.jdbc2.optional.MysqlDataSource"
				and define the access to the "mytestschema" database by setting the Additional Properties:  
								driver=		"com.mysql.jdbc.Driver"
                						url=		"jdbc:mysql://localhost:3306/mytestschema"
                						user=		"root"  
                						password=	"nbuser"
								
				If you want to use LOG4JDBC for SQL error logging, then use this
								DriverClass= 	"net.sf.log4jdbc.sql.jdbcapi.DriverSpy"
								driver=		"net.sf.log4jdbc.DriverSpy" 
								url=		"jdbc:log4jdbc:mysql://localhost:3306/mytestschema"
								user=		"root"  
                						password=	"nbuser"
									

Console Page > Resources > JDBC > JDBC Resources
			Create a new data-source (set JNDI name as "jdbc/myTestDataSource") and associate with the connection pool "myTestPool"
		 

OR

*********************************
Through NetBeans IDE:
*********************************

You can declare the resources(Data-source and Connection-Pool) by creating an entry in the "glassfish-resources.xml" or "sun-resources.xml" file. 
In NetBeans IDE - File > New File > Choose Category "Glassfish" 	
						> Choose File Type "JDBC Resource"  
						> select "Create New JDBC Connection Pool" 
					      	> set JNDI Name as "jdbc/myTestDaSource" 
					      	> set JDBC connection pool name as "myTestPool"
						> Choose "extract from existing connection" - "jdbc:mysql://localhost:3306/mytestschema"
						> set Dasource classname as "com.mysql.jdbc.jdbc2.optional.MysqlDataSource"
						> set Resource type as "javax.sql.ConnectionPoolDataSource" 
						> Finish
A new file - "glassfish-resources.xml" or "sun-resources.xml" will be generated with an entry for JDBC resources (Data-source and Connection-pool) details.
/Server Resources/ glassfish-resources.xml
OR
/Server Resources/ sun-resources.xml

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
<resources>																			
  <jdbc-resource enabled="true" jndi-name="jdbc/myTestDataSource" object-type="user" pool-name="myTestPool">									<description>access the "mytestschema" database</description>
  </jdbc-resource>

  <jdbc-connection-pool name="myTestPool" datasource-classname="com.mysql.jdbc.jdbc2.optional.MysqlDataSource" res-type="javax.sql.ConnectionPoolDataSource">
	<property name="URL" value="jdbc:mysql://localhost:3306/mytestschema?zeroDateTimeBehavior=convertToNull"/>
    	<property name="User" value="root"/>
    	<property name="Password" value="nbuser"/>
  </jdbc-connection-pool>
</resources>
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
If you want more than one datasources("jdbc/myTestDataSource", "jdbc/myTestDataSource2", "jdbc/myTestDataSource3") to access the same database("mytestschema"), 
then you can do this by by editing the "sun-resources.xml" file - add more <jdbc-resource> entries pointing to the same <jdbc-connection-pool name="myTestPool"> entry.

When the web-application is deployed, the Glassfish server reads the resource declarations from this "sun-resources.xml" file and creates the necessary resources(DataSource-"myTestDataSource"  and Connection Pool-"myTestPool") in the Glassfish server. 

You don�t have to create �sun-resources.xml� file again and again for different web application projects in the same local Glassfish server as the necessary JDBC resources (ConnectionPool -�myTestPool�and DataSource -�myTestDataSource�)  are  already created in the Glassfish server.  
The files �sun-resources.xml�  and  �web.xml�  are needed to be bundled in the WAR/EAR file if the application needs to be deployed in a remote server.


(Refer the document "Setting up JDBC Resources (DataSource, ConnectionPool) in Glassfish server.doc")
--------------------------------------------------------------------------------------------------------------------------------------------------------------------














Accessing a database from JSP / Servlet:
========================================

Case:1 (JSP) - Refer WebAppProject7
-------------------------------------
If you don't want to create an entry in the "web.xml" file to refer to the data-source("jdbc/myTestDataSource"), then you have to access the "mytestschema" database directly from the JSP file as follows:
		
		<%@taglib prefix="sql"  uri="http://java.sun.com/jsp/jstl/sql" %>  		--> should be at the beginning of the JSP file
		
		<sql:setDataSource  var=	"myDataSource" 
                        			driver=	"com.mysql.jdbc.Driver"
                        			url=	"jdbc:mysql://localhost:3306/mytestschema"
                        			user=	"root"  
                        			password="nbuser"
		/>


		Now you can operate on the "mytestschema" database by mentioning the datasource name in JSTL-SQL query as follows:
		
		<sql:query var="customerResult" dataSource="${myDataSource}">
			SELECT * FROM customer
		</sql:query>


Case:2 (JSP and web.xml) -  Refer WebAppProject1 
-------------------------------------------------
After setting up the data source and connection pool for the database("mytestschema"), you the need to instruct the application to use the data source("jdbc/myTestDataSource"). This can be done by creating an entry in the application's  deployment descriptor ("web.xml").

		<resource-ref>
        		<description>to access the mytestschema database</description>
        		<res-ref-name>jdbc/myTestDataSource</res-ref-name>
        		<res-type>javax.sql.ConnectionPoolDataSource</res-type>
        		<res-auth>Container</res-auth>
        		<res-sharing-scope>Shareable</res-sharing-scope>
   		</resource-ref>


				

		So in the JSP page, you need not define the database access details.
		You can directly operate on the "mytestschema" database just by mentioning the datasource name in JSTL-SQL query as follows:
		
		<%@taglib prefix="sql"  uri="http://java.sun.com/jsp/jstl/sql" %>  		--> should be at the beginning of the JSP file
		
		<sql:query var="customerResult" dataSource="jdbc/myTestDataSource">
            		SELECT * FROM customer
        	</sql:query>



Case:3 (Servlet) - Refer WebAppProject3
-------------------------------------------
If you don't want to create an entry in the "web.xml" file to refer to the data-source("jdbc/myTestDataSource"), then you can the access the database directly from the servlet by registering the JDBC driver and opening a connection to the database through the DriverManager as follows:

		/* --------------JDBC driver name and database URL for MYSQL dabase server-------------------*/
    			static final String JDBC_DRIVER="com.mysql.jdbc.Driver";
    			static final String DB_URL="jdbc:mysql://localhost:3306/mytestschema";
		/*---------------------------------------------------------------------------------------*/
    
		/*---------------Database credentials---------------------------------------------------------*/
    			static final String USERNAME = "root";
    			static final String PASSWORD = "nbuser";
		/*---------------------------------------------------------------------------------------*/




		/* --------JDBC driver name and database URL for Oracle database server------------------*/
    			//static final String JDBC_DRIVER="oracle.jdbc.driver.OracleDriver";
    			//static final String DB_URL="jdbc:oracle:thin:@localhost:1521:mytestschema";
    
    			//static final String USERNAME = "system";
    			//static final String PASSWORD = "oracle";
		/*---------------------------------------------------------------------------------------*/    

		Connection conn =null;
        	//Statement stmt = null;
        	PreparedStatement ps = null;
        	ResultSet rs = null;
        	String sql = "";

		Class.forName(JDBC_DRIVER);                                     // Register JDBC driver
                conn = DriverManager.getConnection(DB_URL, USERNAME, PASSWORD); // Open a connection
                
                sql = "SELECT * FROM customer";
		//String sql = "SELECT cust_name, cust_address FROM customer WHERE cust_name=?";
                
                
		//stmt = conn.createStatement();                                // create a Statement object                             
                //rs = stmt.executeQuery(sql);                                  // Execute SQL query through Statement object


		
               										
                ps = conn.prepareStatement(sql);                                // create a PreparedStatement object
		//ps.setString(1, req.getParameter("customerName"));  		// Set the input parameter in the Prepared statement					
                rs = ps.executeQuery();                                         // Execute SQL query through PreparedStatement object

										Note:- sql query with "?" for a input parameter(s), if the requested URL is 
											(http://localhost:8080/<ProjectName>/Hello?customerName=Sirish) 

                // Extract data from result set
                while(rs.next()){
                   
                    	//Retrieve by column name
                    	int id  	= rs.getInt("cust_id");
                    	String custName = rs.getString("cust_name");
                  
                    	//Display values
                    	out.println(" Customer ID: " + id + "<br>");
                    	out.println(" Customer Name: " + custName + "<br>");
                    	out.println("<br>");
                }
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
		



















################################# END USEFUL HINTS ###############################################################################################




















################################################## My JAVA WEB APPLICATIOn PROJECTS Created in Net Beans##############################################################




*************************************************************************************************************************
WebAppProject1 (Simple JSP Page with DB operation using JDBC Datasource and JSTL SQL-Query)
-----------------------------------------------------------------------------------------------

/Server Resources/ 
	sun-resources.xml 	- defines the connection pool / jdbc data source details for the database "mytestschema"
				   It can be done through the Glassfish application server-console (localhost:4848) or from the NetBeans IDE


/WEB-IBF/
	web.xml 		- After setting up the data source and connection pool for the database "mytestschema", you then need to instruct the application to  				  	  use the data source("jdbc/mytestDataSource"). It can be done by creating an entry in the application's web.xml deployment descriptor.
				
				  	Note:- You can edit the web.xml directly or through the "servlet" tab of the graphical interface of web.xml


/DisplayRecords/
	testDataSource.jsp  	- displays the customer table data through "DB Report" 
	testDataSource2.jsp  	- displays the customer table data through "DB Query Database" and "JSTL for Each"


/InsertOrUpdateRecords/
	customerForm.jsp  	- Give a reference to the database "mytestschema" directly in the JSP file to get access to the database 
												(You don't have to refer the web.xml file's resource reference entry)

					Code:-
						 <sql:setDataSource  var="myDataSource" 
                            				driver="com.mysql.jdbc.Driver"
                            				url="jdbc:mysql://localhost:3306/mytestschema"
                            				user="root"  
                            				password="nbuser"/>	
        					 	
				- inserts recods in the customer table through JSTL SQL-Query ( ""DB Insert Database"") using the datasouce variable "myDataSource"
				  

Run the jsp page in NetBeans 	-> right click the JSPt file --> Run






*************************************************************************************************************************
WebAppProject2 (simple servlet without DB operation)
-------------------------------------------------------------------
					
/WEB-INF/
	web.xml 		- describes the servlet (TestControllerServlet)'s URL pattern (/testHello)

/myServletPackage/
	ServletWithoutDBConnection.java	
				- a simple servlet to accept the incoming request and displays the session information 
					
					=> the sevlet will be invoked only when the url has a pattern (that ends with "/testHello")

Invoke the servlet 		in NetBeans -> right click the servlet file --> Run
				or 
				in the Browser -> enter the URL (http://localhost:8080/<Project Name>/testHello)








*******************************************************************************************
WebAppProject3 (simple servlet with DB operation using JDBC data source and JDBC query)
-------------------------------------------------------------------------------------------

/Server Resources/ 
	sun-resources.xml 	- defines the connection pool / jdbc data source details for the database "mytestschema"
				   It can be done through the Glassfish application server-console (localhost:4848) or from the NetBeans IDE

/libraries/
	log4j-1.2.17				
	log4jdbc-1.2.jar
	slf4j-api-1.7.5.jar
	slf4j-log4j12-1.7.5.jar - these jar files should also be added to glassfish library folder(C:\Program Files\glassfish-4.1\glassfish\domains\domain1\lib)  
				  This enables the application to recognize the log4jdbc driver in order to print the SQL related loggings to the CONSOLE / a LOG FILE

/WEB-INF/
	lo4j.properties 	- this defines the log4j LOGGER properties for the APPENDER to print the SQL related loggings to the CONSOLE / a LOG FILE


/WEB-INF/
	web.xml 		- After setting up the data source and connection pool for the database "mytestschema", you then need to instruct the application to  				  	  use the data source("jdbc/mytestDataSource"). It can be done by creating an entry in the application's web.xml deployment descriptor.
				
				  	Note:- You can edit the web.xml directly or through the "servlet" tab of the graphical interface of web.xml
				
				- describes the servlets' URL pattern "/testJDBCQuery" or "/hello"
				
				- the properties file will be read by the servlet(ServletwithDBConnection) through the <init param ..> reference 
				   Code:-
					<init-param>
            					<param-name>log4j-init-file</param-name>
            					<param-value>WEB-INF/log4j.properties</param-value>
        				</init-param>

/myServletPackage/
	ServletwithDBConnection.java	
				- a servlet to accept the incoming request and displays the database result (the databas in this example; 
							the database is "mytestschema"
							The database URL is "jdbc:mysql://localhost:3306/mytestschema"
					        	The database driver is "com.mysql.jdbc.Driver"
					
					  => the sevlet will be invoked only when the url has a pattern (that ends with "/testJDBCQuery")
/myServletPackage/
	HelloWebServlet.java	
				- a servlet to accept the incoming request with an input query string and displays only those records which match the querystring 
							the database is "mytestschema"
							The database URL is "jdbc:mysql://localhost:3306/mytestschema"
					        	The database driver is "com.mysql.jdbc.Driver"
					
					  => the sevlet will be invoked only when the url has a pattern (that ends with "/hello?Sambit Sahu")

Invoke the servlet 		in NetBeans -> right click the servlet file --> Run
				or 
				in the Browser -> enter URL (http://localhost:8080/<Project Name>/testJDBCQuery) or (http://localhost:8080/<Project Name>/hello)









**************************************************************************************************************************************************
WebAppProject4 (controller Servlet (that forwards the request to the appropriate view) with DB operation using JDBC Datasource and JSTL SQL-Query)
---------------------------------------------------------------------------------------------------------------------------------------------------

/Server Resources/ 
	sun-resources.xml 	- defines the connection pool / jdbc data source details for the database "mytestschema"
				   It can be done through the Glassfish application server-console (localhost:4848) or from the NetBeans IDE



/WEB-INF/
	web.xml 		- describes the servlet (TestControllerServlet)'s URL pattern (/welcome,/customer)
				- After setting up the data source and connection pool for the database "mytestschema", you then need to instruct the application to  				  	  use the data source("jdbc/mytestDataSource"). It can be done by creating an entry in the application's web.xml deployment descriptor.
				
				  	Note:- You can edit the web.xml directly or through the "servlet" tab of the graphical interface of web.xml



/controller/
	ControllerServletUsingJDBCDataSource.java 
				- servlet to accept the incoming requests and forward to the appropriate jsp page (view) depending on the path value
					=> the sevlet will be invoked only when the url has a pattern (that ends with "/welcome" or "/customer")
					
				  	if path="/welcome"  then forward the request to the "welcome.jsp" page		(using "getRequestDispatcher()" method )
				  	if path="/customer" then forward the request to the "customerDetails.jsp" page	(using "getRequestDispatcher()" method )
	
				  								Ex: request.getRequestDispatcher(url).forward(request, response)
													where url = "/WEB-INF/view" + path + ".jsp"
					      	      							path = request.getServletPath()
/WEB-INF/view/
	welcome.jsp  		- displays the welcome page having a link to the "customerDetails.jsp" page 																		(href="http://localhost:8080/TestWebAppProject2/customer")
	customerDetails.jsp  	- displays the customer table data through "DB Query Database" and "JSTL for Each"



Invoke the servlet 		in NetBeans -> right click the servlet file --> Run
				or 
				in the Browser -> enter the URL (http://localhost:8080/<Project Name>/welcome)






*************************************************************************************************************************
WebAppProject5 (Servlet invoking EJB without DB operation)
-------------------------------------------------------------------

web pages/
	index.xml		- helps the user to enter input data and sumbits the inputs to the servlet for processing the request and respond to the user with data

/WEB-INF/
	web.xml 		- defines the servlets' URL pattern(Ex:- "/testEJBWithFormInput" or "/tesEJB" or "/testInvokeSimpleBean" or "/testInvokeSimpleClass") 
				  Note:- You can edit the web.xml directly or through the "servlet" tab of the graphical interface of web.xml

/myServletPackage/
	ServletAcceptingFormInputsAndInvokingEJBBeanForHandlingBusinessLogic.java	
				- servlet injects the EJB container which instantiates the EJB bean(/myEJBBeanPackage/AddNumbers.java)to handle the business logic  								=> the sevlet will be invoked only when the url has a pattern (that ends with "/testEJBWithFormInput")
				
				We are not doing any business logic operation in this servlet.
				The business logic is performed in the EJB bean and we will just use the EJB bean object("addObj") to invoke the "addNumbers()" method.  				For that, you have to first set relevant EJB bean attributes with the respective FORM inputs through setter  method.
				and then the servlet fetches the add result(stored in a EJB bean attribute) through getter method and  print to browser screen.	


	ServletInvokingEJBBean.java	
				- a servlet injects the EJB container which instantiates the EJB bean(/myEJBBeanPackage/GreetCustomer.java)to handle the business logic  								=> the sevlet will be invoked only when the url has a pattern (that ends with "/testEJB")
				
				We are not doing any business logic operation in this servlet.
				The business logic is performed in the EJB bean and we will just use the EJB bean object("greetCust") to invoke the "sayHello()" method 
				For that, you have to first set the relevant EJB bean attributes with the respective FORM inputs through setter  method 
				and then the servlet fetches the add result(stored in a EJB bean attribute) through getter method print to browser screen.		

	ServletInvokingSimpleBean.java
				- a servlet instantiates a simple bean(/mySimpleBeanPackage/GreetCustomer.java) to handle the business logic  												=> the sevlet will be invoked only when the url has a pattern (that ends with "/testInvokeSimpleBean")
	ServletInvokingSimpleJavaClass.java
				- a servlet instantiates a simple class(/mySimpleClassPackage/GreetCustomer.java) to perform some task through its method  										=> the sevlet will be invoked only when the url has a pattern (that ends with "/testInvokeSimpleClass")



/myEJBBeanPackage/
	AddNumbers.java		
				- a EJB session bean which handles the business logic when gets invoked from the servet 													   (gFormInputsAndInvokingEJBBeanForHandlingBusinessLogic.java)
				  This can be reusable in some other Project or distributed system
				  
					Code :-
						 @EJB                		(Injects the EJB) 
    						 AddNumbers addObj;       	(Here, actually the EJB container instantiates the EJB bean)
										
				Note:-
				Here, instead of EJB bean, We could have created a simple bean "AddNumbers" and instantiated it in normal way like 
							AddNumbers addObj = new AddNumbers() and used its method "addNumbers()" in the servlet. it would still work.
				
				but the issue will arise in the scenario of distributed system. 
				(where, the servlet might be in a server situated at one location and the simple bean might be in a machine at different location)
				In this scenario, the servlet can't invoke the simple bean "AddNumbers".
				So we have to handle this issue by creating EJB bean.
				Since the EJB bean is created inside the EJB container, it can be accessed from a servlet (the server at any location) 	by invoking the 				EJB bean after injecting the EJB. 






	GreetCustomer.java		
				- a EJB session bean which handles the business logic when gets invoked from the servet (ServletInvokingEJBBean.java)
				  This can be reusable in some other Project or distributed system
				  
					Code :-
						 @EJB                		(Injects the EJB) 
    						 GreetCustomer greetCust;       (Here, actually the EJB container instantiates the EJB bean)
										
				Note:-
				Here, instead of EJB bean, We could have created a normal java class "GreetCustomer" and instantiated it in normal way like 
							GreetCustomer bean = new GreetCustomer() and used its method "sayHello()" in the servlet. it would still work.
				
				but the issue will arise in the scenario of distributed system 
				(the servlet is in a server situated at one location and the java class  or a simple bean might be in a machine at different location)
				In this scenario, the servlet can't invoke the simple java class "GreetCustomer".
				So we have to handle this issue by creating EJB bean.
				Since the EJB bean is created inside the EJB container, it can be accessed from a servlet (the server at any location) 	by invoking the 				EJB bean after injecting the EJB. 

/mySimpleBeanPackage/
	GreetCustomer.java		
				- a simple bean which handles the business logic when gets instantiated  from the servet (ServletInvokingSimpleBean.java)
				  This can be reusable in some other Project in the same machine.
				  
/mySimpleClassPackage/
	GreetCustomer.java		
				- a simple class instantiated  from the servlet (ServletInvokingSimpleJavaClass.java) to perform some task through the class's method 
				  

/myBeanPackage/
	BeanToGreetCustomerTest.java	
				- an JUnit test class that tests the MyTestBean class with some test data
				  Right click the MytestBean.java --> "Create/Update Test" --> Junit test --> OK --> MyTestBeanTest.java is created
				  
				  If you want to unit-test the method "sayHello(String customerName)",
				  then inside the "testSayHello()" method of this test class,  
				  Assign a test data ("Sambit") to the variable 'customerName', which is actually a parameter to the mehod sayHello()  
														(code:- String customerName = "Sambit";)
				  Invoke the sayHello() method through the EJB container-instance and store the retuned value in a variable -"actualResult"
				  What is the expected return value of sayHello() method with that test data? Store that value in a vatiable -"expResult"
				  Compare the two values -->  If expResult is equal to actualResult, then the test is passed.

				  Run the test by right clicking the MyTestBeanTest.java --> Click Run 


Invoke the servlet 		in NetBeans -> right click the servlet file --> Run
				or 
				in the Browser -> enter the URL (http://localhost:8080/<Project Name>//testEJBWithFormInput)
									or
								(http://localhost:8080/<Project Name>/testEJB)
									or
								(http://localhost:8080/<Project Name>/testInvokeSimpleBean)
									or
								(http://localhost:8080/<Project Name>/testInvokeSimpleClass)









********************************************************************************************************************************************
WebAppProject6 (controller Servlet invoking EJB session beans and using JDBC Datasource and EJB JTA to operate on DB through entity beans)
--------------------------------------------------------------------------------------------------------------------------------------------

/Server Resources/ 
	sun-resources.xml 	- defines the connection pool / jdbc data source details for the database "mytestschema"
				   It can be done through the Glassfish application server-console (localhost:4848) or from the NetBeans IDE


/WEB-INF/
	web.xml 		- No need to decribes jdbc data source to connect to the "mysqlschema" database as it is defined in "persistence.xml"
				- describes the servlet (TestControllerServlet)'s URL pattern (/welcome,/customer)
				
				  	Note:- You can edit the web.xml directly or through the "servlet" tab of the graphical interface of web.xml



/configuration Files/
	persistence.xml		- Describes the Persistence Unit configuration for the JTA transactions
				  Java Transaction API (JTA) specifies standard Java interfaces between a transaction manager and application server,involved in a 				  	  distributed transaction system
				
				  code:- <persistence-unit name="TestWebAppProject5_ControllerServlet_Using_EJB_forDBtransaction_PU" transaction-type="JTA">
					 <jta-data-source>jdbc/myTestDataSource</jta-data-source>
					 <properties>
						<property name="eclipselink.logging.level" value="FINEST"/>
    					 </properties>
					
					 Note:- EclipseLink (JPA 2.1) is the Persistence Provider as default



/controller/
	ControllerServletInvokingEJBSessionBean.java 
				- servlet to accept the incoming requests and forward to the appropriate jsp page (view) depending on the path value
					=> the sevlet will be invoked only when the url has a pattern (that ends with "/welcome" or "/customer")
					
				  	if path="/welcome" then forward to the "welcome.jsp" page		(using "getRequestDispatcher()" method )
				  	if path="/customer" then forward to the "customerDetails.jsp" page	(using "getRequestDispatcher()" method )
	
				  								Ex: request.getRequestDispatcher(url).forward(request, response)
													where url = "/WEB-INF/view" + path + ".jsp"
					      	      							path = request.getServletPath()

					Query the database for all records of Customer entity by using findAll() functionality of EntityManager 
        				through invoking the "CustomerFacade" session bean and stores the Resultset (List of Customer objects) in a variable 							"customerDetails", which is placed in the ServletContext (=> application-scoped variable) that can be accessed by any JSP page
						
						Code:-	private CustomerFacade customerFacade;
							init(){
								getServletContext().setAttribute("CustomerDetails",customerFacade.findAll());
							}



/entityBeans/
	Customer.java 		- This class is a EJB entity bean which persists its data to the Database table "customer" by implementing 'Serializable' interface.
 
  				- All the attributes of the "Customer" entity class map to the relevant fields of the "customer" table of the relational database
  				  => ORM (Object Relational Mapping)
		



/sessionBeans/
	AbstractFacade.java 	- This class - "AbstractFacade.java" defines all the functionalities/services of the EntityManager component of JPA  
				  

	CustomerFacade.java 	- This class- "customeFacade.java" is a  EJB 'stateless' session bean that implements the business logic
				  and operates on the database table (entity bean - "Customer.java") using the functionalities of "EntityManager" component of JPA 
      				  through inheritance from the class - "AbstractFacade.java"

      				  (Note:- The servlet (or client) can instantiate this EJB session bean later to avail the services / functionalities of the EJB) 


/WEB-INF/view/
	welcome.jsp  		- displays the welcome page having a link to the "customerDetails.jsp" page 																		(href="http://localhost:8080/TestWebAppProject2/customer")
	customerDetails.jsp  	- displays the customer table data through  "JSTL for Each"
					  Collection:  ${customerDetails} -> application scoped variable "customerDetails" is defined in the controller servlet's 									     context parameter.
									     this is the Resultset (List) of all customer records of the "Customer" entity class 					   

					code:-	<c:forEach var="customer" items="${customerDetails}">    
        						<div>
            							<c:out value="${customer.custName}" /> 
        						</div>
    						</c:forEach>


Invoke the servlet 		in NetBeans -> right click the servlet file --> Run
				or 
				in the Browser -> enter the URL (http://localhost:8080/<Project Name>/welcome)















#################################################### My JAVA APPLICATIOn PROJECTS created in Net Beans ##############################################################


JavaApplicationProject1
------------------------------------------------

/libraries/
	log4j-1.2.17				
	log4jdbc-1.2.jar
	slf4j-api-1.7.5.jar
	slf4j-log4j12-1.7.5.jar -  Added these jar files to the library which enable the application to to print developer-customized logs to the CONSOLE / a LOG FILE

package - serializationTest
   		
		- Student.java	
				- Student object that implements Serializable interface 	
		- Persisit.java		
				- Perists the state of the Student object to a file (converts the object to byte stream and write it to a file("testFile.txt")
	  	- DePersisit.java	
				- Deprsists the state of the object from the file (reads the byte stream from the file and convert it back to Student object)
	



JavaApplicationProject2 (Junit Test Example)
------------------------------------------------
package - junitTestExample
   		
		- Customer.java		
				- a java class having a method sayHello(String customerName)
				

package - junitTestExample
		- CustomerTest.java
				           
				- an JUnit test class that tests the Customer class with some test data
				  Right click the Customer.java --> "Create/Update Test" --> Junit test --> OK --> CustomerTest.java is created

				  If you want to unit-test the method "sayHello()",
				  then inside the "testSayHello()" method of this test class,  
				  Assign a test data ("Sambit") to the variable 'customerName', which is actually a parameter to the mehod sayHello()  
														(code:- String customerName = "Sambit";)
				  Invoke the sayHello() method through the Customer class-instance and store the returned value in a variable -"actualResult"
				  What is the expected return value of sayHello() method with that test data? Store that value in a vatiable -"expResult"
				  Compare the two values -->  If expResult is equal to actualResult, then the test is passed.

				  Run the test by right clicking the CustomerTest.java --> Click Run 
					 				             
					  
	
		











################################################## MAVEN PROJECTS ##############################################################


*************************************************************************************************************************
Maven-JavaApplicationProject1 (Simple Java Application with Maven)
-----------------------------------------------------------------------------------------------

Source package 
	-> com.sambit.maven.mytestPackage
   		
		- Student.java	
				- Student class 	



Test Package 
	-> com.sambit.maven.mytestPackageForJUnitTest

		- StudentTest.java
				- Test Class

Test Dependencies 
		- junit-4.10.jar	
				- automatically added when a new Junit test class is created in the Project
		- hamcrest-core-1.1.jar	
				- automatically added when a new Junit test class is created in the Project

				
Project Files	- pom.xml	
				- Project Object Model (has information about the project and configuration details/dependencies, used by Maven to build the project)
				  While compiling the project, maven will first download all the dependencies declared in the "pom.xml" file and then build the project				















#################################################### CREATING DATABASE SCHEMA   ##############################################################



**********************************************************************************************************************
MyTestShema.mwb - 	
			Database schema generated using SQL Work bench and saved as a file - 
	      			(D:\Sambit\NetBeansProject\MyTestShema.mwb)
              		
			You can open the particular schema just by double clicking the schema file





**********************************************************************************************************************

MyTestSchema_DDLscript.sql - 
			The script file was generated from the schema by forward engineering and saved as a file 
				(D:\Sambit\NetBeansProject\MyTestSchema_DDLscript.sql)

			This script content can be copied and run as a script in the MY SQL database server,registered in NetBeans IDE,
			to generate the database ("mytestschema") and also the tables with their relationship inside the database.


















                
