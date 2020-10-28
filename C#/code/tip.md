1. How to combine two dictionary in C#

        > var d = new Dictionary<string, string> { { "a", "1" } };
        > d
        Dictionary<string, string>(1) { { "a", "1" } }
        > var d1 = d.Concat(new Dictionary<string, string> { { "b", "2" } });
        > d1
        ConcatIterator { { "a", "1" }, { "b", "2" } }
        > var d2 = d1.ToDictionary(e => e.Key, e => e.Value);
        > d
        Dictionary<string, string>(1) { { "a", "1" } }
        > d1
        ConcatIterator { { "a", "1" }, { "b", "2" } }
        > d2
        Dictionary<string, string>(2) { { "a", "1" }, { "b", "2" } }
        > 