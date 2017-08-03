# Bateson
Bateson is a datastorage for complex(heavily interlinked) information. It is based on the idea notions of "hierarchy", "objects" and "attributs" are not an intrinsic property of the world but a subjective matter. Therefore it only stores relationships between values, which correspond to sensory observations in the real world. The heart of Bateson are what it calles "Patterns", which allow for multiple overlapping boundries and conflicting hierarchies to exist at the same time.

## Data Model
Bateson can store three types of atomic information: Relata, Relations and Patterns

### A Relatum is an atomic value.
A Relatum is an observation in the world, a piece of information.
* Transaction id
* Relatum id
* Value type
* Value

example
```
tid   rid   type     value
---------------------------
001   001   person   "nora"
002   002   person   "mary"
003   003   person   "anne"

004   004   person   "john"
005   005   person   "wane"
006   006   person   "toby"
```

### A Relation is a two way assiociation between two Relata.
* Transaction id
* Relatum id A
* Relatum id B
* Relation type

example
```
tid   ra    rb    type
------------------------
007   001   002   know
008   002   003   know
009   003   001   know

010   004   005   know
011   005   006   know
012   006   004   know
```

So far so good, This basic model descibes that: 
`nora` `mary` and `anne` each `know` each other.
and similarly that `john` `wane` and `toby` each `know` each other.
These are both groups of three people that each know each other.

### A Pattern is Relata Relating.
A Pattern is a *thing*.

example
```
PATTERN friendgroup (
  person A know person B,
  person B know person C,
  person C know person A
)
```
Patterns are used by Bateson creating, querying and indexing information.

## Querying
### Adding information
You can add data to the database by creating individual element
```
CREATE (person "patrick")
```

You can relate things after you created them by using variables
```
CREATE (
  person A:"patrick",
  person B:"patrick"
) THEN RELATE (
  A know B
)
```

Or you can use patterns to create a whole group in one go.
```
CREATE friendgroup (
  person A:"nora",
  person B:"john",
  person C:"toby"
)
```

### Finding information
Find all the groups of wich john is part
```
FIND friendgroup CONTAINING (person "john")
```

By using the wildcard ? you can do any kind of pattern matching
Find all the groups where A is a person, A in this case refers to the PATTERN variable
```
FIND friendgroup CONTAINING (person A:?)
```

find all the groups where A is any type of thing with a value of "john"
```
FIND friendgroup CONTAINING (? A:"john")
```

You can even create patterns of patterns.
```
PATTERN connected_friendgroup(
    friendgroup.A know friendgroup.A
)
   O         O
 /   \     /   \
O  _  O _ O  _  O
```


### Updating information
Find anything called "john" and rename it to "jon"
```
FIND ("john") AS P THEN UPDATE(P:"jon")
```
