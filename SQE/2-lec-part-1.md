# 📌 Classification of Software Quality Factors

## McCall’s Factor Model

McCall’s Factor Model classifies all software requirements into **11 factors**. These factors are grouped into **3 categories**:

### 1. Product Operation Factors
These factors deal with requirements that directly affect the daily operation of the software.

### 2. Product Revision Factors
These factors deal with requirements that affect software maintenance.

### 3. Product Transition Factors
These factors deal with requirements that affect the adaptation of software to other platforms, environments, and interactions with other software.

---

## Alternative Factor Models

Two factor models, emerging in the late 1980s, are considered alternatives to McCall’s classic factor model (McCall et al., 1977):

### 1. The Evans and Marciniak Factor Model (1987)
### 2. The Deutsch and Willis Factor Model (1988)

---

### Comparison of Factor Models:

1. **Exclusion of Factors**:  
   Both alternative models exclude one of McCall’s 11 factors: **Testability**.
   
2. **Evans and Marciniak Factor Model**:  
   This model consists of **12 factors**, which are classified into **three categories**.

3. **Deutsch and Willis Factor Model**:  
   This model consists of **15 factors**, which are classified into **four categories**.

---

### New Factors Suggested:

A total of **five new factors** were proposed by the alternative models:

#### **Evans and Marciniak Suggested the Following Two New Factors:**
1. **Verifiability**  
   Verifiability requirements address design and programming features that allow for efficient verification of design and programming. This doesn't refer to outputs but focuses on the structure of code, design elements, their dependencies, coupling, cohesion, patterns, modularity, simplicity, and adherence to documentation and programming guidelines.
   
2. **Expandability**  
   Expandability refers to scalability and extensibility to provide more usability, which is essentially McCall’s **Flexibility**.

#### **Deutsch and Willis Suggested the Following Three New Factors:**
1. **Safety**  
   Safety requirements address conditions that could bring the equipment or application down, especially for controlling software like setting alarms or sounding warnings. This is particularly important for process control or real-time software, such as software running conveyor belts or instrumentation for ordnance.

2. **Manageability**  
   Manageability requirements refer to tools primarily for administrative purposes to control versions, configurations, and change management. This is important for managing various versions and configurations that may vary across different customers.

3. **Survivability**  
   Survivability requirements refer to **MTBF** (Mean Time Between Failures) or the continuity of service, as well as **MTTR** (Mean Time to Recover). This is similar to the **Reliability** factor in McCall’s model.

---

By comparing these factor models, we can see how the alternative models add a more comprehensive view, addressing various new aspects related to software quality.
