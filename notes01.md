# random notes from homework one

## ra 

> [course website](https://sites.duke.edu/compsci316_01_f2016/)

> [ra halp](https://sites.duke.edu/compsci316_01_f2016/help/ra/)

#### commands to run

```
\help;  halp

Relational algebra expressions:
R: relation named by R
\select_{COND} EXP: selection over an expression
\project_{ATTR_LIST} EXP: projection of an expression
EXP_1 \join EXP_2: natural join between two expressions
EXP_1 \join_{COND} EXP_2: theta-join between two expressions
EXP_1 \cross EXP_2: cross-product between two expressions
EXP_1 \union EXP_2: union between two expressions
EXP_1 \diff EXP_2: difference between two expressions
EXP_1 \intersect EXP_2: intersection between two expressions
\rename_{NEW_ATTR_NAME_LIST} EXP: rename all attributes of an expression


\list;  lists available tables

bar
beer
drinker
frequents
likes
serves

Total of 6 table(s) found.

```

#### a

```
\select_{bar = 'James Joyce Pub'} serves;

James Joyce Pub|Amstel|3.00
James Joyce Pub|Corona|3.25
James Joyce Pub|Dixie|3.00
James Joyce Pub|Erdinger|3.50

\project_{beer} (\select_{bar = 'James Joyce Pub'} serves);

Amstel
Corona
Dixie
Erdinger
```

DONE!

#### b

```
bar \join
\rename_{name} \project_{bar} ( 
  \select_{price <= 2.25} serves 
);

Talk of the Town|108 E. Main Street
Down Under Pub|802 W. Main Street
Satisfaction|905 W. Main Street

```

#### c

```
bar \join
\rename_{name} 
\project_{bar} (
\project_{beer} (
  \select_{drinker = 'Amy'} likes
)

\join 

\project_{bar, beer} (
  \select_{price <= 2.50} serves 
  )
);

Talk of the Town|108 E. Main Street
```

#### d

```
\rename_{drinkerA, beerA} likes 
  \join_{beerA = beerB and drinkerA != drinkerB}
\rename_{drinkerB, beerB} likes; 

```

how remove duplicates?
