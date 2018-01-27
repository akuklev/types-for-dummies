# Introduction

Type theory begins when one starts to take the notation seriously. In the simplest case,
a type system is given by a collection of (formation) rules defining a certain grammar.
Formation rules consist of a collection of premisses written above a horizontal line,
and a result, written below the line. Here is the definition of a notation for a magma:
a set with a binary operation.
```
 a    b
————————
 (a, b)
```

It means, “whenever we have expressions `a` and `b`, we may construct an expression
`(a, b)`”. Rules can be composed by substitution:
```
 a    b
————————
 (a, b)    c
——————————————
 ((a, b), c)
```
Such “pictures” are called derivation trees.

Expressions are to be understood as their parsing trees (we leave out all technicalities related to parsing,
operator fixity, precedence and gathering rules; they are essential for convinience of notation, but do not
interfere with structure of expressions in any way). Formation rules have to be nonconflicting so every
expression, if written out as a tree, can be considered its own canocical derivation tree.

More interesting type systems also contain some (computation) rules defining allowed symbolic manipulations
on expressions. Take a look at a definition of a notation for a monoid:
```
 a     b        a     b     c
—————————     —————————————————
   a·b         a·(b·c) ⇝ a·b·c
   
              a             a
—————     —————————     —————————   
  e        a·e ⇝ a       e·a ⇝ a    
```

Reflexive-transitive closure of the small-step computation relation `⇝` defines an equivalence relation called
“syntactic equality” on expression. In many importaint cases it is possible to chose the computation rules so that
every possible sequence of their applications eventually leads to an irreducible expression, moreover to the same
irreducible expression, called normal form of the expression. Such systems are said to be confluent and strongly
normalizing, which is a highly desirable property as we'll see later. As a side effect, it ensures that
syntactical equality is desidable: to check whether two expressions are equal simply compute their normal forms
and compare them node-for-node. Recent developments also provide in insight how to deal computationally with
semi-decidable forms of equality. Once we manage to provide a type system for a structure `S` which captures
the suitable notion of equality computationally, we can use the type system as the definition for `S`
which is (a) immediately suitable for computer-checked and computer-aided readoning about the structure
`S` and (b) can be interpreted in nonstandard ways, e.g. internally to any category with enough additional
structure.

Now let's come to the question what the heck types are. For this reason let's consider a “typed” monoid
(think of rectangular matrices under composition) where the composition is defined only if the types of
the elements are compatible in a certain way (the number of columns of the left element must coincide
with the number of rows of the right one). Such typed monoids are very well known throughout mathematics:
that's categories. Let's forget about unit elements for a moment and write down the definition
of a notation for semicategories (categories without identities):
```
 f : X ⟶ Y     g : Y ⟶ Z
—————————————————————————
           g∘f
           
 f : X ⟶ Y    g : Y ⟶ Z    w : Z ⟶ W
—————————————————————————————————————
           w∘(g∘f) ⇝ w∘g∘f
```

Type systems are typically used to provide nice notations for (semi-)categories with additional properties and/or
structure. In this case they are often called “internal languages” of such and such categories.
A very interesting moderately-sized example is the type system defining the notion of weak ω-Categories (see Finster-Mimram 2017).
The main motivating example is a quite involved type system called Homotopy Type Theory (some details of which are not yet completely
settled down) which turns out to be the internal language for elementary ∞-topoi: the well-behaved mathematical universes where any kind
of mathematical structure can be defined and any kind of proof can be carried out.

I would like to conclude with a note called “On syntax” by Michael Shulman from his excellent paper “Homotopy type theory: the logic of space” which
is in my opinion the best introduction into the field of Homotopy Type Theory to date.
