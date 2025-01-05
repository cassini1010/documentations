# Jira Testing Cycle

## Planning and creating test cases.

- requirement gathering: gather based on user stories. 

- test case design: Each test case should have clear steps, expected results, and any prerequisites. 

## Organize the test cases.

- Test Plan: outlines the scope, objectives, resources, and schedule for the testing activities. 

- Test Suites: Group related test cases into test suites for better organization and management. 

## Execution

Test Execution: execute manually or automatically. Note the results in each test step or test case. Attache required evidence. 

## Report bug

Issues found during testing? Create a bug ticket to dev team. Link the relevant test case/user story/requirement to the bug ticket. 

## Retest

After the bug is fixed, the test is redone to ensure its fixed. 

## Test summary

At the end of the testing cycle, compile a test summary report that highlights the overall test execution status, key findings, and any remaining risks.

## Basic testing cycle

Testing hierarchy is categorized into four levels;

- Unit testing : During development phase. 

- Integration testing

- System testing

- Regression Testing : test the maintenance of the application.

### Unit Testing

Performed during the development phase of a software. Testing is done for each small unit of a code module wise. Test cases can be designed in two methods here; 

Using Blackbox method and whitebox method.

Black box test cases are written in the interest of input given and output observed only. The internal structure of the code is not the consideration here. Whitebox on the other hand considers all the internal codes.

### Integration Testing

All the units which are tested separately in unit testing are now integrated with each other rand is tested.

### System testing

This is where the end product is tested on a system level

Non functional testing like load, stress testing comes under this. 

### Regression testing

Usual maintenance of the product is tested. New add on feature is tested. 



## SDLC ( Software development lifecycle):

- Requirement

- analysis

- design : high level design, low level design

- coding : build the software

- testing : test for defect

- deployment/ maintenance : 



> SLA : service level agreement



Agile, waterfall, spiral are different types of SDLC models





### Waterfall:

sequesntial design

every next phase is began when goal of the previous phase is completed

this is preferred where quality is important

Requirements are fixed here and cant be changed in the progress different phases

If requirement change then this is not a best suited model'



### Boehm Spiral model

plan -> risk analysis -> coding testing -> customer evaluation 

The above step repeat after the release of one version and getting customer feedback.

Development of next version is going on while existing version is still there

next version is based on user feedback

Allows requirement changes

not suitable for small project
