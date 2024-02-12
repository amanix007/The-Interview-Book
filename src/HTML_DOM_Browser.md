# HTML & DOM & Browser

# **15. Event bubble**

**Question:** What is event bubble? How does event flows?

**Answer:** To understand event bubble, you have to understand what happen when you click on anything on a page.

**Where you clicked:** If you have a table with multiple rows and multiple columns and you click in one of the cell

- You will think that you have clicked on the cell and browser will know that you have a click handler with the cell that will be fired immediately.
- You are completely wrong. Right away, browser doesn't know where you have clicked.

The way browser find out where you have clicked are as follows-

1. **Capture:** When you clicked, browser knows a click event occurred. It starts from the window (lowest level/root of your website), then goes to document, then html root tag, then body, then table... its trying to reach the the as lowest level of element as possible. This is called capture phase (phase -1).
2. **Target:** When browser reach the lowest level of element. In this case, you have clicked on a table cell (table data) hence target would be "td" tag. Then browser checks whether you have any click handler attached to this element. If there is any, browser executes that click hander. This is called target phase (phase -2).
3. **Bubbling:** After firing click hander attached to "td", browser walks toward root. One level upward and check whether there is any click handler attached with table row ("tr" element). If there is any it will execute that. Then it goes to tbody, table, body, html, document, window. In this stage its moving upward and this is called event bubbling or bubbling phase (phase-3). Please note that, you clicked on cell but all the event handler with parent elements will be fired. This is actually very powerful (check event delegation)

Show a picture of bubble

**Show live demo:** [Go to this link](https://www.thatjsdude.com/jsConcepts/concepts/eventPropagation.html) and click any layer to see event propagation.

# **16. Event Delegate**

**Question:** How would you destroy multiple list items with one click handler?

**Easy Solution:** If you have one hundred list items that have similar event to handle. You can write one hundred event handler (actually copy paste) same code in 99 places. This works but if something changes in the event handler, you have to change in one hundred places. This doesn't call job security. This is called screwed up.

Second problem is if you want to dynamically add a new element, you have to make sure event handler is attached with the new element. More JavaScript code!

**Answer:** We can actually leverage event bubbling. You can have only one event handler attached to the parent element of one hundred list items. In this case, you can attach the event handler to the "ul" tag. After you click on a list item (list item does not have an event), event will bubble and "ul" has a handler. That handler will be fired.

```xml
<ul id="listToDestroy">
    <li><a href="#">first item</a></li>
    <li><a href="#">second item</a></li>
    <li><a href="#">third item</a></li>
    <li><a href="#">forth item</a></li>
    <li><a href="#">Fifth item</a></li>
</ul>

```

```jsx

document.getElementById('listToDestroy').addEventListener('click', function (e) {
    var elm = e.target.parentNode;
        elm.parentNode.removeChild(elm);
        e.preventDefault();
});

```

Show demo

# **17. destroy button**

**Question:** Create a button that is destroyed by clicking on it but two new buttons are created in it's place.

**Answer:** One way of solving is to attach a event handler with the button to destroy itself and append two. However, we can leverage event delegate. If we attach the event hander to the parent div instead of the button itself. We don't have to add the event handler to each button we create. So, we will take advantage of event bubbling.

**Try to be Smart:** If both the newly created button is identical to one we are destroying, why interviewer wants to destroy exactly similar one and then create one. Why not just add one. And end result would be same, you will have two two buttons.

**Interviewer:** I just want to see whether you can destroy any element. Make sure when you are destroying, there is no reference to the element, otherwise, you will have memory leak. If interviewer, says ok, just create one more button on click, then use your brain to change the following code.

```xml
<div id="doubleHolder">
  <button class="double">double</button>
</div>

```

```jsx

document.getElementById('doubleHolder').addEventListener('click', function (e) {
   if(e.target.classList.contains('double')){
      var btn = document.createElement('button');
      btn.setAttribute('class', 'double');
      btn.innerHTML = 'double';

      var btn2 = document.createElement('button');
      btn2.setAttribute('class', 'double');
      btn2.innerHTML = 'double';

      this.appendChild(btn);
      this.appendChild(btn2);
      this.removeChild(e.target);
    }
  });

```

Show clickable demo

ref: [destroy button](http://www.careercup.com/question?id=17328675)

# **18. Capture all click**

**Question:** How could you capture all clicks in a page?

**Answer:** You can leverage, event bubble to capture all the clicks. As all the clicks will be bubbled up to the body.

```jsx

document.querySelector('body').addEventListener('click', function(e){
  console.log('body clicked', e.target);
});

//or
window.onclick =function(e){
  console.log('someone clicked', e.target)
}

```

However, if event bubbling is canceled by `stopPropagation()` your code will not work. Think about it.

# **21. Rapid fire**

**Question:** How could you prevent a click on an anchor from going to the link?

**Answer:** `preventDefault()` inside event handler. However, this doesnt stop further propagation.

**Question:** How could you stop further propagation of an event?

**Answer:** Call `event.stopPropagation();`

**Question:** Can you remove an event handler from an element?

**Answer:** Yes. `target.removeEventListener('click', handler)`

**Question:** How could you run event handler in the capturing phase not in bubble phase?

**Answer:** There is a third (optional) parameter in addEventListener and removeEventLister. You can pass true or false to useCapture phase.

**Question:** How could you prevent multiple event handler to be fired for an event?

**Answer:** If event listeners are attached for the same type event (click, keydown, etc.) of an element for the same event type, you can call `event.stopImmediatePropagation()` in the first event handler. No other event handler will be executed.

**Question:** What are the cancelable events?

**Answer:** Go to [wiki](https://en.wikipedia.org/wiki/DOM_events#HTML_events) find the right most column cancelable.

**Question:** How could I check whether an event is cancelable or not?

**Answer:** Use `event.cancelable` to get true or false return. However, you have to `preventDefault()` to prevent the event.

**Question:** Is there anything you have to be careful when using `node.cloneNode()`?

**Answer:** While cloning, make sure you didnt duplicate ID.

**Question:** What are different nodeTypes?

**Answer:** ELEMENT_NODE (1), TEXT_NODE (3), COMMENT_NODE(8), DOCUMENT_NODE(9), DOCUMENT_TYPE_NODE(10), DOCUMENT_FRAGMENT_NODE(11), etc.

**Question:** What are the differences between node and element?

**Answer:** read [here](http://stackoverflow.com/a/9979779/1535443).

# **20. defer vs async**

**Question:** What is defer and async keyword does in a script tag?

**Answer:** HTML parser will ignore defer and async keyword for inline script (script that does not have a src attribute).

**normal:** When you have a plain script tag (no defer or async keyword), parser will pause parsing, script would be downloaded and exectuted. After that parsing resume.

**defer:** defer keyword in the script tag will defer the execution of the script. Hence script will be executed when DOM is available. Important point is, defer is not supported by all major major browsers.

**async:** If possible, set the execution of the script, asynchronously. `async` keyword has no effect on inline script.

![https://www.thatjsdude.com/images/asyncVsDefer.jpg](https://www.thatjsdude.com/images/asyncVsDefer.jpg)

Image copied from [JS script execution](http://peter.sh/experiments/asynchronous-and-deferred-javascript-execution-explained/)

**Extra:** [async injected scripts are considered harmful](https://www.igvita.com/2014/05/20/script-injected-async-scripts-considered-harmful/)

# **1. doctype**

**Question:** What is doctype? Why do u need it?

**Answer:** doctype is an instruction to the browser to inform about the version of html document and how browser should render it.

It ensures how element should be displayed on the page by most of the browser. And it also makes browser's life easier. otherwise, browser will guess and will go to [quirks mode](https://en.wikipedia.org/wiki/Quirks_mode). Moreover, doctype is required to [validate markup](http://validator.w3.org/).

```xml
<!DOCTYPE html>
<meta charset="UTF-8">

```

**extra:** this the first tag of html file, don't need a closing tag and not case sensitive.

ref:

[don't forget doctype](http://www.w3.org/QA/Tips/Doctype)

,

[Sparse vs Dense Array](http://www.2ality.com/2012/06/dense-arrays.html)

# **2. data-***

**Question:** What is the use of data- attribute?

**Answer:** allow you to store extra information/ data in the DOM. u can write valid html with embedded private data. You can easily access data attribute by using javascript and hence a lot of libraries like knockout uses it.

```xml
<div id="myDiv" data-user="jsDude" data-list-size="5" data-maxage="180"></div>

```

ref: [MDN: data-*](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_data_attributes), [use data attribute](http://www.sitepoint.com/use-html5-data-attributes/)

# **3. keygen**

**Question:** How can u generate public key in html?

**Answer:** html has a keygen element that facilitate generation of key and submission via a form.

```xml
<keygen name="name" challenge="challenge string" keytype="type" keyparams="pqg-params">

```

**extra:** keygen has to be used inside a form.

ref:

[MDN: keygen](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/keygen)

# **4. bdo**

**Question:** How can u change direction of html text?

**Answer:** use bdo (bidirectional override) element of html.

```xml
<!-- Switch text direction -->
<p><bdo dir="rtl">This text will go right to left.</bdo></p>

```

**result:**

This text will go right to left.

**extra:** rtl: right to left. and alternatively you can use, ltr: left to right.

# **5. mark**

**Question:** How can u highlight text in html?

**Answer:** use mark element.

```xml
<p>Some part of this paragraph is <mark>highlighted</mark> by using mark element.</p>

```

**result:**Some part of this paragraph is highlighted by using mark element.

# **6. scoped**

**Question:** Can u apply css rule to a part of html document?

**Answer:** yes. by using "scopped" in the style tag.

ref

[MDN: style](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/style)

# **7. http request**

**Question:** Does the following trigger http request at the time of page load?

```xml
<img src="mypic.jpg" style="visibility: hidden" alt="My photo">

```

**Answer:** yes

```xml
<div style="display: none;">
    <img src="mypic.jpg" alt="My photo">
</div>

```

**Answer:** yes

ref: [David Shariff: quiz](http://davidshariff.com/quiz/)

# **8. download order**

**Question:** Does style1.css have to be downloaded and parsed before style2.css can be fetched?

```xml
<head>
    <link href="style1.css" rel="stylesheet">
    <link href="style2.css" rel="stylesheet">
</head>

```

**Answer:** No

**Question:** Does style2.css have to be downloaded and parsed before Paragraph 1 is rendered on the page?

```xml
<head>
    <link href="style1.css" rel="stylesheet">
</head>
<body>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <link href="style2.css" rel="stylesheet">
</body>

```

**Answer:** yes

ref:

[David Shariff: quiz](http://davidshariff.com/quiz/)

# **9. self closing tag**

**Question:** What are optional closing tag? and why would u use it?

**Answer:** p, li, td, tr, th, html, body, etc. you don't have to provide end tag. Whenever browser hits a new tag it automatically ends the previous tag. However, you have to be careful to escape it.

**reason:** you can save some byte and reduce bytes needs to be downloaded in a html file.

```xml
<p>Some text
<p>Some more text
<ul>
 <li>A list item
 <li>Another list item
</ul>

```

the above html will be parsed as the following blocks.

```xml
<p>Some text</p>
<p>Some more text</p>
<ul>
 <li>A list item</li>
 <li>Another list item</li>
</ul>

```

ref: [W3.org: index of elements](http://www.w3.org/TR/REC-html40/index/elements.html)

# **Old School questions**

# **10. span vs div**

**Question:** What is the difference between span and div?

**Answer:** div is a block element and span is inline element.

**Extra:** It is illegal to put block element inside inline element. div can have a p tag and a p tag can have a span. However, span can't have a div or p tag inside.

ref: [Stackoverflow: div vs span](http://stackoverflow.com/questions/183532/what-is-the-difference-between-html-tags-div-and-span)

# **11. div, section & article**

**Question:** When should you use section, div or article?

**Answer:**

<section>, group of content inside is related to a single theme, and should appear as an entry in an outline of the page. It’s a chunk of related content, like a subsection of a long article, a major part of the page (eg the news section on the homepage), or a page in a webapp’s tabbed interface. A section normally has a heading (title) and maybe a footer too.

<article>, represents a complete, or self-contained, composition in a document, page, application, or site and that is, in principle, independently distributable or reusable, e.g. in syndication. This could be a forum post, a magazine or newspaper article, a blog entry, a user-submitted comment, an interactive widget or gadget, or any other independent item of content.

<div>, on the other hand, does not convey any meaning, aside from any found in its class, lang and title attributes.

**Good Summary:**[div, section & article](http://oli.jp/2009/html5-structure1/)

**Extra:** Authors are strongly encouraged to view the div element as an element of last resort, for when no other element is suitable. Use of more appropriate elements instead of the div element leads to better accessibility for readers and easier maintainability for authors.

ref: (copied from) [W3C: section](http://dev.w3.org/html5/spec-author-view/the-section-element.html#the-section-element), [W3C: div](http://dev.w3.org/html5/spec-author-view/the-div-element.html#the-div-element), [W3c: article](https://www.whatwg.org/specs/web-apps/current-work/multipage/sections.html#the-article-element)

# **12. svg vs canvas**

**Question:** What are the difference between svg and canvas?

**Answer:** [Read this one.](http://www.sitepoint.com/how-to-choose-between-canvas-and-svg/) (I am tired of copy-pasting)

# **13. multiple languages**

**Question:** How to serve a page content in multiple languages?

**Answer:** CMS could be used to deliver content in different language with same structure and style.

ref: [john polacek](https://github.com/johnpolacek/Front-end-Developer-Interview-Questions/blob/master/README.md)

# **14. standard & quirks mode**

**Question:** Difference between standard/ strict mode and quirks mode?

**Answer:** quirks mode in browser allows u to render page for as old browsers. This is for backward compatibility.

# **15. semantic**

**Question:** What is semantic HTML?

**Answer:** Semantic HTML, or "semantically-correct HTML", is HTML where the tags used to structure content are selected and applied appropriately to the meaning of the content.

for example, <b></b> (for bold), and <i></i> (for italic) should never be used, because they’re to do with formatting, not with the meaning or structure of the content. Instead, use the replacements <strong></strong> and <em></em> (meaning emphasis), which by default will turn text bold and italic (but don’t have to do so in all browsers), while adding meaning to the structure of the content.

**Question:** Why you would like to use semantic tag?

**Answer:** Search Engine Optimization, accessibility, repurposing, light code.

Many visually impaired person rely on browser speech and semantic tag helps to interpret page content clearly.

Search engine needs to understand page content to rank and semantic tag helps.

ref: [why important](http://www.adobe.com/devnet/html5/articles/semantic-markup.html#articlecontentAdobe_numberedheader_0), [Wiki: semantic HTML](https://en.wikipedia.org/wiki/Semantic_HTML)

**Question:** What does “semantically correct” mean?

**Answer:** read it in [Stackoverflow](http://stackoverflow.com/questions/1294493/what-does-semantically-correct-mean/1294512#1294512)