---
layout: post
title: "Performance Testing"
date: 2017-03-26
excerpt: "What? Why? When? How? And More."
tags: [performance testing]
comments: true
---

# Performance Testing

## What is Performance Testing?

**Performance Testing** is a type of testing intended to determine the scalability, stability and responsiveness of a system under certain circumstances.

Performance Testing also divided into other types with different names. But mostly we will talk about **Load and Stress Testing**. For short:
* **Load Testing** is conducted to see if the behaviour of the system under a specific expected load can give an outcome as we expected or not so. Then we can ensure that the performance can satisfy our customer or we have to make corrective actions. 
* **Stress Testing** is conducted to understand the upper limits by giving the system an extreme load, we will have a conclusion on how will the system perform sufficiently if the current load goes above the expected maximum load.

Other names you might heard of are Volume, Scalability, Endurance, Spike, Fatigue Testing which follow the same idea above with specific conditions.

## Why do we have to do Performance Testing?

One word: Business Value.

For e-commercial, entertainment or any customer service websites: If users have to wait too long, they lose their interest, you lose your customers.

> Badly performing applications generally don’t deliver their intended benefit to an organization; they create a net cost of time and money, and a loss of kudos from the application users, and therefore can’t be considered reliable assets. If a software application is not delivering its intended service in a performant and highly available manner, regardless of causation, this reflects badly on the architects, designers, coders, and testers (hopefully there were some!) involved in its gestation. 
**Ian Molyneaux - The Art of Application Performance Testing 2015**

So the conclusion is that we want to keep out Business Value and certainly Performance is one of the most critical quality attribute that we have to pay attention.

## When do we have to do it?

Quick Answer: As early as possible.
Most of project do Performance Testing before the deployment. And it's almost too late at the time.

## How do we do it?

Seven steps (activities) of Performance Testing:
1. Understand Project Context
2. Identify Test Environment
3. Determine Performance Testing Acceptance Criteria
4. Planning & Design
5. Implementation
6. Execution
7. Analysis & Assessment

These are major steps that you need to go through each Performance Testing Process. I recommend read the book "The Art of Application Performance Testing" (For them, there are 6 steps and the objectives are the same) to have more understand on what we want to achieve in these steps/ activities.

Then you can use the Performance Testing Guidance for Web Applications by Microsoft as a guideline for your situation.

### Little more about measuring

So how do we go about measuring performance? In order to accurately measure performance, first we must take into account certain key performance indicators (KPIs). We can divide them into two types: service-oriented and efficiency-oriented. Service-oriented indicators are availability and response time; they measure how well (or not) an application is providing a service to the end users. Efficiency-oriented indicators are throughput and capacity; they measure how well (or not) an application makes use of the hosting infrastructure. We can further define these terms briefly as follows: 
* **Availability:** The amount of time an application is available to the end user. Lack of availability is significant because many applications will have a substantial business cost for even a small outage. In performance terms, this would mean the complete inability of an end user to make effective use of the application either because the application is simply not responding or response time has degraded to an unacceptable degree. 
* **Response time:** The amount of time it takes for the application to respond to a user request. In performance testing terms you normally measure system response time, which is the time between the end user requesting a response from the application and a complete reply arriving at the user’s workstation. In the current frame of reference a response can be synchronous (blocking) or increasingly asynchronous, where it does not necessarily require end users to wait for a reply before they can resume interaction with the application. More on this in later chapters. 
* **Throughput:** The rate at which application-oriented events occur. A good example would be the number of hits on a web page within a given period of time. 
* **Utilization:** The percentage of the theoretical capacity of a resource that is being used. 
Examples include how much network bandwidth is being consumed by application traffic or the amount of memory used on a web server farm when 1,000 visitors are active. Taken together, these KPIs can provide us with an accurate idea of an application’s performance and its impact on the hosting infrastructure.

As far as we concern, there are some metrics we need to understand when do Performance Testing and those metrics are related to the above terms.

## Summary

To summarize, in this post I have tried to define Performance Testing for you in my capability and some critical points around the process. You may found other explainations that are clearer and easier to understand.

You may refer to the following sources:
* The Art of Application Performance Testing - Ian Molyneaux
* Performance Testing Guidance for Web Applications - Microsoft
* Guru99.com

---

## Next time

Although I'm planned to cover the following topics in this post but it's kinda long post now and my laziness told me to save these for another post:
* The Tools - General Info.
* The Metrics - Meaning of them. 
* The Challenges

