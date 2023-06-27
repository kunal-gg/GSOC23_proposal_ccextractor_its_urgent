# GSOC23_proposal_ccextractor_its_urgent
#### It's Urgent - Flutter app

---

### Project Overview 
When the phone is in do not disturb mode it doesn't receive any messages/calls. No matter how serious the situation could be, the phone restricts all possible sources of contact. This can prove to have serious consequences in case of emergencies. “It’s Urgent” proposes a solution where a user can try to notify someone, even if they are in do not disturb  mode.

### Proposed Solution

This is the complete breakdown of the solution:
- First the user registers on the app, if he has installed it for the first time. Once registered the user remains logged in (just like any other messaging app like whatsapp or telegram)
- We display the user a list of all the contacts on his phone who have the app installed in alphabetical order. 
- The user clicks on the person he wants to send an urgent notification.
- The user is made to write a custom message to send to the user.
- If the receiver of the notification is not on do not disturb mode we send a usual notification otherwise the user is prompted a random 5 word phrase which he needs to type out and send the notification
- The receiver finally gets a notification and has the option to tap on the notification and make a call.

User Flow for the Sender: 

![image](https://user-images.githubusercontent.com/105335204/225699233-061105e9-6b5e-4ee9-8311-c4dd74322994.png)

User Flow for the receiver: 

![image](https://user-images.githubusercontent.com/105335204/225700408-e021a435-cc4d-40bd-a41c-fb2c948a1e37.png)

---

### Propossed Features
#### Compulsory Features 

- Be able to register on the app using your phone number.
- Send an urgent notification to a user with custom message.
- Be able to block a certain user in case of spam.
- Handle notifications when the app is  in foreground as well as background.
- Once the user is blocked the person will be banned from sending notifications
- Give the user a call back option on tapping the notification

##### Additional Features
- Be able to share the app to other contacts who haven't downloaded the app
- Be able to store the history of the user (the people he has send notifications to along with the message)
- Be able to search a any user who has registered on the app using his/her phone number.
- Implement Light and dark theme

-----

### Implementation Plan
- Overwriting the DND policy and sending notifications:
As stated by in this [Blog](https://sathish76.medium.com/control-dnd-settings-in-flutter-e53481cb6ec5), we can use the [flutter_dnd](https://pub.dev/packages/flutter_dnd) package to overwrite the properties of the do not disturb mode. Along with this we can use firebase or even OneSignal (which is built on top of firebase) to send notifications. 
The basic plan would be as follows:
- The moment we download the app, we would check if the user has granted the required permissions or not(reading and writing contacts, sending notifications etc..). If not we would request for those permissions and if yes we would continue. 

![image](https://user-images.githubusercontent.com/105335204/225698991-618719fb-4513-4fb5-81ba-47171059dbf6.png)

- After this a token would be generated which would be specific to the mobile phone. This token would be used while sending the notification to the specific user. We would store this token in the database. Hence the database would have every user stored in them having three fields: 
  - token 
  - Phone number (to identify the user uniquely)
  - blocked or not (a boolean value). By deafult it will be false

![image](https://user-images.githubusercontent.com/105335204/225696111-14c03cba-81a0-4189-a2a0-93d558dd5f31.png)

- When the user would click a contact and type the custom message, we would send the notification to the user.
- The flutter_dnd package would configure the settings accordingly and allow priority notifications

![image](https://user-images.githubusercontent.com/105335204/225698543-35e273e5-c54b-436e-80ef-9757e5cbbb3e.png)

- When the user receives a notification, he would tap on the notification which would give him two options. He could either call the person who has send a message or block the given user. 
- In case he chooses to block the user, we would add boolean field of the database corresponding to that user which would be checked while sending notifications the next time.

---- 

### Goals for the Project
- Design the UI for the app. 
- Make a database to store all the user information
- Implement the logic given above
- Add tests to the app, once a feature is completed
- Add automated CI/CD on GitHub


### Tentative Plan for the summer
- Milestone 1
  - Coding begins
  - Initialize the flutter and firebase projects
  - Finalize all the features with the mentors
  - Design the UI and finallize the designs with the mentors 

- Milestone 2 Firebase setup
  - Setup a firebase project 
  - Configure Flutter Firestore to store all the data
  - Configure OneSignal.
  - Make Splash screen
  - Config app level settings for both light and dark mode.

- MileStone 3
  - Code the UI for all the screens
  - Show the contacts on the home screen. Depending their contact exists in the database we would show it accordingly
  - Once we fetch the contacts, we would store them locally. We cam implement this using [shared_preferences](https://pub.dev/packages/shared_preferences). 

- Milestone 4
  - This week would go in implementing the auth. The auth could be implemented using this https://firebase.flutter.dev/docs/auth/phone/. 
  - We would also save data of the user on flutter firestore. 
  - We could also Google or easy login

- Milestone 5
  - This week will go in implementing urgent notifications. We would implement the most basic version of it, when the app is in foreground. 
  - We would use the flutter_dnd package for it.
  - Also I have kept this week a little free for any further research we would be required to do, on discussion with the mentors

- MileStone 6
  - In this week we would complete the notifications. 
  - Write tests for this feature

- Milestone 7
  - In these two weeks we would be implementing the feature of blocking the user in case of spam
  - We can handle interactions depending on this [Blog](https://firebase.flutter.dev/docs/messaging/notifications/#:~:text=the%20code%20examples.-,Handling%20Interaction,be%20brought%20to%20the%20foreground.)
  - Also Once a user we would have to send that user a notification that he is blocked. 
  - We would also have to implement feature of giving an option to the user a notification.

---

### Take Home Assignment 
This is a link of the Github Repo of the take home assignment given to us. I have made the flutter auto-zoom app. The app takes a picture and zooms into a bottle present in the picture.

[GitHub](https://github.com/kunal-gg/FlutterAutoZoom)
[Video]() 

--- 
 
 ### Minimum Viable Product)
 While researching about this project I tried to implement how we could implement a solution for this. As a result of which I am attatchig a video and the github repo of the solution which I built. At the moment I am sending to a notification to myself, however we would easily send it to another person as well. We would just need to query the phone-number and replace the token in the code. 
 
 [GitHub](https://github.com/kunal-gg/UrgentNotifications)
 [Video](https://drive.google.com/file/d/1jkZ-JxtusUiVqzsURz0OjIl81EUkKAM5/view)
 
 ---
  

### My Previous Contributions in CCExtractor 

I have gone through the repositories in ccextractor before. I have the following PRs merged.
1. https://github.com/CCExtractor/taskwarrior-flutter/pull/51
2. https://github.com/CCExtractor/taskwarrior-flutter/pull/54
3. https://github.com/CCExtractor/taskwarrior-flutter/pull/53
4. https://github.com/CCExtractor/taskwarrior-flutter/pull/56
5. https://github.com/CCExtractor/taskwarrior-flutter/pull/69

--- 

### Background 
I am second year undergraduate student at the Indian Institue of Technology Jodhpur. I am passionate about open source development and really like building real world applications which people can use. I started contributing to open source in my freshman year and have been doing it for a year now. Some of my projects which I have worked upon are:

- https://github.com/devlup-labs/prometeo-23-app
- https://github.com/kunal-gg/Automating-Payments-Snap 

The tech stack I am familiar with is: **Flutter**, **Node**, **Django**, **React**, **Firebase**, **Docker**, **OpenCV**, **graphQL**, **mongo DB**, **Postgres**. I am familiar with version control system and use VS code along with ubuntu as my primary coding environment. 


I am the core member of the open soure community of our college Devlup labs. As a part of this club we build software all round the year for the students of IITJ. Along with this I also participated in the Inter IIT Tech Meet organized by IIT Kanpur. We stood 9th in the problem statement given to us by Consensys. I have been very active in all the technical events that take place in college. I have participated in two hackathons: Hackoverflow and Youth Conclave Hackathon. The source code of one of our submissions which was shortlisted in the top 10 participating teams is given below: 
- https://github.com/kunal-gg/Prometeo-hackoverflow

Apart from this I have contributed in building the websites and apps of almost all the festivals that were organised in college. These websites become the face of the festival for everyone and also become the platform for the registration of all the participants that take part in the festival.


----

### Motivation
I am really passionate about open source. I built an app for my college festival using flutter, after which i have also worked on various other flutter projects. After working on these college projects I really want to work on something a little more challenging. This project idea is unique, something I have never heard before. Hence this project seems to be the most fun to work on

----

### Summer Plans
I don't have any prior commitments for this summer. I would be sitting at home for the most part of it. I would be able to commit 40-45 hours per week on this project, however if the project demands more I would definitley be willing to put in more hours. 
