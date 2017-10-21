---
layout: post
title: "9cv9 Vietnam Transport Hackathon"
date: 2017-04-15
excerpt: "Organized by 9cv9 - How to solve Traffic Congestion problem"
tags: [hackathon]
comments: false
---

## The Beginning

It all started when my lecturer shared the 9cv9 Hackathon information. I sent it to one of my friends from another university and he signed his team up, I asked to join and they agreed. 

So our team has the line-up:
* Khiem Le - Team Leader and my friend at highschool, he is an Android developer with great coding mindset
* Huu Che - Another friend I knew from highschool, he recently focuses on Python and back-end coding
* Tu Ninh - An Android developer friend which I met a couple times when I hanged out with Khiem
* Loc Mai (me) - At least I know some Python and used to write some Android applications

{% capture images %}
http://i.imgur.com/k12izw9.jpg
{% endcapture %}
{% include gallery images=images caption="Infection Team - From right to left: Khiem,Huu,Tu,Loc" cols=1 %}

We all know that I'm gonna be the burden of the team since I wasn't coding recently to focus on performance testing and some "To-be-Boss" subjects in my university so my programming skill is no where near them. But instead of afraid of the disadvantages, they figure the way out to utilize all the resources we have and I also try my best in any tasks I can contribute. 

We started brainstorming one day before the competition, Huu came up with a lot of great ideas while Khiem and Tu prepared layouts and libraries for the app, I was preparing the slide templates so we don't spend much time for that in the hackathon. Everything is packed up. I went to sleep early since the next day morning I had an exam before going to the Hackathon.

{% capture images %}
http://imgur.com/vvwBN21.jpg
{% endcapture %}
{% include gallery images=images caption="Time to flick some dust off my keyboard, mouse and laptop. Kindle is for some relax moment if needed (later on I realized I didn't charge the battery...)" cols=1 %}

---
## Day 1

On the first day, troubles came to us. We picked the Smart Vehicles topic although not having prepared any idea for that so we have to start from the scratch. We also had trouble with the wifi and didn't do much in about two or three hours due to some mistakes of the organizer (surprisingly none of us or any other teams complain about this). We kept setting our mind on the Android platform, brainstorming some features and narrow them down so we can have enough time to develop all core features that are the most valued and start using our own 3G network to research for some written libraries that we can use.

After a few hours of discussing in team and with the mentors (shout out to Martial Ganiere and Nguyen Thanh Trung), our final plan is to build an application that will keep sending the coordinator of their location by GPS to our server (we build locally on Huu laptop for demonstration purpose), the server will process the data and check if the paths are jammed or not based on the traffic density and velocity of the vehicles. The server will detect the congestion and provide better alternative paths for the users to avoid that congestion point.

{% capture images %}
http://imgur.com/6hbU173.jpg
{% endcapture %}
{% include gallery images=images caption="On the first day" cols=1 %}

Next we tested some methods of Google Map API and figured out the data in JSON files got from another map API we found for the coordinator to display on the map, during the competition, Huu mostly spent time in understanding the JSON and figure out how to extract the data in an efficient way. Tu was helping and preparing the UI. Khiem walked around to network and talk to the mentors (some even came to us and gave us many great suggestions on how to build our system and tips for the hackathon). I was joining the seminars organized by 9cv9, they have plenty of good speakers sharing their Start-up business, unlucky the topics didn't have much value for me and my team. After we came back from lunch, we summarized our plan, idea and orientation. Still no wifi and the noise from the surrounded environment of the location was distracting us so much (which is the reason why on the next day, the organizer have to move the hackathon to the new location). Before we left we had a great seminar from Kyanon Company which the speech was so confident and inspiring. 

We moved back to Tu's house after 5pm. Took a nap and went for dinner. 7pm Huu started coding the server, Tu was doing his homework(did I mention they all have deadlines on those days we participated in the hackathon?), Khiem had to take care of his Joomla work he built for someone. I had to redesign the slides (we decided to choose the red theme just like Kyanon) and tested out some animation for the slides. We also found a short interview clip from HTV7 Channel which Tu was in it! :D
We slept at 3 am on the next day.

---
## Day 2

We moved to Dreamplex 2 building on the 2nd day and it was a great decision made by the organizer. Wifi problem fixed, free coffee, free tea and the workspace is so damn cool. We kept coding, completing the app and the server. Huu had a trouble with the server configuration (later on we found out we weren't on the same network so there was literally no connection between the server and our application). Khiem was writing the function for the app and Tu was handling visual stuffs.

{% capture images %}
http://i.imgur.com/09Bw6oZ.jpg
{% endcapture %}
{% include gallery images=images caption="Staying late" cols=1 %}

At 7pm, we left the Dreamplex building and moved to the Robica Coffee on Ngo Thoi Nhiem street, it's a great coffee shop for staying overnight (we slept on the sofa and even left our laptops turning on that whole night and was waken up by the coffer shop owner on the next day) We coded from 10pm to next day 1am.

We have a short footage video from 9cv9 on day 2
<iframe width="560" height="315" src="https://www.youtube.com/embed/MKWB9TM6TRw" frameborder="0"> </iframe>

In summary, we built an android application to track the GPS and sending the coordinators to the server running on Huu's laptop, the server will based on the two factors: traffic denstiy and velocity to check if there is a congestion point or not.Then we use the dijkstra algorithm to find the best alternative paths and send back the response to the user through Flask application under JSON format and push the notification on Android phone and the Smart band(we tested on the Mi band)

So we were able to detect the congestion, raise alert to the users and find for them other paths to avoid the traffic jams by devices that can integrate into Smart Vehicle and those are the key points of our ideas. Time to finish the slides, record the demo and start practicing the speech for the last day.

---
## Grand Final Day

Khiem and Tu went to the location first, when I came, it seemed like they were in trouble. They couldn't connect to Huu's server and the deadline was shorten by the organizer.Lucky for us, Huu was there in time and we did the record in 5 minutes. We did a rehearsal with the slide and had a trouble with the projector (the plug was loose) so we have to test on many laptops and finally borrowed other team's laptop (which somehow that team is in the same university of my friend and we are both in the top 3 team). We felt like we did great at a time and the other teams not doing that well, our app works fine, the idea is good enough and the slide is professional.

My team let me to present in the final. Again the trouble with the projector, I thought we were lost because of the issue but we fixed it and the presentation went on perfectly. They even laughed when I made a joke :D I didn't remember how well my performance was but at least I kept calm and finished the speech.
We did the presentation and answered questions in English,somehow it was an advantage for us not just in the competition but the recruiters later on contacted us because we can speak English so fluently and they really want to keep in touch with us.(We are the first team they contacted after every team finished the presentation).

After 15 minutes break, we got the final result. We are in the top 3 and run for the Hackathon First place title with the team that lend us their laptop!

{% capture images %}
http://imgur.com/SWoikVm.jpg
{% endcapture %}
{% include gallery images=images caption="Top 2 teams" cols=1 %}

For the final pitch,we didn't do as well as the other team (they are just sophomore but already had a great idea and product for this hackathon!) and eventually we finished in Second place with a small prize award,flower and certifications.

{% capture images %}
http://imgur.com/MmnD4DD.jpg
{% endcapture %}
{% include gallery images=images caption="Top 2 teams" cols=1 %}

---
## In The End

Well I did learn a lot. We achieved our goal to came here and challenge ourselves to build up a solution that solve specific problem in a short time.
And we have been contacted by many recruiters, Thanh Nien newspaper.Tu was on TV. We impressed our mentors and open up our network in the community of technology, made new friends and learned from them. So all of this was great experience for us.


{% capture images %}
http://i.imgur.com/mkrPkCX.jpg{% endcapture %}
{% include gallery images=images cols=1 %}
{% capture images %}
http://i.imgur.com/Nbxb5hu.jpg
http://i.imgur.com/5XfVWRS.jpg{% endcapture %}
{% include gallery images=images caption="We did it guys" cols=2 %}
