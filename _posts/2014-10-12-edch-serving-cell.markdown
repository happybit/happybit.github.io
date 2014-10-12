---
layout: post
title: "E-DCH serving cell"
date: 2014-10-12 17:00
comments: true
categories: Radioaccess
---

Kind of busy these days. I will simply share some basic knowledge from my personal wiki. The first one is about the definition of E-DCH serving cell.

<!--more--> 

Once you read about all kinds of technical materials, like 3GPP technical specification or those feature documentations within your company. You might probably have met several specific terms related to E-DCH serving cell, which are not explicitly explained. Therefore you would confuse about them. Let me get it straight. 

Actually, most of them come from [3GPP TS25.321](http://www.3gpp.org/DynaReport/25321.htm) subclause 3.1.

* **Serving E-DCH cell**: Cell from which the UE receives Absolute Grants from the Node-B scheduler. A UE has one Serving E-DCH cell.
* **E-DCH active set**: The set of cells which carry the E-DCH for one UE. For FDD, in CELL_FACH state and Idle mode, the E-DCH active set consists of the Serving E-DCH cell only. There are **at most 4 cells** within one E-DCH active set for a certain UE.
* **Non-serving E-DCH RL or Non-serving RL**: Cell which belongs to the E-DCH active set but does not belong to the Serving E-DCH RLS and from which the UE can receive one Relative Grant. The UE can have zero, one or several Non-serving E-DCH RL(s).
* **Serving E-DCH RLS or Serving RLS**: Set of cells which contains at least the Serving E-DCH cell and from which the UE can receive and combine one Relative Grant. The UE has only one Serving E-DCH RLS. For FDD, in CELL_FACH state and Idle mode, the Serving E-DCH RLS or Serving RLS contains the Serving E-DCH cell only, from which the UE can receive one Relative Grant.

For better understanding, I draw a picture to illustrate. 

![E-DCH serving cell](https://dl.dropboxusercontent.com/u/6459697/blogimage/20141012_edch_serving_cell.png)

As you can see from above picture, cell 2 of Node B 1 is the Serving E-DCH cell for this UE. Cell 2 and cell 3 from Node B 1 and cell 1 from Node B2 consist of E-DCH active set. While Serving E-DCH RLS includes cell 2 and cell 3 of Node B 1. And Cell 1 of Node B 2 is Non-serving E-DCH RL.

Please note, the presumption for Serving E-DCH RLS in above picture is cell 2 and cell 3 are controlled and scheduled by the same scheduler. Or they share the same source for E-RGCH decision. Otherwise they cannot be called as a Serving E-DCH cell.

And you can find that:

1. Serving E-DCH cell could send E-AGCH and all three kinds of E-RGCH, i.e. UP, Hold, and DOWN;
2. The cells in Serving E-DCH RLS other than Serving E-DCH cell could only send E-RGCH with all three possible decisions: UP/HOLD/DOWN;
3. Non-serving E-DCH RL could only send E-RGCH with two kinds of E-RGCH: HOLD/DOWN;

Why there is no UP for Non-serving E-DCH RL? Think about it. Basically E-RGCH from non-serving E-DCH RL is major for power overload control and not in charge of UE scheduling, which means non-serving E-DCH RL only send E-RGCH once the total cell power is exceeded certain threshold. Then it would send E-RGCH DOWN to those non-serving UEs in order to decrease the interference from other cells.

All above definition are from UE point of view. However there is also a term from cell perspective. That is **Non-serving UE**. Generally non-serving UE is the user equipment whose serving cell is not this cell. Talk to above picture, we can say this UE is non-serving UE for cell 3 of Node B 1 as well as cell 1 of Node B 2.

This is just my personal understanding. Please correct me if I am wrong. I'd be really appreciated.
