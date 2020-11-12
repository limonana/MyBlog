# TDD - A Victory Story
<!-- add intro -->
<!-- should I add a TLDR of TDD? -->
<!-- TBD: projects domain-->
I wrote a new logic and unit tests for it.
```
class ScheduleCalculator
{
    void Calc(ProjectTree projectTree)
    {
        //doing some calculating and setting fields inside projectTree
    }
}
```
I added a new endpoint in the API which contains a simple integration code.
```
class ProjectAPI
{
    void calculateScheduling(String projectId)
    {
        DBLoader loader = new DBLoader();
        ProjectTree projectTree = loader.Load(projectId);
        ScheduleCalculator calculator = new ScheduleCalculator();
        calculator.calc(projectTree);
        SaveToDB(projectTree);
    }
}
```
<!-- TBD: add some name to the new logic -->
`DBLoader` is an existing class which is responsible for loading from the DB and creating a Project Tree structure.
<!-- add explanation about the function-->
```
DBLoader {
   public ProjectTree Load(ObjectIdentifier projectId,bool loadSubProjects);
}
``` 
 
So I wrote an integration test between the new logic to `DBLoader`. 
`DBLoader` was written and tested for a while. That is why I was very surprised when the test failed.
I start debugging and found out that `DBLoader` returns a wrong result. 
Apparently there were no tests of projects containing sub projects so loadSubProjects didn't affect the flow.
<!-- maybe was not executed? -->
My Integration test was the first test where `loadSubProjects` affect the flow.
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
DBLoader{
public ProjectTree Load(ObjectIdentifier projectId,bool loadSubProjects)
{
    …
    var projectTree = WorkitemsLoader.Load(projectId , false);
    ….
    }
}
WorkitemsLoader{
public ProjectTree Load(ObjectIdentifier projectId , bool recursiveLoading){
…..
}
}
``` 
It seems that the habit if writing tests before we are aware of the implementation is affacting the choise of 
which tests we write and of course which bugs we will find.

<!-- add link to why I LOVE TDD -->