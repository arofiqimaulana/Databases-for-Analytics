# Learn Databases

## MySQL

```
# Select All Columns
SELECT * FROM tblclients c
```

```
# Select Several Columns
SELECT 
	c.id,
	c.firstname,
	c.city,
	c.phone
FROM tblclients c
```

```
# Filter using Where
SELECT * FROM tblclients c
WHERE c.city IN ('Malang','Surabaya')
```

```
# Statement AND
SELECT * FROM tblclients c
WHERE DATE(c.lastupdate) > DATE(NOW()) 
AND c.city IN ('Malang','Surabaya')
```

```
# JOIN
SELECT 
	c.id,
	p.name
FROM tblproducts p 
INNER JOIN tblclients c ON c.id=p.userid
```

```
# UNION
SELECT userid FROM tblproduct1
UNION
SELECT userid FROM tblproduct2
```

```
# Sub Query
SELECT * FROM tblclients c
WHERE c.id IN (
	SELECT p.userid FROM tblproducts p WHERE p.name IN ('Mie','Susu','Buah')
	)
```

```
# Sub Query
SELECT 
	p.id,
	p.name,
	(
	  SELECT c.firstname FROM tblclients c WHERE c.id=p.userid
	) as firstname,
	(
	  SELECT c.city FROM tblclients c WHERE c.id=p.userid
	) as kota
FROM tblproducts p
```

```
# CASE WHEN
SELECT
	*,
	CASE WHEN p.status = 'Paid' THEN 1 ELSE 0 END as status
FROM tblproducts p
```

```
# Group By
SELECT 
	p.name,
	COUNT(p.id) AS total_produk
FROM tblproducts p
WHERE p.status = 'Paid'
GROUP BY p.name
```

```
SELECT
	p.name,
	total_produk
FROM
(SELECT 
	p.name,
	COUNT(p.id) AS total_produk
FROM tblproducts p) AS mytable
WHERE total_produk > 50
```