# ink-cheatsheet


## Flow

```
=== paragraph_1 === 
You stand by the wall of Analand, sword in hand.
* [Open the gate] -> paragraph_2 
* [Smash down the gate] -> paragraph_3
* [Turn back and go home] -> paragraph_4

=== paragraph_2 ===
You open the gate, and step out onto the path. 
```

### Includes

Include statements should always go at the top of a file, and not inside knots.

`INCLUDE newspaper.ink`



## Knots & Stiches

`=== top_knot ===`

### Navigate to a knot
```
=== back_in_london ===

We arrived into London at 9.45pm exactly.
-> hurry_home 
```

### Glue
```
=== hurry_home ===
We hurried home <> 
-> to_savile_row 

=== to_savile_row ===
to Savile Row 
-> as_fast_as_we_could
```

### Stiches
`= this is a stich`
```
=== the_orient_express ===
= in_first_class 
    ...
= in_third_class
    ...
= in_the_guards_van 
    ...
= missed_the_train
    ...
```

Navigate to a stich. **The first stitch is the default**.
 
```
*    [Travel in third class]
    -> the_orient_express.in_third_class

*    [Travel in the guard's van]
    -> the_orient_express.in_the_guards_van 
```
From inside a knot, you don't need to use the full address for a stitch.

## Choices

By default, every choice in the game can only be chosen once. 

### Simple

```
Hello world!
*    Hello back!
    Nice to hear from you!
```

### Hide choice's text in output after selecting

```
Hello world!
*    [Hello back!]
    Nice to hear from you!
```

### Tweak the choice's text in output. 
What's before `[]` is printed in both choice and output; what's inside only in choice; and what's after, only in output.

```
"What's that?" my master asked.
*    "I am somewhat tired[."]," I repeated.
    "Really," he responded. "How deleterious."
```

### Fallback choices
A choice without text

`*    -> out_of_options`

or a syntax cheat
```
*     -> 
    Mulder never could explain how he got out of that burning box car. -> season_2
```

### Sticky choices
A sticky choice is simply one that doesn't get used up, and is marked by a `+` bullet.

```
=== homers_couch ===
    +    [Eat another donut]
        You eat another donut. -> homers_couch
```

### Conditional choices

```
*    { not visit_paris }     [Go to Paris] -> visit_paris
+     { visit_paris      }         [Return to Paris] -> visit_paris 
```

Conditionals don't override the once-only behaviour of options, so you'll still need sticky options for repeatable choices.

#### Multiple conditions 
```
*    { not visit_paris }     [Go to Paris] -> visit_paris
+     { visit_paris } { not bored_of_paris } 
    [Return to Paris] -> visit_paris 
```
#### AND/OR/NOT
AND -> `&&`
OR -> `||`
NOT -> `not`

```
*    { not (visit_paris or visit_rome) && (visit_london || visit_new_york) } [ Wait. Go where? I'm confused. ] -> visit_someplace
```
