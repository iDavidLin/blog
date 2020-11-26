---
layout: post
title: "Expected Identifier Error in IE"
date: 2018-01-17
categories: front-end
description: oh, IE agian
tags: [IE, front-end]
---

Recently we are developing a widgets for product which will using in Windows System. So we have to support IE. Luckily we only need to support IE 9+.

We are using React js library (15.6.2).
It’s quite simple so far for our component at the moment. And it works perfectly in the latest version of Windows 10 which is version 17XX.

But when we trying to open that page in Windows 10 (version 16XX) with IE 11. It’s not working, error:

<span style="color:#F50057">`script1010 expected identifier`</span>.

When we trying to debug it in Windows. We found that it works well in emulation version 11001 and 10001. Other versions (as list below) are all having the expected identifier error.

![IE Version](/image/Browser-Emulation.png)

[From microsoft](https://msdn.microsoft.com/en-us/library/ee330730(VS.85).aspx#browser_emulation)

#### This Problem 

Since Babel (We are using ES6) assumes that your code will run in an ES5 environment it uses ES5 functions. So if you’re using an environment that has limited or no support for ES5 such as lower versions of IE then you will got the <span style="color:#F50057">`script1010 expected identifier`</span>.

**Details is:**  
Reserved words such as default are used in your code or in third party packages

#### How to solve this problems?
* Use es3ify or es3ify-loader to transform your code
* Use babel-polyfill.

In our case, we are using this webpack plugin: https://github.com/xcatliu/react-ie8
  
It fix the 'script1010 expected identifier’ problem. BUT then we got the new error <span style="color:#F50057">`Object doesn't support this property or method` `Object.assign`</span>…

OK. Then I add the `babel-polyfill` to fix this problems.  
AND AGAIN We got the new error….

And it’s quite weird that it works well when I host it with nginx in my computer, but after when I upload it to AWS it throw the error.

OK. Let’s try to force the IE to use the latest version by adding meta

<span style="color:#F50057">`<meta http-equiv="x-ua-compatible" content="IE=edge">`</span> under header in the index.html.

And guess what? It fixed the problem...

-----
### The X-UA-Compatible meta tag
The X-UA-Compatible meta tag allows web authors to choose what version of Internet Explorer the page should be rendered as. IE11 has made changes to these modes; see the IE11 note below. Microsoft Edge, the browser that will be released after IE11, will only honor the X-UA-Compatible meta tag in certain circumstances. See the Microsoft Edge note below.

According to Microsoft, when using the X-UA-Compatible tag, it should be as high as possible in your document head:

If you are using the X-UA-Compatible META tag you want to place it as close to the top of the page's HEAD as possible. Internet Explorer begins interpreting markup using the latest version. When Internet Explorer encounters the X-UA-Compatible META tag it starts over using the designated version's engine. This is a performance hit because the browser must stop and restart analyzing the content.

```
Edge mode tells Internet Explorer to display content in the highest mode 
available.With Internet Explorer 9, this is equivalent to IE9 mode.
If a future release of Internet Explorer supported a higher compatibility
mode, pages set to edge mode would appear in the highest mode supported 
by that version. Those same pages would still appear in IE9 mode when viewed
with Internet Explorer 9. Internet Explorer supports a number of document 
compatibility modes that enable different features and can affect the way
content is displayed:
```

Reference  
[What does \<meta http-equiv=“X-UA-Compatible” content=“IE=edge”> do?
](https://stackoverflow.com/a/6771584)

