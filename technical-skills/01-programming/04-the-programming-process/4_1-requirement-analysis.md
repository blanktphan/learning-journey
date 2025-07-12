# 📖 Topic: 4.1 Requirement Analysis

## 💡 Basic knowledge required

- An understanding of the overall purpose of programming (from Chapter 1).

## 🎯 Learning Objectives

- Define "Requirement Analysis" and explain its role as the most critical first step of a project.
- Differentiate between Functional and Non-Functional Requirements.
- Identify techniques used to gather requirements from stakeholders.
- Understand the importance of a Requirements Specification Document.

---

### Introduction to Chapter 4

In the previous chapter, we learned about the "components" or "tools" that programming languages provide, such as variables, loops, and functions. In this chapter, we will step back to see the bigger picture and learn the "workflow" that programmers and software engineers use to systematically build a program, from receiving a vague request from a user to delivering a working piece of software.

### 1. Introduction: The Most Common Point of Project Failure

Statistics in the software industry show that many projects fail not because of "bad code," but because they "built the wrong thing" or "solved the wrong problem." Requirement Analysis is the systematic process of discovering, analyzing, defining, and documenting the requirements for a new system. It is the most crucial step in answering the question "What are we going to build?" before we think about "How are we going to build it?"

This initial phase sets the foundation for the entire project. A mistake here can have a cascading effect, leading to wasted time, budget overruns, and a final product that does not meet user needs.

```
+--------------------------+      +------------------------+      +----------------------+
|      Vague Idea          |----->| Requirement Analysis   |----->|  Clear, Actionable   |
| "We need a note app."    |      | (Asking "What?")       |      |         Plan         |
+--------------------------+      +------------------------+      +----------------------+
```

### 2. Types of Requirements

We can classify requirements into two main types that must always be considered:

#### A. Functional Requirements

These define what the system "must do." They describe the specific behaviors, features, and functions of the software.

- Example 1: "The system must allow users to log in with a username and password."
- Example 2: "The system must be able to calculate the total price of items including value-added tax."
- Example 3: "The user must be able to upload a profile picture."

#### B. Non-Functional Requirements (NFRs)

These define the qualities, characteristics, or constraints of the system. They describe "how well" the system should perform its functions.

- Performance: "The website's homepage must load completely within 2 seconds."
- Security: "All user passwords must be stored only in a hashed format."
- Reliability: "The system must have an uptime of 99.9%."
- Scalability: "The system must support 10,000 concurrent users."
- Usability: "A new user must be able to successfully purchase an item without reading a manual."

### 3. The Requirement Gathering Process

This is an investigative phase to extract information from stakeholders, who could be users, business owners, or department managers. Various techniques are used:

- Interviews: Direct conversations with stakeholders.
- Questionnaires: Collecting information from a large number of users.
- Observation: Watching users perform their current tasks to identify real problems.
- Document Analysis: Studying existing manuals or legacy systems.
- Prototyping: Creating models or mockups of the program to allow users to try them and provide early feedback.

```
Stakeholders -> [Interview] ->  +-----------+
(Users, Biz)  -> [Survey]  ->   |           | -> [Analysis] -> Requirements
              -> [Observe] ->   | Raw Data  |                  Specification
              -> [Docs]    ->   +-----------+
```

### 4. The Outcome: Requirements Specification Document

The ultimate goal of this phase is to create a formal document, such as a Software Requirements Specification (SRS). This document details all functional and non-functional requirements. It acts as a "contract" between the development team and the stakeholders, ensuring everyone has a clear and shared understanding of what is being built. This document becomes the primary input for the subsequent design phase.

---

## 📋 Comprehensive Summary & Practical Exercise

### Comprehensive Summary

Requirement Analysis is the critical first step to understand "what to build." It involves gathering both Functional Requirements (what the system does) and Non-Functional Requirements (how well the system performs) to produce a clear specification document. This process minimizes the risk of building the wrong product and sets the project up for success.

### Practical Exercise

Imagine you are tasked with creating a simple "Note-taking App."
1.  List three essential Functional Requirements (e.g., "A user must be able to...").
2.  List two important Non-Functional Requirements (e.g., "How fast must the app open? Should the data be secure?").

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
