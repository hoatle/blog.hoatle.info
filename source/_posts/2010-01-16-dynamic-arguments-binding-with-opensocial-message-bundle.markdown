---
layout: post
title: "Dynamic arguments binding with OpenSocial message bundle"
author: hoatle
date: 2010-01-16 19:44
comments: true
categories:
    - "en"
tags:
    - "OpenSocial"
cover:
description: Dynamic arguments binding with OpenSocial message bundle
keywords: Dynamic arguments binding with OpenSocial message bundle
published: true
---

Problem
-------

- Working with OpenSocial message bundle for localization, sometimes it's necessary to bind dynamic
arguments to the message. For example, we have greeting message like this: `Hello {user}` in which
user will be replaced by user's name. But currently with OpenSocial api, we can't. We just can get
message bundle by the key without passing any arguments for substitution.

- So this is my approach: using `eXo.social.Locale.getMsg(key)` the same as `prefs.getMsg(key)` and
`eXo.social.Locale.getMsg(key, [val1, val2,...]);` for dynamic arguments binding with message bundle.

<!-- more -->

Solution
--------

- Create `eXo.social.Locale class:`

```javascript
/**
 * Locale.js
 * Utility for Locale, dynamic binding message bundle with arguments
 * Usage:
 * eXo.social.Locale.getLang(); the same as prefs.getLang();
 * eXo.social.Locale.getCountry(); the same as prefs.getCountry();
 * eXo.social.Locale.getMsg(key); the same as prefs.getMsg(key);
 * eXo.social.Locale.getMsg(key, args); dynamic binding argument to message bundle
 * @author  hoatle
 * @since   October 27, 2009
 * @copyright   eXo Platform
 */

(function() {
    //prefs object to get lang, country, message bundle
    var prefs;

    /**
     * private function to lazily initialize prefs object
     */
    function getPrefs() {
        if (!prefs) {
            prefs = new gadgets.Prefs();
        }
        return prefs;
    }
    /**
     * Class definition
     */
    var Locale = function() {

    }
    /**
     * gets current lang
     * @static
     */
    Locale.getLang = function() {
        prefs = getPrefs();
        return prefs.getLang();
    }
    /**
     * gets current country
     * @static
     */
    Locale.getCountry = function() {
        prefs = getPrefs();
        return prefs.getCountry();
    }
    /**
     * alternative for prefs.getMsg(key)
     * uses to getMsg with provided key and substitute args
     *
     * eg: Test for {0}, {1}
     * If args does not match num of {\d}, warning and try to replace by corresponding index.
     * {0} should be replaced by args[0], etc.,
     * If args not provided, functions as prefs.getMsg(key)
     * @param   key String
     * @param   opt_args Array
     * @static
     */
    Locale.getMsg = function(key, opt_args) {
        prefs = getPrefs();
        if (!key) {
            debug.warn('key is null!');
            return '';
        }
        var msg = prefs.getMsg(key);
        if (msg === '') {
            debug.warn('Can not find resource bundle with key = ' + key);
            return msg;
        }
        if (!opt_args) return msg;

        //checks if number of {\d} in msg matches opt_args.length
        var regex = /{\d+}/g;
        var matches = msg.match(regex);
        if (matches.length !== opt_args.length) {
            debug.warn("required " + matches.length + " args, provided: " + opt_args.length);
        }
        //substitutes by index: {0} in msg should be replaced by opt_args[0] and so on
        for (var i = 0, l = matches.length; i < l; i++) {
            var index = matches[i].match(/\d+/g)[0];
            //TODO should improve performance
            var strToReplace = opt_args[index];
            if (!strToReplace) {
                debug.warn('matches[' + i + ']: ' + matches[i] + ' but no opt_args[' + index + ']');
            } else {
                msg = msg.replace(matches[i], opt_args[index]);
            }
        }
        return msg;
    }
    //Expose
    window.eXo = window.eXo || {};
    window.eXo.social = window.eXo.social || {};
    window.eXo.social.Locale = Locale;
})();
```

Note: The `eXo.social.Locale` class uses `debug`, thanks @cowboy for his excellent JavaScript
log/debug. I love it <3. All my projects and apps use it, you should also use this way of debug/log
instead of alert :).

Download sample app for testing at http://github.com/hoatle/opensocial/downloads

Source code available at: http://github.com/hoatle/opensocial/tree/master/message-bundle

The xml app file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Module>
    <ModulePrefs title="Arguments Binding Message Bundle"
                 description="Simple-App for arguments binding with message bundle"
                 author_email="hoatlevan@gmail.com"
                 author_affiliation="eXo Platform">
        <Locale messages="locale/ALL_ALL.xml" />
        <Locale lang="en" messages="locale/en_ALL.xml" />
        <Locale lang="vi" messages="locale/vi_ALL.xml" />
        <Require feature="opensocial-0.8" />
    </ModulePrefs>
    <Content type="html">
    <![CDATA[
        <link rel="stylesheet" type="text/css" href="style/style.css" />
        <script type="text/javascript" src="script/debug.js"></script>
        <script type="text/javascript" src="script/eXo/social/Locale.js"></script>
        <script type="text/javascript" src="script/app.js"></script>
        <p>Resource bundle rendered by server: <strong>__MSG_hello_world__</strong></p>
        <p>Resource bundle rendered by JavaScript:</p>
        <div id="helloMsg"></div>
        <div id="helloMsgArgs"></div>
    ]]>
    </Content>
</Module>
```

In the app code above, `__MSG_hello_world__` will be substituted by server with found message bundle
with key "hello_world" defined in message bundles files. (in `/locale` folder).

To test `eXo.social.Locale` class, we have the `app.js`:

```javascript
function run() {
    var prefs = new gadgets.Prefs(),
        helloWorld = prefs.getMsg('hello_world');
    alert(helloWorld); //"Hello world!" if current language is English
                       //"Chào thế giới!" if current language is Vietnamese

    //eXo.social.Locale usage
    var Locale = eXo.social.Locale;
    var helloMsgEl = document.getElementById('helloMsg'),
        helloMsgArgsEl = document.getElementById('helloMsgArgs');

    helloMsgEl.innerHTML = Locale.getMsg('hello_world');
    helloMsgArgsEl.innerHTML = Locale.getMsg('hello_user_to_place', ['hoatle', 'Vietnam']);
}

gadgets.util.registerOnLoadHandler(run);
```

You can test this sample app from any OpenSocial container. Happy coding :D.

P/S: We can use OpenSocial template for arguments binding with message bundle but it's currently
not fully supported by all containers.
