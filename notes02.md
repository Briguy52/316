

a. 
```
SELECT beer 
FROM serves 
WHERE bar='James Joyce Pub';

Amstel
Corona
Dixie
Erdinger
```

b. 
```
SELECT bar.name, bar.address
FROM serves, bar
WHERE serves.price<2.25;

       name       |      address       
------------------+--------------------
 Down Under Pub   | 802 W. Main Street
 The Edge         | 108 Morris Street
 James Joyce Pub  | 912 W. Main Street
 Satisfaction     | 905 W. Main Street
 Talk of the Town | 108 E. Main Street
```

c. 
```
SELECT DISTINCT bar.name
FROM likes, serves, bar
WHERE serves.price<2.5 AND likes.drinker='Amy'

       name       
------------------
 Satisfaction
 The Edge
 Talk of the Town
 Down Under Pub
 James Joyce Pub
```

d. 

```
SELECT DISTINCT l1.drinker AS drinker1, l2.drinker AS drinker2 
FROM likes AS l1, likes AS l2
WHERE l1.beer = l2.beer AND l1.drinker != l2.drinker AND l1.drinker > l2.drinker

 drinker1 | drinker2 
----------+----------
 Dan      | Coy
 Dan      | Ben
 Eve      | Dan
 Eve      | Ben
 Dan      | Amy
 Ben      | Amy
 Eve      | Amy
(7 rows)

```

e. 

```
SELECT likes.drinker
FROM likes
WHERE likes.beer='Dixie'
EXCEPT ALL
SELECT DISTINCT frequents.drinker
FROM frequents, seres
WHERE serves.beer='Dixie'
AND freqents.bar = serves.bar;
```

f.

```
SELECT *
FROM frequents 
EXCEPT ALL


SELECT DISTINCT f1.drinker, f1.bar, f1.times_a_week
FROM frequents AS f1, frequents AS f2
WHERE f1.drinker = f2.drinker AND f1.times_a_week < f2.times_a_week;


SELECT *
FROM frequents 
EXCEPT ALL
SELECT DISTINCT f1.drinker, f1.bar, f1.times_a_week
FROM frequents AS f1, frequents AS f2
WHERE f1.drinker = f2.drinker AND f1.times_a_week < f2.times_a_week;

 drinker |       bar        | times_a_week 
---------+------------------+--------------
 Dan     | Satisfaction     |            2
 Dan     | Down Under Pub   |            2
 Amy     | James Joyce Pub  |            2
 Coy     | The Edge         |            1
 Coy     | Down Under Pub   |            1
 Eve     | James Joyce Pub  |            2
 Dan     | Talk of the Town |            2
 Ben     | Satisfaction     |            2
(8 rows)
```

g. 

Find names of all drinkers who frequent only those bars that serve some beers they like.

all drinkers in frequent - people who go to bars that serve stuff they like = people who go to bars they don't like
all drinkers - above = answer

```
SELECT DISTINCT temp.drinker
FROM (
(SELECT drinker, bar
FROM frequents
EXCEPT ALL

(SELECT DISTINCT frequents.drinker, frequents.bar
FROM frequents
EXCEPT ALL

SELECT DISTINCT likes.drinker, serves.bar
FROM serves, likes, frequents
WHERE serves.beer = likes.beer AND serves.bar = frequents.bar)
)
) AS temp
;
```

h. 

Find names of all drinkers who frequent every bar that serves some beers they like

people who DON'T go to bar that serve what they like = frequents - people who go to bars they like

frequents - people who DON'T go to bar that serve what they like  

```
SELECT DISTINCT drinker
FROM frequents
EXCEPT ALL
(
SELECT DISTINCT temp.drinker
FROM (
SELECT DISTINCT likes.drinker, serves.bar
FROM likes, serves
WHERE serves.beer = likes.beer
EXCEPT ALL 
SELECT drinker, bar
FROM frequents
) AS temp);

 drinker 
---------
 Dan
(1 row)
```

i.

```
SELECT *
FROM 
(SELECT temp.bar, temp.count, AVG(serves.price)
FROM serves,
(SELECT frequents.bar, COUNT(*)
FROM frequents, bar
GROUP BY frequents.bar, bar.name
HAVING frequents.bar=bar.name) AS temp
GROUP BY temp.bar, temp.count, serves.bar
HAVING serves.bar=temp.bar) AS temp2
ORDER BY temp2.count DESC

       bar        | count |        avg         
------------------+-------+--------------------
 James Joyce Pub  |     4 | 3.1875000000000000
 Down Under Pub   |     2 | 2.6666666666666667
 Satisfaction     |     2 | 2.6500000000000000
 Talk of the Town |     2 | 2.3500000000000000
 The Edge         |     2 | 2.7500000000000000
(5 rows)

```
