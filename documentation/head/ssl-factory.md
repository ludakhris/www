---
layout: default_docs
title: Custom SSLSocketFactory
header: Chapter 4. Using SSL
resource: media
previoustitle: Configuring the Client
previous: ssl-client.html
nexttitle: Chapter 5. Issuing a Query and Processing the Result
next: query.html
---

PostgreSQL™ provides a way for developers to customize how a SSL connection is
established. This may be used to provide a custom certificate source or other
extensions by allowing the developer to create their own `SSLContext` instance 
or otherwise control or configure the SSL connection to PostgresSQL. There are
several connection URL parameters available that you can set in the connection
string all are listed on the [PostgreSQL JDBC Driver Developer Page](https://github.com/pgjdbc/pgjdbc).
The connection URL parameters `sslContextProtocol` allow the user to specify which SSL\TLS
protocol will be used when creating the SSLContext, valid values for Java 8 are 
documented here: [SSLContext Reference](http://docs.oracle.com/javase/8/docs/technotes/guides/security/StandardNames.html#SSLContext)

The connection URL parameters `sslfactory` and `sslfactoryarg` allow the user
to specify which custom class to use for creating the `SSLSocketFactory`. The
class name specified by `sslfactory` must extend `javax.net.ssl.SSLSocketFactory`
and be available to the driver's classloader. This class must have a zero argument
constructor or a single argument constructor which takes a Properties object as an 
argument (this Properties object will contain all of the JDBC URL properties set 
for the connection). This argument may optionally be supplied by `sslfactoryarg`.

Information on how to actually implement such a class is beyond the scope of this
documentation. Places to look for help are the [JSSE Reference Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jsse/JSSERefGuide.html)
and the source to the `NonValidatingFactory` provided by the JDBC driver.

The Java SSL API is not very well known to the JDBC driver developers and we
would be interested in any interesting and generally useful extensions that you
have implemented using this mechanism. Specifically it would be nice to be able
to provide client certificates to be validated by the server.
