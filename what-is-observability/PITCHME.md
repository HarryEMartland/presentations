## What is Observability?

---

@quote[In control theory, observability is a measure of how well internal states of a system can be inferred from knowledge of its external outputs.](wikipedia.org/wiki/Observability)

Note:
- Internal state
- Measurement not functionality
- External exposing metrics

---

@quote[Capable of being or liable to be observed; noticeable; visible; discernible:](dictionary.com/browse/observability)

Note:
- Capability this is more about functionality
- Something that may be watched (liable) you might not need it at the time
---

@quote[Worthy or important enough to be celebrated, followed, or observed:](dictionary.com/browse/observability)

Note:
- Do we want our apps to be observable?
- Followed (constantly being monitored?) 

---

@quote[Deserving of attention; noteworthy.](dictionary.com/browse/observability)

Note:
- This is saying that it is important if it is observable
---

@quote[Observability is the extent to which the walls of a system have been made transparent](David Duke)

Note:
- Looking inside a system
- Extent is a measure not a feature
---

@quote[The tools that we use to tell us what is going on within our microservices and between our microservices so that we can operate them effectively.](Colin Break (QCon 19))

Note:
- https://www.infoq.com/presentations/challenges-operationalizing-microservices?itm_source=infoq&itm_medium=QCon_EarlyAccessVideos&itm_campaign=QConLondon2019
- 14:50
- More about tools
- Inside and between
- This talk was about microservices but I think it apples to anything
- Reason why we want observability so we can improve applications
---

@quote[Monitoring tells you whether a system is working, observability lets you ask why it isn't working.](vividcortex.com/blog/monitoring-isnt-observability)

Note:
- more indepth than just monitoring
- hints on a tool so you can ask questions (was from vividcortex)
- reason why we want observability figure out why its not working

---

@quote[“Observability”, according to {a twitter blog post}, is a superset of “monitoring”, providing certain benefits and insights that “monitoring” tools come a cropper at.](medium.com/@copyconstruct/monitoring-and-observability-8417d1952e1c)

Note: 
- Not just monitoring
- Mentions tools again
- Better than monitoring
---

@quote[It can be tempting to combine monitoring with other aspects of inspecting systems, debugging, tracking exceptions or crashes, load testing, log collection, or traffic inspection. While most of these subjects share commonalities with basic monitoring, blending together too many results in overly complex and fragile systems.](Google SRE Book)

Note:
- This is more about monitoring than observability
- Mentions we can have too much information
- Worry about breaking monitoring if there is too much
- If these are not monitoring I don't think they are part of observability too
---

@quote[Let me start with what i think observability is not: Observability is not a dashboard, it's not an alert that tells you your CPU has increased. Observability isn't a single activity you do before or after a release, and it's not a tool that you use to debug a particular fault. Observability is a feature of your system, its a culture you adopt. ](Emma Preston)

Note:
- More about the culture
- Feature of a system
- More thinks which are buzz words/tools which people say make your app observable
---

#### Sum Up

- Not just monitoring
- Culture
- Measurement
- Not tools
- See inner workings
- Used to find issues