# CS500 final

## CS500 lecture list
```
midterm 1
previous link : https://list.unm.edu/cgi-bin/wa?A2=CS500-L;7c67dac8.2303&S=

Lecture011723.pdf ; size of a set
Lecture011923.pdf ; two sets of same size ; cantor
Lecture012323.pdf ; FSM
Lecture012623.pdf ; union of two DFA
Lecture013123.pdf ; closure properties of regular language
Lecture020223.pdf ; minimization of DFA
Lecture020723.pdf ; partition ; iso- homo- morphism
Lecture020923.pdf ; myhill nerode thm
Lecture021423.pdf ; myhill nerode thm
Lecture021623.pdf ; arden's lemma
Lecture022123.pdf ; chomsky hierarchy
Lecture022323.pdf ; CFL example: balanced parenthesis
Lecture022823.pdf ; CFL example, NPDA from CFG
Lecture030223.pdf ; closure properties of CFL



midterm 2
previous link : https://list.unm.edu/cgi-bin/wa?A2=CS500-L;147860f4.2304&S=

Lecture022323.pdf ; CFL example: balanced parenthesis
Lecture022823.pdf ; CFL example, NPDA from CFG
Lecture030223.pdf ; closure properties of CFL

Lecture030723.pdf ; homomorphism (maybe this will not be in midterm 2?)
Lecture030923 : 1st midterm
Lecture031423 : spr break
Lecture031623 : spr break
Lecture032123 : went over 1st midterm

Lecture032323.pdf : Cantor's thm: |P(S)| > |S| ; recursively enumerable ; semi-decidable
Lecture032823.pdf : PDA to CFG
Lecture033023.pdf ; church turing thesis ; TM: 7 tuple ; configuration: 3-tuple
Lecture040423.pdf ; U.TM ; TM transition function ; diagonalization: 1.characteristic function of a set ; 2.x∈A | x∉f(A)
Lecture040623.pdf ; TM: string of 0s 1s ; undecidability ; reducibility
Lecture041123 (no pdf?) reducibility
Lecture041323.pdf ; Cook–Levin theorem ; DNF, CNF, tseiten transformation


pdf and topics after midterm 2:
Lecture041823 ; tseytin transformation ; def of NP ; TM configuration
Lecture042023 ; midterm 2
Lecture042523 ; (no pdf?) logic Resolution ; equi-satisfiability ; intro to Rice's thm
Lecture042723 ; cook-levin thm ; Clique to 3SAT ; Vertex-cover to 3SAT
Lecture050223 ; Rice's thm ; space complexity
Lecture050423 ; savitch's thm configuration i to j ; pspace-complete ; primitive recursive func. ; kleene minimization operator
```

### Lecture020223.pdf ; minimization of DFA
* The Quotient Construction ; How do we know in general when two states can be collapsed safely without changing the set accepted? [kozen]

### Lecture030223.pdf ; closure properties of CFL
* https://sites.cs.ucsb.edu/~cappello/136/lectures/17cfls/slides.pdf
  * L1 ∩ L2 = \{anbnan| n ≥ 0\}, which is known not to be a CFL

### Lecture041823 ; tseytin transformation ; def of NP ; TM configuration
* https://www.youtube.com/watch?v=v2uW258qIsM
  * bi-implication is just a conjunction  of two implications  one from left to right and one from  right to left  and if we consider the implication from  left to right  we see p implies q or r  is equivalent to not p or q or r  which is a clause itself  and the other direction q or  r implies p is equivalent to  not q or r or p and by the morgan rules  it can be written in this way  and by applying distributivity we get  these two clauses


||||
|---|---|---|
|![](https://i.imgur.com/Ch9lNIW.png)|![](https://i.imgur.com/BSfuWUB.png)| ![](https://i.imgur.com/YpXx0JQ.png)|
|![](https://i.imgur.com/IV873Pr.png)|![](https://i.imgur.com/FtvWK6J.png)|
|![](https://i.imgur.com/y8ydznh.png)|![](https://i.imgur.com/eDAxOAS.png)|
|||



### Lecture042723 ; cook-levin thm ; Clique to 3SAT ; Vertex-cover to 3SAT
* sipser ; 304 ; The Cook–Levin Theorem
  * φcell ∧ φstart ∧ φmove ∧ φaccept
  * Q and Γ are the state set and tape alphabet of N, respectively. Let C = Q ∪ Γ ∪ {#}
* 

## CS500 mailing list

### converting a regular expression to a ndfa
* Mogensen's compiler book, "Fig. 1.4 Constructing NFA fragments from regular expressions"
* how to convert NFA to regular expression
* some details mentioned by the Mogensen compiler book:
  * These half-transitions are the entry and exit to the fragment and are used to connect it to other fragments or additional “glue” states.
  * The symbol on the outgoing half-transition is not shown when an NFA fragment is shown as a dotted oval (it is “hidden” inside the oval).
  * When an NFA fragment has been constructed for the whole regular expression, the construction is completed by connecting the outgoing half-transition to an accepting state.
* And regarding concatenation, I think there is a difference between concatenating machines and regular expression: 

### today lecture 021623
* machine for \{}
* machine for \{ε}, (NFA)
* machine for \{ε}, (DFA)
* Arden's Lemma
  * Jeffrey D. Ullman et al's "Introduction to Automata Theory" 
    * 3rd ed, 2006
    * 1st edition
  * https://wwwlehre.dhbw-stuttgart.de/~sschulz/TEACHING/FLA2016/FLA2016_ho.pdf
  * 
* 

### conversion from pdas to grammars
* what method/conversion did you use?


## CS500 HW
### HW?
* ADD - REGULAR
* MULTIPLY

### HW2
* Q1, prove in your own words that the machine only accepts binary representation of multiples of 3
* Q3, intersection of two simpler languages. .. then combine using the construction
* Q5, obtain an equivalent DFA for each of the following DFAs that has the minimal number of states

### HW3
* Q3, if A, B are regular languages, prove the following
* Q4, prove the following languages are not regular using myhill-nerode theorem
* Q5, define a homomorphism from A to B by defining the functions in each algebraic structure with their usual meaning

### HW4
* Q1, prove that removing unreachable states from a DFA leaves the resulting machine to be a DFA, unlike if a dead state is removed
* Q2, 
  * minimize product construction of HW2 Q3
  * minimize the subset construction of HW2 Q4
* Q3, use the pumping lemma to prove the following language not regular:
* Q4, convert the NFAs in HW2 Q4 to the corresponding reg expr using Arden's lemma
* Q5, convert reg expr to NFAs
* Q6, regular grammars for NFAs in HW2 Q4
* Q7, minimize Q5 (HW3 Q1) NFAs

### HW5
* Q4, Show that the grammar G is ambiguous
  * sipser ; DEFINITION 2.7 ; A string w is derived ambiguously in context-free grammar G if it has two or more different leftmost derivations. Grammar G is ambiguous if it generates some string ambiguously.
* 

### HW6

* Q1, Use the pumping lemma for Context-free languages to prove that the following languages are not context free.
* Q2, Let L, P be context-free languages. Prove that:
  * L ∪ P is a context-free language.
* Q3, Convert the following PDAs to CFGs
* Q4, Obtain the grammars produced by the PDAs from Exercise 2 from the previous homework.
* Q5, Prove or disprove that the complement of a recursively enumerable set is also recursively enumerable?
* Q6, If a set and its complement is both recursively enumerable, is the membership in the set decidable?
* Q7, Prove that N4, the subset of N consisting of all multiples of 4, is of the same cardinality as the subset N6 of N consisting of all multiples of 6
* Q8, Prove that (N × N) is of the same cardinality as N. How about [(N × N) × N]? What can we then say about the cardinality of (N × N × ... × N) (k-times)?
* Q9,  If A is a set, then suppose that f is a one-to-one function from A to P(A), the power set of A and let B = \{a ∈ A | a /∈ f(a)\}. For the following sets, give examples of at least three different functions from A to P(A) and construct the set B:

### HW8
* Q1, mapping reducibility and Turing reducibility
  * https://www.cs.mcgill.ca/~prakash/Courses/Comp330/Notes/reductions.pdf
    * Thus, for example, one can easily2 show that ATM ≤T ATM which is of course not possible with mapping reduction
    * Indeed this is trivial, make sure you understand this.
  * sipser ; The sensitivity of mapping reducibility to complementation is important in the use of reducibility to prove nonrecognizability of certain languages.
  * https://cseweb.ucsd.edu/classes/fa01/cse105_B/hw3ans.pdf
* Q2, Show that the Post Correspondance Problem is decidable over the unary alphabet
  * https://cs.brown.edu/courses/gs019/asgn/hw2.sol.pdf
* Q3, class P of languages whose membership can be decided by a TM using polynomially many steps in the size of the input is closed under complement.
  * https://cseweb.ucsd.edu/classes/fa01/cse105_B/hw3ans.pdf
* Q4, obtain the Conjunctive normal form (i.e. conjunction of disjunctions) of the following formulas. 
* Q5, Prove that the procedure discussed in class to transform any formula into a conjunctive normal form preserves satisfiability, i.e. if the original formula is satisfiable, then the obtain formula is also satisfiable.
* Q6, Say that two Boolean formulas are equivalent if they have the same set of variables and are true on the same set of assignments to those variables (i.e., they describe the same Boolean function). A Boolean formula is minimal if no shorter Boolean formula is equivalent to it. Let MIN-FORMULA be the collection of minimal Boolean formulas. Show that if P = NP, then MIN-FORMULA ∈ P.

## CS500 midterm

### midterm 1
#### Part 1
* what is a regular language
* difference: DFA, NFA
* when are two FSM considered equivalent
* type 0, 1, 2, 3 grammars
  * https://en.wikipedia.org/wiki/Chomsky_hierarchy
  * Type-0 ; Recursively enumerable ; Turing machine
  * Type-1 ; Context-sensitive ; Linear-bounded non-deterministic Turing machine
  * Type-2 ; Context-free ; Non-deterministic pushdown automaton
  * https://en.wikipedia.org/wiki/Recursively_enumerable_language
    * i.e., if there exists a Turing machine which will enumerate all valid strings of the language.
    * https://en.wikipedia.org/wiki/Recursive_language ; Recursive languages are also called decidable.
  * 
* can a FSM accept a type 2 language
* what can be said about the intersection of two regular languages
  * construct a DFA
* intersection of two non-regular languages non-regular?
* state precisely the myhill-nerode theorem
* Q9, indistinguishability relation on the strings of an alphabet (in the context of myhill-nerode theorem)
* Q10, if a language is not regular, what will myhill-nerode theorem based construction give?
* Q11, given a regular language L, is every subset of L also regular? Justify
* Q12, is a language consisting of finitely many strings regular? justify
* Q13, can the same regular language have different grammars generating it? Justify
* Q14, state arden's lemma and explain what it is used for
* Q15, state precisely the pumping lemma for regular languages. use to prove a language regular?
* Q16, Li, i N, be regular languages. U i=0..inf is also
* Q17, Li, i N, be regular languages. 
* Q18, when is a grammar of language ambiguous
* Q19, is the intersection of CFLs a CFL
* Q20, state precisely the pumping lemma for CFLs. In what way, is it different from the one for regular languages?
* Q21, what is chomsky normal form for a CFG? How is it different from a CFG

#### Part 2 ; constructions
* Q1, give a state diagram of a DFA recognizing the following language. Generate a regular expr from the resulting machine.
* Q2, give a state diagram of a NFA recognizing the following regular expr
* Q3, construct a reg expr corresponding to the complement of the language generated by the reg expr
* Q4, is the language regular? if yes, give a FSM. if no, give an argument proving that it is not regular.

#### part 3 ; comprehensive
* Q1, using the NFA below, is aabaa == aba?
* Q2, obtain all the equivalence classes induced by the NFA using myhill-nerode theorem
* Q3, convert the NFA to a DFA
* Q4, minimize the states of the obtained DFA
* Q5, using the minimized DFA, use Arden's lemma to get a regular expr for the language accepted by the machine
* Q6, give a regular grammar for the language in 5

### midterm 2

#### DCFL (deterministic)
* http://www.cs.toronto.edu/~ashe/CFL.pdf
  * DCFL is not closed under union, and not closed under intersection.
* 


## Michael Sipser - Introduction to the Theory of Computation (2013)
* THEOREM 1.26 The class of regular languages is closed under the concatenation operation.


## Kozen - Automata and Computability 2012

* If A and B are regular, then so is AB. To see this, let M be an automaton for A and N an automaton for B. Make a new automaton P whose states are the union of the state sets of M and N, and take all the transitions of M and N as transitions of P. Make the start states of M the start states of P and the final states of N the final states of P. Finally, put f-transitions from all the final states of M to all the start states of N. Then L(P) = AB.
* 

### Lecture 4
* multiple of 3 in binary
* the product construction
  * Assume that A and B are regular. Then there are automata
  * To show that An B is regular, we will build an automaton M3 such that L(M3) = An B.
  * Intuitively, M3 will have the states of M1 and M2 encoded somehow in its states. On input x € *, it will simulate M₁ and M₂ simultaneously on x, accepting iff both M1 and M2 would accept. Think about putting a pebble down on the start state of M₁ and another on the start state of M2. As the input symbols come in, move both pebbles according to the rules of each machine. Accept if both pebbles occupy accept states in their respective machines when the end of the input string is reached.
* 

```
The Product Construction
Assume that A and B are regular. Then there are automata
M1 = (Q1, 2, 61, S1, F1),
M2 = (Q2, E, 82, 82, F2)
with L(M1) = A and L(M2) = B. 
```


### Lecture 6 ; subset construction
* more closure properties

### Lecture 9 ; regular expressions and finite automata
* Just because all states of an NFA are accept states doesn't mean that all  strings are accepted! Note that in Example 9.2, 000 is not accepted. 

### Lecture 11 ; limitations of finite automata
* Because of the alternating "for all/there exists" form of (.,P), we can think of this as a game between you and a demon.

### Lecture 13 ; DFA state minimization
* quotient construction
  * The Quotient Construction  How do we know in general when two states can be collapsed safely without  changing the set accepted? How do we do the collapsing formally? Is there  a fast algorithm for doing it? How can we determine whether any further  collapsing is possible?  Surely we never want to collapse an accept state p and a reject state q,  because if p = 6(s, x) E F and q = 6(s,y) (j F, then x must be accepted  and y must be rejected even after collapsing, so there is no way to declare  the collapsed state to be an accept or reject state without error. Also, if  we collapse p and q, then we had better also collapse 6 (p, a) and 6 (q, a) to  maintain determinism. These two observations together imply inductively  that we cannot collapse p and q if 6(p, x) E F and 6(q,x) (j F for some  string x
* 

### Lecture 14 ; a minimization algorithm
* Repeat the following until no more changes occur: if there exists an  unmarked pair {p,q} such that {6(p,a),6(q,a)} is marked for some  a E~, then mark {p,q}.
* Correctness of the Collapsing Algorithm 
  * Theorem 14.3 The pair {p, q} is marked by the above algorithm if and only if there exists  x E ~* such that 6(p, x) E F and 6( q, x) f/. F or vice versa; i. e., if and only  ifp ~ q.  Proof. This is easily proved by induction. We leave the proof as an exercise  (Miscellaneous Exercise 49). 
* 

## 18-404j-t.o.c /lecture-notes/

* https://ocw.mit.edu/courses/18-404j-theory-of-computation-fall-2020/pages/lecture-notes/
  * https://ocw.mit.edu/courses/18-404j-theory-of-computation-fall-2020/9b025394d997750b3cd765c7a074881f_MIT18_404f20_lec17.pdf
  * 17. Space Complexity, PSPACE, Savitch's Theorem-cT_qwkTigv4.en.srt
  * https://ocw.mit.edu/courses/18-404j-theory-of-computation-fall-2020/88f789664d3236a64481714fc911d119_MIT18_404f20_lec18.pdf
* 

### 17. Space Complexity, PSPACE, Savitch's Theorem-cT_qwkTigv4
![](https://hackmd.io/_uploads/ByMcLuQNn.png)

* https://www.youtube.com/watch?v=cT_qwkTigv4
* you know there are some collapses  that obviously could not uh occur like p  if p equals np it's also going to equal  cohen p  um so you can't get some there are  obviously some crazy collapses which  could not  uh happen that p collapsing p and np  being the same but different from cohen  b that can't happen  but um  avoiding some obvious contradictory  situations everything else is possible ; 36:51
* you can't necessarily  complement the  behavior of an np machine and end up  with an np machine  so a question how do we know that cohen  p is a complete class of problems i  didn't say that there's anything about  completeness and cohen p is just a  collection of languages i'm not saying  it's anything any particular feature  about it in fact it does have a complete  problem just like np has a complete  complete problem the complements  and i'm not going to prove this right  here but though it's pretty  straightforward  complements of all the np-complete  languages are going to be co-np-complete  languages
* p space itself is closed under  complement  because it is  defined in terms of deterministic  machines and deterministic machines you  can always flip the answer  and get a machine  of the same type  which um  uh  uh will decide the complementary  language  so for deterministic machines  deterministic deciders i should say um  you can always flip the answer  um  now  so here we have anything that's in p  space  it has a deterministic polynomial time a  polynomial space uh machine and so its  complementary line which is also going  to be in p space so p space and cos base  p co p space are equal and so that's why  coen p  uh is going to be in p space it's going  to be a subset of p space
