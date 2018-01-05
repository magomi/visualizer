# About

Small app to show data (current values and time series) from my houses heating control. Data is stored on an influx db and retrieved via http calls.

# Implementation

This version of the visualizer app uses 

* bootstrap for styling
* jquery for dynamic html
* vanilla ajax for retrieving data
  * TODO/FIXME: "[Deprecation] Synchronous XMLHttpRequest on the main thread is deprecated because of its detrimental effects to the end user's experience. For more help, check https://xhr.spec.whatwg.org/."
 
# Deployment

## Mapping the database url

One of the main constraint is that the data must be load from a sub url (data)  of the apps base url. This can be done by defining a proxy for the sub url.

Below is a sample config for nginx.

    location /data/ {
        proxy_pass http://<INFLUX-DB-SERVER>/;
    }

## Authentication

For simplest authentication the methods already provided by the webserver shall be used. A nginx sample configuration can is provided below.

    auth_basic "Visualizer";                                   
    auth_basic_user_file <PATH-DO-USERS-FILE>;

The users file can be created using the apache htpasswd utility.

# Tasks

* [x] correct labels at charts (depending on the number of values)
* [x] self host necessary resources
* [ ] configurable from the outside
* [x] auto update the values
* [x] auto update the graphs
* [x] show timestamps for values
* [x] show detailed tooltips for the graphs
* [ ] clean up the user interface
* [ ] select ranges for the charts
* [x] basic authentication

# Useful resources

This list stores all resources that I visited to do the implementation. A lot of the resources are quite trivial.

* move in #vi #insert mode: https://stackoverflow.com/questions/19204396/jump-to-the-next-word-in-insert-mode
* check for an #undefined var in #javascript: https://stackoverflow.com/questions/3390396/how-to-check-for-undefined-in-javascript
* #maps in #javascript: https://stackoverflow.com/questions/4246980/how-to-create-a-simple-map-using-javascript-jquery
* handling #javascript #date: http://blog.stevenlevithan.com/archives/date-time-format
* update a #chartist graph: https://github.com/gionkunz/chartist-js/issues/321
* #functions in #javascript: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions
* #date in #javascript: https://www.w3schools.com/js/js_date_formats.asp
* #bottongroup in #bootstrap: https://getbootstrap.com/docs/4.0/components/button-group/
* #ajax requests in #javascript: https://stackoverflow.com/questions/247483/http-get-request-in-javascript
* #chartist line chart example: http://gionkunz.github.io/chartist-js/examples.html#example-line-series-override
* #influxdb query last value: https://docs.influxdata.com/influxdb/v1.3/query_language/data_exploration/#example-1-return-the-newest-points-first
* #vi set #tabs and #spaces: https://stackoverflow.com/questions/234564/tab-key-4-spaces-and-auto-indent-after-curly-braces-in-vim (tl;dr: "set expandtab ts=4 sw=4 ai")
* #javascript #math #round: https://www.w3schools.com/jsref/jsref_round.asp
* #vi configuration: http://www.peachpit.com/articles/article.aspx?p=31442&seqNum=7
* #nginx server config: https://www.nginx.com/resources/wiki/start/topics/examples/server_blocks/
* #nginx #authorization: https://www.nginx.com/resources/admin-guide/restricting-access-auth-basic/
* #nginx restart #osx: https://serverfault.com/questions/225948/how-to-restart-nginx-on-mac-os-x
