---
layout: post
title:  "Zodiac Worksheet Solutions"
date:   2017-08-11
categories: week3
tags: week3, cases, guards
---

# Solutions to Zodiac Worksheet

## Question 1: Match a name to a year

Basic solution:
```haskell
nameToYear :: String -> Int
nameToYear name = case name of
	"Tiggy" -> 1997
	"Lachie" -> 1997
	"Tina" -> 1998
	"Ella" -> 1998
```

Solution with error handling:
```haskell
nameToYear2 :: String -> Int
nameToYear name = case name of
	"Tiggy" -> 1997
	"Lachie" -> 1997
	"Tina" -> 1998
	"Ella" -> 1998
	_ -> error "Name not recognized!"
```

Solution with Maybe type:
```haskell
nameToYear3 :: String -> Maybe Int
nameToYear name = case name of
	"Tiggy" -> Just 1997
	"Lachie" -> Just 1997
	"Tina" -> Just 1998
	"Ella" -> Just 1998
	_ -> Nothing
```
The use of a Maybe type allows us to handle errors more elegantly by outputting `Nothing` instead of explicitly throwing an error.
  
## Question 2: Match a year to a zodiac

String solution:
```haskell
yearToZodiac :: Int -> String
yearToZodiac year = case year of
	1997 -> "Ox"
	1998 -> "Tiger"
```

Data Type solution:
While the String solution works perfectly well, the Data type solution is more elegant as it is more clearly defined for pattern matching and takes away the need for quotation marks.
```haskell
data ChineseZodiac = Rat | Ox | Tiger | Rabbit | Dragon | Snake | Horse | Goat | Monkey | Rooster | Dog | Pig
    deriving (Show)
yearToZodiac :: Int -> ChineseZodiac
yearToZodiac year = case year of
	1997 -> Ox
	1998 -> Tiger
```

Data Type solution with error handling:
```haskell
yearToZodiac2 :: Int -> ChineseZodiac
yearToZodiac2 year = case year of
	1997 -> Ox
	1998 -> Tiger
	_ -> error "Your birthday isn't valid!"
```

Data Type solution with Maybe types:
```haskell
yearToZodiac3 :: Maybe Int -> Maybe ChineseZodiac
yearToZodiac3 year = case year of
	1997 -> Ox
	1998 -> Tiger
	_ -> Nothing
```

## Question 3: Match a name to a zodiac
```haskell
nameToZodiac :: String -> ChineseZodiac
nameToZodiac name = yearToZodiac (nameToYear name)
```
Note: the type signature can change depending on how you wrote your previous functions e.g. with or without `Maybe` types






```haskell
head' :: [a] -> a
head' list = case list of
    [] -> error "no elements in input list"
    (x:xs) -> x
```

```haskell
-- note you can use Int or Float or Double, etc, instead of a
-- a is polymorphic which allows it to work over all numbers
-- if we restrict a to Num
add2 :: (Num a) => [a] -> a
add2 list = case list of
    [] -> error "no elements in input list"
    [x] -> error "only one element in input list"
    (x:y:xs) -> x + y
```

```haskell
length' :: [a] -> Int
length' list = case list of
    [] -> 0
    (x:xs) -> 1 + length' xs
```

```haskell
sum' :: (Num a) => [a] -> a
sum' list = case list of
    [] -> 0
    (x:xs) -> x + sum' xs
```

```haskell
square_list :: (Num a) => [a] -> [a]
square_list list = case list of
    [] -> []
    (x:xs) -> x*x:(square_list xs)
```


```haskell
extract :: Int -> [a] -> a
extract num list = case list of
 [] -> error "list not long enough!"
 x:xs
  | num == 0 -> error "you can't take the 0th element of a list!"
  | num == 1 -> x
  | otherwise -> extract (num-1) xs
```

```haskell
reverse_slow :: [a] -> [a]
reverse_slow list = case list of
 [] -> []
 x:xs -> (reverse_slow xs) ++ [x]
```

```haskell
reverse_fast :: [a] -> [a]
reverse_fast list = reverse_fast' list []
```

```haskell
reverse_fast' :: [a] -> [a] -> [a]
reverse_fast' list1 list2 = case list1 of
 [] -> list2
 x:xs -> reverse_fast' xs (x:list2)
```


```haskell
find :: (Eq a) => a -> [a] -> Int
find elem list = find' elem list 1
```

```haskell
find' :: (Eq a) => a -> [a] -> Int -> Int
find' elem list counter = case list of
 [] -> error "element not found"
 x:xs
  | x == elem -> counter
  | otherwise -> find' elem xs (counter+1)
```

```haskell
split :: [a] -> Int -> ([a],[a])
split list num = (take (num-1) list, drop (num-1) list)
```


```haskell
delete :: (Eq a) => [a] -> a -> [a]
delete list val = ((fst (split list (num)) )) ++ (tail (snd (split list (num)) ))
 where
 	num = find val list
```


