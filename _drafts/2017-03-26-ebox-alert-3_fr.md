---
published: false
title: Déployer une application Java disponible 24h/24 dans le cloud pour 0$
---

Cet article fait suite à [Passer EBOX Alert à l'échelle en contournant les restrictions]({% post_url 2017-01-22-ebox-alert-2 %}). Il est surprenant de pouvoir rouler une application Java-Spring Boot + tomcat (gourmande en mémoire), de la rendre disponible 24h/24, et de supporter le protocole https, le tout pour 0$/mois (hors coût du domaine si vous voulez votre propre nom de domaine). Pourtant c'est possible, voici comment je procède pour ebox-alert.ca.

Voici un aperçu de l'architecture du service:
![Architecture EBOX]({{site.baseurl}}/images/EBOX-Architecture.png)

### Free SMS notifications

First of all, the SMS. This typically costs a cent or two if you really want to send an actual SMS to any Canadian phone number. There are ways to send free MMS that are mobile carrier specific, but for SMS, carriers will charge a (small) fee.

Given the small number of SMS that I need to send, I don't want to handle the complexity of using or integrating with an open-source SMS gateway. AND I've found [ClickSend](https://www.clicksend.com). New accounts get 1$ free credit, which is not a lot but enough to send a bit less than 100 SMS.

I used to send SMS notifications for every alert threshold (75%, 90%, 100% and the +10GB threshold - 10GB over the plan), but then I figured the only thresholds that deserve an immediate notification are the 100% threshold (after which you start getting charges for over-usage) and the +10GB threshold (after which you should really buy usage blocks). And very few of my users reach 100% usage. So, by choosing which alerts deserve an immediate alert, I reduced the number of SMS sent by month to less than 10. And the free credit can last a few months.

What should I do when I don't have credit left? Just close the account, register a new one, and change the access key through Heroku Dashboard. A few minute configuration once or twice a year at most.

\[edit\]: Another alternative would be [Amazon SNS](https://aws.amazon.com/en/sns/sms-pricing) with *no required payment upfront* -- pay as you go --, and less than 0,004$/sms or even less for most operators (less than 0,001$ for Rogers).

### Free application hosting

I host my application at [Heroku](https://heroku.com), because it is a Java application and Heroku allows me to focus on the app and not on hosting (I deliver the webapp as a war and they basically take care of the rest, in the [Platform as a Service](https://en.wikipedia.org/wiki/Platform_as_a_service) fashion). They have a [free plan and a paid hobby plan](https://www.heroku.com/pricing). But there are not a lot of difference between the 2:

- in the free tier, the application will sleep after 30min without web traffic (and boot if traffic comes)
- free dyno are given 550h of run time but you can [bump it up to 1000h if you register a valid credit card](https://devcenter.heroku.com/articles/free-dyno-hours#consuming-hours).

My app is a Java/Spring Boot webapp so it takes a noticeable amount of time to boot (sometimes more than 1min). So I cannot afford it to go sleeping or it will look as if the site is down when users come.
To prevent it to fall asleep, I just need to ping it every 29min. 1000h of free tier is more than I need for a full time running app (I need 744h to be precise).

To ping it at regular interval, I use [Uptime Robot](http://uptimerobot.com/) which is free to monitor my website every 5 min. The previous service I used [Monitor.us](http://www.monitor.us/) had limitations on the frequency and was pushing me to hard towards a paid plan. Now, thanks to the monitoring, my application never sleeps. And I get a nice email if there is anything wrong, plus statistics for the response time of my homepage as a bonus.

### Free monitoring solutions

There are three aspects of [ebox-alert] that deserve a proper monitoring solution (I'll discuss the monitoring more in depth in a future post):

- _"is the site up?"_: this is covered by [Uptime Robot](http://uptimerobot.com/) free plan as I mentioned earlier
- _"are there any alerts/warnings in the logs (including memory over usage and other Heroku events)?"_: I use [logentries](https://logentries.com/), which is an Heroku addon with a free plan that is enough to get alerts by email when important events occur
- _"is my background refresh&alert process running as expected?"_: this is actually the most critical part, for which [DeadManSnitch](https://deadmanssnitch.com) is the perfect fit. Whether my app crashes without logging anything, or the background process dies without notice, if DeadManSnitch does not see my app check in for an hour straigth, I'll get an alert by email from them. The free plan allows for a single "snitch" so I had to implement it in a way that ensures [ebox-alert] is 100% reliable.

### Free mailing solution

That one is easy, the volume of emails sent by [ebox-alert] is low enough to remain in the free plan of [SendGrid](https://app.sendgrid.com/), also an Heroku addon.

In next article (in French), I will be talking more in depth about the [monitoring and reliability of EBOX Alert]({% post_url 2017-01-24-ebox-alert-monitoring %}).

[ebox-alert]: http://www.ebox-alert.ca "ebox-alert.ca"
