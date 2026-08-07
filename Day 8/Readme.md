# Sprint 8 – Asynchronous Apex (Future, Queueable, Batch & Scheduled Apex)

## Overview

Sprint 8 introduces **Asynchronous Apex**, which allows Salesforce to perform certain tasks in the background instead of making users wait for every operation to complete.

The main objective is to understand **when work should happen immediately (synchronous)** and **when it can happen later (asynchronous)** to improve system performance and user experience.

---

## Learning Objectives

By completing this sprint, you will be able to:

* Understand synchronous and asynchronous processing.
* Identify tasks that should run in the background.
* Use Future Methods for simple asynchronous operations.
* Use Queueable Apex for structured background processing.
* Use Batch Apex for processing large datasets.
* Use Scheduled Apex for time-based automation.
* Choose the correct asynchronous mechanism for different business scenarios.
* Understand Governor Limits in asynchronous processing.
* Explain asynchronous Apex concepts in interviews.

---

## Key Concepts

### 1. Synchronous Processing

Work is completed before the user receives a response.

**Example:**

* Validate student eligibility.
* Save an application.
* Display success or error messages.

### 2. Asynchronous Processing

Work is performed in the background after the user receives a response.

**Example:**

* Sending emails.
* External system integrations.
* Analytics generation.
* Audit logging.

---

## Asynchronous Apex Types

### Future Method

Used for simple background tasks.

```apex
@future
public static void processAsync(Id recordId) {
    // Background logic
}
```

**Use Cases**

* Sending data to external systems.
* Lightweight background processing.

---

### Queueable Apex

Provides a structured job-based approach for asynchronous work.

```apex
public class OfferProcessingJob implements Queueable {
    public void execute(QueueableContext context) {
        // Background processing
    }
}
```

Execute:

```apex
System.enqueueJob(new OfferProcessingJob());
```

**Use Cases**

* Complex background operations.
* Chained asynchronous jobs.
* Better maintainability than Future Methods.

---

### Batch Apex

Used when processing very large datasets.

```apex
public class ApplicationBatch
implements Database.Batchable<SObject> {

    public Database.QueryLocator start(
        Database.BatchableContext bc) {

        return Database.getQueryLocator(
            'SELECT Id FROM Application__c'
        );
    }

    public void execute(
        Database.BatchableContext bc,
        List<Application__c> scope) {

        // Process records
    }

    public void finish(
        Database.BatchableContext bc) {

        // Completion logic
    }
}
```

**Use Cases**

* Processing thousands of records.
* Data cleanup.
* Historical data updates.
* Analytics calculations.

---

### Scheduled Apex

Runs Apex at a specified time.

```apex
public class JobScheduler
implements Schedulable {

    public void execute(
        SchedulableContext sc) {

        // Scheduled work
    }
}
```

**Use Cases**

* Daily reports.
* Expired job processing.
* Nightly maintenance tasks.

---

## Future vs Queueable

| Feature                         | Future         | Queueable |
| ------------------------------- | -------------- | --------- |
| Simple Async Work               | Yes            | Yes       |
| Structured Class                | No             | Yes       |
| Better Maintainability          | No             | Yes       |
| Job Chaining                    | Limited        | Yes       |
| Recommended for New Development | Less Preferred | Preferred |

---

## Batch Apex Lifecycle

### Start()

Identifies records to process.

### Execute()

Processes records in smaller batches.

### Finish()

Runs after all batches are completed.

---

## Scheduled + Batch Architecture

```text
Scheduled Apex
       ↓
Starts Batch Apex
       ↓
Processes Large Dataset
       ↓
Finish Processing
```

Example:

* Every Sunday night, process placement analytics for all applications.

---

## Best Practices

* Keep essential user actions synchronous.
* Move secondary tasks to asynchronous processing.
* Use Queueable Apex for new background jobs.
* Use Batch Apex for large datasets.
* Use Scheduled Apex for time-based automation.
* Continue following bulkification principles.
* Avoid SOQL and DML inside loops.
* Implement proper error handling and monitoring.

---

## Interview Questions

### What is Asynchronous Apex?

Asynchronous Apex allows Salesforce to execute tasks in the background without making users wait for completion.

### When should Queueable Apex be used?

When background work requires a structured, maintainable, and potentially chained job design.

### When should Batch Apex be used?

When processing very large numbers of records that cannot be handled efficiently in a single transaction.

### What are the three methods of Batch Apex?

* Start()
* Execute()
* Finish()

### What is Scheduled Apex?

Scheduled Apex runs business logic automatically at a specified date and time.

---

## Conclusion

Sprint 8 focuses on designing scalable Salesforce applications by deciding **when work should be executed**. Developers learn to separate immediate user actions from background processing using Future Methods, Queueable Apex, Batch Apex, and Scheduled Apex to build efficient enterprise solutions.
