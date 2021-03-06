# Filter on 'All' Activities in Dynamics 365

![](https://user-images.githubusercontent.com/14048382/30040310-a776ba02-9231-11e7-86d9-e6a165d07af1.png)

Call the ```filterAllActivities();``` function from the Account/Contact OnLoad event. This will default the "Filter on" drop down to show "All" activities, rather than last 30 days. Note that the default associated view still only shows "Open" activities, so you may want to customize this view to include "Closed" activities as well.

```javascript
function filterAllActivities() {
    $("#navActivities").click(function () {
        _filterAllActivitiesBase();
    });
}

function _filterAllActivitiesBase() {
    var frame = $("#areaActivitiesFrame");
    if (frame == null || frame.length == 0) {
        setTimeout(_filterAllActivitiesBase, 100);
        return;
    }

    frame.on("load", function () {
        var entityName = Xrm.Page.data.entity.getEntityName();
        var entity = entityName.charAt(0).toUpperCase() + entityName.substr(1);
        var doc = this.contentWindow.document;
        var filterOn = doc.getElementById("crmGrid_" + entity + "_ActivityPointers_datefilter");

        filterOn.value = "All";

        var evt = doc.createEvent("HTMLEvents");
        evt.initEvent("change", false, true);
        filterOn.dispatchEvent(evt);
    });
}
```

Note: This code is unsupported, and is likely to break in any major releases (as it has in the past). The idea of sourcing this project on GitHub is that if/when it does break again, it can be updated here rather than having to release new blog posts and hoping people who have previously used it see it. Also if it breaks in an update and I don't get a chance to fix it, someone else can fix it :)

Created by [Paul Nieuwelaar](http://paulnieuwelaar.wordpress.com) - [@paulnz1](https://twitter.com/paulnz1)  
Sponsored by [Magnetism Solutions - Dynamics CRM Specialists](http://www.magnetismsolutions.com)

[![](https://user-images.githubusercontent.com/14048382/30045114-3805d840-9256-11e7-9bdb-323760fb43ea.png)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=89YXEVDJPTFDG)
