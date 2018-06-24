
JNDI

Client tier
Middle tier
EIS

Java EE works within the realm of the Middle tier, although it touches both the Client and the EIS
tiers. The Middle tier receives requests from the Client tier application. The Middle tier’s Web layer
processes the request and prepares a response, which it sends back to the Client tier, whereas the
Business layer applies the business logic before persisting it in the EIS tier. Within the Middle tier,
there is fl uid communication between the layers and the EIS tier, while preparing the response to the
Client tier.


THE MIDDLE TIER
The Java EE server sits on the Middle tier and provides two logical containers: the web container
and the EJB container. These containers roughly correspond to the Web layer and the Business layer,
respectively. Each layer has distinct but sometimes overlapping responsibilities.

Web Layer
The Web layer manages the interactions between the Client tier and the Business layer.

Business Layer
The Business layer executes business logic that resolves business problems or satisfi es a particular
business need within the business domain.
Normally, this would involve data that has been retrieved from the database in the EIS tier or
collected from the client.


THE EIS TIER
The EIS tier consists of data storage units, often in the form of databases, but they can be any
resource that provides data. It may be an antiquated legacy system or a fi le system.


Java EE is based on 30 standards, called Java Specifi cation Requests (JSRs) ( http://www.oracle.com/technetwork/java/javaee/tech/index.html ). These requests go through the Java
Community Process (JCP)