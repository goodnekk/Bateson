# Bateson
Bateson is a datastorage for complex information. Complex information, in the sense of heavily interlinked.
Bateson used relationality and patterns to store and retreive data. 

## Data Model
Bateson can store three types of atomic information A Relatum, A Relation and A Patterns

### A Relatum is an atomic value.
A Relatum is an observation in the world, a piece of information.
* Transaction id
* Relatum id
* Value type
* Value

example
```
tid   rid   type   value
------------------------
001   001   name   nora
002   002   name   mary
003   003   name   anne

004   004   name   john
005   005   name   wane
006   006   name   toby
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
Group: A know B know C know A
```

