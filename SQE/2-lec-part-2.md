# 📌 Boehm’s Quality Model (1978)

Boehm’s Quality Model (1978), similar to the McCall Quality Model, presents a **hierarchical quality model** structured around:

- **High-level characteristics**
- **Intermediate-level characteristics**
- **Primitive characteristics** (Software Quality Assurance - SQA)

---

## High-level Characteristics (Primary Characteristics)

The high-level characteristics represent the basic high-level requirements of actual use to which evaluation of software quality could be put. These characteristics address the **general utility** of the software and are essential for understanding the usability of a system.

### Main Questions Addressed for the Buyer of Software:
1. **As-is utility**:  
   How well (easily, reliably, efficiently) can I use it as-is?
   
2. **Maintainability**:  
   How easy is it to understand, modify, and retest?

3. **Portability**:  
   Can I still use it if I change my environment?

---

## Intermediate-level Characteristics

The intermediate-level characteristics represent **Boehm's 7 quality factors** that together reflect the qualities expected from a software system.

1. **Portability** *(General utility characteristics)*:  
   Code possesses the characteristic of portability if it can be easily operated on other computer configurations apart from the current one.

2. **Reliability** *(As-is utility characteristics)*:  
   Code possesses reliability if it can be expected to perform its intended functions satisfactorily.

3. **Efficiency** *(As-is utility characteristics)*:  
   Code is efficient if it fulfills its purpose without wasting resources.

4. **Usability** *(As-is utility characteristics, Human Engineering)*:  
   Code is usable if it is reliable, efficient, and human-engineered, ensuring it is easy for users to interact with.

5. **Testability** *(Maintainability characteristics)*:  
   Code is testable if it supports the establishment of verification criteria and facilitates evaluation of its performance.

6. **Understandability** *(Maintainability characteristics)*:  
   Code is understandable if its purpose is clear to the inspector or developer.

7. **Flexibility** *(Maintainability characteristics, Modifiability)*:  
   Code is flexible if it allows for easy incorporation of changes once the desired change has been identified.

---

## Lowest-level Structure (Measurable Properties)

The lowest level structure in Boehm’s quality model is the **primitive characteristics metrics hierarchy**. These primitive characteristics provide the foundation for defining quality metrics, which was one of the main goals behind the creation of the model.

### Key Point:
While **Boehm’s** and **McCall’s** models may seem similar, the primary difference is that McCall’s model mainly focuses on the precise measurement of high-level characteristics, especially "As-is utility". In contrast, Boehm’s model expands the focus to a wider range of characteristics, placing a detailed emphasis on **maintainability**.

---

This hierarchical model from Boehm allows for comprehensive assessment and measurement of software quality, with an extended focus on aspects like **maintainability**.

---
# 📌 Dromey’s Quality Model (1995)

Dromey's Quality Model provides a framework for evaluating software components by measuring tangible quality properties. This model analyzes the quality of software artifacts produced throughout the software life cycle. Each artifact, depending on its stage, can be associated with a quality evaluation model.

### Software Components in Dromey's Model:
- **Implementation Model**: Components such as variables, functions, and statements.
- **Requirements Model**: A requirement is considered a component in this model.
- **Design Model**: A module is a component in the design model.

---

## Four Categories of Quality Evaluation

Dromey suggests that all these components possess intrinsic properties that can be classified into **four categories**:

1. **Correctness**:  
   This category evaluates whether any basic principles have been violated within the component. For example, it ensures that the component does not produce errors or unexpected behaviors.

2. **Internal**:  
   This category measures how well a component has been deployed according to its intended use. It focuses on the internal structure and functionality of the component.

3. **Contextual**:  
   This category deals with the external influences and conditions that affect the use of a component. For instance, how a component behaves in a particular environment or under certain conditions.

4. **Descriptive**:  
   This category measures the descriptiveness of a component, such as whether it has a meaningful name or if it is easily understandable by other developers or users.

---

## Mapping Categories to Quality Attributes
The four categories described above (Correctness, Internal, Contextual, and Descriptive) can be mapped to different **quality attributes** to evaluate software in a comprehensive manner.


---
# Key Differences Between McCall’s, Boehm’s, and Dromey’s Quality Models

## 1. **McCall’s Quality Model (1977)**
- **Focus**: McCall’s model focuses on **high-level software quality factors** and categorizes them into three main groups: 
  - Product Operation Factors
  - Product Revision Factors
  - Product Transition Factors
- **Quality Factors**: McCall defines 11 quality factors such as reliability, efficiency, usability, maintainability, and portability.
- **Focus on Measurement**: Primarily aims to **measure the operational aspects** of software such as how well it performs its tasks, and how easily it can be modified or adapted.
- **Main Focus**: It places a significant emphasis on **As-is utility** (how well the software performs as-is).

---

## 2. **Boehm’s Quality Model (1978)**
- **Focus**: Boehm’s model is **hierarchical**, with a primary focus on the **general utility** of software and its maintainability. The model addresses the following:
  - High-level characteristics (As-is utility, Maintainability, Portability)
  - Intermediate-level characteristics (Portability, Reliability, Efficiency, Usability, Testability, Understandability, Flexibility)
  - Low-level measurable properties (primitive characteristics).
- **Quality Factors**: Boehm introduces **seven intermediate-level characteristics** such as reliability, efficiency, and flexibility.
- **Maintainability Emphasis**: Boehm’s model has a strong focus on **maintainability** and how easily the software can be modified or updated in the future.
- **Key Question**: It answers questions such as "How easy is it to understand, modify, and retest?"

---

## 3. **Dromey’s Quality Model (1995)**
- **Focus**: Dromey’s model focuses on the **measurement of tangible properties** of software components throughout the software lifecycle.
- **Quality Categories**: Dromey categorizes quality into **four properties**:
  - Correctness
  - Internal
  - Contextual
  - Descriptive
- **Quality Evaluation Framework**: The model evaluates software based on **product properties**, such as whether the component violates basic principles (Correctness) or whether it is understandable (Descriptive).
- **Focus on Components**: Each component (e.g., variables, modules, requirements) is analyzed based on intrinsic properties. 
- **Unique Approach**: Focuses on **intrinsic properties of individual components**, mapping these properties to software quality attributes.

---

## **Key Differences in Summary**

| **Aspect**                      | **McCall’s Model**                              | **Boehm’s Model**                               | **Dromey’s Model**                               |
|----------------------------------|-------------------------------------------------|-------------------------------------------------|--------------------------------------------------|
| **Focus**                        | High-level software quality factors             | Hierarchical approach with emphasis on maintainability | Measurement of tangible properties of software components |
| **Quality Categories**           | 11 factors divided into 3 categories (Operation, Revision, Transition) | 3 levels: high, intermediate, low-level characteristics | 4 categories (Correctness, Internal, Contextual, Descriptive) |
| **Maintainability Emphasis**     | Moderate                                       | High, focuses on maintainability and adaptability | Moderate, but focuses on internal properties of components |
| **Components Analyzed**          | General software system qualities               | Utility of software across different environments | Focus on individual components (e.g., variables, modules) |
| **Measurability**                | Emphasizes operational and modification aspects | Detailed metrics for evaluating maintainability and utility | Focuses on evaluating intrinsic properties of components |
| **Software Lifecycle Focus**     | Primarily on product operation and transition   | Complete lifecycle from operational to maintenance stages | Focuses on the measurement of components across lifecycle |

---

## Conclusion:
- **McCall’s** model provides a comprehensive set of **quality factors** focused on **performance and usability**.
- **Boehm’s** model offers a **hierarchical quality evaluation** with an emphasis on **maintainability** and **flexibility**.
- **Dromey’s** model evaluates **intrinsic properties** of software components, categorizing them into **correctness, internal, contextual, and descriptive** properties.


---
# Process Quality Standards

## Overview of Process Quality Standards
Process Quality Standards define best practices for software development and business processes to ensure high-quality products. These standards are essential for improving the development process, ensuring that software is produced efficiently and meets user needs.

There are **two kinds of quality standards**:
1. **Maturity Models**: Measure how well-developed (mature) a software process is within an organization and predict the likelihood of producing quality results.
2. **Certification Standards**: Assess an organization's software process against a defined standard and certify the organization if its process meets the required standard.

---

## ISO 9000 Family of Standards

### Introduction to ISO 9000
- The **ISO 9000 Family of Standards** was originally developed in **1987** and revised multiple times (in **1994, 2000, and 2005**).
- These standards are a set of guidelines for **quality assurance management**.
- Many customers, especially in Europe, require **ISO 9000 registration** for their suppliers.
- **ISO 9000 "registered"** status is granted after a formal audit by ISO (International Organization for Standardization).
- The standards are **documentation-based**, meaning that every aspect of the software process must be backed up by formal documentation.
  
### Key Documentation Guidelines:
- **Owner** of the document must be specified.
- Distribution and version control of documents must be managed.
- Each page should be **numbered**, and the total number of pages should be on the title page.
- There should be a procedure for the **destruction of obsolete documents**.

### Complexity and Stringency:
- ISO 9000 standards are known for being **complex, detailed, and stringent**, with an emphasis on maintaining comprehensive records.

---

## Capability Maturity Model (CMM)

### Overview of CMM
The **Software Engineering Institute (SEI)** developed the **CMM** to evaluate the maturity of an organization’s software process.
- The **CMM defines a five-level scale** for process maturity.
- The organization is assessed at levels such as **CMM-1**, **CMM-3**, or **CMM-5**, which indicate the organization's process maturity.

### CMM Levels:

1. **CMM Level 1 - "Initial"**:
   - At this level, processes are **ad-hoc** or non-existent.
   - Software production is **chaotic**, and success depends on individuals rather than defined processes.
   - **Challenges**: When individuals leave, there’s a lack of understanding of what has been done and what needs to be done.
   - **Result**: Low-quality software.

2. **CMM Level 2 - "Repeatable"**:
   - At this stage, basic project management practices like tracking costs and schedules are in place.
   - Techniques such as **function point analysis** and **COCOMO** are used for cost estimation.
   - The organization can **repeat successes** on similar projects but is still limited to projects of the same type.

3. **CMM Level 3 - "Defined"**:
   - Processes for both **management** and **development** activities are defined and documented.
   - There is an organization-wide understanding of roles and responsibilities.
   - However, **quality metrics** are not yet measured at this level.
   - **ISO 9000** aims to help organizations reach this level.

4. **CMM Level 4 - "Managed"**:
   - The focus shifts to **software metrics**: 
     - **Product metrics** (e.g., size, reliability).
     - **Process metrics** (e.g., defect correction time, productivity).
   - Quantitative goals for the products are set.
   - **Process measurements** are used to evaluate the performance of projects rather than improving processes.

5. **CMM Level 5 - "Optimizing"**:
   - At this stage, continuous process improvement is achieved through **quantitative feedback** and the application of **innovative ideas**.
   - The organization collects both **process and product metrics**.
   - Lessons learned from previous projects are applied to enhance processes.
   - Innovations such as new tools, methods, or technologies are implemented to optimize software processes.

---

## Conclusion

### Comparison:
- **ISO 9000** focuses on establishing a formal, documented process for **quality assurance** in software development.
- **CMM** provides a **five-level maturity model**, aiming to help organizations improve their software processes over time by focusing on levels of process maturity.
- Both ISO 9000 and CMM emphasize the **importance of process documentation**, but CMM goes further by providing detailed steps for continuous **process improvement**.

