title: External and Internal Software Quality Characteristics
author: lyenliang
date: 2017-12-03 10:23:34
tags:
---
The following contents are extracted from [Code Complete: A Practical Handbook of Software Construction, Second Edition](https://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670). This is one of the chapters that impressed me. So I think I should write it down on my blog.

Software quality has both external and internal characteristics. External characteristics are characteristics that a user of the product is aware of, including the following:

###### Correctness 
    The degree to which a system is free from faults in its specification, design, and implementation.

###### Usability 
    The ease with which users can learn and use a system.

###### Efficiency
    Minimal use of system resources, including memory, CPU usage, and execution time.

###### Reliability
    The ability of a system to perform its required functions under stated conditions whenever required-having a long mean time between failures.

###### Integrity
    The degree to which a system prevents unauthorized or improper access to its programs and its data.

###### Adaptability
    The extent to which a system can be used, without modification, in applications or environments other than those for which it was specifically designed.

###### Accuracy
    The degree to which a system is free from error, especially with respect to quantitative outputs. For example, if a calculator program on your computer says that 1 + 1 = 3, then the accuracy of the program is bad.
    
    The difference between accuracy and correctness is that accuracy is a determination of how well a system does the job it's built for rather than whether it was built correctly.

###### Robustness 
    The degree to which a system continues to function in the pressence of invalid inputs or stressful environmental conditions.

Internal characteristics are characteristics that only the programmers of the product can be aware of, including

###### Maintainability
    The ease with which you can modify a software system to change or add features, improve performance, or correct defects.

###### Flexibility
    The extent to which you can modify a system for uses or environments other than those for which it was specifically designed.

###### Portability
    The ease with which you can modify a system to operate in an environment different from that for which it was specifically designed. For example, if you find that it's easy to modify a program which was designed to run specifically on windows system to run on linux system, then portability of them program is good.

###### Reusability
    The extent to which and the ease with which you can use parts of a system in other systems.

###### Readability
    The ease with which you can read and understand the source code of a system.

###### Testability
    The degree to which you can unit-test and system-test a system; the degree to which you can verify that the system meets its requirements.

###### Understandability
    The ease with which you can comprehend a system at both the system-organizational and detailed-statement levels. Understandability has to do the coherence of the system at a more general level than readability does.