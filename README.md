# Haskell-style-guide
Notes for myself on how to stay consistent

Incantation at the top of each file:
```Haskell
{-# LANGUAGE MultiWayIf
           , PatternGuards
           , PatternSynonyms
   #-}
```

Sometimes combining MultiWayIf with PatternGuards can lead to a more consistent style. Sometimes it can be ugly. Below are some examples where it's locally equivalent or worse.
```Haskell
if b
   then y
   else z

-- vs

if
   | b         -> y
   | otherwise -> z


case f x of y -> z
   
-- vs

if | y <- f x  -> z


foo x
   | p x       = y
   | otherwise = z

-- vs

foo x = if
   | p x       -> y
   | otherwise -> z


foo x
   | P y <- f x
   = y

-- vs

foo x = if
   | p y <- f x
   -> y


case f x of
   C x 
      | p x -> x
      | q x -> y
   z -> v

-- vs (alas)

let u = f x in if
   | C x <- u 
   -> if
      | p x -> x
      | q x -> y
   | z <- u
   -> v

\case
   y -> v
   z -> u

-- vs (alas)

\ x -> if
   | y <- x  -> v
   | z <- x  -> u

-- or

\ x -> if
   | y <- x
   -> v
   | z <- x
   -> u
```
