---
layout: post
title: WardScore
byline: League of Legends Ward Tracker
img: ward.png
liveurl: http://wardscore.loltools.net
---
#What's the Score? A Postmortum on WardScore

At the tail end of the year, Riot Games released their League of Legends API for an open developer beta. I remember coming back to my desk and seeing a multitude of messages from a friend of mine, Maxwell. He was saying that he should make a project on top of the API. He then messaged me a bit later asking for my help. I plunged in head first, and a few months later WardScore is by far and away one of the most popular things I've ever made. It's to me one of the best examples thus far of the types of insights that arise from the new API. It also provided a look at how far I've come as a developer, and how much further I have to go.

##About Us

My name is William, but I usualy go by either Lego, or Enigma. I'm a sophmore at Olin College of Engineering. I'm a caster for League of Legends with the College of Casting and for TF2 with eXtelevision. I'm also a Co-Founder of [EnigmaSM Studios](http://www.enigmasm.com), a hacker collective consisting of me, Max, and Jeffery. I met them at summer camp in 2008 and have stayed connected with ever since. We build all sorts of cool projects together, and for this project, max and I built WardScore.

##Beginings

We built the project on top of a simple PHP backend with jQuery driving the frontend. MySQL was our database of choice. Our hosting plan was original the 3 dollar hosting from NameCheap, which only supported PHP. This prevented us from using newer alternatives like Node.js. Regardless, the first thing that I did on the project was changing around our database backend. Max's original model for the database was to have each player's game records occupy their own table in the database. For an app that would soon track over 200k summoners (though we wouldn't know it yet), this system was disastrous. I immediately changed the way our script wrote to the database. We would only have 2 tables: Players and Matches, this would soon include a third for the Games themselves.

##Less is More

The More/Less feature was an idea that I had to provide a bit more insight and clean up some language. I went through the HTML to color code the word "more" depending on how good you warded, and switch it to "less" when you were below average. We used a consistent color scheme where red was low and a blue green was high. We used those same colors to highlight that word to provide a bit more insight into your performance. Me and Max talked out the idea and demoed it for each other, and we ended up deciding to cut it. Why?

The answer is simple. Information overload can be a big problem. I, as a developer, have a tendency to put more and more features into an app because I find it to be fun and challenging to do. Yet, in this case, the addition of the "more or less" text only caused for confusion. You might only see 90%, and when you could be 90% more then average and 90% less then average, it made things hard to understand at a glance. We cut the feature because all it did was confuse the user, and with such a simple app, we didn't want to confuse.

##Launching Woes

After we had almost finished work on the base feature set, we needed data. I went to the Collegiate Organizer's Facebook group and posted the link looking for feedback. Our website exploded. Folks like [Riot Pwyff](https://twitter.com/riotpwyff/status/413053239433510912) [Riot Nurse Flan](https://twitter.com/riotnurseflan/status/413139841585381377), and many more started talking about their ward scores on social media! A couple of European personalities tweeted about it, which caused a massive influx of people to the site. It was much more than we could handle. We immediately set to work fixing bugs, one of the biggest was SQL sessions taking 60+ seconds to timeout. This was locking up resources that other viewers used to access to the site. We also were still on the beta test key, which meant we could only handle around 10 requests every 5 seconds. When you have 100+ people on the site at once it overloads the site.

It was around that time that folks like Riot Jaws and Pwyff reached out to us and put us in contact with the people managing the API. After a quick approval process we got our key by the end of the week. Our website then continued to grow, and we reached 100k summoners by the end of the week.

##Lessons from Live

###Don't Break While You Fix

During a spike of traffic, I had to fix a bug with how we were handling errors to clarify why certain requests were failing. In that process, I accidentally wrote some text at the start of the PHP file. This meant that requests to the PHP file contained dummy text at the beginning of the JSON. This broke the entire site for anyone using it. It took too long to find the fix, and I had no backups of what I was doing. For all future changes, I instead duplicated the file in question, made changes and tested them on that duplicate. I made one final duplication of the working one and moved the changes on top. For a small scale project like this, a full Git repo would have been overkill, so this was a good compromise.

###Be Careful Who You Share With

We were so excited to see all the people loving WardScore! But, this popularity meant that the site was sometimes non functional. We should have a better plan in place to accommodate such a situation to prevent a super overload on our resources. The first was that our hosting could not scale. Our hosting was a shared box we had no control over: The hosting limited concurrent processes to 20 at one time. Because of this, users got 503 overloads often. If 20 people tried to access the site at the same time (or 20 people searched for WardScores) any extra users would either get cryptic errors or were just not be able to access the site. In response, we moved the site over to [Digital Ocean](https://www.digitalocean.com/?refcode=350d6ef8fdab). The second problem was the key. We were on the trial key, which was rate limited. As explained above, even if you got through to the site there might be no requests remaining on the key. While we fixed that after a few days, that was something that was frustrating for us. In short, while getting users to test your product is key, make sure you can handle a slashdot/reddit hug. Sometimes it can be more prudent to just wait for the rest of the dominos to fall in place. Then again, if WardScore didn't get the same kind of reception we might be still waiting for our key today. Weigh the ups and downs.

###Respond to the Users

One of the most fun I've had on this project was responding to users inquiries and working with them on bugs. I have a twitter search saved for WardScore, where I retweet occasional WardScores that I find interesting. I always make a point to respond to people who message me about WardScore. For people using your project, it builds a connection with them that you now share. Your project now has linked you two together. Relish those connections. Build them. It's fun to do! You never know where it might lead...

##Big Mover

The other major component of the WardScore adventure was my transition to [Digital Ocean](https://www.digitalocean.com/?refcode=350d6ef8fdab). I had never had to set up a web server from scratch before, but I dove right in. I was installing nginx, ssh, sftp, php, node.js, and so much more from a bare bones setup. It was quite a change from just having to drop files into a server, and it was welcome. EnigmaSM now has a full site where they can do whatever they want whenever they want on whatever platform we choose! My only regret is that I'm on the 10 dollar a month plan, when with some careful optimization I could hit 5. To me, the extra power is worth being able to play around with my first real linux box outside of fooling around in high school on an old server.

##The Aftershock

I list WardScore as one of my best projects of Late 2013/Early 2014 because of the wealth of information it provided me as a learner. It was one of my most successful projects to date, and one of the most fun to build. Watching Google Analytics go crazy throughout the day, fixing bugs, and learning new tricks was a fun way to spend a few months. As of the writing, we've crossed 20 million wards and well over 200k summoners. Plus, people still visit the site organically. I bill this project as the reason why I'm getting more interviews in my internship search. It encapsulates where I stand as a developer: Willing to work on projects in any language and build them with the users in mind. Of course, there is still a long way to go. I'm reminded of Facebook's saying that the journey is 1% finished. My journey as a web developer and as a developer in general is only 1% finished. I can't wait to see what new projects I discover and build next.