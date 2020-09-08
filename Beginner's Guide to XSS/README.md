# Beginner's Guide to XSS

In this section you will learn about finding and exploiting XSS vulnerabilities and more importantly _exploring_ the _World of XSS!_

## Introduction to XSS

The term _XSS_ or _Cross Site Scripting_ was first introduced by Microsoft engineers in January 2000. Since then, it has become very popular among security researchers.

> **Cross Site Scripting** are a type of code injection vulnerabilities found typically in Web Applications that involve an attacker to inject malicious code into the Web Application's front-end.A successful XSS attack would be able to execute malicious code in the victim's browser from a trusted and benign looking web-page or application and perform unintended actions on behalf of the user.

The malicious code are written prominently in **JavaScript** but **Java**, **HTML**, **Flash**, **VBScript** and **ActiveX** are also used.

## Types of XSS

There isn't any standardized classification of XSS, but the most prominent are **Reflected XSS**, **Persistent XSS** and **DOM Based XSS**.

### Reflected XSS

> **Reflected XSS** are type of XSS Vulnerabilities that arises when a user input is taken in a HTTP request by the server and is immediately included in HTTP response without sanitizing it properly.

It is the most simplest form of XSS vulnerability that are found in Web Applications.

**Example:**

Let's say there is an e-commerce website now, you need to search for a nice fancy laptop for yourself. In the search input field you enter `laptop`. As a result you get list of all the laptops available on the site.

You notice that on the URL bar you have your search query as `https://example-site.com/search?term=laptop`.
And that query term is reflected in the page as `Here are the results for 'laptop'`.

Now, what if you insert,

```html
<h1>Laptop</h1>
```

Bang! After inserting above code you see that your HTML code gets rendered by the browser. In our case, you see heading of **Laptop**.

What if you insert,

```html
<script>
  alert("XSS");
</script>
```

Hmm, any guesses? When you enter the above code you are greeted with **XSS**.
**Hooray! You just found an XSS Vulnerability!**

But, the major problem with it is that, only you can see the alert and if you want anyone else to see your victory you have to tell them to enter the above snippet. So boring.

Hmm, did you notice that URL param `term`?. Yes, now the only thing you need to do is send the URL containing the search query term to your victim.
`https://https://example-site.com/search?term=<script>alert("XSS")</script>`
When they visit the URL they will be greeted with **XSS**. This isn't any harmful snippet but this is exactly how an malicious attacker would design his attack. To learn more,
[Read More..](./Reflected%20XSS.md)

### Persistent XSS

> **Persistent XSS** or **Stored XSS** is the most damaging type of XSS Vulnerabilities that arises when a user input from a un-trusted source is stored by the server in the database and then, displayed to all the users visiting the web pages of the application.

It is the most damaging type of XSS vulnerability because the surface area of this attack is huge.

**Example:**

After spending a while on the e-commerce you finally end your hunt for laptop, you think for getting social _(bruh)_. So, you visit `https://social-website.com`. You find a funny post with lots of comments in it.

Remembering your previous XSS finding you try to write a comment,

```html
<strong>Hmm, hi peeps!</strong>
```

**WTH!** You see your comment in bold. Genius! Now, for fun you enter your _very malicious javascript code_.

```html
<script>
  alert("Gimme your money!");
</script>
```

Bang! You get an alert with some _serious threat._

The biggest take from that comment is that now everyone who sees your comment will get an alert `Gimme your money!`.

Now, that's enough for you to get in trouble with the social media company. To learn more,
[Read More..](./Persistent%20XSS.md)

### DOM-based XSS

> In **DOM-based XSS**, the injected malicious code is reflected directly in the client side code without it ever reaching the server.
>The malicious code is injected into the input which the client side JavaScript reflects directly to the page without any server queries. If, the malicious input isn't sanitized properly by the client side code then the malicious code gets placed in the page as normal JS or HTML code and gets executed by the browser.

**Example:**

Taking our example on **Reflected XSS**, lets say that the web page auto-fills the search input by looking at the contents from the URL query string.

```javascript
var query = new URLSearchParams(window.location.search).get("term");
if (query) {
  document.write("<input type='text' value='" + query + "'>");
}
```

The first line looks for URL query parameter `term` and the condition checks if it has any. If there is a query string then, write a input tag,

`<input type='text' value='query string here'>` 

to the DOM.

Now if you try to put the script,

```html
<script>
  alert("XSS");
</script>
```

you won't get any alert, instead you will get a input tag with `<script>alert("XSS")</script>` inside of it.

It's normal because `document.write` is doing what it is told.

Now it's time to think different!
When we look in the code snippet from above. We notice that our search term is getting inside the `value` attribute of input tag.
Look closely on how the HTML code is outputted by the JavaScript. 

What if we enter a  quote inside the search query?

If we put  quote inside query the resultant HTML output will be,

```html
  <input type='text' value='"'>
```

Hmm, Do you notice anything? The quote got pasted as it is?

 Now, what if we input single quote inside of it?

```html
  <input type='text' value='''>
```

Did you notice that HTML code got broken?

Why did it even broke? Because, if you see, our single quote got inside of the `value` attribute which caused the `value` to terminate early and left behind `'>`.

Now if we but `'>`, the  `value` will be `value=''>'`, the single quote will end `value` attribute and `>` will close the input tag which makes the last single quote and the closing tag out of input tag and makes it a general string.

```html
  <input type='text' value=''>'>
```

For final showdown, lets get XSS!
We enter the following snippet in the url query string,

`'><script>alert("XSS")</script>`

Yeah! We get **XSS!**
What actually happened?
The input tag now becomes,

```html
  <input type='text' value=''><script>alert("XSS")</script>'>
```

The `'>` ended the input tag properly and then, we immediately add `script` following it which gets executed by the browser.
 The `'>` can be seen in the end left behind. If you want you can even hide them using some extra HTML!

Now that's your job!

To learn more,[Read More..](./DOM-based%20XSS.md)
