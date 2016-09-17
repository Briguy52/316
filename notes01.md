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
  \select_{price < 2.25} serves 
);

Talk of the Town|108 E. Main Street

```

#### c

```
\project_{name} (
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
)
);

Talk of the Town|108 E. Main Street
```

#### d

```
\select_{drinkerA < drinkerB}
\project_{drinkerA, drinkerB} (
\rename_{drinkerA, beerA} likes 
  \join_{beerA = beerB and drinkerA != drinkerB}
\rename_{drinkerB, beerB} likes
);
```

how remove duplicates? use a select to choose first name < second name (thanks david!!)

#### e 

```
\rename_{dBar} 
\project_{bar} (
\select_{beer = 'Dixie'} serves
)

\join_{dBar != bar}

\project_{drinker, bar} (
frequents \join 
\project_{drinker} (
\select_{beer = 'Dixie'} likes
)
);

Coy|Down Under Pub !!!
Coy|The Edge !!!
Dan|Down Under Pub
Dan|James Joyce Pub
Dan|Satisfaction
Dan|Talk of the Town
Dan|The Edge

```

#### f

```
// people with more than one favorite
\project_{drinker1, bar2} (
\rename_{drinker, bar, times} frequents 
  \join_{drinker = drinker0} 
\rename_{drinker0, bar0, times0} frequents 

\diff
(
\rename_{drinker1, bar1, times1} frequents 
  \join_{drinker1 = drinker2 and times1 < times2}
\rename_{drinker2, bar2, times2} frequents
);

)



```
