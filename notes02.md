

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
