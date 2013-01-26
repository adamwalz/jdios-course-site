---
layout: base
title: 2013 Syllabus
---
#Spring 2013 Administrative Details

##Instruction
**Instructor**: Adam Walz  
**Email**: <adamwalz@jdchs.org>  
**github**: [www.github.com/jd-adam](https://github.com/jd-adam)  
**twitter**: [JDAdamwalz](https://twitter.com/JDAdamwalz)

**Website**: [jdios.jdchs.org](http://jdios.jdchs.org)

**Meeting Times**: Wednesday 1:40-2:40, Friday 3:00-4:00 (both days are required)

-------------------------------

##Course Material
Introduction to mobile programming, Objective-C language syntax,
memory management, static code analysis, custom classes, computer graphics,
mobile application lifecycles, Model-View-Controller design patterns,
designing for re-use, web service integration, RESTful web services,
hardware interaction, power as a first-order design constraint,
and source code management with git and github.

##Course Outcomes
At the conclusion of this course, students should be able to:

1. Design and implement applications on a mobile device using the
    model-view-controller design pattern.
2. Understand and be able to quantify the effects of different software
    design decisions on mobile device battery life.
3. Design and implement self-contained, reusable user interface elements
    that meet or exceed the design criteria of existing industry standard
    user interface libraries.
4. Understand how to use distributed source code management tools as an
    individual programmer and as part of a team.
5. Possibly make money by putting your work in this course on the
    App Store&trade;.

##What to expect
-------------------------------

####Work load
We will try to tailor the programming workload so that projects can be completed
during class time. This will allow for students without an iOS programming
environment (OS X, Xcode, etc.) to not be disadvantaged. To this end, this course
will be "flipped" from a normal lecture course. Lectures will be recorded a posted
to the course webpage. It will then be your responsibility to watch the lectures
as homework and come to class ready to implement the ideas from that lecture.

- 2[^1] hours in class per week (working on programming assignments)
- 2 hours of lectures per week
- 1 hour reading documentation per week

####Programming Assignments
Programming assignments will be due weekly starting in the third week of classes. 
This course will utilize the source control management (SCM) system git, which is
integrated into the development environment Xcode. All code will be stored on
the git servers at github.com and this site will be used to turn in all assignments.

After the due date, any code pushed to your online repository will be graded. We
will talk more about the details of this as well as the course late policy in 
the first few weeks of class. The syllabus will be updated accordingly at that
time.

We will also use github for handing out assignments. Each week I will make a
"pull request" to your repository which includes a partial implementation of that
weeks assignment. You will then merge that request into your code base and finish
the implementation.

The nature of a programming course is that not all students may finish each
assignment. Due to this, I will work hard to ensure that back-to-back assignments
do not depend on each other. Therefore, not finishing an assignment will not be
cause to miss subsequent assignments. After the late deadline, I will also post
my solution, which you can merge into your own repository if desired.

####Video Lectures
Each week, two video lectures will be released on the class website. These lectures
will cover iOS, Objective-C, and software development concepts. Most will include 
slides and a coding session to make the concepts more concrete. They must be watched
before the next class persiod. The period for which they are due will be indicated on
the course website.

####Quizzes
At the beginning of each class period, a quiz will be administered which covers the
video lectures assinged. This quiz will likely be simple and only assess whether the
lectures were watched or not. Having said that, the quizzes are worht a substantial
percentage of your course grade. This is necessary becuase the concepts cannot be
learned in such a short period of time by just hacking. The quizzes assess theoretical
knowledge, while the projects assess practical knowledge.

####Semester Grading

<table border="1" cellpadding="5">
  <tr>
    <th>Programming Assignments</th>
    <td>50%</td>
  </tr>
  <tr>
    <th>Quizzes</th>
    <td>20%</td>
  </tr>
  <tr>
    <th>Tests</th>
    <td>10%</td>
  </tr>
  <tr>
    <th>Final Exam</th>
    <td>20%</td>
  </tr>
</table>

For each quarter, this breaks down to Programming Assignments being worth 62.5%, Quizzes worth 25%, and Tests worth 12.5%. 

####Academic Honesty
Each student in coming into this course at a different level of experience and
your personal tastes will show through in your projects. Except when explicitly 
designated otherwise, each assignment is to be done individually.

Here is a list of do's and don'ts for what is considered acceptable behavior for
individual work.

<table border="1" cellpadding="5">
  <caption align="bottom">This list is subject to change with notification</caption>
  <tr>
    <th>Do's</th>
    <th>Dont's</th>
  </tr>
  <tr>
    <td><ul>
      <li>Talking at a high level with classmates about your implemenation</li>
      <li>Using third party libraries and toolkits</li>
      <li>Using code from the industry standard API collection</li>
      <li>Copying code from Apple's documentation</li>
    </ul>
    </td>
    <td><ul>
      <li>Copying another student's work</li>
      <li>Programming side-by-side while talking about the solution</li>
    </ul>
    </td>
  </tr>
</table>

All bullets in the _Do's_ header must be documented and sourced if used. Most
third party libraries and toolkits require that your re-print their licenses. 
In this course, we will require that each project has a .LICENSE file that 
contains all of the licenses of anything that you have used, as well as your 
own license. 

_Warning_: I have been teaching at the University level for the past two years
and have become good at spotting duplicate solutions. If you have any questions
about what constitutes acceptable behavior please ask.

Academic dishonesty will receive a zero on the current week's assignment and be
required to re-do the assigned work.

####Attendance
1. This zero-hour course requires two (2) hours[^2] of in-class work per week and meets each week on Monday and Wednesday. Class will be in session from 1:40 to 2:40 on Wednesdays and 3:00 to 4:00 on Fridays.
2. Attendance will be taken on A and C days. Any attendance on days between A and C days will be entered on the following A or C day.
3. The school policy of seven (7) or more Unexcused absences leading to an F grade for the quarter will be followed.


##About the Instructor
Adam Walz is a former student of Juan Diego Catholic High School and is currently
enrolled in the masters program at the University of Utah studying Computer
Science with an emphasis in Artificial Intelligence and Maching Learning. He has
served as a teaching assistant in the School of Computing for the past five
semesters teaching Introduction to Computer Science I and II, Discrete Mathematics, 
and Probability and Statistics. Adam has held positions as a software developer
in iOS mobile development and is excited to relay his experiences on to his students.

-------------------------------

#Syllabus
<table border="1" cellpadding="10">
  <caption>Quarter 3 - iOS 5 and Single-User Applications</caption>
  <tr>
    <th>Week</th>
    <th>Topic(s)</th>
    <th>Assignment</th>
  </tr>
  <tr>
    <td>1</td>
    <td>Model, View, Controller</td>
    <td>None</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Objective-C Basics</td>
    <td>None</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Views and Gestures</td>
    <td><a href="/assignments/2013/01/21/assign-1">Real World MVC</a></td>
  </tr>
  <tr>
    <td>4</td>
    <td>Table View and Page View</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Storyboarding, Navigation, Scrolling</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Data Persistence</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>7</td>
    <td>Web Services</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>8</td>
    <td>Camera and Alerts</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>9</td>
    <td>Universal Apps</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>10</td>
    <td>Push Notifications</td>
    <td>TBA</td>
  </tr>
</table>

<table border="1" cellpadding="10">
  <caption>Quarter 4 - iOS 6 and Multi-User Applications</caption>
  <tr>
    <th>Week</th>
    <th>Topic(s)</th>
    <th>Assignment</th>
  </tr>
  <tr>
    <td>1</td>
    <td>iOS 6 Features</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Multi-User: Database Integration</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Multi-User: Syncing with iCloud/Google</td>
    <td>TBA</td>
  </tr>
  <tr>
    <td>4-8</td>
    <td>Class Choice</td>
    <td>Final Projects</td>
  </tr>

</table>


[^1]: If more time is required for assignments outside of the two hours of allotted class time, the instructor will be available for a short time after class ends. Otherwise, students should find a time in the lab either before school, after school, or during lunch to finish programming assignments.
[^2]: Same as 1