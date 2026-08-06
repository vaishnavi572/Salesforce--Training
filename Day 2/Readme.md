# Salesforce Developer Bridge Program – Day 2

*Name:* Golla Vaishnavi
*Date:* July 29, 2026

## Overview

Day 2 focused on understanding Apex Collections, Governor Limits, Bulkification, Asynchronous Apex, and Lightning Web Component (LWC) Communication. The goal was to write scalable and efficient Salesforce code while following platform best practices.

---

## Day 2 Objectives

* Understand Apex Collections (List, Set, Map)
* Learn Governor Limits in Salesforce
* Understand Bulkification techniques
* Create and test a bad trigger and fix it
* Learn Asynchronous Apex using @future methods
* Understand LWC Component Communication
* Improve trigger design and interview readiness

---

## Quick Recap from Day 1

### Topics Completed

* Salesforce Data Modeling
* Lookup Relationships
* Schema Builder
* SOQL Queries
* Apex Basics
* First Trigger
* Trigger Handler Class

### Key Learnings

* Trigger logic should be written in a Handler Class.
* Trigger.new contains records currently being processed.
* Handler classes improve code maintenance and readability.

---

## Block 1 – Apex Collections

### What is a List?

A List is an ordered collection of elements.

#### Features

* Allows duplicate values
* Maintains insertion order
* Indexed collection

#### Example

apex
List<String> cities = new List<String>{
    'Hyderabad',
    'Bangalore',
    'Chennai',
    'Mumbai',
    'Delhi'
};

for(String city : cities){
    System.debug(city.toUpperCase());
}


#### Expected Output

text
HYDERABAD
BANGALORE
CHENNAI
MUMBAI
DELHI


---

### What is a Set?

A Set stores unique values only.

#### Features

* No duplicate values
* Faster searching
* Commonly used to collect record IDs

#### Example

apex
Set<Id> patientIds = new Set<Id>();

for(Patient__c p :
    [SELECT Id FROM Patient__c]){
    patientIds.add(p.Id);
}

System.debug('Set Size: ' + patientIds.size());


#### Expected Result

The Set size equals the number of unique Patient records.

---

### What is a Map?

A Map stores key-value pairs.

#### Features

* Fast record lookup
* Frequently used in bulkified triggers

#### Example

apex
Map<Id, Patient__c> patientMap =
    new Map<Id, Patient__c>(
        [SELECT Id, Name
         FROM Patient__c]
    );

Id sampleId =
    patientMap.keySet().iterator().next();

System.debug(
    patientMap.get(sampleId).Name
);


---

## Block 2 – Governor Limits and Bulkification

### What are Governor Limits?

Salesforce is a multi-tenant platform. Governor Limits ensure that one organization does not consume excessive resources and impact others.

### Common Limits

* Maximum 100 SOQL Queries
* Maximum 150 DML Statements
* CPU Time Limits
* Heap Size Limits

---

### Bad Trigger Example

The following trigger contains SOQL inside a loop.

apex
trigger BadApplicationTrigger
on Application__c(before insert){

    for(Application__c app : Trigger.new){

        Student__c student =
            [SELECT Id, CGPA__c
             FROM Student__c
             WHERE Id = :app.Student__c];

    }
}


### Problem

For 200 records:

* One query executes for each record.
* Governor limit can be exceeded.

### Typical Error

text
System.LimitException:
Too many SOQL queries: 101


---

### Bulkified Version

apex
Set<Id> studentIds = new Set<Id>();

for(Application__c app : Trigger.new){
    studentIds.add(app.Student__c);
}

Map<Id, Student__c> studentMap =
    new Map<Id, Student__c>(
        [SELECT Id, CGPA__c
         FROM Student__c
         WHERE Id IN :studentIds]
    );


### Improvements

* SOQL outside loops
* Supports bulk inserts
* Better performance
* Follows Salesforce best practices

---

### What is Bulkification?

Bulkification means writing code that can process many records in a single transaction efficiently.

### Best Practices

* Never write SOQL inside loops
* Never write DML inside loops
* Use Lists, Sets, and Maps
* Query records in bulk

---

## Block 3 – Asynchronous Apex

### What is Asynchronous Apex?

Asynchronous Apex executes in the background rather than immediately in the current transaction.

### Benefits

* Faster user experience
* Handles long-running operations
* Reduces transaction load

---

### Future Method Example

apex
public class FuturePatientUpdater {

    @future
    public static void updatePatient(Id patientId){

        Patient__c patient =
            [SELECT Id, Status__c
             FROM Patient__c
             WHERE Id = :patientId];

        patient.Status__c = 'Updated';

        update patient;
    }
}


### Execute Anonymous

apex
FuturePatientUpdater.updatePatient(
    'PATIENT_RECORD_ID'
);


---

### Future Method vs Queueable Apex

| Future Method             | Queueable Apex           |
| ------------------------- | ------------------------ |
| Simple implementation     | More flexible            |
| Primitive parameters only | Supports complex objects |
| Cannot chain jobs         | Supports chaining        |
| Older approach            | Recommended approach     |

---

### Why Use Batch Apex?

Batch Apex is useful when:

* Processing thousands of records
* Large data cleanup
* Scheduled maintenance jobs
* Data migration activities

---

## Block 4 – Lightning Web Components (LWC)

### Parent to Child Communication

The parent component passes data to the child using a public property.

#### Child Component

javascript
import { LightningElement, api } from 'lwc';

export default class ChildComponent
extends LightningElement {

    @api recordId;
}


#### Usage in Parent

html
<c-child-component
record-id={recordId}>
</c-child-component>


---

### Child to Parent Communication

#### Child Component

javascript
handleClick(){

    const event =
        new CustomEvent('notify');

    this.dispatchEvent(event);
}


#### Parent Component

html
<c-child-component
onnotify={handleNotify}>
</c-child-component>


#### Parent JavaScript

javascript
handleNotify(){

    this.message =
        'Event Received';
}


---

## Interview Questions and Answers

### What is a Governor Limit?

A Salesforce restriction that ensures fair usage of shared resources.

### Why should SOQL not be used inside loops?

It can exceed the maximum query limit and cause runtime failures.

### What is Bulkification?

Writing code that efficiently processes multiple records at once.

### Difference Between Trigger.new and Trigger.newMap

*Trigger.new*

* Returns a list of records.

*Trigger.newMap*

* Returns a map of Id to record.

### What is a Future Method?

A method that executes asynchronously in the background.

### Difference Between Future and Queueable Apex

Queueable Apex is more flexible and supports job chaining, while Future methods are simpler and support only primitive parameters.

### What is the purpose of List?

Stores ordered collections.

### What is the purpose of Set?

Stores unique values.

### What is the purpose of Map?

Stores key-value pairs for fast lookups.

---

## Challenges Faced

* Understanding Map lookups
* Identifying SOQL inside loops
* Understanding Governor Limit errors
* Learning asynchronous execution concepts

---

## Skills Gained

* Apex Collections (List, Set, Map)
* Governor Limits
* Bulkification Techniques
* Trigger Optimization
* Asynchronous Apex
* Future Methods
* Queueable Apex Concepts
* Lightning Web Component Communication
* Salesforce Best Practices

---

## Outcome

Successfully completed Day 2 of the Salesforce Developer Bridge Program. Gained hands-on experience in writing efficient and scalable Apex code, understanding Salesforce Governor Limits, implementing Bulkification techniques, working with Asynchronous Apex, and enabling communication between Lightning Web Components
