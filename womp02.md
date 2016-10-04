(a) Enforce key and foreign key constraints implied by the description in Homework #1.

Added a bunch of `FOREIGN KEY` statements to the Pokemon table:

```
 FOREIGN KEY trainer_id REFERENCES Trainer(id),
 FOREIGN KEY species REFERENCES Species(name),
 FOREIGN KEY quick_move REFERENCES Move(name),
 FOREIGN KEY charged_move REFERENCES Move(name)
```

(b) Enforce that trainers have unique nick names (a new constraint).

Added the `UNIQUE` keyword to the nick name row

(c) Enforce that all species base attack, defense, and stamina values are greater than 0, and that all individual Pokemon attack, defense, and stamina values are between 0 and 15 (inclusive).

Species
```
 attack INTEGER NOT NULL CHECK (attack>0),
 defense INTEGER NOT NULL CHECK (defense>0),
 stamina INTEGER NOT NULL CHECK (stamina>0),
```

Pokemon
```
 attack INTEGER NOT NULL CHECK (attack >= 0 AND attack <= 15),
 defense INTEGER NOT NULL CHECK (defense >= 0 AND defense <= 15),
 stamina INTEGER NOT NULL CHECK (stamina >= 0 AND stamina <= 15),
```

(d) Enforce that if a Pokemon is not owned by a trainer (i.e., Pokemon.trainer is NULL), then it cannot be (d) Enforce that if a Pokemon is not owned by a trainer (i.e., Pokemon.trainer is NULL), then it cannot be 

```
 trainer_id INTEGER REFERENCES favorite,
 favorite CHAR(1) REFERENCES trainer_id,
```

(e) Using triggers, enforce that Pokemon.quick_move and Pokemon.charged_move indeed refer to moves of the (e) Using triggers, enforce that Pokemon.quick_move and Pokemon.charged_move indeed refer to moves of the 


