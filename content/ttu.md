#Texas Tech Bootcamp

This last weekend, John Fonner and I taught a bootcamp for scientists in [Texas Tech's](http://www.ttu.edu/) [Atmospheric Science](http://www.atmo.ttu.edu/index.php) group.

##What worked:

+ Lots of skilled helpers: [Eric Bruning's](http://www.atmo.ttu.edu/bruning/) crew, Vanna Sullivan, Tony Reinhart and Aaron Hill all know their stuff, which meant learners weren't waiting long for help.

+ Online resources: We put up most of our material [online](https://github.com/wrightaprilm/TTU). We had a lot of intermediate and advanced students, but also some novices. This is a tricky balance: we don't want students to be bored, but we don't want to lose the novice tail. At various points, when looking at people's screens, I could see more advanced learners working on testing out supplementary materials.

+ Hands-on time: Particularly during the second day, we gave a lot of time to work through challenges and exercises. This meant we covered less material (we have one notebook that we didn't even get to), but the caliber of question asked by the students indicates that this time was worth it for advancing their understanding.

+ Minute papers: Before leaving for lunch, and before leaving for the day, we did minute papers. On their green stickies, we had students write one thing that worked; on red, one that didn't. These were very helpful. For example, after lunch on the first day, we spent a couple minutes clarifying the dictionary  .keys() method and having a useful discussion about object methods and how to find out which objects have what methods.

+ The learners: We had some issues related to pitching the material with multiple levels of learners present. But I think they all had really great attitudes about that, and were aware of those challenges and sought actively to make their own experience worthwhile.
	+ Novice learners weren't shy about asking questions. The rate of questions was a positive sign that teaching (e.g.) very basic shell was a good idea.
	+ For many experienced learners version control, unit testing, and classes were still genuinely new ideas. 


##What didn't:

+ Multiple levels in one room: I [April] wasn't forceful enough on this, and it came back to bite me. For an intermediate audience, not as much of the 'how-to' is needed on the nuts-and-bolts of programming with Python. For people who know C or Fortran, they can mostly pick up syntax and basics immediately. What they need is the layer on top: testing, sharing, collaborating and code reuse. They don't need the particular beast (Python), but they need to control its environment. 

A way to handle this might be to have a Python I and II session. Python I makes sure we're all on the same page. Python II is mostly practice for novices. During Python II, there could be a breakout covering importing functions as modules, classes, etc. There's a bit of self-selection bias in that that I find worrying, but maybe a checklist of things that qualify learners for an intermediate session could help.

+ Related to the first, I [April again] prepped too much material. The week before the bootcamp, I was looking at the responses to the pre-assessment and fipping out just a touch because so many learners seemed so advanced that I was worried we'd fly through everything. We didn't. 
	+ But the overage is in an iPython notebook, so learners can walk through this at their leisure.
	
+ We had one disastrous git merge example. That'll learn us for trying to show an example workflow in response to student questions.

+ There was some evidence among the experienced learners of a subset which desired a rules-based, task-focused accretion of skills. They probably would have enjoyed a pretty difficult example, integrating version control and unit testing, drawn from the numpy / matplotlib material. I [Eric] wonder if these students also needed a model workflow for learning from the internet and documentation — for instance, how do you identify an authoritative best-practice once you leave the classroom?

+ In retrospect, as an organizer, I [Eric] would have liked to have been pushed to engage a bit more to distill my hazy cloud of objectives and desire to serve every learning level. Does the lesson repo have a high-level list of topics and associated teaching times from which I could have assembled a draft schedule? I see this as a tool the instructors could have used to keep me honest about how an actual workshop tends to go.
