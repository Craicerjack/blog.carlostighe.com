---
title: Excel
image:
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Wed Oct 31 2018 16:07:29 GMT+0000 (GMT)
tags:
  - new
---

# Excel  

Have the joy of reverse engineering an excel application into a web application, with the added benefit of the guy who developed the excel having left the company.  
Its been a long time since Ive done much in excel but just keeping track of tidbits here and there that I pick up on my current sojurn down microsoft lane.  

`{}`:  
**Array Forumla**  
Anything wrapped in curly braces is an array formula. Single cell array formulas perform multiple calculations in a single cell.  
Instead of having a column performing one calculation and then having another calculation performed on the results you can do an array formula to complete multiple calculations in the same cell. The first results are stored in memory.  

`VLOOKUP()`  
Function to lookup a certain value in a section of the excel sheet.  
`VLOOKUP( 1, 2, 3, TRUE/FALSE)`   

 1. The Value to lookup.  
 2. Range where you want to look up that value.  
 3. Column number containing return value.  
 4. Exact or approximate match.  FALSE means exact. 

`RANK(number, ref, [order])`  
Function to rank something in terms of a list of somethings in ascending or descending order.  
`RANK(R161, $R$161:$V$161, 0)`  
rank r161 in terms of the list r161-v161 in descending order.  
3 Arguments:  

 1. number: the number to rank  
 2. ref: referenced range of numbers to compare/rank against  
 3. order: use 0 or leave blank to rank in descending order. For ascending use 1  



