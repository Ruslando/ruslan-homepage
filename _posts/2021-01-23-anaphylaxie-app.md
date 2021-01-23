---
title: 'Project: "Anaphylaxie App"'
subtitle: Android application that supports parents with children with anaphylaxis
content_img_alt: lorem-ipsum
thumb_img_alt: lorem-ipsum
excerpt: lorem-ipsum
date: '2021-01-23'
layout: post
---
##### Introduction

As part of a yearly competition between the students of the media computer science course at our university, me and a team of six students were comissioned to create an application that should help adults and parents give fast and reliable help for children, who suffer from anaphylaxis. This project was commised by the occupational medicine center of the Charite, Berlin and was supervised by one of the staff members that works with such children.

In situtations of imminent or already ongoing anaphylactic shocks, many parents and other adults may act unpredictable under the influence of stress and fear, despite training and instruction. In the case that new symptoms arise that have not been seen before, parents usually wont act under the influence of fear that they will something wrong, which can harm the child. This is a typical situation that can be observed in any situation where first aid has to be given. This application should give the user the correct instructions for the right situation and should guide them through all steps and give them a sense of safety and certainty in every action they take.

Our task was to create a prototype for such an application taking into account the technical know-how of the potential users, the technology available to them, their experiences and many other factors. We have decided to create a native android application with an low api-level that provides compatibility to almost any android device and that will work smoothly under any circumstance.

Link to the GitHub repository: [omshill0305/Anaphylaxie-App (github.com)](https://github.com/omshill0305/Anaphylaxie-App)

##### My tasks

One of my tasks was to create a database solution for our native android application. Our application should record data on application use such as input speed or the selected symptoms, that will be used for research.

After some research we have decided to use the Room Persistance Library, which is a library that helps store data locally on the device. This library uses MySQL as a backbone, while the actual implementation can be achieved through basic Java scripting. In essence, every data object is treated as a Java/Kotlin class that can have references to other data objects in the database and has the possibility to save query searches as functions. This way it is very easy to map queries to action calls in the application, so that the entire team can easily use and understand each database call.

We have created a first-draft database concept that defines all data objects and their releationship between them and recreated our concept as a Room database. After initializing the database and creating some test data, we were finally able to save and load data.

The biggest problem we had encountered was the fact that the database operations and the main application were running on the same thread. Running the database operations in a "blocking" pattern ensures the success of each consecutive operation but resulted in huge lags when running actions linked to database operations. When running it "non-blocking", we run into the problem that we could not ensure the running order of the operations, so for example methods in order 1, 2 ,3 could run in order 3,1,2 , which is a pretty common problem in multi-thread operations. As a example, let's image a method to save some data (1) and a method to delete this exact data (2). After (1) has been called, the method starts the operation on the database, but at this time method (2) has already called. As method (2) cannot find the data for deletion, it throws an error and a bit later, method (1) has finally completed its database operation. The result: Data has been written but not deleted and the application crashes.

We have used the RxJava library that introduces a observer-pattern like behaviour and parallel operation. This way we could combat our issue from before and ensured the correct order of operation, which previously resulted in unexpected behaviour. It is also possible to track if a operations has succeeded or failed and implement alternatives or any other behaviour, which is really useful for error messages or for operations that rely on each other. The biggest downside to it was the complexity that it brought with it.

##### End result

At the day of presentation, we have used an Samsung Galaxy S5 phone on the latest supported android version. The prototype was running and was fairly stable.

We were luckily able to finish the profile section of our application and could successfully save and load profile information and were also able to make changes to our data without any hitch or sign of slowdown, but were not able to implement it on our whole application.

Despite being the only group that had almost zero technical consultation, which forced our group to develop and research everything on our own, our application has won 1st place out of 6 groups in the bachelors category. We believe that this was one of the reason why we might have won the competition, as the other projects were definetly not worse than ours, but were either supported by professors or were commissioned and supervised by companies.
