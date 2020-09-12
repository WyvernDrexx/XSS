# Persistent XSS

>A **Persistent XSS** or **Stored XSS** is a type of XSS Vulnerability in which a malicious XSS payload is stored in the database of the server which makes the payload *persistent* and it is sent to users in each following requests. Thus, making the XSS Payload *persistent*. The server ***stores*** the payload not by the **influence** from the malicious actor/s but, due to it's own **functionality**.

Unlike Reflected XSS, in Persistent XSS the payload is not sent directly to the victim through any medium but it is indirectly send through the vulnerable site.

`Persistent XSS is really hard to catch because, not only is the payload is  invisible to the user through the natural UI of the browser but also, a proper XSS Payload would just blend into it's environment.`

The most dangerous part of a **Persistent XSS** vulnerability is that, it can effect extremely large number of audiences. For example, there is a Persistent XSS vulnerability in one popular website's comment section. Imagine, if someone uploads a stealthy malicious payload and hundred's of thousands of people view it. None of them would notice it because it's stealthy.

By the time it gets noticed, large number of people would  already be compromised.
