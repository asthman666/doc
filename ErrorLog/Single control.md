I found a deep hidden bug today, I think the root cause is the HTML element's visible is controlled by multiple objects.

I can simplify the problem to below:

    <div class="item-list">
        @if (Model.Items != null && Model.Items.Count > 0) {
            <div class="item-list-header">
                Name
            </div>            
            foreach ( var item in Model.Items) {
                <div class="item">@item.name</div>
            }
        }
        <div class="item-no-result">No result.</div>
    </div>

    <script>
        function show() {
            if ($(".item-list").find("item").length > 0) {
                // has some items
                $(".item-list-header").show(); // show item header
                $(".item-no-result").hide(); // hide no result information
            } else {
                // no item
                $(".item-list-header").hide(); // hide item header
                $(".item-no-result").show(); // show no result information
            }
        }
        show()
    </script>

Q: Did you think above code work correctly? 

A: Of course not.

    <div class="item-list-header">
        Name
    </div>     

Look at this piece of code, this element's visible is controlled by 

* `Model.Items != null && Model.Items.Count > 0`
* `show()` javascript function

If `Model.Items == null` or `Model.Items.Count == 0`, this HTML code will not be generated, the javascript code can never make it visible.

So we should change code like:

```diff
    <div class="item-list">
-        @if (Model.Items != null && Model.Items.Count > 0) {
            <div class="item-list-header">
                Name
            </div>            
+        @if (Model.Items != null && Model.Items.Count > 0) {
            foreach ( var item in Model.Items) {
                <div class="item">@item.name</div>
            }
        }
        <div class="item-no-result">No result.</div>
    </div>
```    

Through above changes, the `item-list-header` HTML code's visible only be controlled by javascript code. That's really simple and correct.
