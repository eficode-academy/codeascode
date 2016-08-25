# CoDefying Your Own project
As a project for the "Bringing it all together" part of CoDe-Academy you can bring
one of your own projects up to CoDe.

These are some pointers as to what you could do in order to implement Continuous Delivery.

## Distributed Version Control
Your code is already under Version Control, right?
Otherwise this should be your one and only priority.
Put it in a GitHub repository or some equivalent.

## Agile task management
As your project is obviously in some awesome central repository - You should have some issue management.
If you are using GitHub you can use [Waffle.io](http://waffle.io) .

You can reasonably add your conversion to CoDe tasks in here as well.

## Testing 
Testing is an essential part of Continuous
Delivery. Depending on your project domain and scope different types
of tests have value. What is important is that you have tests that you can use as toll-gate criteria.

## Automation
Everything in your project should of course be automated. Build, test, deploy and so on and so forth.
We've been using Jenkins, but there are alternatives. Circle-ci, Travis and Concourse are options.

Travis CI is free for public github repositories. ( The others might also be, but I haven't checked :D ).

## Pretested Integration
As you know you should have pretested integration in your project.
This will help you keep your master clean. 
Using Jenkins you can use the pretested integration plugin.



## Docker
Running your application in Docker allows us to bundle dependencies along with the application, easing deployment ( and test of deployment ).
Depending on the complexity of your application, this can be quite a daunting task.
