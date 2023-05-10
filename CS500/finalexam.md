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

### Lecture030223.pdf ; closure properties of CFL
* https://sites.cs.ucsb.edu/~cappello/136/lectures/17cfls/slides.pdf
  * L1 ∩ L2 = \{anbnan| n ≥ 0\}, which is known not to be a CFL

### Lecture041823 ; tseytin transformation ; def of NP ; TM configuration
* https://www.youtube.com/watch?v=v2uW258qIsM
  * bi-implication is just a conjunction  of two implications  one from left to right and one from  right to left  and if we consider the implication from  left to right  we see p implies q or r  is equivalent to not p or q or r  which is a clause itself  and the other direction q or  r implies p is equivalent to  not q or r or p and by the morgan rules  it can be written in this way  and by applying distributivity we get  these two clauses

![](https://i.imgur.com/Ch9lNIW.png)

![](https://i.imgur.com/BSfuWUB.png)

![](https://i.imgur.com/FtvWK6J.png)

![](https://i.imgur.com/eDAxOAS.png)

![](https://i.imgur.com/IV873Pr.png)

![](https://i.imgur.com/y8ydznh.png)

![](https://i.imgur.com/YpXx0JQ.png)


## CS500 HW
### HW?
* ADD - REGULAR
* MULTIPLY

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

### midterm 2

#### DCFL (deterministic)
* http://www.cs.toronto.edu/~ashe/CFL.pdf
  * DCFL is not closed under union, and not closed under intersection.
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
