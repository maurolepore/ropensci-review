Exercise Types
Every good carpenter has a set of screwdrivers, and every good teacher has different kinds of exercises to check what learners are actually learning, help them practice their new skills, and keep them engaged. This chapter starts by describing several kinds of exercises you can use to check if your teaching has been effective. It then looks at the state of the art in automated grading, and closes by exploring discussion, projects, and other important kinds of work that require more human attention to assess. Our discussion draws in part on the Canterbury Question Bank [Sand2013], which has entries for various languages and topics in introductory computing.

The Classics
As Section 2.1 discussed, multiple choice questions (MCQs) are most effective when the wrong answers probe for specific misconceptions. They are usually designed to test the lower levels of Bloom’s Taxonomy (Section 6.2), but can also require learners to exercise judgment.

A Multiple Choice Question
In what order do operations occur when the computer evaluates the expression price = addTaxes(cost - discount)?

subtraction, function call, assignment

function call, subtraction, assignment

function call, then assignment and subtraction simultaneously

none of the above

The second classic type of programming exercise is code and run (C&R), in which the learner writes code that produces a specified output. C&R exercises can be as simple or as complex as the teacher wants, but when used in class, they should be brief and have only one or two plausible correct answers. It’s often enough to ask novices to calculate and print a single value or call a specific function: experienced teachers often forget how hard it can be to figure out which parameters go where. For more advanced learners, figuring out which function to call is more engaging and a better gauge of their understanding.

Code & Run
The variable picture contains a full-color image read from a file. Using one function, create a black and white version of the image and assign it to a new variable called monochrome.

Write and run exercises can be combined with MCQs. For example, this MCQ can only be answered by running the Unix ls command:

Combining MCQ with Code & Run
You are in the directory /home. Which of the following files is not in that directory?

autumn.csv

fall.csv

spring.csv

winter.csv

C&Rs help people practice the skills they most want to learn, but they can be hard to assess: there can be lots of unexpected ways to get the right answer, and people will be demoralized if an automatic grading system rejects their code because it doesn’t match the teacher’s. One way to reduce how often this occurs is to assess only their output, but that doesn’t give them feedback on how they are programming. Another is to give them a small test suite they can run their code against before they submit it (at which point it is run against a more comprehensive set of tests). Doing this helps them figure out if they have completely misunderstood the intent of the exercise before they do anything that they think might cost them grades.

Instead of writing code that satisfies some specification, learners can be asked to write tests to determine whether a piece of code conforms to a spec. This is a useful skill in its own right, and doing it may give learners a bit more sympathy for how hard their teachers work.

Inverting Code & Run
The function monotonic_sum calculates the sum of each section of a list of numbers in which the values are strictly increasing. For example, given the input [1, 3, 3, 4, 5, 1], the output is [4, 12, 1]. Write and run unit tests to determine which of the following bugs the function contains:

Considers every negative number the start of a new sub-sequence.

Does not include the first value of each sub-sequence in the sub-sum.

Does not include the last value of each sub-sequence in the sub-sum.

Only re-starts the sum when values decrease rather than fail to increase.

Fill in the blanks is a refinement of C&R in which the learner is given some starter code and has to complete it. (In practice, most C&R exercises are actually fill in the blanks because the teacher provides comments to remind the learners of the steps they should take.) Questions of this type are the basis for faded examples; as discussed in Chapter 4, novices often find them less intimidating than writing all the code from scratch, and since the teacher has provided most of the answer’s structure, submissions are much more predictable and therefore easier to check.

Fill in the Blanks
Fill in the blanks so that the code below prints the string ’hat’.

text = 'all that it is'
slice = text[____:____]
print(slice)
Parsons Problems also avoid the “blank screen of terror” problem while allowing learners to concentrate on control flow separately from vocabulary [Pars2006,Eric2015,Morr2016,Eric2017]. Tools for building and doing Parsons Problems online exist [Ihan2011], but they can be emulated (albeit somewhat clumsily) by asking learners to rearrange lines of code in an editor.

Parsons Problem
Rearrange and indent these lines to sum the positive values in a list. (You will need to add colons in appropriate places as well.)

total = 0
if v > 0
total += v
for v in values
Note that giving learners more lines than they need, or asking them to rearrange some lines and add a few more, makes Parsons Problems significantly harder [Harm2016].

Tracing
Tracing execution is the inverse of a Parsons Problem: given a few lines of code, the learner has to trace the order in which those lines are executed. This is an essential debugging skill and a good way to solidify learners’ understanding of loops, conditionals, and the evaluation order of function and method calls. The easiest way to implement it is to have learners write out a sequence of labeled steps. Having them choose the correct sequence from a set (i.e. presenting this as an MCQ) adds cognitive load without adding value, since they have to do all the work of figuring out the correct sequence, then search for it in the list of options.

Tracing Execution Order
In what order are the labeled lines in this block of code executed?

A)     vals = [-1, 0, 1]
B)     inverse_sum = 0
       try:
           for v in vals:
C)             inverse_sum += 1/v
       except:
D)         pass
Tracing values is similar to tracing execution, but instead of spelling out the order in which code is executed, the learner lists the values that one or more variables take on as the program runs. One way to implement this is to give the learner a table whose columns are labeled with variable names and whose rows are labeled with line numbers, and ask them to fill in the values taken on by the variables on those lines.

Tracing Values
What values do left and right take on as this program executes?

A) left = 23
B) right = 6
C) while right:
D)     left, right = right, left % right
Line	left	right
You can also require learners to trace code backwards to figure out what the input must have been for the code to produce a particular result [Armo2008]. These reverse execution problems require search and deductive reasoning, and when the output is an error message, they help learners develop valuable debugging skills.

Reverse Execution
Fill in the missing number in values that caused this function to crash.

values = [ [1.0, -0.5], [3.0, 1.5], [2.5, ___] ]
runningTotal = 0.0
for (reading, scaling) in values:
    runningTotal += reading / scaling
Minimal fix exercises also help learners develop debugging skills. Given a few lines of code that contain a bug, the learner must find it and make one small change to fix it. Making the change can be done using C&R, while identifying it can be done as a multiple choice question.

Minimal Fix
This function is supposed to test whether a number lies within a range. Make one small change so that it actually does so.

def inside(point, lower, higher):
    if (point <= lower):
        return false
    elif (point <= higher):
        return false
    else:
        return true
Theme and variation exercises are similar, but the learner is asked to make a small alteration that changes the output in some specific way instead of making a change to fix a bug. Allowed changes can include changing a variable’s initial value, replacing one function call with another, swapping inner and outer loops, or changing the order of tests in a complex conditional. Again, this kind of exercise gives learners a chance to practice a useful real-world skill: the fastest way to produce the code they need is to tweak code that already does something close.

Theme and Variations
Change the inner loop in the function below so that it fills the upper left triangle of an image with a specified color.

function fillTriangle(picture, color) is
    for x := 1 to picture.width do
        for y := 1 to picture.height do
            picture[x, y] = color
        end
    end
end
Refactoring exercises are the complement of theme and variation exercises: given a working piece of code, the learner has to modify it in some way without changing its output. For example, the learner could replace loops with vectorized expressions or simplify the condition in a while loop. This is also a useful real-world skill, but there are often so many ways to refactor code that grading requires human inspection.

Refactoring
Write a single list comprehension that has the same effect as this loop.

result = []
for v in values:
    if len(v) > threshold:
        result.append(v)
Diagrams
Having learners draw concept maps and other diagrams gives insight into how they’re thinking (Section 3.1), but free-form diagrams take human time and judgment to assess. Labeling diagrams, on the other hand, is almost as powerful pedagogically but much easier to scale.

Rather than having learners create diagrams from scratch, provide them with a diagram and a set of labels and have them put the latter in the right places on the former. The diagram can be a data structure (“after this code is executed, which variables point to which parts of this structure?”), a chart (“match each of these pieces of code with the part of the chart it generated”), or the code itself (“match each term to an example of that program element”).

Labeling a Diagram
Figure 12.1 shows how a small fragment of HTML is represented in memory. Put the labels 1–9 on the elements of the tree to show the order in which they are reached in a depth-first traversal.


Labeling a diagram
Another way to use diagrams is to give learners the pieces of the diagram and ask them to arrange them correctly. This is a visual equivalent of a Parsons Problem, and you can provide as much or as little of a skeleton to help with placement as you think they’re ready for. I have fond memories of trying to place resistors and capacitors in a circuit diagram in order to get the right voltage at a certain point, and have seen teachers give learners a fixed set of Scratch blocks and ask them to create a particular drawing using only those blocks.

Matching problems can be thought of as a special case of labeling in which the “diagram” is a column of text and the labels are taken from the other column. One-to-one matching gives the learner two lists of equal length and asks them to pair corresponding items, e.g. “match each piece of code with the output it produces.”

Matching
Match each regular expression operator in Figure 12.2 with what it does.


Matching items
With many-to-many matching the lists aren’t the same length, so some items may be matched to several others and others may not be matched at all. Many-to-many are more difficult because learners can’t do easy matches first to reduce their search space. Matching problems can be implemented by having learners submit lists of matching pairs (such as “A3, B1, C2”), but that’s clumsy and error-prone. Having them recognize a set of correct pairs in an MCQ is even worse, as it’s painfully easy to misread. Drawing or dragging works much better, but may require some work to implement.

Ranking is a special case of matching that is (slightly) more amenable to answering via lists, since our minds are pretty good at detecting errors or anomalies in sequences. The ranking criteria determine the level of reasoning required. If you have learners order sorting algorithms from fastest to slowest you are probably exercising recall (i.e. asking them recognizing the algorithms’ names and know their properties), while asking them to rank solutions from most robust to most brittle exercises reasoning and judgment.

Summarization also requires learners to use higher-order thinking and gives them a chance to practice a skill that is very useful when reporting bugs. For example, you can ask learners, “Which sentence best describes how the output of f changes as x varies from 0 to 10?” and then given several options as a multiple choice question. You can also ask for very short free-form answers to questions in constrained domains, such as, “What is the key feature of a stable sorting algorithm?” We can’t fully automate checks for these without a frustrating number of false positives (accepting wrong answers) and false negatives (rejecting correct ones), but questions of this kind lend themselves well to peer grading (Section 5.3).

Automatic Grading
Automatic program grading tools have been around longer than I have been alive: the earliest published mention dates from 1960 [Holl1960], and the surveys published in [Douc2005,Ihan2010] mention many specific tools by name. Building such tools is a lot more complex than it might first seem. How are assignments represented? How are submissions tracked and reported? Can learners co-operate? How can submissions be executed safely? [Edwa2014a] is an entire paper devoted to an adaptive scheme for detecting and managing infinite loops in code submissions, and that’s just one of the many issues that comes up.

When discussing auto-graders, it is important to distinguish learner satisfaction from learning outcomes. For example, [Magu2018] switched informal programming labs for a second-year CS course to a weekly machine-evaluated test using an auto-grader. Learners didn’t like the automated system, but the overall failure rate for the course was halved and the number of learners gaining first class honors tripled. In contrast, [Rubi2014] also began to use an auto-grader designed for competitions, but saw no significant decrease in their learners’ dropout rates; once again, learners made some negative comments about the tool, which the authors attribute to the quality of its feedback messages rather than to dislike of auto-grading.

[Srid2016] took a different approach. They used fuzz testing (i.e. randomly generated test cases) to check whether learner code does the same thing as a reference implementation supplied by the teacher. In the first project of a 1400-learner introductory course, fuzz testing caught errors that were missed by a suite of hand-written test cases for more than 48% of learners.

[Basu2015] gave learners a suite of solution test cases, but learners had to unlock each one by answering questions about its expected behavior before they were allowed to apply it to their proposed solution. For example, suppose learners had to write a function to find the largest adjacent pair of numbers in a list. Before being allowed to use the question’s tests, they had to choose the right answer to, “What does largestPair(4, 3, -1, 5, 3, 3) produce?” In a 1300-person university course, the vast majority of learners chose to validate their understanding of test cases this way before attempting to solve problems, and then asked fewer questions and expressed less confusion about assignments.

Against Off-the-Shelf Tools
It’s tempting to use off-the-shelf style checking tools to grade learners’ code. However, [Nutb2016] initially found no correlation between human-provided marks and style-checker rule violations. Sometimes this was because learners violated one rule many times (thereby losing more points than they should have), but other times it was because they submitted the assignment starter code with few alterations and got more points than they should have.

Even tools built specifically for teaching can fall short of teachers’ needs. [Keun2016a,Keun2016b] looked at the messages produced by 69 auto-grading tools. They found that the tools often do not give feedback on how to fix problems and take the next step. They also found that most teachers cannot easily adapt most of the tools to their needs: like many workflow tools, they tend to enforce their creators’ unrecognized assumptions about how institutions work. Their classification scheme is a useful shopping list when looking at tools of this kind.

[Buff2015] presents a well-informed reflection on the whole idea of providing automated feedback. Their starting point is that, “Automated grading systems help learners identify bugs in their code, [but] may inadvertently discourage learners from thinking critically and testing thoroughly and instead encourage dependence on the teacher’s tests.” One of the key issues they identified is that a learner may thoroughly test their code, but the feature may still not be implemented according to the teacher’s specifications. In this case, the “failure” is not caused by a lack of testing but by a misunderstanding of the requirements, and it is unlikely that more testing will expose the problem. If the auto-grading system doesn’t provide insightful, actionable feedback, this experience will only frustrate the learner.

In order to provide that feedback, [Buff2015]’s system identifies which methods in the learner’s code are executed by failing tests so that the system can associate failed tests with particular features within the learner’s submission. The system decides whether specific hints have been “earned” by seeing whether the learner has tested the associated feature enough, so learners cannot rely on hints instead of doing tests.

[Srid2016] describes some other approaches for sharing feedback with learners when automatically testing their code. The first is to provide the expected output for the tests—but then learners hard-code output for those inputs (because anything that can be gamed will be). The second is to report the pass/fail results for the learners’ code, but only supply the actual inputs and outputs of the tests after the submission date. However, telling learners that they are wrong but not telling them why is frustrating.

A third option is to use a technique called hashing to generate a value that depends on the output but doesn’t reveal it. If the user produces exactly the right output then its hash will unlock the solution, but it is impossible to work backward from the hash to figure out what the output is supposed to be. Hashing requires more work and explanation to set up, but strikes a good balance between revealing answers prematurely and not revealing them when it would help.

Higher-Level Thinking
Many other kinds of programming exercises are hard for teachers to assess in a class with more than handful of learners and equally hard for automated platforms to assess at all. Larger programming projects are (hopefully) what classes are building toward, but the only way to give feedback is case by case.

Code review is also hard to grade automatically in general, but can be tackled if learners are given a list of faults to look for and asked to match particular comments against particular lines of code. For example, the learner can be told that there are two indentation errors and one bad variable name and asked to point them out. If they are more advanced, they could be given half a dozen kinds of remarks they could make about the code without being told how many of each they should find.

[Steg2016b] is a good starting point for a code style rubric, while [Luxt2009] looks at peer review in programming classes more generally. If you are going to have learners do reviews, use calibrated peer review (Section 5.3) so that they have models of what good feedback should look like.

Code Review
Mark the problems in each line of code using the rubric provided.

01)  def addem(f):
02)      x1 = open(f).readlines()
03)      x2 = [x for x in x1 if x.strip()]
04)      changes = 0
05)      for v in x2:
06)          print('total', total)
07)          tot = tot + int(v)
08)      print('total')
1. poor variable name	2. use of undefined variable
3. missing return value	4. unused variable
Exercises
