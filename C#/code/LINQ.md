1. TBD

        var nums = new List<int> {1, 0, -1};
        nums.Where(n => n < null).Any(); // always false
        nums.Where(n => n > null).Any(); // always false