# p-agi_ilivalidator_streaming_format


## Cache
```
./Users/stefan/Downloads/duckdb dmavcache.duckdb
```

```
INSTALL spatial;
LOAD spatial;
``` 

```
CREATE TABLE mopublic_bodenbedeckung AS SELECT * FROM ST_Read('/Users/stefan/tmp/mopublic_bodenbedeckung.fgb');
CREATE TABLE mopublic_bodenbedeckung AS SELECT * FROM ST_Read('./mopublic_bodenbedeckung.fgb');
```

```
SELECT * FROM mopublic_bodenbedeckung WHERE t_id = '167203267';
```


```
SELECT 
    * 
FROM 
    mopublic_bodenbedeckung 
WHERE 
    ST_Intersects(ST_Point(2607893, 1228263), mopublic_bodenbedeckung.geom)
;
```


## Local
```
INSTALL spatial;
LOAD spatial;
INSTALL httpfs;
LOAD httpfs;
```

```
ATTACH 'https://s3.eu-central-1.amazonaws.com/ch.so.agi.geodata-dev/dmavcache.duckdb' AS dmavcache_db (READ_ONLY);
```
ATTACH muss nach jedem Start gemacht werden. 


```
SELECT count(*) FROM dmavcache_db.mopublic_bodenbedeckung;
```

```
SELECT * FROM dmavcache_db.mopublic_bodenbedeckung WHERE t_id = '167203267';
```

ATTACH 'https://s3.eu-central-1.amazonaws.com/ch.so.agi.geodata-dev/dummy.duckdb' AS dummys3_db (READ_ONLY);



CREATE TABLE zuerihaus AS SELECT * FROM ST_Read('./zuerihaus.fgb');
ATTACH 'https://s3.eu-central-1.amazonaws.com/ch.so.agi.geodata-dev/zuerihauscache.duckdb' AS zuerihauscache (READ_ONLY);

SELECT 
    * 
FROM 
    zuerihauscache.zuerihaus 
WHERE 
    ST_Intersects(ST_Point(2607893, 1228263), zuerihaus.geom)
;



ATTACH 'https://s3.eu-central-1.amazonaws.com/ch.so.agi.geodata-dev/boflaeche.duckdb' AS boflaechecache (READ_ONLY);


SELECT 
    * 
FROM 
    boflaechecache.mopublic_bodenbedeckung 
WHERE 
    ST_Intersects(ST_Point(2607893, 1228263), mopublic_bodenbedeckung.geom)
;

SELECT 
    * 
FROM 
    boflaechecache.mopublic_bodenbedeckung 
WHERE 
    ST_Intersects(ST_Point(2621540.865, 1237593.709), mopublic_bodenbedeckung.geom)
;

2621540.865, 1237593.709