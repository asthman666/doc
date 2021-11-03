```diff
    private Args GetArgs(string eventId)
    {
        var intEventId = int.Parse(eventId);
        var @event = _iEventRepository.Get2(x => x.Id == intEventId)
            .Include(x => x.County)
            .Include(x => x.County.Region)
+            .Include(x => x.County.RegionalTrainingOfficer)
            .FirstOrDefault();
        if (@event.County == null) return null;
-        if (@event.County.Region == null) return null;

        return new Args()
        {
            CountyName = @event.County.Name,
-            RegionName = @event.County.Region.Name,
+            RegionName = @event.County.Region?.Name ?? string.Empty,
+            RegionalTrainingOfficerName = @event.County.RegionalTrainingOfficer?.Name ?? string.Empty,
            EventName = @event.Name,
            Recipients = @event.County.Region.ContactEmail,
        };
    }
```        

1. Remove the code `if (@event.County.Region == null) return null;`, that means Region maybe null in the following code, so need to check all @event.County.Region places. The above code miss the change for `@event.County.Region.ContactEmail`, should be changed to `@event.County.Region?.ContactEmail`.

2. Add the code `.Include(x => x.County.RegionalTrainingOfficer)` and `RegionalTrainingOfficerName = @event.County.RegionalTrainingOfficer?.Name ?? string.Empty,`, that means need some RegionalTrainingOfficer information. `Recipients` still use the `@event.County.Region`'s `ContactEmail`, it maybe cause bugs.