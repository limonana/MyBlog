# A Tale About A Little Breakpoint Who Stuck a Huge Application

This is a story about a strange thing happened to me when I worked with visual studio 2005 (yes, it was long long ago),but I assume it can happen in any IDE. 

I was working on a WinForms application. I ran the application in Debug mode and it seems to be stuck. Then I ran the application not in debug mode. Everything seems fine. Weird... TBD:confused/thinkiing emoj

Appearntly I added a conditional breakpoint somewhere deep in the infra code which occurs a lot of times. This caused such slowness that it seems like the application is stuck.I guess the condition I set also took a lot of time to evaluate. 

This breakpoint wasn't even related to the task I was working on, but it was left  there from the previous task.

So this is another reason to start fresh for each new task: delete obsolete breakpints and bookmarks.
TBD: other reasons - order, unrelevent breapoints that disturb debuggibg.
TBD:In intelij it comes free when you crreate a new branch.

Did you encontred this problem before? I love to hear about other strange problems you encontered.