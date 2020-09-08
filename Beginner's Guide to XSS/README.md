
# Beginner's Guide to XSS

In this section you will learn about finding and exploiting XSS vulnerabilities and more importantly *exploring* the *World of XSS!*

## Introduction to XSS

The term *XSS* or *Cross Site Scripting* was first introduced by Microsoft engineers in January 2000. Since then, it has become very popular among security researchers.

>**Cross Site Scripting** are a type of code injection vulnerabilities found typically in Web Applications that involve an attacker to inject malicious code into the Web Application's front-end.A successful XSS attack would be able to execute malicious code in the victim's browser from a trusted and benign looking web-page or application and perform unintended actions on behalf of the user.

The malicious code are written prominently in **JavaScript** but **Java**, **HTML**, **Flash**, **VBScript** and **ActiveX** are also used.

## Types of XSS

There isn't any standardized classification of XSS, but the most prominent are **Reflected XSS**, **Persistent XSS** and **DOM Based XSS**.

### Reflected XSS

>**Reflected XSS** are type of XSS Vulnerabilities that arises when a user input is taken in a HTTP request by the server and is immediately included in HTTP response without sanitizing it properly.

It is the most simplest form of XSS vulnerability that are  found in Web Applications.

**Example:**
Let's say there is a e-commerce website that lists all the available products on the home page. Now, you need to search for a nice fancy laptop for yourself. In the search input field you type `laptop`. As a result you get list of all the laptops available on the site.

You notice that on the URL bar you have your search query as `https://example-site.com/search?term=laptop`.
And that query term is reflected in the page as `Here are the results for 'laptop'`.

Now, what if you insert,

```html
  <h1>Laptop</h1>
```  

Bang! After inserting above code  you see that your HTML code gets rendered by the browser. In our case, you see heading of **Laptop**. 

What if you insert,

```html
  <script>alert("XSS")</script>
```

Hmm, any guesses? When you enter the above code you get greeted with **XSS**.
**Hooray! You just found an XSS Vulnerability!**
But, the major problem with it is that only you can see and if you want anyone else to see your victory you have to tell them to enter it. So boring.

Hmm, did you notice that URL param `term`?. Yes, now the only thing you need to do is send the URL containing the search query term the victim.
`https://https://example-site.com/search?term=<script>alert("XSS")</script>`
When they click on this they will be greeted with **XSS**.

[Read More..](./Reflected%20XSS.md)

### Persistent XSS

>**Persistent XSS** or **Stored XSS** is the most damaging type of XSS Vulnerabilities that arises when a user input from a un-trusted source is stored by the server in the database and then, displayed to all the users visiting the web pages of the application.

It is the most damaging type of XSS vulnerability because the surface area of this attack is huge.
[Read More..](./Persistent%20XSS.md)

### DOM-based XSS

>In **DOM-based XSS**, the injected malicious code is reflected directly in the client side code without it ever reaching the server.

The malicious code is injected into the input which the client side JavaScript reflects directly to the page without any server queries. If, the malicious input isn't sanitized properly by the client side code then the malicious code gets placed in the page as normal JS or HTML code and gets executed by the browser.
[Read More..](./DOM-based%20XSS.md)