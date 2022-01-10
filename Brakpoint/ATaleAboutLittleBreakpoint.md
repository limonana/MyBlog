# A Tale About A Little Breakpoint That Stuck A Huge Application

![suprised breakpoint](suprisied_brakpoint\breakpoint_talking_bubble.png)

This is a story about a strange issuse I had when I worked with Microsoft Visual Studio 2005 (yes, it was a long time ago).I assume it can happen in any IDE.

I was working on a WinForms application (Did I say it was a long time ago?). I ran the application in Debug mode and it seems to be stuck. Then I ran the application without debug mode, it seems fine. Weird...🤔

![visual studio run vs debug menu](images\vs_run_debug_menu.png)

Appearntly I added a conditional breakpoint somewhere deep in the infra code which occurs a lot of times. This caused such slowness that it seems like the application is stuck. I guess the condition I set also took a lot of time to evaluate. 

This breakpoint wasn't even related to the task I was working on! it was left  there from the previous task.

So this is another reason to start fresh, with no breakpoints, when starting a new task. If you start a new task with clean enviorment, you have an easier time navigating code and debugging.Think about how annoying it is to start debug a scenario and keep deleting old breakpoints until you FINALLLY reach the code you actually want to debug. 

Intelij, has a feature called [Tasks](https://www.jetbrains.com/help/idea/managing-tasks-and-context.html#work-with-context.using).Using this feature we can start a new task with its own branch and a clean enviorment.

Did you encontred this problem before? 

I love to hear about other strange problems you have encontered.