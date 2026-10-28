# Present (v1)
.prsnt - A more "learnable" alternative to JSON
# About
.prsnt (pronounced Present) is a file format made for storing things in a "database" of sorts. It removes all the annoying quote and comma drama of JSON. Instead of counting nested brackets, everything is tracked line-by-line with simple type prefixes and IDs so it's super easy for humans to read and write without breaking it.

## Example
```
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
```
# The Rules

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
List
```
The Pure Group contains pure data like text, a number, or a true/false value.

The Storage Group are like folders. You can include things from the Pure Group or nest them together.

The Misc Group are things that do not fit in the other two.

Since most of the things here are self-explanatory, this tutorial shows what the more complicated things do.

## Why Nested Storage needs an ID

Nested Storage is formatted like `NestStorageStart/example: 1`. But why? Well, when you close a Nested Storage, its name does not need to match, only the ID does, like this: `NestStorageEnd/test: 1`. Normal Storage is the only one that doesn't need an ID because it's at the bottom of the stack.

## What are the available options?

The opt Storage can only be used once and must be used with opt/prsnt and opt/end. This can only contain **specific Booleans**. There are 3 options as of now:

```
Boo/tabs = true
=c=If it allows indents. True by default.=ce=

Boo/requireCaps = false
=c=Makes it so you have to use proper capitalization if true. False by default.=ce=

Boo/booleanNeedsEqual = true
=c=Self-explanitory. True by default.=ce=
```

If opt is missing, it should use the default options.

## What does ver do?

ver is the only required data in a `.prsnt`, and it looks like this.

`ver/prsnt: 1`

If it is not there, the parser should throw Error Code 1: ver/prsnt is missing!

## How does a List work?

Lists are the most complicated data by far. They also are the only type with 4 letters. Here is how they work.

Lists are started like this:

`List/Example//`

and ended with a `\\`. 
<!-- also this is line 100! yippie! -->
Lists use a way to differentiate between a string and a number. Strings are surrounded by `"` while numbers are plain.

The seperator between data is `/`

(Also, lists are very difficult to use, I would recommend using Nested Storage instead.)

# Rules for making parsers

1. Parsers are NOT converters:

A converter turns prsnt into JSON
A parser reads prsnt and actually understands it.

Parsers should be built into things that actually use prsnt
Converters should be built into things that only understand JSON

Know the difference!

2. Error messages should be easy to read:

I set up an Error Guide (written in Present) for people that want to make parsers and converters.

3. Think like a user would:

The average user would probably not want to mess around in the command line. You can still make a command line tool, but also make something graphical, like a website.
