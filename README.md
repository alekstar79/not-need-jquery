Not Need jQuery

*   [AJAX](#ajax)
    
    *   [JSON](#json)
    *   [Load](#load)
    *   [Post](#post)
    *   [Request](#request)
*   [Effects](#effects)
    
    *   [Fade In](#fade_in)
    *   [Fade Out](#fade_out)
    *   [Hide](#hide)
    *   [Show](#show)
    *   [Toggle](#toggle)
*   [Elements](#elements)
    
    *   [Add Class](#add_class)
    *   [After](#after)
    *   [Append](#append)
    *   [Append To](#append_to)
    *   [Before](#before)
    *   [Children](#children)
    *   [Clone](#clone)
    *   [Closest](#closest)
    *   [Contains](#contains)
    *   [Contains Selector](#contains_selector)
    *   [Contents](#contents)
    *   [Create Elements](#create_elements)
    *   [Each](#each)
    *   [Empty](#empty)
    *   [Filter](#filter)
    *   [Find Children](#find_children)
    *   [Find Elements](#find_elements)
    *   [Find Selector](#find_selector)
    *   [First](#first)
    *   [Get Attributes](#get_attributes)
    *   [Get Height](#get_height)
    *   [Get HTML](#get_html)
    *   [Get Outer HTML](#get_outer_html)
    *   [Get Style](#get_style)
    *   [Get Text](#get_text)
    *   [Get Width](#get_width)
    *   [Has Class](#has_class)
    *   [Index](#index)
    *   [Inner Height](#inner_height)
    *   [Inner Width](#inner_width)
    *   [Is Hidden](#is_hidden)
    *   [Is Visible](#is_visible)
    *   [Last](#last)
    *   [Matches](#matches)
    *   [Matches Selector](#matches_selector)
    *   [Next](#next)
    *   [Offset](#offset)
    *   [Offset Parent](#offset_parent)
    *   [Outer Height](#outer_height)
    *   [Outer Height With Margin](#outer_height_with_margin)
    *   [Outer Width](#outer_width)
    *   [Outer Width With Margin](#outer_width_with_margin)
    *   [Parent](#parent)
    *   [Parents](#parents)
    *   [Position](#position)
    *   [Position Relative To Viewport](#position_relative_to_viewport)
    *   [Prepend](#prepend)
    *   [Prev](#prev)
    *   [Remove](#remove)
    *   [Remove Attributes](#remove_attributes)
    *   [Remove Class](#remove_class)
    *   [Replace From HTML](#replace_from_html)
    *   [Scroll Left](#scroll_left)
    *   [Scroll Top](#scroll_top)
    *   [Serialize](#serialize)
    *   [Set Attributes](#set_attributes)
    *   [Set Height](#set_height)
    *   [Set HTML](#set_html)
    *   [Set Style](#set_style)
    *   [Set Text](#set_text)
    *   [Set Width](#set_width)
    *   [Siblings](#siblings)
    *   [Toggle Class](#toggle_class)
    *   [Unwrap](#unwrap)
    *   [Val](#val)
    *   [Wrap](#wrap)
*   [Events](#events)
    
    *   [Click](#click)
    *   [Delegate](#delegate)
    *   [Off](#off)
    *   [On](#on)
    *   [Ready](#ready)
    *   [Trigger Custom](#trigger_custom)
    *   [Trigger Native](#trigger_native)
*   [Utils](#utils)
    
    *   [Array Each](#array_each)
    *   [Bind](#bind)
    *   [Deep Extend](#deep_extend)
    *   [Extend](#extend)
    *   [Index Of](#index_of)
    *   [Is Array](#is_array)
    *   [Is Numeric](#is_numeric)
    *   [Map](#map)
    *   [Now](#now)
    *   [Object Each](#object_each)
    *   [Parse HTML](#parse_html)
    *   [Parse JSON](#parse_json)
    *   [Slice](#slice)
    *   [To Array](#to_array)
    *   [Trim](#trim)
    *   [Type](#type)

You might not need jQuery
=========================

jQuery and its cousins are great, and by all means use them if it makes it easier to develop your application.  
  
If you're developing a library on the other hand, please take a moment to consider if you actually need jQuery as a dependency. Maybe you can include a few lines of utility code, and forgo the requirement. If you're only targeting more modern browsers, you might not need anything more than what the browser ships with.  
  
At the very least, make sure you know what [jQuery is doing for you](https://docs.google.com/document/d/1LPaPA30bLUB_publLIMF0RlhdnPx_ePXm7oW02iiT6o), and what it's not. Some developers believe that jQuery is protecting us from a great demon of browser incompatibility when, in truth, post-IE8, browsers are pretty easy to deal with on their own; and after the Internet Explorer era, the browsers do even more.


[AJAX](#ajax)
-------------

### Alternatives:

*   [fetch](https://github.com/github/fetch)


### [JSON](#json)

#### jquery

    $.getJSON('/my/url', function (data) {});

#### ie8+

    var request = new XMLHttpRequest();
    request.open('GET', '/my/url', true);
    
    request.onreadystatechange = function () {
      if (this.readyState === 4) {
        if (this.status >= 200 && this.status < 400) {
          // Success!
          var data = JSON.parse(this.responseText);
        } else {
          // Error :(
        }
      }
    };
    
    request.send();
    request = null;

#### ie9+

    var request = new XMLHttpRequest();
    request.open('GET', '/my/url', true);
    
    request.onload = function () {
      if (request.status >= 200 && request.status < 400) {
        // Success!
        var data = JSON.parse(request.responseText);
      } else {
        // We reached our target server, but it returned an error
      }
    };
    
    request.onerror = function () {
      // There was a connection error of some sort
    };
    
    request.send();

#### ie10+

    var request = new XMLHttpRequest();
    request.open('GET', '/my/url', true);
    
    request.onload = function () {
      if (this.status >= 200 && this.status < 400) {
        // Success!
        var data = JSON.parse(this.response);
      } else {
        // We reached our target server, but it returned an error
      }
    };
    
    request.onerror = function () {
      // There was a connection error of some sort
    };
    
    request.send();

#### modern

    const response = await fetch('/my/url');
    const data = await response.json();


### [Load](#load)

#### jquery

    $('#some.selector').load('/path/to/template.html');

#### ie8+

    function load(selector, path) {
      var request = new XMLHttpRequest();
      request.open('GET', path, true);
      request.onreadystatechange = function () {
        if (this.readyState === 4) {
          if (this.status >= 200 && this.status < 400) {
            // Success!
            var elements = document.querySelector(selector);
            for (var i = 0; i < elements.length; i++) {
              elements[i].innerHTML = this.responseText;
            }
          } else {
            // Error :(
          }
        }
      };
    }
    
    load('#some.selector', '/path/to/template.html');

#### modern

    const response = await fetch('/path/to/template.html');
    const body = await response.text();
    
    document.querySelector('#some.selector').innerHTML = body;


### [Post](#post)

#### jquery

    $.ajax({
      type: 'POST',
      url: '/my/url',
      data: data
    });

#### ie8+

    var request = new XMLHttpRequest();
    request.open('POST', '/my/url', true);
    request.setRequestHeader(
      'Content-Type',
      'application/x-www-form-urlencoded; charset=UTF-8'
    );
    request.send(data);

#### modern

    await fetch('/my/url', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(data)
    });


### [Request](#request)

#### jquery

    $.ajax({
      type: 'GET',
      url: '/my/url',
      success: function (resp) {},
      error: function () {}
    });
    

#### ie8+

    function request(success, error) {
      var request = new XMLHttpRequest();
      request.open('GET', '/my/url', true);
    
      request.onreadystatechange = function () {
        if (this.readyState === 4) {
          if (this.status >= 200 && this.status < 400) {
            // Success! If you expect this to be JSON, use JSON.parse!
            success(this.responseText, this.status);
          } else {
            error();
          }
        }
      };
    
      request.send();
    }

#### ie9+

    function request(success, error) {
      var request = new XMLHttpRequest();
      request.open('GET', '/my/url', true);
    
      request.onload = function () {
        if (this.status >= 200 && this.status < 400) {
          // Success! If you expect this to be JSON, use JSON.parse!
          success(this.responseText, this.status);
        } else {
          // We reached our target server, but it returned an error
          error();
        }
      };
    
      request.onerror = function () {
        error();
      };
    
      request.send();
    }

#### modern

    const response = await fetch('/my/url');
    
    if (!response.ok) {
    }
    
    const body = await response.text();
    

[Effects](#effects)
-------------------

### Alternatives:

*   [animate.css](https://animate.style)
*   [move.js](https://github.com/visionmedia/move.js)
*   [velocity.js](https://julian.com/research/velocity/)


### [Fade In](#fade_in)

#### jquery

    $(el).fadeIn();

#### ie8+

    function fadeIn(el, speed = 400) {
      var opacity = 0;
    
      el.style.opacity = 0;
      el.style.filter = '';
    
      var last = +new Date();
      var tick = function () {
        opacity += (new Date() - last) / speed;
        if (opacity > 1) opacity = 1;
        el.style.opacity = opacity;
        el.style.filter = 'alpha(opacity=' + (100 * opacity || 0) + ')';
    
        last = +new Date();
    
        if (opacity < 1) {
          (window.requestAnimationFrame && requestAnimationFrame(tick)) ||
            setTimeout(tick, 16);
        }
      };
    
      tick();
    }
    
    fadeIn(el);

#### ie9+

    function fadeIn(el, speed = 400) {
      el.style.opacity = 0;
    
      var last = +new Date();
      var tick = function () {
        el.style.opacity = +el.style.opacity + (new Date() - last) / speed;
        if (opacity > 1) opacity = 1;
        last = +new Date();
    
        if (+el.style.opacity < 1) {
          (window.requestAnimationFrame && requestAnimationFrame(tick)) ||
            setTimeout(tick, 16);
        }
      };
    
      tick();
    }
    
    fadeIn(el);

#### ie10+

    el.classList.add('show');
    el.classList.remove('hide');
    

    .show {
      transition: opacity 400ms;
    }
    .hide {
      opacity: 0;
    }

#### modern

    el.classList.replace('hide', 'show');
    

    .show {
      transition: opacity 400ms;
    }
    .hide {
      opacity: 0;
    }


### [Fade Out](#fade_out)

#### jquery

    $(el).fadeOut();

#### ie8+

    function fadeOut(el, speed = 400) {
      var opacity = 1;
    
      el.style.opacity = 1;
      el.style.filter = '';
    
      var last = +new Date();
      var tick = function () {
        opacity -= (new Date() - last) / speed;
        if (opacity < 0) opacity = 0;
        el.style.opacity = opacity;
        el.style.filter = 'alpha(opacity=' + 100 * opacity + ')';
    
        last = +new Date();
    
        if (opacity > 0) {
          (window.requestAnimationFrame && requestAnimationFrame(tick)) ||
            setTimeout(tick, 16);
        }
      };
    
      tick();
    }
    
    fadeOut(el);

#### ie9+

    function fadeOut(el, speed = 400) {
      el.style.opacity = 1;
    
      var last = +new Date();
      var tick = function () {
        el.style.opacity = +el.style.opacity - (new Date() - last) / speed;
        if (opacity < 0) opacity = 0;
        last = +new Date();
    
        if (+el.style.opacity > 0) {
          (window.requestAnimationFrame && requestAnimationFrame(tick)) ||
            setTimeout(tick, 16);
        }
      };
    
      tick();
    }
    
    fadeOut(el);

#### ie10+

    el.classList.add('hide');
    el.classList.remove('show');
    

    .show {
      opacity: 1;
    }
    .hide {
      opacity: 0;
      transition: opacity 400ms;
    }

#### modern

    el.classList.replace('show', 'hide');
    

    .show {
      opacity: 1;
    }
    .hide {
      opacity: 0;
      transition: opacity 400ms;
    }


### [Hide](#hide)

#### jquery

    $(el).hide();

#### ie8+

    el.style.display = 'none';


### [Show](#show)

#### jquery

    $(el).show();

#### ie8+

    el.style.display = '';


### [Toggle](#toggle)

#### jquery

    $(el).toggle();

#### ie8+

    function toggle(el) {
      if (el.style.display == 'none') {
        el.style.display = '';
      } else {
        el.style.display = 'none';
      }
    }


[Elements](#elements)
---------------------

### Alternatives:

*   [bonzo](https://github.com/ded/bonzo)
*   [$dom](https://github.com/julienw/dollardom)

### [Add Class](#add_class)

#### jquery

    $(el).addClass(className);

#### ie8+

    if (el.classList) {
      el.classList.add(className);
    } else {
      var current = el.className,
        found = false;
      var all = current.split(' ');
      for (var i = 0; i < all.length, !found; i++) found = all[i] === className;
      if (!found) {
        if (current === '') el.className = className;
        else el.className += ' ' + className;
      }
    }

#### ie10+

    el.classList.add(className);


### [After](#after)

#### jquery

    $(target).after(element);

#### ie8+

    target.insertAdjacentElement('afterend', element);

#### modern

    target.after(element);


### [Append](#append)

#### jquery

    $(parent).append(el);

#### ie8+

    parent.appendChild(el);

#### modern

    parent.append(el);


### [Append To](#append_to)

#### jquery

    $(el).appendTo(parent);

#### ie8+

    parent.appendChild(el);

#### modern

    parent.append(el);


### [Before](#before)

#### jquery

    $(target).before(element);

#### ie8+

    target.insertAdjacentElement('beforebegin', element);

#### modern

    target.before(el);


### [Children](#children)

#### jquery

    $(el).children();

#### ie8+

    var children = [];
    for (var i = el.children.length; i--; ) {
      // Skip comment nodes on IE8
      if (el.children[i].nodeType != 8) children.unshift(el.children[i]);
    }

#### ie9+

    el.children;


### [Clone](#clone)

#### jquery

    $(el).clone();

#### ie8+

    el.cloneNode(true);


### [Closest](#closest)

#### jquery

    $(el).closest(sel);

#### ie8+

    function closest(el, sel) {
      Element.prototype.matches ||
        (Element.prototype.matches =
          Element.prototype.matchesSelector ||
          Element.prototype.mozMatchesSelector ||
          Element.prototype.msMatchesSelector ||
          Element.prototype.oMatchesSelector ||
          Element.prototype.webkitMatchesSelector ||
          function (b) {
            b = (this.document || this.ownerDocument).querySelectorAll(b);
            for (var a = b.length; 0 <= --a && b.item(a) !== this; );
            return -1 < a;
          });
      Element.prototype.closest ||
        (Element.prototype.closest = function (b) {
          var a = this;
          do {
            if (a.matches(b)) return a;
            a = a.parentElement || a.parentNode;
          } while (null !== a && 1 === a.nodeType);
          return null;
        });
      return el.closest(sel);
    }
    
    closest(el, sel);

#### ie9+

    function closest(el, sel) {
      Element.prototype.matches ||
        (Element.prototype.matches =
          Element.prototype.msMatchesSelector ||
          Element.prototype.webkitMatchesSelector);
      Element.prototype.closest ||
        (Element.prototype.closest = function (c) {
          var a = this;
          do {
            if (a.matches(c)) return a;
            a = a.parentElement || a.parentNode;
          } while (null !== a && 1 === a.nodeType);
          return null;
        });
      return el.closest(sel);
    }
    
    closest(el, sel);

#### ie10+

    el.closest(sel);


### [Contains](#contains)

#### jquery

    $.contains(el, child);

#### ie8+

    el !== child && el.contains(child);

#### modern

    node.contains(anotherNode);


### [Contains Selector](#contains_selector)

#### Alternatives:

*   [xpath](https://www.w3schools.com/xml/xpath_intro.asp)


#### jquery

    $("div:contains('my text')");

#### modern

    [...document.querySelectorAll('div')].filter((el) =>
      el.textContent.includes('my text')
    );


### [Contents](#contents)

#### jquery

    $(el).contents();

#### modern

    el.childNodes;


### [Create Elements](#create_elements)

#### jquery

    $('<div>Hello World!</div>');

#### ie8+

    function generateElements(html) {
      var div = document.createElement('div');
      div.innerHTML = html;
      return div.children;
    }
    
    generateElements('<div>Hello World!</div>');

#### modern

    function generateElements(html) {
      const template = document.createElement('template');
      template.innerHTML = html.trim();
      return template.content.children;
    }
    
    generateElements('<div>Hello World!</div>');


### [Each](#each)

#### jquery

    $(selector).each(function (i, el) {});

#### ie8+

    function forEachElement(selector, fn) {
      var elements = document.querySelectorAll(selector);
      for (var i = 0; i < elements.length; i++) fn(elements[i], i);
    }
    
    forEachElement(selector, function (el, i) {});

#### ie9+

    var elements = document.querySelectorAll(selector);
    Array.prototype.forEach.call(elements, function (el, i) {});

#### modern

    document.querySelectorAll(selector).forEach((el, i) => {});


### [Empty](#empty)

#### jquery

    $(el).empty();
    

#### ie8+

    while (el.firstChild) el.removeChild(el.firstChild);
    

#### modern

    el.replaceChildren();
    

### [Filter](#filter)

#### jquery

    $(selector).filter(filterFn);
    

#### ie8+

    function filter(selector, filterFn) {
      var elements = document.querySelectorAll(selector);
      var out = [];
      for (var i = elements.length; i--; ) {
        if (filterFn(elements[i])) out.unshift(elements[i]);
      }
      return out;
    }
    
    filter(selector, filterFn);
    

#### ie9+

    Array.prototype.filter.call(document.querySelectorAll(selector), filterFn);
    

#### modern

    [...document.querySelectorAll(selector)].filter(filterFn);
    

### [Find Children](#find_children)

#### jquery

    $(el).find(selector);
    

#### ie8+

    el.querySelectorAll(selector);
    

#### modern

    // For direct descendants only, see https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelectorAll#user_notes
    el.querySelectorAll(`:scope ${selector}`);
    

### [Find Elements](#find_elements)

#### Alternatives:

*   [qwery](https://github.com/ded/qwery)
*   [sizzle](https://sizzlejs.com/)

#### jquery

    $('.my #awesome selector');
    

#### ie8+

    document.querySelectorAll('.my #awesome selector');
    

### [Find Selector](#find_selector)

#### jquery

    $(el).find(selector).length;
    

#### ie8+

    !!el.querySelector(selector);
    

### [First](#first)

#### jquery

    $(el).first();
    

#### ie8+

    document.querySelector(el);
    

### [Get Attributes](#get_attributes)

#### jquery

    $(el).attr('tabindex');
    

#### ie8+

    el.getAttribute('tabindex');
    

### [Get Height](#get_height)

#### jquery

    $(el).height();
    

#### ie8+

    function getHeight(el) {
      var d = /^\d+(px)?$/i;
      if (window.getComputedStyle)
        el = parseFloat(getComputedStyle(el, null).height.replace('px', ''));
      else {
        var c = el.currentStyle.height;
        if (d.test(c)) el = parseInt(c);
        else {
          d = el.style.left;
          var e = el.runtimeStyle.left;
          el.runtimeStyle.left = el.currentStyle.left;
          el.style.left = c || 0;
          c = el.style.pixelLeft;
          el.style.left = d;
          el.runtimeStyle.left = e;
          el = c;
        }
      }
      return el;
    }
    
    getHeight(el);
    

#### ie9+

    parseFloat(getComputedStyle(el, null).height.replace('px', ''));
    

#### modern

    el.getBoundingClientRect().height;
    

### [Get HTML](#get_html)

#### jquery

    $(el).html();
    

#### ie8+

    el.innerHTML;
    

### [Get Outer HTML](#get_outer_html)

#### jquery

    $(el).prop('outerHTML');
    

#### ie8+

    el.outerHTML;
    

### [Get Style](#get_style)

#### jquery

    $(el).css(ruleName);
    

#### ie8+

    // Varies based on the properties being retrieved, some can be retrieved from el.currentStyle
    // https://github.com/jonathantneal/Polyfills-for-IE8/blob/master/getComputedStyle.js
    

#### ie9+

    getComputedStyle(el)[ruleName];
    

### [Get Text](#get_text)

#### jquery

    $(el).text();
    

#### ie8+

    el.textContent || el.innerText;
    

#### ie9+

    el.textContent;
    

### [Get Width](#get_width)

#### jquery

    $(el).width();
    

#### ie8+

    function getWidth(el) {
      var d = /^\d+(px)?$/i;
      if (window.getComputedStyle)
        el = parseFloat(getComputedStyle(el, null).width.replace('px', ''));
      else {
        var c = el.currentStyle.width;
        if (d.test(c)) el = parseInt(c);
        else {
          d = el.style.left;
          var e = el.runtimeStyle.left;
          el.runtimeStyle.left = el.currentStyle.left;
          el.style.left = c || 0;
          c = el.style.pixelLeft;
          el.style.left = d;
          el.runtimeStyle.left = e;
          el = c;
        }
      }
      return el;
    }
    
    getWidth(el);
    

#### ie9+

    parseFloat(getComputedStyle(el, null).width.replace('px', ''));
    

#### modern

    el.getBoundingClientRect().width;
    

### [Has Class](#has_class)

#### jquery

    $(el).hasClass(className);
    

#### ie8+

    if (el.classList) el.classList.contains(className);
    else new RegExp('(^| )' + className + '( |$)', 'gi').test(el.className);
    

#### ie10+

    el.classList.contains(className);
    

### [Index](#index)

#### jquery

    $(el).index();
    

#### ie8+

    function index(el) {
      if (!el) return -1;
      var i = 0;
      while (el) {
        el = el.previousSibling;
        if (el && el.nodeType === 1) i++;
      }
      return i;
    }
    

#### ie9+

    function index(el) {
      if (!el) return -1;
      var i = 0;
      while ((el = el.previousElementSibling)) {
        i++;
      }
      return i;
    }
    

#### modern

    [...el.parentNode.children].indexOf(el);
    

### [Inner Height](#inner_height)

#### jquery

    $(el).innerHeight();
    $(el).innerHeight(150);
    

#### modern

    function innerHeight(el, value) {
      if (value === undefined) {
        return el.clientHeight;
      } else {
        el.style.height = value;
      }
    }
    
    innerHeight(el);
    innerHeight(el, 150);
    

### [Inner Width](#inner_width)

#### jquery

    $(el).innerWidth();
    $(el).innerWidth(150);
    

#### modern

    function innerWidth(el, value) {
      if (value === undefined) {
        return el.clientWidth;
      } else {
        el.style.width = value;
      }
    }
    
    innerWidth(el);
    innerWidth(el, 150);
    

### [Is Hidden](#is_hidden)

#### jquery

    $(el).is(':hidden');
    

#### modern

    function isHidden(el) {
      return !(el.offsetWidth || el.offsetHeight || el.getClientRects().length);
    }
    

### [Is Visible](#is_visible)

#### jquery

    $(el).is(':visible');
    

#### modern

    function isVisible(el) {
      return !!(el.offsetWidth || el.offsetHeight || el.getClientRects().length);
    }
    

### [Last](#last)

#### jquery

    $(el).last();
    

#### ie8+

    var els = document.querySelectorAll(el);
    els[els.length - 1];
    

#### modern

    [...document.querySelectorAll(el)].at(-1);
    

### [Matches](#matches)

#### jquery

    $(el).is($(otherEl));
    

#### ie8+

    el === otherEl;
    

### [Matches Selector](#matches_selector)

#### jquery

    $(el).is('.my-class');
    

#### ie8+

    var matches = function (el, selector) {
      var _matches =
        el.matches ||
        el.matchesSelector ||
        el.msMatchesSelector ||
        el.mozMatchesSelector ||
        el.webkitMatchesSelector ||
        el.oMatchesSelector;
    
      if (_matches) {
        return _matches.call(el, selector);
      } else {
        if (el.parentNode === null) return false;
        var nodes = el.parentNode.querySelectorAll(selector);
        for (var i = nodes.length; i--; ) {
          if (nodes[i] === el) return true;
        }
        return false;
      }
    };
    
    matches(el, '.my-class');
    

#### ie9+

    var matches = function (el, selector) {
      return (
        el.matches ||
        el.matchesSelector ||
        el.msMatchesSelector ||
        el.mozMatchesSelector ||
        el.webkitMatchesSelector ||
        el.oMatchesSelector
      ).call(el, selector);
    };
    
    matches(el, '.my-class');
    

#### modern

    el.matches('.my-class');
    

### [Next](#next)

#### jquery

    $(el).next();
    

#### ie8+

    // nextSibling can include text nodes
    function nextElementSibling(el) {
      do {
        el = el.nextSibling;
      } while (el && el.nodeType !== 1);
      return el;
    }
    
    el.nextElementSibling || nextElementSibling(el);
    

#### ie9+

    el.nextElementSibling;
    

#### modern

    function next(el, selector) {
      const nextEl = el.nextElementSibling;
      if (!selector || (nextEl && nextEl.matches(selector))) {
        return nextEl;
      }
      return null;
    }
    
    next(el);
    // Or, with an optional selector
    next(el, '.my-selector');
    

### [Offset](#offset)

#### jquery

    $(el).offset();
    

#### ie8+

    function offset(el) {
      var docElem = document.documentElement;
      var rect = el.getBoundingClientRect();
      return {
        top:
          rect.top +
          (window.pageYOffset || docElem.scrollTop) -
          (docElem.clientTop || 0),
        left:
          rect.left +
          (window.pageXOffset || docElem.scrollLeft) -
          (docElem.clientLeft || 0)
      };
    }
    

#### ie9+

    function offset(el) {
      box = el.getBoundingClientRect();
      docElem = document.documentElement;
      return {
        top: box.top + window.pageYOffset - docElem.clientTop,
        left: box.left + window.pageXOffset - docElem.clientLeft
      };
    }
    

### [Offset Parent](#offset_parent)

#### jquery

    $(el).offsetParent();
    

#### ie8+

    el.offsetParent || el;
    

### [Outer Height](#outer_height)

#### jquery

    $(el).outerHeight();
    

#### ie8+

    el.offsetHeight;
    

### [Outer Height With Margin](#outer_height_with_margin)

#### jquery

    $(el).outerHeight(true);
    

#### ie8+

    function outerHeight(el) {
      var height = el.offsetHeight;
      var style = el.currentStyle || getComputedStyle(el);
    
      height += parseFloat(style.marginTop) + parseFloat(style.marginBottom);
      return height;
    }
    
    outerHeight(el);
    

#### ie9+

    function outerHeight(el) {
      var height = el.offsetHeight;
      var style = getComputedStyle(el);
    
      height += parseFloat(style.marginTop) + parseFloat(style.marginBottom);
      return height;
    }
    
    outerHeight(el);
    

#### modern

    function outerHeight(el) {
      const style = getComputedStyle(el);
    
      return (
        el.getBoundingClientRect().height +
        parseFloat(style.marginTop) +
        parseFloat(style.marginBottom)
      );
    }
    
    outerHeight(el);
    

### [Outer Width](#outer_width)

#### jquery

    $(el).outerWidth();
    

#### ie8+

    el.offsetWidth;
    

### [Outer Width With Margin](#outer_width_with_margin)

#### jquery

    $(el).outerWidth(true);
    

#### ie8+

    function outerWidth(el) {
      var width = el.offsetWidth;
      var style = el.currentStyle || getComputedStyle(el);
    
      width += parseFloat(style.marginLeft) + parseFloat(style.marginRight);
      return width;
    }
    
    outerWidth(el);
    

#### ie9+

    function outerWidth(el) {
      var width = el.offsetWidth;
      var style = getComputedStyle(el);
    
      width += parseFloat(style.marginLeft) + parseFloat(style.marginRight);
      return width;
    }
    
    outerWidth(el);
    

#### modern

    function outerWidth(el) {
      const style = getComputedStyle(el);
    
      return (
        el.getBoundingClientRect().width +
        parseFloat(style.marginLeft) +
        parseFloat(style.marginRight)
      );
    }
    
    outerWidth(el);
    

### [Parent](#parent)

#### jquery

    $(el).parent();
    

#### ie8+

    el.parentNode;
    

### [Parents](#parents)

#### jquery

    $(el).parents(selector);
    

#### ie9+

    function parents(el, selector) {
      var parents = [];
      while ((el = el.parentNode) && el !== document) {
        // See "Matches Selector" above
        if (!selector || matches(el, selector)) parents.push(el);
      }
      return parents;
    }
    

#### modern

    function parents(el, selector) {
      const parents = [];
      while ((el = el.parentNode) && el !== document) {
        if (!selector || el.matches(selector)) parents.push(el);
      }
      return parents;
    }
    

### [Position](#position)

#### jquery

    $(el).position();
    

#### ie8+

    function position(el) {
      var box = el.getBoundingClientRect();
      var docElem = document.documentElement;
      var marginLeft = 0;
      var marginTop = 0;
      if (typeof getComputedStyle === 'function') {
        var style = window.getComputedStyle(el);
        marginLeft = parseInt(style.marginLeft, 10);
        marginTop = parseInt(style.marginTop, 10);
      } else if (el.currentStyle) {
        marginLeft = el.currentStyle['marginLeft']
          ? parseInt(el.currentStyle['marginLeft'], 10)
          : 0;
        marginTop = el.currentStyle['marginTop']
          ? parseInt(el.currentStyle['marginTop'], 10)
          : 0;
      }
      return {
        top: box.top + (window.pageYOffset || docElem.scrollTop) - marginTop,
        left: box.left + (window.pageXOffset || docElem.scrollLeft) - marginLeft
      };
    }
    

#### modern

    function position(el) {
      const {top, left} = el.getBoundingClientRect();
      const {marginTop, marginLeft} = getComputedStyle(el);
      return {
        top: top - parseInt(marginTop, 10),
        left: left - parseInt(marginLeft, 10)
      };
    }
    

### [Position Relative To Viewport](#position_relative_to_viewport)

#### jquery

    function offset(el) {
      var offset = $(el).offset();
      return {
        top: offset.top - document.body.scrollTop,
        left: offset.left - document.body.scrollLeft
      };
    }
    

#### ie8+

    el.getBoundingClientRect();
    

### [Prepend](#prepend)

#### jquery

    $(parent).prepend(el);
    

#### ie8+

    parent.insertBefore(el, parent.firstChild);
    

#### modern

    parent.prepend(el);
    

### [Prev](#prev)

#### jquery

    $(el).prev();
    // Or, with an optional selector
    $(el).prev('.my-selector');
    

#### ie8+

    // prevSibling can include text nodes
    function previousElementSibling(el) {
      do {
        el = el.previousSibling;
      } while (el && el.nodeType !== 1);
      return el;
    }
    
    el.previousElementSibling || previousElementSibling(el);
    

#### ie9+

    el.previousElementSibling;
    

#### modern

    function prev(el, selector) {
      const prevEl = el.previousElementSibling;
      if (!selector || (prevEl && prevEl.matches(selector))) {
        return prevEl;
      }
      return null;
    }
    
    prev(el);
    // Or, with an optional selector
    prev(el, '.my-selector');
    

### [Remove](#remove)

#### jquery

    $(el).remove();
    
    // multiple elements
    $(selector).remove();
    

#### ie8+

    if (el.parentNode !== null) {
      el.parentNode.removeChild(el);
    }
    

#### modern

    el.remove();
    
    // multiple elements
    for (const el of document.querySelectorAll(selector)) {
      el.remove();
    }
    

### [Remove Attributes](#remove_attributes)

#### jquery

    $(el).removeAttr('tabindex');
    

#### ie8+

    el.removeAttribute('tabindex');
    

### [Remove Class](#remove_class)

#### jquery

    $(el).removeClass(className);
    

#### ie8+

    function removeClass(el, className) {
      var classes = className.split(' ');
      for (var i = 0; i < classes.length; i++) {
        if (el.classList) {
          el.classList.remove(classes[i]);
        } else {
          el.className = el.className
            .replace(new RegExp('(?:^|\\s)' + classes[i] + '(?:\\s|$)'), ' ')
            .replace(new RegExp(/^\s+|\s+$/g), '');
        }
      }
    }
    

#### ie10+

    el.classList.remove(className);
    

### [Replace From HTML](#replace_from_html)

#### jquery

    $(el).replaceWith(string);
    

#### ie8+

    el.outerHTML = string;
    

### [Scroll Left](#scroll_left)

#### jquery

    $(window).scrollLeft();
    

#### modern

    function scrollLeft(el, value) {
      var win;
      if (el.window === el) {
        win = el;
      } else if (el.nodeType === 9) {
        win = el.defaultView;
      }
    
      if (value === undefined) {
        return win ? win.pageXOffset : el.scrollLeft;
      }
    
      if (win) {
        win.scrollTo(value, win.pageYOffset);
      } else {
        el.scrollLeft = value;
      }
    }
    

### [Scroll Top](#scroll_top)

#### jquery

    $(window).scrollTop();
    

#### modern

    function scrollTop(el, value) {
      var win;
      if (el.window === el) {
        win = el;
      } else if (el.nodeType === 9) {
        win = el.defaultView;
      }
    
      if (value === undefined) {
        return win ? win.pageYOffset : el.scrollTop;
      }
    
      if (win) {
        win.scrollTo(win.pageXOffset, value);
      } else {
        el.scrollTop = value;
      }
    }
    

### [Serialize](#serialize)

#### jquery

    $(formElement).serialize();
    

#### modern

    new URLSearchParams(new FormData(formElement)).toString();
    

### [Set Attributes](#set_attributes)

#### jquery

    $(el).attr('tabindex', 3);
    

#### ie8+

    el.setAttribute('tabindex', 3);
    

### [Set Height](#set_height)

#### jquery

    $(el).height(val);
    

#### ie8+

    function setHeight(el, val) {
      if (typeof val === 'function') val = val();
      if (typeof val === 'string') el.style.height = val;
      else el.style.height = val + 'px';
    }
    
    setHeight(el, val);
    

### [Set HTML](#set_html)

#### jquery

    $(el).html(string);
    

#### ie8+

    el.innerHTML = string;
    

### [Set Style](#set_style)

#### jquery

    $(el).css('border-width', '20px');
    

#### ie8+

    // Use a class if possible
    el.style.borderWidth = '20px';
    

### [Set Text](#set_text)

#### jquery

    $(el).text(string);
    

#### ie8+

    if (el.textContent !== undefined) el.textContent = string;
    else el.innerText = string;
    

#### ie9+

    el.textContent = string;
    

### [Set Width](#set_width)

#### jquery

    $(el).width(val);
    

#### ie8+

    function setWidth(el, val) {
      if (typeof val === 'function') val = val();
      if (typeof val === 'string') el.style.width = val;
      else el.style.width = val + 'px';
    }
    
    setWidth(el, val);
    

### [Siblings](#siblings)

#### jquery

    $(el).siblings();
    

#### ie8+

    var siblings = function (el) {
      if (el.parentNode === null) return [];
    
      var siblingElements = Array.prototype.slice.call(el.parentNode.children);
    
      for (var i = siblingElements.length; i--; ) {
        if (siblingElements[i] === el) {
          return siblingElements.splice(i, 1);
        }
      }
    
      return siblingElements;
    };
    
    siblings(el);
    

#### ie9+

    var siblings = function (el) {
      if (el.parentNode === null) return [];
    
      return Array.prototype.filter.call(el.parentNode.children, function (child) {
        return child !== el;
      });
    };
    
    siblings(el);
    

#### modern

    [...el.parentNode.children].filter((child) => child !== el);
    

### [Toggle Class](#toggle_class)

#### jquery

    $(el).toggleClass(className);
    

#### ie8+

    if (el.classList) {
      el.classList.toggle(className);
    } else {
      var classes = el.className.split(' ');
      var existingIndex = -1;
      for (var i = classes.length; i--; ) {
        if (classes[i] === className) existingIndex = i;
      }
    
      if (existingIndex >= 0) classes.splice(existingIndex, 1);
      else classes.push(className);
    
      el.className = classes.join(' ');
    }
    

#### ie9+

    if (el.classList) {
      el.classList.toggle(className);
    } else {
      var classes = el.className.split(' ');
      var existingIndex = classes.indexOf(className);
    
      if (existingIndex >= 0) classes.splice(existingIndex, 1);
      else classes.push(className);
    
      el.className = classes.join(' ');
    }
    

#### ie10+

    el.classList.toggle(className);
    

### [Unwrap](#unwrap)

#### jquery

    $(el).unwrap();
    

#### modern

    el.replaceWith(...el.childNodes);
    

### [Val](#val)

#### jquery

    $(el).val();
    

#### modern

    function val(el) {
      if (el.options && el.multiple) {
        return el.options
          .filter((option) => option.selected)
          .map((option) => option.value);
      } else {
        return el.value;
      }
    }
    

### [Wrap](#wrap)

#### jquery

    el.wrap('<div></div>');
    

#### modern

    function wrap(el) {
      const wrappingElement = document.createElement('div');
      el.replaceWith(wrappingElement);
      wrappingElement.appendChild(el);
    }
    

[Events](#events)
-----------------

### Alternatives:

*   [ftdomdelegate](https://github.com/ftlabs/ftdomdelegate)
*   [defer](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attr-defer)
*   [modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

### [Click](#click)

#### jquery

    $(el).click(function () {});
    

#### ie8+

    var onClick = function (element, handler) {
      if (element.addEventListener) {
        element.addEventListener('click', handler, false);
      } else {
        element.attachEvent('onclick', handler);
      }
    };
    
    onClick(el, function () {});
    

#### ie9+

    el.addEventListener('click', function () {});
    

#### modern

    el.addEventListener('click', () => {});
    

### [Delegate](#delegate)

#### jquery

    $(document).on(eventName, elementSelector, handler);
    

#### ie8+

    document.addEventListener(
      eventName,
      function (e) {
        // loop parent nodes from the target to the delegation node
        for (
          var target = e.target;
          target && target != this;
          target = target.parentNode
        ) {
          if (target.matches(elementSelector)) {
            handler.call(target, e);
            break;
          }
        }
      },
      false
    );
    

#### modern

    document.addEventListener(eventName, (event) => {
      if (event.target.closest(elementSelector)) {
        handler.call(event.target, event);
      }
    });
    

### [Off](#off)

#### jquery

    $(el).off(eventName, eventHandler);
    

#### ie8+

    function removeEventListener(el, eventName, handler) {
      if (el.removeEventListener) el.removeEventListener(eventName, handler);
      else el.detachEvent('on' + eventName, handler);
    }
    
    removeEventListener(el, eventName, handler);
    

#### ie9+

    el.removeEventListener(eventName, eventHandler);
    

### [On](#on)

#### jquery

    $(el).on(eventName, eventHandler);
    // Or when you want to delegate event handling
    $(el).on(eventName, selector, eventHandler);
    

#### ie8+

    function addEventListener(el, eventName, handler) {
      if (el.addEventListener) {
        el.addEventListener(eventName, handler);
        return handler;
      } else {
        var wrappedHandler = function (event) {
          handler.call(el, event);
        };
        el.attachEvent('on' + eventName, wrappedHandler);
        return wrappedHandler;
      }
    }
    
    // Use the return value to remove that event listener, see #off
    var handlerToRemove = addEventListener(el, eventName, handler);
    

#### ie9+

    function addEventListener(el, eventName, eventHandler, selector) {
      if (selector) {
        var wrappedHandler = function (e) {
          if (e.target && e.target.matches(selector)) {
            eventHandler(e);
          }
        };
        el.addEventListener(eventName, wrappedHandler);
        return wrappedHandler;
      } else {
        el.addEventListener(eventName, eventHandler);
        return eventHandler;
      }
    }
    
    // Use the return value to remove that event listener, see #off
    addEventListener(el, eventName, eventHandler);
    // Or when you want to delegate event handling
    addEventListener(el, eventName, eventHandler, selector);
    

#### modern

    function addEventListener(el, eventName, eventHandler, selector) {
      if (selector) {
        const wrappedHandler = (e) => {
          if (!e.target) return;
          const el = e.target.closest(selector);
          if (el) {
            eventHandler.call(el, e);
          }
        };
        el.addEventListener(eventName, wrappedHandler);
        return wrappedHandler;
      } else {
        const wrappedHandler = (e) => {
          eventHandler.call(el, e);
        };
        el.addEventListener(eventName, wrappedHandler);
        return wrappedHandler;
      }
    }
    
    // Use the return value to remove that event listener, see #off
    addEventListener(el, eventName, eventHandler);
    // Or when you want to delegate event handling
    addEventListener(el, eventName, eventHandler, selector);
    

### [Ready](#ready)

#### jquery

    $(document).ready(function () {});
    

#### ie8+

    function ready(fn) {
      if (document.readyState != 'loading') {
        fn();
      } else if (document.addEventListener) {
        document.addEventListener('DOMContentLoaded', fn);
      } else {
        document.attachEvent('onreadystatechange', function () {
          if (document.readyState != 'loading') fn();
        });
      }
    }
    

#### ie9+

    function ready(fn) {
      if (
        document.attachEvent
          ? document.readyState === 'complete'
          : document.readyState !== 'loading'
      ) {
        fn();
      } else {
        document.addEventListener('DOMContentLoaded', fn);
      }
    }
    

#### modern

    function ready(fn) {
      if (document.readyState !== 'loading') {
        fn();
      } else {
        document.addEventListener('DOMContentLoaded', fn);
      }
    }
    

### [Trigger Custom](#trigger_custom)

#### Alternatives:

*   [EventEmitter](https://github.com/Wolfy87/EventEmitter)
*   [Vine](https://github.com/arextar/Vine)
*   [microevent](https://github.com/jeromeetienne/microevent.js)

#### jquery

    $(el).trigger('my-event', {some: 'data'});
    

#### ie8+

    // Custom events are not natively supported, so you have to hijack a random
    // event.
    //
    // Just use jQuery.
    

#### ie9+

    if (window.CustomEvent && typeof window.CustomEvent === 'function') {
      var event = new CustomEvent('my-event', {detail: {some: 'data'}});
    } else {
      var event = document.createEvent('CustomEvent');
      event.initCustomEvent('my-event', true, true, {some: 'data'});
    }
    
    el.dispatchEvent(event);
    

#### modern

    const event = new CustomEvent('my-event', {detail: {some: 'data'}});
    el.dispatchEvent(event);
    

### [Trigger Native](#trigger_native)

#### jquery

    $(el).trigger('focus');
    

#### ie8+

    function trigger(el, eventType) {
      if (typeof eventType === 'string' && typeof el[eventType] === 'function') {
        el[eventType]();
      } else if (eventType === 'string') {
        if (document.createEvent) {
          var event = document.createEvent('HTMLEvents');
          event.initEvent(eventType, true, false);
          el.dispatchEvent(event);
        } else {
          el.fireEvent('on' + eventType);
        }
      } else {
        el.dispatchEvent(eventType);
      }
    }
    
    // For a full list of event types: https://developer.mozilla.org/en-US/docs/Web/API/document.createEvent
    trigger(el, 'focus');
    

#### ie9+

    function trigger(el, eventType) {
      if (typeof eventType === 'string' && typeof el[eventType] === 'function') {
        el[eventType]();
      } else {
        var event;
        if (eventType === 'string') {
          event = document.createEvent('HTMLEvents');
          event.initEvent(eventType, true, false);
        } else {
          event = eventType;
        }
        el.dispatchEvent(event);
      }
    }
    
    // For a full list of event types: https://developer.mozilla.org/en-US/docs/Web/API/document.createEvent
    trigger(el, 'focus');
    

#### modern

    function trigger(el, eventType) {
      if (typeof eventType === 'string' && typeof el[eventType] === 'function') {
        el[eventType]();
      } else {
        const event =
          typeof eventType === 'string'
            ? new Event(eventType, {bubbles: true})
            : eventType;
        el.dispatchEvent(event);
      }
    }
    
    trigger(el, 'focus');
    // For a full list of event types: https://developer.mozilla.org/en-US/docs/Web/API/Event
    trigger(el, new PointerEvent('pointerover'));
    

[Utils](#utils)
---------------

### [Array Each](#array_each)

#### jquery

    $.each(array, function (i, item) {});
    

#### ie8+

    function forEach(array, fn) {
      for (var i = 0; i < array.length; i++) fn(array[i], i);
    }
    
    forEach(array, function (item, i) {});
    

#### ie9+

    array.forEach(function (item, i) {});
    

#### modern

    array.forEach((item, i) => {});
    

### [Bind](#bind)

#### jquery

    $.proxy(fn, context);
    

#### ie8+

    fn.apply(context, arguments);
    

#### ie9+

    fn.bind(context);
    

### [Deep Extend](#deep_extend)

#### jquery

    $.extend(true, {}, objA, objB);
    

#### ie8+

    function deepExtend(out) {
      out = out || {};
    
      for (var i = 1; i < arguments.length; i++) {
        var obj = arguments[i];
    
        if (!obj) continue;
    
        for (var key in obj) {
          if (obj.hasOwnProperty(key)) {
            var rawType = Object.prototype.toString.call(obj[key]);
            if (rawType === '[object Object]') {
              out[key] = deepExtend(out[key], obj[key]);
            } else if (rawType === '[object Array]') {
              out[key] = deepExtend(new Array(obj[key].length), obj[key]);
            } else {
              out[key] = obj[key];
            }
          }
        }
      }
    
      return out;
    }
    
    deepExtend({}, objA, objB);
    

#### modern

    function deepExtend(out, ...arguments_) {
      if (!out) {
        return {};
      }
    
      for (const obj of arguments_) {
        if (!obj) {
          continue;
        }
    
        for (const [key, value] of Object.entries(obj)) {
          switch (Object.prototype.toString.call(value)) {
            case '[object Object]':
              out[key] = out[key] || {};
              out[key] = deepExtend(out[key], value);
              break;
            case '[object Array]':
              out[key] = deepExtend(new Array(value.length), value);
              break;
            default:
              out[key] = value;
          }
        }
      }
    
      return out;
    }
    
    deepExtend({}, objA, objB);
    

### [Extend](#extend)

#### Alternatives:

*   [Lodash](https://lodash.com/docs#assign)
*   [Underscore](https://underscorejs.org/#extend)
*   [ECMA6](https://www.2ality.com/2014/01/object-assign.html)

#### jquery

    $.extend({}, objA, objB);
    

#### ie8+

    var extend = function (out) {
      out = out || {};
    
      for (var i = 1; i < arguments.length; i++) {
        if (!arguments[i]) continue;
    
        for (var key in arguments[i]) {
          if (arguments[i].hasOwnProperty(key)) out[key] = arguments[i][key];
        }
      }
    
      return out;
    };
    
    extend({}, objA, objB);
    

#### modern

    const result = {...objA, ...objB};
    

### [Index Of](#index_of)

#### jquery

    $.inArray(item, array);
    

#### ie8+

    function indexOf(array, item) {
      for (var i = 0; i < array.length; i++) {
        if (array[i] === item) return i;
      }
      return -1;
    }
    
    indexOf(array, item);
    

#### ie9+

    array.indexOf(item);
    

### [Is Array](#is_array)

#### jquery

    $.isArray(arr);
    

#### ie8+

    isArray =
      Array.isArray ||
      function (arr) {
        return Object.prototype.toString.call(arr) == '[object Array]';
      };
    
    isArray(arr);
    

#### ie9+

    Array.isArray(arr);
    

### [Is Numeric](#is_numeric)

#### jquery

    $.isNumeric(val);
    

#### ie8+

    function isNumeric(num) {
      if (typeof num === 'number') return num - num === 0;
      if (typeof num === 'string' && num.trim() !== '')
        return Number.isFinite ? Number.isFinite(+num) : isFinite(+num);
      return false;
    }
    
    isNumeric(val);
    

#### modern

    function isNumeric(num) {
      if (typeof num === 'number') return num - num === 0;
      if (typeof num === 'string' && num.trim() !== '')
        return Number.isFinite(+num);
      return false;
    }
    
    isNumeric(val);
    

### [Map](#map)

#### jquery

    $.map(array, function (value, index) {});
    

#### ie8+

    function map(arr, fn) {
      var results = [];
      for (var i = 0; i < arr.length; i++) results.push(fn(arr[i], i));
      return results;
    }
    
    map(array, function (value, index) {});
    

#### ie9+

    array.map(function (value, index) {});
    

#### modern

    array.map((value, index) => {});
    

### [Now](#now)

#### jquery

    $.now();
    

#### ie8+

    new Date().getTime();
    

#### ie9+

    Date.now();
    

### [Object Each](#object_each)

#### jquery

    $.each(obj, function (key, value) {});
    

#### ie8+

    function objectEach(obj, callback) {
      for (var key in obj) {
        if (Object.prototype.hasOwnProperty.call(obj, key)) {
          callback(key, obj[key]);
        }
      }
    }
    
    objectEach(obj, function (key, value) {});
    

#### modern

    for (const [key, value] of Object.entries(obj)) {
    }
    

### [Parse HTML](#parse_html)

#### jquery

    $.parseHTML(htmlString);
    

#### ie8+

    var parseHTML = function (str) {
      var el = document.createElement('div');
      el.innerHTML = str;
      return el.childNodes;
    };
    
    parseHTML(htmlString);
    

#### ie9+

    var parseHTML = function (str) {
      var tmp = document.implementation.createHTMLDocument('');
      tmp.body.innerHTML = str;
      return Array.prototype.slice.call(tmp.body.childNodes);
    };
    
    parseHTML(htmlString);
    

#### modern

    function parseHTML(str) {
      const tmp = document.implementation.createHTMLDocument('');
      tmp.body.innerHTML = str;
      return [...tmp.body.childNodes];
    }
    
    parseHTML(htmlString);
    

### [Parse JSON](#parse_json)

#### jquery

    $.parseJSON(string);
    

#### ie8+

    JSON.parse(string);
    

### [Slice](#slice)

#### jquery

    $(els).slice(begin, end);
    

#### ie8+

    function slice(els, start, end) {
      var f = Array.prototype.slice;
      try {
        f.call(document.documentElement);
      } catch (h) {
        Array.prototype.slice = function (g, b) {
          b = 'undefined' !== typeof b ? b : this.length;
          if ('[object Array]' === Object.prototype.toString.call(this))
            return f.call(this, g, b);
          var e = [];
          var a = this.length;
          var c = g || 0;
          c = 0 <= c ? c : Math.max(0, a + c);
          var d = 'number' == typeof b ? Math.min(b, a) : a;
          0 > b && (d = a + b);
          d -= c;
          if (0 < d)
            if (((e = Array(d)), this.charAt))
              for (a = 0; a < d; a++) e[a] = this.charAt(c + a);
            else for (a = 0; a < d; a++) e[a] = this[c + a];
          return e;
        };
      }
      return els.slice(start, end);
    }
    
    slice(els, start, end);
    

#### ie9+

    els.slice(begin, end);
    

### [To Array](#to_array)

#### jquery

    $(selector).toArray();
    

#### ie8+

    function toArray(selector) {
      var array = [];
      var elements = document.querySelectorAll(selector);
      for (var i = 0; i < elements.length; i++) array.push(elements[i]);
      return array;
    }
    

#### modern

    const array = [...document.querySelectorAll(selector)];
    

### [Trim](#trim)

#### jquery

    $.trim(string);
    

#### ie8+

    string.replace(/^\s+|\s+$/g, '');
    

#### ie9+

    string.trim();
    

### [Type](#type)

#### jquery

    $.type(obj);
    

#### ie8+

    Object.prototype.toString
      .call(obj)
      .replace(/^\[object (.+)\]$/, '$1')
      .toLowerCase();

