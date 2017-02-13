One problem I have noticed several times now is that of Zombie Scrum, or Scrum-by-numbers. It's an issue where someone has implemented Scrum some time back, and the implementation has stagnated.

Symptoms usually include the team doing all the ceremonies correctly, but not yielding the on-going benefits. A lot of practices (especially the daily Scrum) start to feel forced, or lose purpose.

(Note, this isn't limited to Scrum, but Scrum is the one I'm most familiar with. It can happen with any process, and seems to only get worse the more prescriptive the process is, presumably because buy-in and engagement by the development team was less to begin with.)

It's usually categorised by a conversation that goes:

Me: "Do you use an agile process?"
Them: "Yes, we do Scrum"
Me: "So what's your process look like?"
Them: "Err, we do Scrum?"
Me: "Ok, but what does your process look like day to day?"
Them: "Oh, yes we do stand-ups too!"

When people transition to Scrum, from something like waterfall, there are a lot of benefits you get immediately: iterative development, tighter feedback loops, increased communication, increased transparency. These are all good things. But old habits die hard, and after a time, it can become very mechanical, and you see the team stabilise and start to cruise again. There is no more improvement in the system. And of course they're doing retro's, right? Probably, but I have rarely seen real, measurable change come out of a retro. Not that retro's are bad, just that they are hard, and you need to be able to quantify whatever it is you're looking to improve to know you've improved it, and most teams aren't that advanced in their metrics (other than gross measures like a shift in velocity).

I can see two reasons this happens. The first is that people have been told that if you do Scrum then you have to do it "properly". No Scrum-but, or Scrum-hybrid etc. I think this is useful for teams starting out. I think this is detrimental to more advanced teams, teams that have been working together for some time and who have a good understanding of what agile software development is all about (more on this in a bit).

The other reason I think this happens is that three ideas have been conflated together: processes and frameworks, practices and techniques and the manifesto for agile software development.

The first category, processes and frameworks, are things like Scrum, which mandate certain activities and workflows. The second, practices and techniques, includes things like XP, refactoring, CI etc.

By conflating these ideas, usually under the banner captial-A Agile, it's easy for a team to think they are going along great, being agile, when they are missing out on the big payoff: continuous improvement. Yes, they may be doing retro's. But if you consider Agile = Scrum, then you aren't going to see bigger gains after the initial shift. Examples here might include things like: trying mobbing, no estimates, speed pairing, variable length Sprints, and so on.

I started thinking about this after listening to an Agile For Humans podcast (great podcast), where Ron Quartel discussed how his team was using Scrum, but with no estimates and variable length iterations. They got tremendous benefits from it. He also made reference to discovering the opening statement of the manifesto:

"We are *uncovering* better ways of developing
software by doing it and helping others do it.
Through this work we have come to value:"

Now, I'm certain I've read that statement previously, but I too had never fully grasped the importance of the word *uncovering*. We should be constantly working towards new and better ways of working. Scrum is great, but so is Lean. You like no estimates? Do it. Let's look at the 12 principals from the manifesto (I've only grabbed a few, the full list is xxx here xxx):

Our highest priority is to satisfy the customer
through early and continuous delivery
of valuable software.

Business people and developers must work 
together daily throughout the project.

Build projects around motivated individuals. 
Give them the environment and support they need, 
and trust them to get the job done.

Working software is the primary measure of progress.

Simplicity--the art of maximizing the amount 
of work not done--is essential.

The best architectures, requirements, and designs 
emerge from self-organizing teams.

...

You can see that following these principals is key to being agile and much more important than following a process. In fact, it says this right in the first value of the manifesto:

Individuals and interactions over *processes* and tools

I see the conflation of the ideas as a problem, because people are afraid to try something new, because it "isn't Scrum", or it "isn't Lean" or worse, we don't want to do a "hybrid". Who cares! Just be agile. And let's not forget the irony in not wanting to deviate from scrum when the PO doesn't sit with the team, isn't full time, there's no scrum master, the team isn't self selecting ...

I believe the key is to simply embrace the agile mindset. Be courageous with your process, because if you follow the agile values and principals you can trust that the process will deliver a delightful experience for both your team and your customer.

One cautionary note: agile is based on the empirical model for process control. That is, frequent _inspection and adaptation_ for processes that are imperfectly defined and generate _unpredictable and unrepeatable_ outputs. If you _are_ going to change your process, ensure you have the means to measure the resulting change in some meaningful way, that will allow you to determine if it was beneficial or not.

Lastly, I wanted to quote a slide from Dave Thomas' "Agile is Dead" presentation (which is great if you haven't seen it). He boils the agile process down to the following:

```
Find out where you are
Take a small step towards your goal
Adjust your understanding based on what you learned
Repeat

When faced with two or more alternatives that deliver roughly the same value, take the path that makes future change easier.
```

That's it! It's as simple as developing a complex software system in a difficult business environment :) Hang tough though, have the courage to stick to the agile principals and let's all make software development a better place to live.