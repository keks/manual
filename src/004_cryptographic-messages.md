Cryptographic Messages {#sec:cryptographic-messages}
====================================================

A cryptographic message is either a constant `c` or a message `f(m1,...,mN)`
corresponding to the application of the `N`-ary function `f` to `N` cryptographic
messages `m1`, ..., `mN`.

FIX: `crypto messages => semantics`, `message patterns => specification of rules`

Message patterns can additionally contain (typed) message
variables that can be instantiated with arbitrary cryptographic messages of the
correct type.


Constants
---------

We distinguish between two types of constants:

* Public constants model publicly known atomic messages such as agent
  identities and labels. We use the notation `'some_identifier'` to denote public
  constants in Tamarin.
* Fresh constants model random values such as secret keys or random
  nonces. We use the notation `~'some_identifier'` to denote fresh
  constants in Tamarin. Note that fresh *constants* are seldomly used, a fresh
  *variable* is almost always the right choice.

Function Symbols
----------------

Tamarin supports a fixed set of builtin function symbols and additional user-defined
function symbols. The builtin function symbols are included in signatures. To include
a signature `some-sig`, include the line `builtins: some-sig` in your file. The
builtin signatures are.

diffie-hellman

: FIXME

bilinear-pairing

: FIXME

some more

: FIXME




Sorts/Types
-----------

Variables
---------

Equational theories
-------------------

OLD
---




Certain equational theories are used very often when modeling
cryptographic messages. We therefore provide builtins definitions for
them, using the keyword 'builtins'. The above theory could also be
enabled using the declaration

  builtins: hashing, asymmetric-encryption

We support the following builtins theories:

  diffie-hellman, signing, asymmetric-encryption, symmetric-encryption,
  hashing



Note that the theory for hashing only introduces the function symbol 'h/1'
and contains no equations.
Apart from 'diffie-hellman', all of these theories are subterm-convergent and
can therefore also be declared directly, as above. You can inspect their
definitions by uncommenting the following two line-comments and calling

  tamarin-prover Tutorial.spthy

// builtins: diffie-hellman, signing, asymmetric-encryption, 
symmetric-encryption,
//          hashing



**FIX: Cas has moved the below from 005_, to be integrated into this section**

Cryptographic messages as terms
-------------------------------

To model cryptographic messages we use terms, represented by trees where the
nodes are operators (such as pairing, function application, concatenation,
encryption) and the leaves are constants or variables.

For the leaves, we have two main sorts:

[fresh names]:
	Model random messages such as keys or nonces.

[public names]:
	Model known constants such as agent identities.

For example, in the Naxos protocol, `eskI` and `eskR` are freshly generated for
each new session. Additionally, the agent's long-term keys (`lkI`, `lkR') are
freshly generated before the agent starts communicating. We therefore model them
as fresh names.

The identities `I` and `R` can be instantiated by any concrete agent identity,
modeled as public names.





There is a
shorthand for the `pair` using `<` and `>` which is right-associative
and allows one to write `<a,b,c>` to represent `pair(a,pair(b,c))`.