# Introduction #

To see some examples and information look here:
http://lux.vu/iphone/oscemote/webpanels/

# Details #

Custom panels in OSCemote are basically web pages, so you can use whatever HTML/javascript creation tools you are comfortable with.

To make your own, just make an HTML page with osc: links in it and type the URL for that page into the bar at the top of the Custom panel in OSCemote.

Feel free to copy any of the examples on this page http://lux.vu/iphone/oscemote/webpanels/ as a templates to get started. They are normal HTML, CSS and JavaScript with a couple of special exceptions as follows.

  * They will be viewed with an embedded iPhone Safari (WebKit)
  * Pages are at a fixed zoom level of 1.0
  * They support osc: URLs like these:
  * osc:/simple/message
  * osc:/example/A?i=99&f=3.14
  * osc:/example/B?s=foodles

The osc: link format is defined as:
  * "osc:" followed by the OSC message path (usually words separated by slashes)
  * An optional "?" followed by one or more of the following typed arguments separated by ampersands (&):
  * "i=" followed by an integer
  * "f=" followed by a floating point number
  * "s=" followed by a string.  Strings should be escaped according to normal URL escaping rules.  Specifically spaces should be replaced by a "+" and other non-alphanumeric characters should be turned into %## codes.

I recommend using [Safari](http://www.apple.com/safari/) (Mac and Windows) on your desktop to test with as it is very similar to Safari for iPhone. You may also want to refer to this [Apple Documentation for Safari](http://developer.apple.com/safari/). You may need to sign up for the free Apple Developer program to view this documentation.

Note that Safari on the iPhone is capable of some really cool CSS effects that could be put to great use here.  See for example: [jQTouch](http://www.jqtouch.com/) and [Pie Guy](http://mrgan.tumblr.com/post/257187093/pie-guy)

# Examples #

The two example custom panels were made in Dashcode (an Apple HTML/javascript editor)
You can find the source for the example panels using View Source in your browser, or download them in a bundle here: http://lux.vu/iphone/oscemote/webpanels/examples.tgz

# Reusing the Built-in Controls #

The built-in panels aren't made with the same technology as the custom ones for two reasons.  One I added the custom panels after the built-in ones were already done and two because the custom panels aren't able to get the high performance that I had hoped.  The speed is reasonable, but not ideal, mostly because of the speed of the javascript engine.

The examples above give a starting point for similar controls, but are incomplete.

# Multiple Messages #

Note that if you use window.location="osc:..." then there is a limit of one OSC message per javascript event.  This is a side effect of the way that the javascript engine handles urls.  To get around this limitation you can create an iframe for each OSC message you want to send:

```
iFrame = document.createElement("IFRAME");
iFrame.setAttribute("src", "osc:/example/A");
document.body.appendChild(iFrame); 
iFrame.parentNode.removeChild(iFrame);
iFrame = null;
```

Thanks to Jamie Bullock for pointing me to this entry on [StackOverflow](http://stackoverflow.com/questions/2934789/triggering-shouldstartloadwithrequest-with-multiple-window-location-href-calls).