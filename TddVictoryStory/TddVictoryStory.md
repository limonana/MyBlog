# Test Driven Development - A Victory Story
TBD:Intro
<!-- If you are not familiar with TDD read the following  add TDD 101 -->
<!-- TBD: projects domain-->
I worked on a Jira like system which its domain is projects and tasks.
Project can contain another projects and tasks. 
A task has an estimated duration - how much time it should take to finish and
constraints like when it can start, which tasks should be finished before this task can start and many more. 
<!-- TBD: Image of project tree -->
I wrote a new logic which calculate the schedule for the project.
The schedule is the estimated start time and end time for all the tasks and projects under a specific project.
The scheduling is calculated according to the tasks constraints and estimated durations.
So I wrote the class ScheduleCalculator and unit tests for it.
```
class ScheduleCalculator
{
    void Calc(ProjectTree projectTree)
    {
        //calculate the schedule save it inside the projectTree objects.
    }
}
```
I added a new endpoint in the API which contains a simple integration code
and wrote an integration test for it.
```
class ProjectAPI(DBLoader loader, ScheduleCalculator scheduleCalculator)
{
    void CalculateScheduling(String projectId)
    {
        ProjectTree projectTree = loader.Load(projectId,true);
        scheduleCalculator.calc(projectTree);
        SaveToDB(projectTree);
    }
}
```
`DBLoader` is an existing class which is responsible for loading from the DB and creating a Project Tree structure.
When loadSubProjects = true for a project that contains sub projects, the sub projects are loaded as trees with all their children.
When loadSubProjects = false for a project that contains sub projects, only the sub projects are loaded without their children.
loadSubProjects has no effect project which doesn't contain sub projects.
<!-- should replace this with a comment in code? -->
```
class DBLoader
{
   public ProjectTree Load(String projectId, bool loadSubProjects)
   {
    .....
   }
}
``` 
`DBLoader` was written and tested for a while. `ProjectAPI.CalculateScheduling` contain a really simple logic.
This is why I was very surprised when the test of `ProjectAPI.CalculateScheduling` failed.

I start debugging and found out that `DBLoader` returns a wrong result. 
Apparently there were no tests for `DBLoader` that check it with projects containing sub projects => loadSubProjects didn't affect the flow.
So the test of `ProjectAPI.calculateScheduling` was the first test where `loadSubProjects` should affect the flow.

So I wrote a new test for the DBLoader which represent the same scenario.
The test failed, I solved the bug. The 2 tests now pass (green?). Everything is sababa 😎

Since I realized that DBLoader wasn't tested with scenarios that loadSubProjects have effect the result, 
I decided to add more tests to DBLoader even though my integration test pass.
I checked which tests I can add. Since the code was already written
I tried to understand where the code can break by reading it. I couldn't think of any tests, I don't see any reason for the code to break.

Then I stopped an told myself: "Wait... This is not the way I usually write tests". I usually work in TDD. Meaning I think of a test plan which contains the different dimensions of the problem , the values for each dimenstion and I choose the relvent combinations odf values. (since checking all combinations is infinite.)
Do you want to guess ?  I found a bug ! :griningEmoji
A really stupid bug which caused by refactoring.  DBLoader pass false instead of loadSubProjects.
```
DBLoader
{
    public ProjectTree Load(ObjectIdentifier projectId,bool loadSubProjects)
    {
        …
        var projectTree = WorkitemsLoader.Load(projectId , false); //false is the bug. should pass loadSubProjects 
        …
    }
}

WorkitemsLoader
{
    public ProjectTree Load(ObjectIdentifier projectId , bool recursiveLoading)
    {
        …
    }
}
``` 
It seems that the habit of writing tests before we are aware of the implementation is affacting the choise of 
which tests we write and of course which bugs we will find.

<!-- add link to why I LOVE TDD -->