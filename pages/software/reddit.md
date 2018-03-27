

So there I am, trying to figure out how to grab posts from Reddit in
real time. I google [get reddit stream]. Score! There's a link to a
Reddit thread where someone suggests [PRAW](http://praw.readthedocs.io/en/latest/).

Once there, I navigate to the quickstart page, which tells me I need
to sign up for Reddit API access at... www.reddit.com. Awesome. So I
Google "Reddit API", which returns results on how to use the API but
nothing about how to signup. Okay, how about "Reddit API signup"?

Sweet! I get the [access page](https://www.reddit.com/wiki/api), which
sends me to a Google Docs survey. There I'm told I *first* need to get
an OAuth client ID from [here](https://www.reddit.com/prefs/apps).

After clicking "create application," I find I need to enter a name,
and click a radio button. The right one seems to be
"Script for personal use. Will only have access to the developers accounts",
even though I don't know what "will only have access to the developers
accounts means."

Then I have to enter an "about url" and a "redirect uri." What are those?
I enter my personal blog uri and cross my fingers. It complains. Maybe
I have to start it with "http://"? Score!

Now where do I get that "OAuth client ID?" It created a section

