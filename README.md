# Present (v1)
.prsnt - A more "learnable" alternative to JSON
# About
.prsnt (pronounced Present) is a file format made for storing things in a "database" of sorts. It removes all the annoying quote and comma drama of JSON. Instead of counting nested brackets, everything is tracked line-by-line with simple type prefixes and IDs so it's super easy for humans to read and write without breaking it.

## Quick Example
Ver/prsnt: 1

opt/prsnt
	boo/tabs = true
 boo/requireCaps = false
 boo/booleanNeedsEqual = true
opt/end

StorageStart/MyData
	Txt/json: Sucks!
	Num/pi: 3.14
	Boo/PresentIsAwesome = true

	NestStorageStart/ThisIsUseful: 1
		List/CoolList//
		"Gaming"/123/\\
	NestStorageEnd/TrustMe: 1
	
	=c= This is a comment! =ce=
StorageEnd/Go and try prsnt!

## The Rules

Every part of a .prsnt is full of data. The data is formatted like this:

```Type/Name: Data```

Each type has a group.

```Pure Group

Txt
Num
Boo

Storage Group

StorageStart + StorageEnd
NestStorageStart + NestStorageEnd
opt

Misc Group

ver
List```

The Pure Group contains pure data like text, a number, or a true/false value.

The Storage Group are like folders. You can include things from the Pure Group or nest them together.

The Misc Group are things that do not fit in the other two.

Since most of the things here are self-explanatory, this tutorial shows what the more complicated things do.

# Why Nested Storage needs an ID

Nested Storage is formatted like `NestStorageStart/example: 1`. But why? Well, when you close and Nested Storage, it's name does not need to match, only the ID does, like this: `NestStorageEnd/test: 1`. Normal Storage is the only one that doesn't need an ID because it's at the bottom of the stack.


yk what I'm getting really tired I'll finish this tomorrow 