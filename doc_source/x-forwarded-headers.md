# HTTP Headers and Classic Load Balancers<a name="x-forwarded-headers"></a>

HTTP requests and HTTP responses use header fields to send information about the HTTP messages\. Header fields are colon\-separated name\-value pairs that are separated by a carriage return \(CR\) and a line feed \(LF\)\. A standard set of HTTP header fields is defined in RFC 2616, [Message Headers](http://tools.ietf.org/html/rfc2616#section-4.2)\. There are also non\-standard HTTP headers available that are widely used by the applications\. Some of the non\-standard HTTP headers have an `X-Forwarded` prefix\. Classic Load Balancers support the following `X-Forwarded` headers\.

For more information about HTTP connections, see [Request Routing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html#request-routing) in the *Elastic Load Balancing User Guide*\.

**Prerequisites**
+ Confirm that your listener settings support the X\-Forwarded headers\. For more information, see [Listener Configurations for Classic Load Balancers](using-elb-listenerconfig-quickref.md)\.
+ Configure your web server to log client IP addresses\.

**Topics**
+ [X\-Forwarded\-For](#x-forwarded-for)
+ [X\-Forwarded\-Proto](#x-forwarded-proto)
+ [X\-Forwarded\-Port](#x-forwarded-port)

## X\-Forwarded\-For<a name="x-forwarded-for"></a>

The `X-Forwarded-For` request header helps you identify the IP address of a client when you use an HTTP or HTTPS load balancer\. Because load balancers intercept traffic between clients and servers, your server access logs contain only the IP address of the load balancer\. To see the IP address of the client, use the `X-Forwarded-For` request header\. Elastic Load Balancing stores the IP address of the client in the `X-Forwarded-For` request header and passes the header to your server\.

The `X-Forwarded-For` request header takes the following form:

```
X-Forwarded-For: client-ip-address
```

The following is an example `X-Forwarded-For` request header for a client with an IP address of `203.0.113.7`\.

```
X-Forwarded-For: 203.0.113.7
```

The following is an example `X-Forwarded-For` request header for a client with an IPv6 address of `2001:DB8::21f:5bff:febf:ce22:8a2e`\.

```
X-Forwarded-For: 2001:DB8::21f:5bff:febf:ce22:8a2e
```

## X\-Forwarded\-Proto<a name="x-forwarded-proto"></a>

The `X-Forwarded-Proto` request header helps you identify the protocol \(HTTP or HTTPS\) that a client used to connect to your load balancer\. Your server access logs contain only the protocol used between the server and the load balancer; they contain no information about the protocol used between the client and the load balancer\. To determine the protocol used between the client and the load balancer, use the `X-Forwarded-Proto` request header\. Elastic Load Balancing stores the protocol used between the client and the load balancer in the `X-Forwarded-Proto` request header and passes the header along to your server\.

Your application or website can use the protocol stored in the `X-Forwarded-Proto` request header to render a response that redirects to the appropriate URL\.

The `X-Forwarded-Proto` request header takes the following form:

```
X-Forwarded-Proto: originatingProtocol
```

The following example contains an `X-Forwarded-Proto` request header for a request that originated from the client as an HTTPS request:

```
X-Forwarded-Proto: https
```

## X\-Forwarded\-Port<a name="x-forwarded-port"></a>

The `X-Forwarded-Port` request header helps you identify the destination port that the client used to connect to the load balancer\.