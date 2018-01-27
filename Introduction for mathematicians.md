# Introduction

Type theory begins when one starts to take the notation seriously. In the simplest case,
a type system is given by a collection of (formation) rules defining a certain grammar.
Formation rules define expression formers (written below a horizontal line) admissible under a number of premisses written above the line. Here is the definition of a notation for a magma:
a set with a binary operation.
```
 a    b
————————
 (a, b)
```

It means, whenever we have expressions `a` and `b`, we may construct an expression
`(a, b)`”.

Rules can be composed by substitution:
```
 a    b
————————
 (a, b)    c
——————————————
 ((a, b), c)
```
Such “pictures” are called derivation trees.

Expressions are to be understood as their parsing trees (we leave out all technicalities related to parsing,
operator fixity, precedence and gathering rules; they are essential for convinience of notation, yet have nothing to do with the intrinsic structure of expressions). Formation rules have to be nonconflicting so every
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
————————————————————————————
           g∘f
           
 f : X ⟶ Y    g : Y ⟶ Z    w : Z ⟶ W
—————————————————————————————————————————
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

“Mathematicians often have a lot of difficulty understanding type theory (and the author was no exception).
One reason is that the usual presentation of type theory is heavy on _syntax_, which most mathematicians are not used to thinking about.
Thus, it is appropriate to begin with a few general remarks about syntax, what it is, and its role in type theory and in mathematics more generally.

In general, _syntax_ refers to a system of formal symbols of some sort, whereas _semantics_ means the interpretation of those symbols as “things”.
In the language of category theory, we can generally think of syntax as describing a _free_ (or _presented_) object, and semantics as the morphisms out of that object determined by its universal property.

For instance, in group theory we may write a sequence of equations such as
```
  (g h) h⁻¹ = g (h h⁻¹) = g e = g.   (*1)
```
Where does this computation take place?
One obvious answer is “in an arbitrary group”.
But another is “in the free group $F\langle g,h\rangle$ generated by two symbols `g` and `h`.”
Since the elements of `F⟨g,h⟩` are literally strings of symbols (“words”) produced by multiplication and inversion from `g` and `h`, strings such as `(g h)h⁻¹` _are themselves_ elements of `F⟨g,h⟩`, and (#1) holds as an equality between these elements, i.e. a statement _in syntax_.
Now if we have any other group `G` and two elements of it, there is a unique group homomorphism from `F⟨g,h⟩` to `G` sending the letters `g` and `h` to the chosen elements of `G`.
This is the _semantics_ of our syntax, and it carries the equation (#1) in `F⟨g,h⟩` to the analogous equation in `G`.
Such reasoning can be applied to arguments involving hypotheses, such as “if `g² = e`, then `g⁴ = (g²)² = e² = e`”, by considering (in this case) the group `F⟨g|g² = e⟩` _presented_ by one generator `g` and one equation `g² = e`.
(A free group, of course, has a presentation with no equations.)

In other words, we can regard an argument such as (#1) either as a “semantic” statement about “all groups” or as a “syntactic” statement about a particular free or presented group. The former is a consequence of the latter, by the universal property of free groups and presentations.

This may seem like mere playing with words, and the reader may wonder how such a viewpoint could ever gain us anything. The reason is that often, we can say more about a free object than is expressed tautologically by its universal property.
Usually, this takes the form of an explicit and tractable construction of an object that is then _proven_ to be free.
Of course, _any_ construction of a free object must be proven correct, but such a proof can range from tautological to highly nontrivial.
The less trivial it is, the more potential benefit there is from working syntactically with the free object.

For instance, a “tautological” way to define `F⟨g,h⟩` is by “throwing in freely” the group operations of multiplication and inversion, obtaining formal “words” such as `(gg⁻¹)(h⁻¹(h g))`, and then quotienting by an equivalence relation generated by the axioms of a group.
The universal property of a free group is then essentially immediate.
But a more interesting and useful construction of `F⟨g,h⟩` consists of “reduced words” in `g`, `h`, and their formal inverses (finite sequences in which no cancellation is possible), such as `g h g⁻¹ g⁻¹ h h g h⁻¹`, with multiplication by concatenation and cancellation.
The proof that this yields a free group is not entirely trivial (indeed, even the definition of the group multiplication is not completely trivial); but once we know it, it can simplify our lives.

As a fairly banal example of such a simplification, recall that the _conjugation_ of `h` by `g` is defined by `h^g = g h g⁻¹`.
Here is a proof that conjugation by `g` is a group homomorphism:
```
  h^g k^g = (g h g⁻¹)(g k g⁻¹) = g h k g⁻¹ = (hk)^g  (*2)
```
As straightforward as it is, this is not, technically, a complete proof from the usual axioms of a group.
For that, we would have to choose parenthesizations and use the associativity and unit axioms explicitly:
```
  h^g k^g = ((g h) g⁻¹)((g k) g⁻¹) = (g (h g⁻¹))((g k) g⁻¹) = ((g (h g⁻¹))(g k)) g⁻¹
  = (g ((h g⁻¹)(g k))) g⁻¹ = (g (h (g⁻¹(g k)))) g⁻¹ = (g (h ((g⁻¹ g) k))) g⁻¹
  = (g (h (e k))) g⁻¹ = (g (h k)) g⁻¹ = (h k)^g   (*3)
```
Of course, this would be horrific, so no one ever does it.
If mathematicians think about this sort of question at all, they usually call (#2) an “acceptable abuse of notation”.
But with the above explicit description of free groups, we can make formal sense of (#2) as a calculation in `F⟨g,h⟩`, wherein `g h g⁻¹` and `g k g⁻¹` are specific elements whose product is `g h k g⁻¹`.
Then we can extend this conclusion to every other group by freeness.
Note that if we tried to do the same thing with the “tautological” presentation of a free group, we would be forced to write down (#3) instead, so no simplification would result.

In general, there are several ways that a presentation of a free object might make our lives easier.
One is if its elements are “canonical forms”, as for free groups (e.g. `g h k g⁻¹` is the canonical form of `((g h) g⁻¹)((g k) g⁻¹)`).
This eliminates (or simplifies) the quotient by an equivalence relation required for “tautological” constructions.
Often there is a “reduction” algorithm to compute canonical forms, making equality in the free object computationally decidable.

Another potential advantage is if we obtain a “version” of a free object that is _actually_ simpler.
For instance, it might be stricter than the one given by a tautological construction.
This is particularly common in category theory and higher category theory, where it can be called a _coherence theorem_.

Finally, a particular construction of a free object might also be _psychologically_ easier to work with, or at least suggest a different viewpoint that may lead to new insights.
The best example of this is type theory itself: though it also offers the advantages of canonical forms and strictness, arguably its most important benefit is a way of thinking.”
