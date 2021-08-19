I run into a bug in my code, I can simplify it, for example:

There is a class:

    public class ItemManageInventoryViewModel
    {
        public int Id { get; set; }
        public string ItemName { get; set; }
        public int AvailableInventory { get; set; }
        public int? Threshold { get; set; }
    }

We have the backend(C#) code:

    // item is a instance of the class ItemManageInventoryViewModel
    if (item.Threshold.HasValue && item.AvailableInventory < item.Threshold.Value) {
        // add item to ReOrderList and ReOrderList will show in "Re-Order" section of the page
    }

At the same time, we have the frontend(javascript) code:

    if (data.ItemManageInventory.AvailableInventory
        && data.ItemManageInventory.Threshold
        && data.ItemManageInventory.AvailableInventory < data.ItemManageInventory.Threshold
    ) {
        // find item need to "Re-Order" section of the page
    }

When `AvailableInventory` field's value is `0`, the frontend will never move item to "Re-Order" section because of `0` is false in javascript, but backend will use the condition `item.AvailableInventory < item.Threshold.Value` to judge if we can show item in "Re-Order" section. It will cause issue. There are two different conditions judge whether the item show in "Re-Order" section. In fact, they're the same.

So we can use encapsulation to solve the issue, see below:

**In the class:**

```diff
        public string ItemName { get; set; }
        public int AvailableInventory { get; set; }
        public int? Threshold { get; set; }
+       public bool NeedReOrder {
+           get {
+               return Threshold.HasValue && AvailableInventory < Threshold.Value;
+           }
+       }
    }
}
```

**In the backend:**

```diff
    // item is a instance of the class ItemManageInventoryViewModel
-   if (item.Threshold.HasValue && item.AvailableInventory < item.Threshold.Value) {
+   if (item.NeedReOrder) { 
        // add item to ReOrderList and ReOrderList will show in "Re-Order" section of the page
    }
```    

**In the frontend:**

```diff
-   if (data.ItemManageInventory.AvailableInventory
-       && data.ItemManageInventory.Threshold
-       && data.ItemManageInventory.AvailableInventory < data.ItemManageInventory.Threshold
+   if (data.ItemManageInventory.NeedReOrder)
    ) {
        // find item need to "Re-Order" section of the page
    }
```     

After these changes, we use the same logic in frontend and backend. We can confirm this feature correct easily, because we only need to test `NeedReOrder` property in backend, not both.
