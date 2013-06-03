postmessage
===========

Backwards compatible window.postMessage()

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

* [Read more about this library](http://www.onlineaspect.com/2010/01/15/backwards-compatible-postmessage/) by [Josh Fraser](http://joshfraser.com)
* Released under Apache 2.0 license
