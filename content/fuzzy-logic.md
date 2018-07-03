---
title: Fuzzy Logic
image:/images/fuzlog.png
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Jul 03 2018 11:59:19 GMT+0100 (IST)
tags:
  - programming  
  - fuzzy logic  
  - python  
---

# Fuzzy Logic
<http://cs.bilkent.edu.tr/~zeynep/files/short_fuzzy_logic_tutorial.pdf>

> Nonlinear mapping of an input data set to scalar output data  

## FLS (fuzzy logic system)  

 1. fuzzifier  
 2. rules  
 3. inference engine  
 4. defuzzifier  

![Fuzzy Logic System](/images/fls.png)  


 1. A crisp set of input data gathered and converted to fuzzy set using:  
     * fuzzy linguistic variables  
     * fuzzy linguistic terms  
     * membership functions  
 2. An inference is made based on a set of rules  
 3. Resulting fuzzy output is mapped to a crisp output using the membership functions.  

#### Algorithm 1 - Fuzzy Logic Alogorithm  

 1. Define the linguistic varibales and terms (initialisation)  
 2. Construct the membership functions (initialisation)  
 3. Construct the rule base (initialisation)  
 4. Convert crisp innput data to fuzzy values using the membership functions (fuzzification)  
 5. Evaluate the ruels in the rule babse (inference)  
 6. Combine the result of each rule (inference)  
 7. Convert the output data to non-fuzzy values (defuzzification)  


#### Linguistic Variables  

Linguistic variables are the input/output variables of the system, the values of which are words or sentences from a natural language, and not numerical values.  
A linguistic variable is generally decomposed into a set of linguistic terms.  

#### Membership Functions  
Membership functions are used in the fuzzification and defuzzification steps of an FLS, to map the non-fuzzy input values to linguistic terms and vice versa.
A membership function is used to quantify a linguistic term. 
![Temp Membership Functions](/images/temp.jpg)
Membership Functions for T(temperature) = {too-cold, cold, warm, hot, too-hot}.
There are different forms of membership functions such as triangular, trape-zoidal, piecewise linear, Gaussian, or singleton (Figure 4). The most common types of membership 
functions are triangular, trapezoidal, and Gaussian shapes. The type of the membership function can be context dependent and it is generally chosen arbitrarily according to the user experience  

#### Fuzzy Rules
In an FLS, a rule base is constructed to control the output variable. **A fuzzy rule is a simple IF-THEN rule with a condition and a conclusion**.  
So rules for DSF similar to:  
*If one is more important than other then answer is how much more important*    
Row captions in the matrix contain the values that current room temperature can take, column captions contain the values for target temperature, and each cell is the resulting
command when the input variables take the values in that row and column. For instance, the cell (3, 4) in the matrix can be read as follows: If temperature is cold and target is warm then command is heat.  

#### Fuzzy Set Operations
The evaluations of the fuzzy rules, and the combination of the results of the individual rules are performed using fuzzy set operations.  
  `μA(x) = 1 − μA(x)`  
  **MATHS**
After evaluating the result of each rule, these results should be combined to obtain a final result. This process is called inference.   
  **MORE MATHS**  

*what are the formuals that the DSF uses for these.*  

#### Defuzzification  
After the inference step, the overall result is a fuzzy value. This result should be defuzzied to obtain a final crisp output. Defuzzification is performed according to the membershop function of the output variable.  
**ALOGORITHMS for Defuzzification**  
![Variables used in Defuzzification](/images/defuzz2.png)  
![Defuzzification Algos](/images/defuzz1.png)  
