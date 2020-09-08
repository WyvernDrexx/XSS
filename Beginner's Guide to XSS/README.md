
# Beginner's Guide to XSS

In this section you will learn about finding and exploiting XSS vulnerabilities and more importantly *exploring* the *World of XSS!*

## Introduction to XSS

The term *XSS* or *Cross Site Scripting* was first introduced by Microsoft engineers in January 2000. Since then, it has become very popular among security researchers.

>**Cross Site Scripting** are a type of code injection vulnerabilities found typically in Web Applications that involve an attacker to inject malicious code into the Web Application's front-end.A successful XSS attack would be able to execute malicious code in the victim's browser from a trusted and benign looking web-page or application and perform unintended actions on behalf of the user.

The malicious code are written prominently in **JavaScript** but **Java**, **HTML**, **Flash**, **VBScript** and **ActiveX** are also used.

## Types of XSS

There is any standardized classification of XSS, but the most prominent are **Reflected XSS**, **Persistent XSS** and **DOM Based XSS**.

### Reflected XSS

>**Reflected XSS** are type of XSS Vulnerabilities that arises when a user input is taken in a HTTP request by the server and is immediately included in HTTP response without sanitizing it properly.

It is the most simplest form of XSS vulnerability that are  found in Web Applications.
[Read More..](./Reflected%20XSS.md)

### Persistent XSS

>**Persistent XSS** or **Stored XSS** is the most damaging type of XSS Vulnerabilities that arises when a user input from a un-trusted source is stored by the server in the database and then, displayed to all the users visiting the web pages of the application.

It is the most damaging type of XSS vulnerability because the surface area of this attack is huge.
[Read More..](./Persistent%20XSS.md)

### DOM-based XSS

>In **DOM-based XSS**, the injected malicious code is reflected directly in the client side code without it ever reaching the server.

The malicious code is injected into the input which the client side JavaScript reflects directly to the page without any server queries. If, the malicious input isn't sanitized properly by the client side code then the malicious code gets placed in the page as normal JS or HTML code and gets executed by the browser.
[Read More..](./DOM-based%20XSS.md)