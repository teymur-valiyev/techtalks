
# Aurora framework how is works and its internal 

## cms 

core aurora classes
```
tr.com.cs.aurora.auroracore.utility.*
```

> A delimiter is one or more characters that separates text 


## CSBag

```

	private Hashtable pool = new Hashtable();


   public CSBag put(String key, String value) {
        key = clearKey(key);
        pool.put(key, new CSBagValue(value));
        return this;
    }

```

uses for row column value 
Dim1
Dim2


## CSBagValue

it store value and can convert it nassery csbag type

## CSAbstractCaller

```
public CSBag call(String serviceName, CSBag inBag) throws Throwable {
    inBag.setServiceName(serviceName);
    CSService service = CSCacheFactory.getService(serviceName);
    if (service == null) {
        throw new ClassNotFoundException("No Such Service (see /service.xml): " + serviceName);
    }
    Method method = service.getMethod();
    try {
        return (CSBag) method.invoke(null, new Object[]{inBag});
    } catch (IllegalArgumentException e) {
        CSLogger.error(e, "", ID);
        throw e;
    } catch (IllegalAccessException e) {
        CSLogger.error(e, "", ID);
        throw e;
    } catch (InvocationTargetException e) {
        throw e.getTargetException();
    }
}
```


## CSCacheFactory
```
    private Hashtable cachePool = new Hashtable();
```

```
Element cacheNode = (Element) caches.item(s);
CSCache cache = (CSCache) Class.forName(CSXMLUtil.getChild(cacheNode, "cacheclass").getTextContent()).newInstance();
cache.setCode(CSXMLUtil.getAttr(cacheNode, "code", ID));
cache.setName(CSXMLUtil.getChild(cacheNode, CONSTANTS.name).getTextContent());
cachePool.put(cache.getCode(), cache);
```

parsing  cache.xml            
fileName = "/cache.xml";

```
<CACHES>
   <cache code="DOMAIN">
      <name>Aurora Domain Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSDomainCache</cacheclass>
   </cache>
   <cache code="MENU">
      <name>Aurora Menu Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSMenuCache</cacheclass>
   </cache>
   <cache code="MESSAGE">
      <name>Aurora Message Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSMessageCache</cacheclass>
   </cache>
   <cache code="REFERENCEDATA">
      <name>Aurora Reference Data Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSReferenceDataCache</cacheclass>
   </cache>
   <cache code="SERVICE">
      <name>Aurora Service Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSServiceCache</cacheclass>
   </cache>
</CACHES>
```

and creates CSCache object with code and name

CSDomainCache
CSMenuCache
CSMessageCache
CSReferenceDataCache
CSServiceCache


## CSCache 
```
    private Node root = null;
    private Hashtable pool = new Hashtable(); 
```
root - stored node of current  Cache class
pool - stores of current Class

## CSService
part of cache implementation 
user for class mand method calls


## CSXMLUtil 
class for working with xml object

## CSCaller

```
String serviceCaller = ServerServlet.getInstance().getProperty("service-caller-class");
setCaller((CSAbstractCaller) Class.forName(serviceCaller).newInstance());
```

## ServerServlet 
```
tr.com.cs.aurora.cms.server.ServerServlet
```
parsing Server.xml file
Server.xml
it has Configuration class which stores all Server.xml methods for working with calls

it is servlet thats does cms work


## Configuration
```
tr.com.cs.aurora.utility.Configuration
```
parsing storest all commands from Server.xml


## SCommand

in server xml files there are commands classes

```
tr.com.cs.aurora.cms.SCommand;
```



## Application bootstrap

### ServerServlet

package tr.com.cs.aurora.cms.server.ServerServlet

init method
Servlet container calls servlet init() method before handling client requests. It is called just one times after servlet is created.

```
String[] caches = CSCacheFactory.getCacheNames();
...
cache.refresh();
```
if there is any cache it will remove it 

####  constructor start
will read Server.xml file
```
readConfiguration("/Server.xml");
```

```
protected void readConfiguration(String confFileName) throws Exception {
    configuration = new Configuration(confFileName);
}
```
it will create new Configuration object


package tr.com.cs.aurora.utility.Configuration
```
	private Hashtable		properties		= new Hashtable();
	private Hashtable		connections		= new Hashtable();
	private Hashtable		localCommands	= new Hashtable();
	private Hashtable		remoteCommands	= new Hashtable();
```
it will read all xml nodes and add it to Hashtable

```
public String getProperty(String propName) {
    return configuration.getProperty(propName);
}
```
will get all configuration properties



tr.com.cs.aurora.utility.CONSTANTS

it stores all constants for cms

CONSTANTS.data, CONSTANTS.help, CONSTANTS.image,

then it creates all folders

### constructor end

```
public Element executeNode(Element commandNode) {
    try {
        String commandClassName = getLocalCommand(commandNode.getTagName());
        SCommand command = (SCommand) Class.forName(commandClassName).newInstance();
        return command.executeNode(commandNode);
    } catch (Exception e) {
        return CSXMLUtil.createErrorNode(e, ID);
    }
}

public String getLocalCommand(String localName) {
    return configuration.getLocalCommand(localName);
}
```


all local commands extends tr.com.cs.aurora.cms.SCommand
```
tr.com.cs.aurora.cms.server.command.server.CMSGetFile
```
this commands resolves the request node and does required actions

### CMSRemoteCall

tr.com.cs.aurora.cms.server.command.server.CMSRemoteCall

```
	CSBag oBag = CSCaller.call(iBag.getServiceName(), iBag);
```

it calls services

#### CSCaller

```
	String serviceCaller = ServerServlet.getInstance().getProperty("service-caller-class");

// <service-caller-class>tr.gov.ggm.vedop2.vedop.vedop2core.utility.CSVedopCaller</service-caller-class>

	setCaller((CSAbstractCaller) Class.forName(serviceCaller).newInstance());

```

```
inBag.setServiceName(serviceName);
CSBag beforeBag = caller.beforeCall(inBag);
CSBag callBag = caller.call(serviceName, beforeBag);
CSBag afterBag = caller.afterCall(callBag);
```

tr.com.cs.aurora.auroracore.utility.CSAbstractCaller

all caller mehods extends CSAbstractCaller class
```
 public CSBag call(String serviceName, CSBag inBag) throws Throwable {
        inBag.setServiceName(serviceName);
        CSService service = CSCacheFactory.getService(serviceName);
        if (service == null) {
            throw new ClassNotFoundException("No Such Service (see /service.xml): " + serviceName);
        }
        Method method = service.getMethod();

        return (CSBag) method.invoke(null, new Object[]{inBag});
    }

```

### CSCacheFactory

```
 CSService service = CSCacheFactory.getService(serviceName);
```

```
private CSCacheFactory() {
            String fileName = "/cache.xml";
            InputStream inStream = CSStream.getInputStream(getClass(), fileName);
            Element fileRoot = (Element) CSXMLUtil.parse(inStream);
            NodeList caches = fileRoot.getElementsByTagName("cache");
            for (int s = 0; s < caches.getLength(); s++) {
                Element cacheNode = (Element) caches.item(s);
                CSCache cache = (CSCache) Class.forName(CSXMLUtil.getChild(cacheNode, "cacheclass").getTextContent()).newInstance();
                cache.setCode(CSXMLUtil.getAttr(cacheNode, "code", ID));
                cache.setName(CSXMLUtil.getChild(cacheNode, CONSTANTS.name).getTextContent());
                cachePool.put(cache.getCode(), cache);
            }
       
    }
```

parsing  cache.xml            
fileName = "/cache.xml";

```
<CACHES>
   <cache code="DOMAIN">
      <name>Aurora Domain Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSDomainCache</cacheclass>
   </cache>
   <cache code="MENU">
      <name>Aurora Menu Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSMenuCache</cacheclass>
   </cache>
   <cache code="MESSAGE">
      <name>Aurora Message Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSMessageCache</cacheclass>
   </cache>
   <cache code="REFERENCEDATA">
      <name>Aurora Reference Data Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSReferenceDataCache</cacheclass>
   </cache>
   <cache code="SERVICE">
      <name>Aurora Service Cache</name>
      <cacheclass>tr.com.cs.aurora.auroracore.utility.CSServiceCache</cacheclass>
   </cache>
</CACHES>
```

and creates CSCache object with code and name

CSDomainCache
CSMenuCache
CSMessageCache
CSReferenceDataCache
CSServiceCache

it resolves the xml files and it proper objects

CSDomain
CSMenu
CSMessage
CSReferenceData
CSService

### CSServiceCache
parsing 
service.xml , - 
special_services.xm
```
private void loadServiceXML() throws Exception
{
	setRoot(CSXMLUtil.createNewDocument("SERVICES"));
	parseFilesAndAddTaggedNodesToRoot("/special_services.xml", "service");
	parseFilesAndAddTaggedNodesToRoot("/service.xml", "service");
}
```

parseFilesAndAddTaggedNodesToRoot parses file asignes to root variable

CSCache
```
    private Node root = null;
``` 

