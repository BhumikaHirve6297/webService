# Web-Service 
Web-Service is framework for making ease in website creation.
# Install
Download the jar and place it in the ../WEB-INF/lib folder of your web application.
# Usage
for security check a class must be created which implements interface named as SecureInterface ,and should override the methods :
```python
public void setSecure()
{
//code 
}
public Boolean isSecure()
{
// code
return true/false;
}
```
For using the framework given annotation must be applied to the class,and the url request should be in the form -
In case of json:-
URL:application_name/Service/student/kite
where,
 /student:-belongs to the class for which request is given,
 /kite:-belogs to method of the class 
In case of file Uploading:-
URL:application_name/Upload/student/kite
where,
 /student:-belongs to the class for which request is given,
 /kite:-belogs to method of the class 
Example:
```python
@Path(key="/student")
public class Student
{
@ReturnType(key="html/text")
@Forward(key="/student/mate") //forward to another service
@Secure(key="com.thinking.machines.Safe.class") //name of the class which implements SecureInterface
@Path(key="/kite")
public String getStudent(StudentBean s,HttpSession httpSession,HttpServletRequest request )
{
//code
}
@ReturnType(key="html/text")
@Forward(key="/Students.jsp")
@Secure(key="com.thinking.machines.Safe.class")
@Path(key="/mate")
public String getResult(String record)
{
//code
return " result...";
}
@ReturnType(key="NOTHING")
@Forward(key="/Students.jsp")
@Secure(key="com.thinking.machines.Safe.class")
@Path(key="/fileupload")
@Multifile
public void fileToUpload(File[] files)
{
//code
}
}
```
Following code should be placed in the WEB-INF folder of your web-application
between <web-app> tag.
```python
<web-app>

<servlet>
<servlet-name>StartUp</servlet-name>
<servlet-class>com.thinking.machines.service.StartUpServlet</servlet-class>
<load-on-startup>1</load-on-startup>  
</servlet>

<servlet>
<servlet-name>Servlet1</servlet-name>
<servlet-class>com.thinking.machines.service.TMService</servlet-class>
    </servlet>
<servlet-mapping>
<servlet-name>Servlet1</servlet-name>
<url-pattern>/Service/*</url-pattern>
</servlet-mapping>

<servlet>
<servlet-name>Servlet2</servlet-name>
<servlet-class>com.thinking.machines.upload.TMUpload</servlet-class>
    </servlet>
<servlet-mapping>
<servlet-name>Servlet2</servlet-name>
<url-pattern>/Upload/*</url-pattern>
</servlet-mapping>

</web-app>
```
Request should only contain JSON,no other type of request is supported by the framework and first parameter of the method should be of classtype in which json needs to be converted .
Naming convention should be followed the last of that class must ends with Bean and the classes should be placed in the bean folder. Given in the above example(StudentBean).  
6)Following is the discription of the annotation:-
@Path:-It contains the request part for which request has been sent for class or method.
@Forward:-request will be forwarded to the page(jsp/html) or other service mentioned in the key. 
@Secure:-class name with package which implements the SecureInterface.
@ReturnType:- the type of data method will return (JSON,html/text,NOTHING)only these 3 values can be assign to key.
@MultipleFile:-this annotation is applied when the file needs to
Complie the following packages with:
For example:-tomcat9 is folder placed in c drive
```bash 
javac -classpath path c:\tomcat9\lib\*;c:\tomacat\webapps\application-name\WEB-INF\lib\*;c:\tomacat\webapps\application-name\WEB-INF\classes; *.java
```
