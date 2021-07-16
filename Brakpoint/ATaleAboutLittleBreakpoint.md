# A Tale About A Little Breakpoint That Stuck A Huge Application

TBD: image

This is a story about a strange issuse I had when I worked with visual studio 2005 (yes, it was long long ago).I assume it can happen in any IDE.

I was working on a WinForms application (Did I say it was long time ago?). I ran the application in Debug mode and it seems to be stuck. Then I ran the application without debug mode, it seems fine. Weird...🤔
TBD: image of visual studio menus

Appearntly I added a conditional breakpoint somewhere deep in the infra code which occurs a lot of times. This caused such slowness that it seems like the application is stuck.I guess the condition I set also took a lot of time to evaluate. 

This breakpoint wasn't even related to the task I was working on, but it was left  there from the previous task.

So this is another reason to start fresh for each new task: delete obsolete breakpints and bookmarks.
if you start a new task with 0 bookmarks and breapoints, you can utilze these tools better to ease code navigation and debugging. How annying it is to start debug a scenario and keep deleting old breakpoints until you finnaly reach the code you actually want to debug. 
TBD:In intelij it comes free when you crreate a new branch.

Did you encontred this problem before? I love to hear about other strange problems you encontered.