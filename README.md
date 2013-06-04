postmessage
===========

Backwards compatible window.postMessage()

**Demo**

[See an example of this library in action](http://onlineaspect.com/uploads/postmessage/parent.html) or [read how it works](http://www.onlineaspect.com/2010/01/15/backwards-compatible-postmessage/) on my blog.

**Usage**

There are two parts to using this code: posting and listening. Both are relatively simple. To post a message we call XD.postMessage with a message, a URL and the frame that we want to talk to. Notice that we start off by passing the URL of the parent page to the child frame. This is important so the child knows how to talk back to the parent.

    // pass the URL of the current parent page to the iframe using location.hash
    src = 'http://joshfraser.com/code/postmessage/child.html#' + encodeURIComponent(document.location.href);
    document.getElementById("xd_frame").src = src;

    function send(msg) {
        XD.postMessage(msg, src, frames[0]);
        return false;
    }

Setting up the listener on the child is also easy to do:

    var parent_url = decodeURIComponent(document.location.hash.replace(/^#/, ''));

    XD.receiveMessage(function(message){
        window.alert(message.data + " received on "+window.location.host);
    }, 'http://onlineaspect.com');


**Credits & license:**

* Released by [Josh Fraser](http://joshfraser.com) (joshfraz@gmail.com)
* Released under Apache 2.0 license
