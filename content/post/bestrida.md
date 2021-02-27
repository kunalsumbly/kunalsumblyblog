+++
author = "Justin Zimmerman"
date = "2016-09-04T09:45:50-04:00"
description = "Bestrida React Native iOS Application"
keywords = ["Bestrida", "React Native", "React", "Native", "Strava", "Developer", "Challenge"]
tags = ["Bestrida", "React Native", "Strava"]
title = "Bestrida"
topics = ["Bestrida", "React Native"]
type = "post"

+++

I recently published [Bestrida](https://appsto.re/us/lBRCeb.i) to the iOS app store for my submission to the 2016 Strava Developer Challenge. Here is a brief overview of the application. Strava.com is a popular and widely used website and mobile app that over one million cyclists and runners use to track their activity via GPS. Whenever you go for a run or ride your bike, Strava will track and store your activity and provide you with useful statistics. As awesome as it is, a major thing Strava does not offer is a way to challenge your friends.

### Bestrida

Bestrida, swedish translation "to challenge", is a Strava.com segment based application that allows you to challenge your friends to running and cycling segments. With the chaotic schedules many of us have, it’s hard to carve out time to actually meet up with a friend and go for a run or ride. Your friends no longer have an excuse to keep dodging your challenges just because you're an Ironman and they’re a weekend warrior. You can challenge your friends using the app, anytime, anywhere.

### Challenge Feed

After logging in, the user is presented with the Challenge Feed. The Challenge Feed aggregates all of the challenges that the user has received from other users and challenges that the user has sent out to their friends. The user can click on a particular challenge and preview the segment for that challenge. Here we can see the relevant metrics for this segment. The user can also have the option to cancel the challenge. Users can accept or decline challenges from the feed as well.  

### Create Challenge

At the top of the screen, the user can click on the “Create Challenge” button to create a new challenge. To create a challenge, the user will first select a challenger. They have the option to either select from a list of their 3 most frequently challenged friends or search from the list of their Strava friends to challenge. The user will then select a segment. Similar to selecting a challenger, the user will have the option to either select from a list of their 3 most frequently completed segments or search for starred or recently completed segments. The last step is to select a completion date which acts like an expiration date by which both users must complete that particular challenge. Once the challenge has been created and accepted by the other user, it will be displayed on the “Active Challenges” tab.

### Active Challenges

In the “Active Challenges” tab, the user can view a list of all active challenges, which are challenges that have been accepted
by both parties. The Active Challenge feed shows the opponent, the segment, and the completion date. You can click on the
active challenge to view more detailed information about that particular challenge.

Once the user completes an activity on Strava that covers the segment, the user can click in to the Active Challenge Detail view to complete the challenge.

### Completed Challenges

Once the challenge is completed, the user can view the Completed Challenge feed to see whether they have won, lost, or are waiting for their opponent to complete the challenge. When the challenge is completed by both parties, you can see whether you won or lost, the segment name, the distance and specific details about the user and their opponent including completion time, heart rate, cadence, and wattage during the segment.

This application was built with React Native, and Node, with a Mongo database to store users, segments, and challenges.

Thanks for reading. Download [Bestrida](https://appsto.re/us/lBRCeb.i) today to start challenging your friends and improving your workouts and segment times!
