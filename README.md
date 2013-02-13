Scroll Pagination Utility
=========================

A JavaScript utility for infinite scrolling.

## Installation

Includes the following files.

```html
<link rel="stylesheet" href="assets/scroll-pagination.css">
<script type="text/javascript" src="http://yui.yahooapis.com/3.5.0/build/yui/yui-min.js"></script>
<script type="text/javascript" src="scroll-pagination.js"></script>
```    
    
## Usage    

```javascript
YUI().use("scroll-pagination", function (Y) {

    var scroll = new Y.ScrollPagination({
        data: {
            source: "ajax.php", // API Entrypoint.
            schema: {
                metaFields: { // Your data schema for JSON. You can customize for your need.
                    count: "result.count",
                    last_id: "result.last_id",
                    last_timestamp: "result.last_timestamp",
                    html: "result.html"
                }
            },
            request: "?page=1&r=" + parseInt(new Date().getTime(), 10) // Upcoming API request.
        }
    });

    scroll.on("load", function (e) {
        // Set for next request.
        self.set("data.request", [
            "?last_id=" + data.last_id,
            "&last_timestamp=" + data.last_timestamp,
            "&page=" + page
        ].join(""));
        // Inject HTML.
        Y.one("#foo").append(data.html);
    });
    
});
```
