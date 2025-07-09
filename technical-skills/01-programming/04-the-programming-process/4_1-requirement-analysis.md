# 📖 Requirement Analysis

## 💡 Basic knowledge required:

Understanding of the overall goals of programming (from Module 1)

## 🎯 Learning Objectives

By the end of this lesson, you will be able to:

- Define "requirement analysis" and explain its role as the most critical first step of any project
- Distinguish between Functional and Non-Functional Requirements
- Identify techniques used to gather requirements from stakeholders
- Understand the importance of Requirements Specification Documents

---

## 1. Introduction: Where Most Projects Fail

Statistics in the software industry show that many projects fail not because of "bad code" but because they "build the wrong thing" or "solve the wrong problem." 

Requirement Analysis is a systematic process of discovering, analyzing, defining, and documenting the requirements for a new system. It is the most critical step in answering the question "What are we going to build?" before we think about "How are we going to build it?"

```
Project Failure vs Success Pattern:

Failed Project:
Code Quality: ████████░░ 80%
Right Solution: ███░░░░░░░ 30%
Result: FAILURE

Successful Project:
Code Quality: ██████░░░░ 60%
Right Solution: ████████░░ 80%
Result: SUCCESS
```

## 2. Types of Requirements

We can categorize requirements into two main types that must always be considered:

### Functional Requirements

Description: These define what the system "must be able to do." They describe the behavior, features, and functions of the software directly.

Examples:
- "The system must allow users to log in with username and password"
- "The system must be able to calculate product prices including value-added tax"
- "Users must be able to upload profile pictures"

### Non-Functional Requirements (NFRs)

Description: These define the qualities, characteristics, or constraints of the system. They describe how well the system should perform its functions.

Examples:

Performance: "The website homepage must load completely within 2 seconds"
Security: "All user passwords must be stored in hashed format only"
Reliability: "The system must have 99.9% uptime availability"
Scalability: "The system must support 10,000 concurrent users"
Usability: "New users must be able to complete their first purchase without reading any manual"

```
Requirements Classification:

Functional Requirements          Non-Functional Requirements
┌─────────────────────┐         ┌─────────────────────────┐
│ What system does    │         │ How well system does it │
│                     │         │                         │
│ • Login feature     │         │ • Performance (speed)   │
│ • Calculate prices  │         │ • Security (safety)     │
│ • Upload files      │         │ • Reliability (uptime)  │
│ • Generate reports  │         │ • Scalability (users)   │
│ • Search products   │         │ • Usability (ease)      │
└─────────────────────┘         └─────────────────────────┘
```

## 3. Requirement Gathering Process

This is the investigative process of extracting information from stakeholders, who may be users, business owners, or department managers. Various techniques are used:

### Techniques for Gathering Requirements

Interviews: Direct conversations with stakeholders
- One-on-one meetings with key users
- Group discussions with multiple stakeholders
- Structured question sessions

Questionnaires: Collecting data from large numbers of users
- Online surveys for broad feedback
- Paper forms for specific departments
- Rating scales for feature prioritization

Observation: Watching users work in current processes to identify real problems
- Workplace shadowing
- Process documentation
- Pain point identification

Document Analysis: Studying existing work manuals or legacy systems
- Current system documentation
- Business process flows
- Regulatory requirements

Prototyping: Creating mockups or prototypes of the program for early user feedback
- Paper wireframes
- Digital mockups
- Interactive prototypes

```
Requirement Gathering Flow:

Stakeholders ──► Techniques ──► Analysis ──► Documentation
     │               │              │              │
     ▼               ▼              ▼              ▼
┌─────────┐   ┌─────────────┐   ┌─────────┐   ┌─────────┐
│ Users   │   │ Interviews  │   │ What?   │   │   SRS   │
│ Owners  │   │ Surveys     │   │ How?    │   │Document │
│ Managers│   │ Observation │   │ When?   │   │         │
└─────────┘   └─────────────┘   └─────────┘   └─────────┘
```

## 4. Output: Requirements Specification Document

The ultimate goal of this phase is to create formal documentation, such as a Software Requirements Specification (SRS), which details all functional and non-functional requirements. 

This document serves as a "contract" between the development team and stakeholders, ensuring everyone has a clear and consistent understanding of what is being built. This document becomes the most important foundation for the subsequent design phase.

```
Requirements Specification Document Structure:

┌─────────────────────────────────────────┐
│            SRS Document                 │
├─────────────────────────────────────────┤
│ 1. Introduction & Scope                 │
│    - Project overview                   │
│    - System boundaries                  │
├─────────────────────────────────────────┤
│ 2. Functional Requirements              │
│    - User login system                  │
│    - Data processing features           │
│    - Report generation                  │
├─────────────────────────────────────────┤
│ 3. Non-Functional Requirements          │
│    - Performance standards              │
│    - Security requirements              │
│    - Usability guidelines               │
├─────────────────────────────────────────┤
│ 4. Acceptance Criteria                  │
│    - Success measurements               │
│    - Testing standards                  │
└─────────────────────────────────────────┘
```

---

## 📋 Summary & Practical Exercise

### Comprehensive Summary

Requirement analysis is the most critical first step in understanding "what to build." It involves gathering both Functional Requirements (what the system can do) and Non-Functional Requirements (how well the system performs) to create clear specification documents.

Key concepts:
- Requirement Analysis: Systematic process answering "What to build?"
- Functional Requirements: System capabilities and features
- Non-Functional Requirements: System quality and performance standards
- Stakeholders: People affected by or interested in the system
- SRS Document: Formal contract between developers and stakeholders

### Practical Exercise

Thinking Challenge: Suppose you are assigned to create a simple "Note-taking App":

1. List 3 essential Functional Requirements (e.g., users must be able to...)
2. List 2 important Non-Functional Requirements (e.g., how fast should the app open? How secure should the data be?)

Step-by-Step Solution:

```
Note-taking App Requirements Analysis:

FUNCTIONAL REQUIREMENTS (What it does):
┌─────────────────────────────────────────────┐
│ 1. Users must be able to create new notes   │
│    with titles and content                  │
│ 2. Users must be able to edit and delete    │
│    existing notes                           │
│ 3. Users must be able to search through     │
│    notes by title or content                │
└─────────────────────────────────────────────┘

NON-FUNCTIONAL REQUIREMENTS (How well it works):
┌─────────────────────────────────────────────┐
│ 1. Performance: App must open and display   │
│    note list within 1 second                │
│ 2. Security: All notes must be encrypted    │
│    and protected with user authentication   │
└─────────────────────────────────────────────┘
```

Additional considerations for comprehensive analysis:

```
Requirement Gathering for Note-taking App:

Interview Questions:
• How many notes do you typically create per day?
• What devices do you use for note-taking?
• Do you need to share notes with others?

Observation Points:
• Current note-taking habits
• Frustrations with existing tools
• Workflow patterns

Success Metrics:
• User can create first note in under 30 seconds
• App crashes less than 0.1% of the time
• 95% user satisfaction rating
```

This exercise demonstrates how to systematically identify both functional capabilities and quality standards, ensuring comprehensive requirement coverage for successful project development.

---

📍 Since most of the techniques and skills I've shared and demonstrated here were acquired through self-study, there might be some errors or omissions.
