

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


```
