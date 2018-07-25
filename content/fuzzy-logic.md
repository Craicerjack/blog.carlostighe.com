---
title: Fuzzy Logic
image: /images/fuzlog.png  
featured: true
author: carlos
date: Tue Jul 03 2018 11:59:19 GMT+0100 (IST)
tags:
  - programming  
  - fuzzy logic  
  - python  
---

# Fuzzy Logic
[The saucy sauce these notes were taken from](http://cs.bilkent.edu.tr/~zeynep/files/short_fuzzy_logic_tutorial.pdf)

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


## Scikit Fuzzy
Python library for Fuzzy Logic.   
`pip install -U scikit-fuzzy`  

Works with `numpy` arrays. Packag is imported as skfuzzy.  
```python  
import numpy as np
import skfuzzy as fuzz  
```  

Fuzzy Logic is a methodology predicated on the idea that the 'truthiness' of something can be expressed over a continuum. This is to say that something isnt *true* or *false* but indtead partially true or partially false.  

A fuzzy variable has a crisp value which takes on some number over a pre-defined domain (in fuzzy logic terms, called a universe). The crisp value is how we think of the variable using normal mathematics. *For example, if my fuzzy variable was how much to tip someone, it’s universe would be 0 to 25% and it might take on a crisp value of 15%.*  
A fuzzy variable also has several terms that are used to describe the variable. The terms taken together are the fuzzy set which can be used to describe the “fuzzy value” of a fuzzy variable. These terms are usually adjectives like “poor,” “mediocre,” and “good.” Each term has a membership function that defines how a crisp value maps to the term on a scale of 0 to 1. In essence, it describes “how good” something is

A fuzzy variable also has several terms that are used to describe the variable. The terms taken together are the fuzzy set which can be used to describe the “fuzzy value” of a fuzzy variable. These terms are usually adjectives like “poor,” “mediocre,” and “good.” Each term has a membership function that defines how a crisp value maps to the term on a scale of 0 to 1. In essence, it describes “how good” something is. *So, back to the tip example, a “good tip” might have a membership function which has non-zero values between 15% and 25%, with 25% being a “completely good tip” (ie, it’s membership is 1.0) and 15% being a “barely good tip” (ie, its membership is 0.1).*

A fuzzy control system links fuzzy variables using a set of rules. These rules are simply mappings that describe how one or more fuzzy variables relates to another. These are expressed in terms of an IF-THEN statement; the IF part is called the antecedent and the THEN part is the consequent. In the tiping example, one rule might be “IF the service was good THEN the tip will be good.”   
The exact math related to how a rule is used to calcualte the value of the consequent based on the value of the antecedent is outside the scope of this primer.


##### Antecedents (Inputs)  
 - service  
     - Universe (crisp value range): How good was the service, on a scale of 1 - 10.  
     - Fuzzy set (fuzzy value range): poor, acceptable, amazing  
 - food quality  
     - Universe: How tasty was food, scale 1 -10  
     - Fuzzy set: bad, decent, great  

##### Consequents (Outputs)  
  - tip
      - Universe: How much should we tip scale 0-25%  
      - Fuzzy set: bad, decent, great

##### Rules  
  -   **IF** the *service* was good *or* the *food quality* was good **THEN** the tip will be high  
  - **IF** the *service* was average **THEN** the tip will be medium  
  - **IF** the *service* was poor *and* the *food quality* was poor **THEN** the tip will be low  

##### Usage  
  - If I tell this controller that I rated
      - the service as 9.8 and  
      - the quality as 6.5  
  - it would recommend I leave a 20.2% tip  

#####   
