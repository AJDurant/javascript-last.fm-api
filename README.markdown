##JavaScript last.fm API Readme

###Overview

The JavaScript last.fm API allows you to call last.fm API methods and get the
corresponding JSON responses. Basically it just acts as a wrapper that gives
easy access to API methods. Responses can be cached using the localStorage API.


###Encoding

You don't need to worry about encoding when calling API methods. Everything
should automatically be UTF-8 encoded and decoded by your browser if you set
the Content-Type for your document to UTF-8:

    <meta http-equiv="Content-Type" content="text/html;charset=utf-8" />


###Authentication

It's easy to fetch a session for a user account. This allows you to perform
actions on that account in a manner that is secure for last.fm users. All
write services require authentication.


###Submissions

Scrobbling is possible once a user is authenticated by adding their session 
data to the api call.


###Usage

You need to add the following scripts to your code in order to work with the
JavaScript last.fm API:

    <script src="lastfm.api.md5.js"></script>
    <script src="lastfm.api.js"></script>

The API depends upon jQuery for sending AJAX requests:

    <script src="//ajax.googleapis.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>

For older browser support (IE 6, 7 & 8) use the 1.x version of jQuery.

If you want to use caching, you need to add another script:

    <script src="lastfm.api.cache.js"></script>

Built in JSON support should be available in modern browsers, if you want to
be sure it's supported, include the following:

    <script src="json2.js"></script>

You can get that file at http://www.json.org/json2.js , and make sure you've
removed the first line before using it.

Now you can use the JavaScript last.fm API like this:

    /* Create a cache object */
    var cache = new LastFMCache();

    /* Create a LastFM object */
    var lastfm = new LastFM({
      apiKey    : 'f21088bf9097b49ad4e7f487abab981e',
      apiSecret : '7ccaec2093e33cded282ec7bc81c6fca',
      cache     : cache
    });

    /* Load some artist info. */
    lastfm.artist.getInfo({artist: 'The xx'}, {success: function(data){
      /* Use data. */
    }, error: function(code, message){
      /* Show error message. */
    }});

###Example

Example application code / more useful wrapper functions can be found in lastfm.js
this includes specific functions for easily calling updateNowPlaying and scrobble
and setting up the session.

The code in here relies upon jquery.cookie plugin for persistant sessions.

The toggle scrobble button functionality uses jqueryUI on:

    <input type="checkbox" id="toggleScrobble"><label for="toggleScrobble">Scrobble</label>

With the CSS:

    .toggleScrobble {
        border: none;
        background: none;
    }
    .toggleScrobble .ui-button-text {
        width: 80px;
        height: 28px;
        padding: 0;
        background: url(http://cdn.last.fm/flatness/badges/lastfm_black_small.gif);
    }
    .toggleScrobble .ui-button-text:hover,
    .toggleScrobble .ui-button-text:active,
    .toggleScrobble.ui-state-hover .ui-button-text,
    .toggleScrobble.ui-state-active .ui-button-text {
        background: url(http://cdn.last.fm/flatness/badges/lastfm_red_small.gif);
    }

###More

For further information, please visit the official API documentation:
http://www.last.fm/api
