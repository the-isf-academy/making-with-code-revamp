---
Title: Data Stuctures Project
---

# Unit 01 Data Structures Project

For this project, you will implement a queue that will be used
to serve orders to an imaginary internet shopping company.

{{< figure src="images/courses/cs10/unit00/00_project_model.png" width="100%" >}}

## Starter Code

{{< code-action >}} Starter code for the project is provided in the
`project-queue` repo. Download it *onto your laptop*.

```shell
$ cd cs10/unit_01
$ git clone https://github.com/the-isf-academy/project-queue-YOUR-GITHUB-USERNAME.git
```

## Planning Document
This project will require you to explore the theory behind efficient data
structure design. You will likely changes your plans frequently as you
try out different ideas for how to make your queue faster. As such, rather
than a planning document, this project comes with an ideating document to
help you keep track of your ideas for designing your queue.
*You can find your ideating doc in your Google Drive folder called "cs10 -
Unit 00 Data Structure Project: Ideating Document".*

As we go through the development of a basic queue in class together, you
can start by using this document to take notes on how we design the queue,
the interfaces it implements, and ideas for how to make them better.

## Deliverables 

- An ideation document in your Google Drive folder 
- A `queue.py` file with your implementation of a queue containing the
following interfaces (which pass the tests in `test_queue.py`):
    - `queue()` - add element to the end of the queue
    - `popleft()` - remove element from the front of the queue
    - `insert()` - add an element at a particular index of the queue
    - `__len__()` - returns the number of items in the queue
- At least 5 substantial Git commit messages, each explaining what you've
changed and why.
- An `assessment.md` file with a completed self-assessment of your project.

### Extension
Additionally, as an extension and for extra credit, you can implment the
following additional interfaces for your queue in `queue.py`:
- `remove()` - Removes the first instance of a value from the queue.
Throws an error if the value doesn't exist in the list.
- `index()` - Finds the first instance of a value within the queue and 
returns the index of the value.
- `count()` - Counts the number of times a value appears in the queue and 
returns the count.
- `__getitem__()` - operator overload to get the item in the list at
a particular index.

**You can find more documentation about what each of the files should 
contain within the README.md file in the project directory.**

## Timeline
### cs10.1
{{< figure src="images/courses/cs10/unit01/01_project_cs10_1.png" width="100%" >}}
### cs10.2
{{< figure src="images/courses/cs10/unit01/01_project_cs10_2.png" width="100%" >}}

## Assessment
The assessment for this project will be slightly different than
for your other projects. In `assessment.md`, you are required to explain
how your project should be scored, and to give evidence to support your
assessment.

For criterion A, the rubruc is based on the performance of your queue.

For criteria B and C, the rubric is based on claims that you should be able 
to make about your learning in this unit. Each of these claims comes with
examples of evidence that would show that you can make the claim about your
learning.

**To do well in this project, you should pass the test harness requirements
for criterion A and be able to concretely justify that you have achieved
each of the learning claims for criteria B and C.**

As a reminder, here's a guide for using the rubric for Criteria B and C:
- Read the learning claims of the criterion for this unit in the rubric and consider how they relate to
the description of the criterion.
- For each learning claim in the criterion:
    - Evidence: Identify 1-5 elements of your project that provide evidence for the learning claim.
    - Reasoning: Provide specific reasoning that presents how the piece(s) of evidence you identified
    support the claim about your learning.
- Determine the level between 1-8 that represents your overall learning in the criterion based on the
evidence and reasoning you provided for the learning claims of the criterion.

## Rubric 

Each project will be assessed with a rubric tailored to the skills and concepts the project targets.
This project is focused on developing the skills learned throughout the drawing unit. 


### Criterion A: Knowing, understanding, and computational thinking 

> Students appropriately apply computer science concepts and tools in context. On top of computer
> science concepts and tools, students apply computational thinking practices including habits such 
> as writing pseudocode, developing iteratively, using abstractions, decomposing problems, and debugging.

Your score for criterion A will be based on your queue's performace on with
our test harness for functionality and speed.

| Score | Functionality                     | Speed                     |
|-------|-----------------------------------|---------------------------|
| 8     | all basic queue functions working | in the top 80% of queues\* |
| 7     | all basic queue functions working | in the top 60% of queues\* |
| 6     | all basic queue functions working | in the top 40% of queues\* |
| 5     | all basic queue functions working | –                         |
| 4     | 3 working queue functions         | –                         |
| 3     | 2 working queue functions         | –                         |
| 2     | 1 working queue function          | –                         |
| 1     | no working queue functions        | –                         |


\* Queue ranking will be determined by adding each queue's iterations per
second on each of the four basic function tests to generate a queue score.
Then, we will take the percentile ranking of each queue (based on the queue 
score) in the distribution of queues which passed all of the basic
functionality tests.

### Criterion B: Planning and development
> Students create personally meaningful projects through an iterative design cycle. Students’ work is
> grounded in a development plan which students create before beginning the project. Students document
> the development of their projects in order to create a record of decisions, assumptions, and
> lingering flaws. Students define the intended functionality and develop towards evaluation.

In this unit, you will need to build a fast, efficient, and effective queue.
This will challenge your planning, researching, and iterative development
skills.

| Learning Claim                                                                  | Possible Forms of Evidence                                                                                                                                                                                                                                                                                                 |
|---------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| I can thoughtfully plan a large computer science project.                       | <ul><li>A thorough ideation document.</li> <li>Updates to your project plan to account for challenges or discoveries during development</li></ul>                                                                                                                                                                                         |
| I can iteratively develop a project using version control tools such as GitHub. | <ul><li>At least 5 regular and descriptive git commits on your project</li> <li>A stub function you wrote to stand in for a function that had not yet been developed.</li> <li>A transition from a basic set of interface functions to a more robust set (either in number or efficiency)</li></ul> |
| I can document my software so that it is readable and usable by others.         | <ul><li>Comments for each of the functions you write for your queue's interface</li></ul>                                                                                                                                                                                                                                    |

### Criterion C: Evaluation 
> Students produce evidence of a testing plan that evaluates the main areas of functionality of the
> product and reflect on the development process as well as a proposal for further development to
> improve the shortcomings of the current product.

As you develop your queue, you will need to constantly be testing and
debugging to make sure changes to your queue do not affect its functionality.
Additionally, you will need to account for edge cases amongst your queue's
use cases so that your queue works under a variety of circumstances.

| Learning Claim                                                                                                                        | Possible Forms of Evidence                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| I can identify different scenarios in which my code may be used and outline the expected functionality of my code in these instances. | <ul><li>A list of general use cases for each of your queue's functions including the expected functionality of your queue in those cases</li> <li>An identification of the edge cases (erroneous or malicious uses of your software that fall outside of the basic use cases)</li></ul> |
| I can develop a testing strategy to ensure my code works as expected.                                                                 | <ul><li>A list of tests you will run to make sure your code works based on your use cases and responses</li> <li>Changes your made after finishing development and running your tests</li></ul>                                                                            |