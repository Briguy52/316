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

- [ ] How do you reference foreign keys? 

```
CREATE TRIGGER EnforceQuick
  BEFORE INSERT OR UPDATE ON Pokemon
  FOR EACH ROW
  WHEN (Pokemon.quick_move.type != 'quick')
  SET Pokemon.quick_move.type = 'quick';
  
CREATE TRIGGER EnforceCharged
  BEFORE INSERT OR UPDATE ON Pokemon
  FOR EACH ROW
  WHEN (Pokemon.charged_move.type != 'charged')
  SET Pokemon.charged_move.type = 'charged';
```

(f) Write an INSERT statement that fails because a Pokemon refers to a non-existent move.

(g) Write an INSERT statement that fails because of violating (b).

(h) Write two INSERT statements that fail because of violating constraints in (c) on Species and Pokemon, 

(i) Write two UPDATE statements that fail because of violating the two cases under (d), respectively.

check this one

(j) Write an INSERT statement that fails because of violating (e).

(k) Write an UPDATE Move statement that fails because of violating (e).

(l) Define a view that lists, for each Pokemon, its combat power (CP), defined as follows:(l) Define a view that lists, for each Pokemon, its combat power (CP), defined as follows:
