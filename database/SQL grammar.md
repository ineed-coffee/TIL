# SQL Grammar

---

### `Modulation`

```mysql
SELECT *
FROM TABLE_NAME
WHERE FIELD%NUM=REMAIN;
```

​		

### `Unique value` 

```mysql
SELECT DISTINCT(FIELD_NAME)
FROM TABLE_NAME;
-- DISTINCT 는 NULL 값도 포함되어서 나온다..
```

​	

### `Counting` 

```mysql
SELECT COUNT(FIELD_NAME)
FROM TABLE_NAME;
```

​	

### `Length of string` 

```mysql
SELECT LENGTH(FIELD_NAME)
FROM TABLE_NAME;
```

​	

### `Sort`

```mysql
SELECT FEILD1
FROM TABLE_NAME
ORDER BY FIELD2 ASC , FIELD3 DESC....;
```

​	

### `Limiting rows` 

```mysql
SELECT FIELD_NAME
FROM TABLE_NAME
LIMIT ROW_CNT;
```

​	

### `Connecting queries`

```mysql
(SELECT FIELD_NAME
FROM TABLE_NAME)
UNION
(SELECT FIELD_NAME
FROM TABLE_NAME);
```

​	

### `Substring` 

```mysql
SELECT LEFT("HELLO",1);
SELECT RIGHT("HELLO",1);
SELECT SUBSTR("HELLO",3,1);
```

​	

### `Regular Expression` 

```mysql
SELECT *
FROM TABLE_NAME
WHERE FIELD REGEXP "^[A-Z]+.*[0-1]$";
```

​	

### `CASE`

```mysql
SELECT
    CASE
        WHEN CONDITION1 THEN RETURN1
        WHEN CONDITION2 THEN RETURN2
        WHEN CONDITION3 THEN RETURN3
        ELSE RETURN4
    END AS CUSTOM_NAME
FROM TABLE_NAME;
```

​	

### `String concatenation`

```mysql
SELECT CONCAT(STR1,STR2)
FROM TABLE_NAME;
```



### `Grouping`

```mysql
SELECT GROUP_COL,AGG(FIELD)
FROM TABLE_NAME
GROUP BY GROUP_COL;
# 여러개로 그룹핑 할 수 있으며, ORDER BY 문법은 GROUP BY 뒤에서만 사용 가능하다(각 그룹이 아니라 그룹 칼럼을 기준으로 그룹들이 정렬됨) , 정렬->그룹핑을 원하면 서브쿼리!
```

