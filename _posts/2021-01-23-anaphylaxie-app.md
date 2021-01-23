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

As part of a yearly competition between the students of the media computer science course, me and a team of six students were comissioned to create an application that should help adults and parents give fast and reliable help for children who suffer from anaphylaxia. This project was commised by the occupational medicine center of the Charite, Berlin and was supervised by one of the staff members that works with children who suffer from anaphlaxia.

In situtations of imminent or already ongoing anaphylactic shocks, many parents and other people may act unpredictable, even if they were already instructed and trained on certain situations. And in the case that new symptoms arise that have not been seen before, people usually won't act at all, as they are afraid of doing something wrong that will harm the child in the process. This is a typical situation in any situation were first aid has to be given. This application should give the user the correct instructions for the right situation and should guide them through all steps and give them a sense of safety and certainty in every action they take.

Our task was to create a prototype for such an application taking into account the technical know-how of the potential users, the technology available to them, their experiences and many other factors. We have decided to create a native android application with an low api-level that provides compatibility to almost any android device and that will work smoothly under any circumstance.

Link to the GitHub repository: [omshill0305/Anaphylaxie-App (github.com)](https://github.com/omshill0305/Anaphylaxie-App)

##### My tasks

One of my tasks was to create a database solution for our native android application. Our application should record data on application use such as input speed or the selected symptoms, that will be used for research. It should send the data to the servers of the facility whenever possible.

After some research we have decided to use the Room Persistance Library, which is a library that helps store data locally on the device. This library uses MySQL as a backbone, while the actual database implementation can be achieved through basic Java scripting. In essence, every data object is treated as a Java/Kotlin class that can have references to other data objects in the database and the possibility to save query searches as functions. This way it is very easy to map queries to action calls in the application.

We have created a first-draft database concept that defines all data objects and their releationship between them and recreated our concept as a Room database. After initializing the database and creating some dummy data, we were finally able to save and load data.

The biggest problem we had encountered was the fact that the database operations and the main application were running on the same thread. Running the database operations in a "blocking" pattern ensure the success of each consecutive operation but resulted in a huge lags in the application. When running it "non-blocking", we run into the problem that we could not ensure that operations could run in the defined order, so for example methods in order 1, 2 ,3 could run in order 3,1,2 , which is a pretty common problem in multi-thread operations.

We have used the RxJava library that introduced a observer-pattern like behaviour and parallel operation. This way we could combat our issue from before and ensured the correct order of operation, which previously resulted in unexpected behaviour. It is also possible to track if a operations has failed and implement alternatives or any other behaviours, which is really useful for error messages or for operations that rely on each other. The biggest downside to it was the complexity that it brought with it.

We were luckily able to finish the profile section of our application and could successfully save and load profile information and also made changes to our data without a hitch or any sign of slowdown.
