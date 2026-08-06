# Salesforce Developer Bridge – Day 1 Documentation

*Name:* Golla Vaishnavi
*Scenario:* Hospital OPD Management System
*Date:* 28 July 2026

## Overview

This project is part of the Salesforce Developer Bridge Program. The objective of Day 1 was to understand Salesforce data modeling, Apex programming fundamentals, SOQL queries, and Apex Triggers through the Hospital OPD Management System scenario.

---

## Task 1 – Data Model Design

### Objects Created

#### Patient__c

* Name
* Age__c
* Gender__c
* Contact_Number__c

#### Doctor__c

* Name
* Specialization__c
* Experience__c

#### Appointment__c

* Patient__c (Lookup to Patient)
* Doctor__c (Lookup to Doctor)
* Appointment_Date__c
* Status__c

### Relationships

* A Patient can have multiple Appointments.
* A Doctor can have multiple Appointments.
* Appointment acts as the junction object connecting Patients and Doctors.

---

## Task 2 – Apex Basics

### Trailhead Module Completed

* Apex Basics & Database

### Activities Performed

* Learned the fundamentals of Apex programming language.
* Practiced variables, data types, operators, and control statements.
* Created and executed Apex code using Execute Anonymous in the Developer Console.
* Learned how to use System.debug() and analyze Debug Logs.
* Practiced writing and executing SOQL queries.
* Retrieved records from Salesforce objects using SOQL.
* Understood how Apex interacts with Salesforce data through sObjects.

### Sample Apex Code Executed

apex
Integer num = 10;
String message = 'Hello Salesforce';

System.debug(num);
System.debug(message);


### Result

The code executed successfully in Execute Anonymous, and the expected output was displayed in the Debug Log.

### Key Concepts Learned

* Apex Classes
* Variables and Data Types
* Methods
* System.debug()
* SOQL Queries
* sObjects
* Developer Console
* Debug Logs

---

## Task 3 – SOQL Practice

### Query 1 – WHERE Clause

sql
SELECT Name, Age__c
FROM Patient__c
WHERE Age__c > 30


*Output*

* Total Rows: 0

---

### Query 2 – ORDER BY + LIMIT

sql
SELECT Name
FROM Patient__c
ORDER BY CreatedDate DESC
LIMIT 5


*Output*

* Patient-0001
* Patient-0002
* Patient-0003

Total Rows: 3

---

### Query 3 – Relationship Query

sql
SELECT Name,
       Patient__r.Name,
       Doctor__r.Name
FROM Appointment__c


*Output*

* Appointment-0001 | John | Dr. Smith
* Appointment-0002 | Mary | Dr. Rao

Total Rows: 2

---

### Query 4 – Aggregate Query

sql
SELECT COUNT(Id)
FROM Appointment__c


*Output*

| expr0 |
| ----- |
| 2     |

---

### Query 5 – Comparison Operator (>=)

sql
SELECT Name, Age__c
FROM Patient__c
WHERE Age__c >= 18


*Output*

* John | 25
* Mary | 32

Total Rows: 2

---

## Task 4 – Apex Trigger

### Appointment Trigger

apex
trigger AppointmentTrigger on Appointment__c (
    before insert,
    after update
) {

    if(Trigger.isBefore && Trigger.isInsert){
        AppointmentTriggerHandler.beforeInsert(Trigger.new);
    }

    if(Trigger.isAfter && Trigger.isUpdate){
        AppointmentTriggerHandler.afterUpdate(Trigger.new);
    }
}


### Purpose

* Executes validation and business logic before appointment records are inserted.
* Performs post-processing activities after appointment records are updated.
* Uses a Trigger Handler pattern to maintain clean, reusable, and scalable code.

---

## Skills Gained

* Salesforce Data Modeling
* Apex Programming Fundamentals
* SOQL Query Development
* Salesforce Object Relationships
* Debugging with Developer Console
* Apex Trigger Development
* Trigger Handler Design Pattern

---

## Outcome

Successfully completed all Day 1 activities of the Salesforce Developer Bridge Program and gained hands-on experience in Salesforce development fundamentals using the Hospital OPD Management System use case.
