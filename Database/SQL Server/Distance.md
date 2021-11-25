Use `geography::STGeomFromText` generate `geography`

    DECLARE @g geography;
    DECLARE @h geography;
    SET @g = geography::STGeomFromText('POINT(-93.15302 44.874376)', 4326);
    SET @h = geography::STGeomFromText('POINT(-77.5619419 38.9847719)', 4326);
    SELECT @g.STDistance(@h)/1609.344 as Miles, @g.STDistance(@h)/1000 as KiloMeters

Use `geography::Point` generate `geography`

    DEClARE
        @lat decimal(18,15),
        @lng decimal(18,15)
    SET @lat = 47.639322;
    SET @lng = -122.128383;
        
    Declare @source geography = geography::Point(30.20491677226107, -95.45612258030434, 4326);
    Declare @destination geography= geography::Point(30.120021042878015, -95.44187468725596, 4326);
        
    Select @source.STDistance(@destination) as Meters
    Select @source.STDistance(@destination) / 1000 as Kilometers
    Select @source.STDistance(@destination) / 1609.344 as Miles