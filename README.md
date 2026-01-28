# EC34 - Data Science for Economists

Spring 2026

M/W 1:15-2:30 Location: SCI 183

**Prof. Aleksandr Michuda**\
Email: amichud1\@swarthmore.edu

Office: Kohlberg 220

Office Hours: MW 12-1 and by appointment

TA:

Aayma Hamid [ahamid1\@swarthmore.edu](mailto:ahamid1@swarthmore.edu)

Matvey Ivanov [mivanov1\@swarthmore.edu](mailto:mivanov1@swarthmore.edu)

Clinic Hours: Kohlberg 116 Tuesdays 7-9pm

**Course objectives:** The course introduces students to basic practices and tools that will enhance your ability to conduct empirical research and analysis in microeconomics in a data-rich world. By the end of the course, students will be proficient in various data management, visualization and quantitative techniques necessary to efficiently conduct independent research. The course format is “hands-on” and students will conduct most of their work on their personal computers using python and VSCode.

The skills you learn may be applied to other languages and programming (such as in R and Stata).

**Pre-requisite:** EC 31

## **Expected outcomes:**

1.  Proficient in reproducible python programming
2.  Capable of gathering, manipulating and visualizing various types of data effectively for research purposes
3.  Capable of employing simulation and resampling methods in applied research

## **Grading:**

Students will be graded on class participation (10%), homework assignments (10%), a Midterm (30%) and a final reproducible project (20%+20%+10%). 20% will be for the submission of a short project description, 20% will be for the clarity and quality of your presentation of the work and the remaining 10% will be based on the grading of each other's work.

## Reproducible Project

The largest part of your grade will be based on a project that you will work on groups of 3-4 people. You will be expected to use the tools you learned here and write up an analysis. A good research idea will include 2/3 components:

1.  Tight visualizations

2.  Data analysis and cleaning using regression, prediction

3.  Extraction of interesting data from the web or other sources.

Once you submit your final project, I will assign a random student in the class not in your group to review the clarity and reproducibility of your project. Students will evaluate each other's work based on three key components:

1.  How organized is package. Does data, code and output have dedicated folders?
2.  How easy is it to replicate? Is there a README that outlines how to run the code and generate the output?
3.  How easy it is to follow the code and understand what's happening?

The grade from this will be the average of the grades by each individual. Extra credit will be given to the whole class for any student that can write simulation code in Python that illustrates an individual student's optimal strategy on how to grade. This simulation must model a student's tradeoffs on how to grade and be a rich enough model that it convinces me.

## **Homework**

Homework will be due a week after it is assigned. These will involve more difficult empirical exercises. You should start these early. During the weeks when there is no problem set due on Friday, please stay engaged with Moodle, as there may be activities or readings that will help solidify your understanding of the material. All homework assignments should be submitted via Moodle as a replication package (i.e. .zip file containing all code and data necessary to reproduce your results).

## Assignments

In the `assignments` folder, there are assignments that I will make us do during class. These are not graded, but do provide a useful way to practice the material we are learning in class as well as material that will help you for the midterm.

## Special Topic

The last lecture of the course will be a special topic that I will write up based on what students want. I will send out a poll to see which topic would be most interesting. Topics include, but are not limited to:

2.  More machine learning

3.  Google Earth API

4.  Advanced web scraping with Selenium

## Policies

Make-up exams will not be given unless you provide documented evidence of a circumstance that merits rescheduling (e.g., illness). If the conflict is known beforehand, you must make arrangements with me well before the exam date. Late problem sets will only be accepted with permission from me, will suffer a grade penalty, and will not be accepted once the solutions have been posted on Moodle.

If you believe you need accommodations for a disability or a chronic medical condition, please visit the Student Disability Services website for details about the accommodations process. Since accommodations require early planning and are not retroactive, contact Student Disability Services as soon as possible. You are also welcome to contact me privately to discuss your academic needs. However, all disability-related accommodations must be arranged, in advance, through Student Disability Services.

Within this class, you are welcome to use foundation models in a totally unrestricted fashion, for any purpose, at no penalty. However, you should note that all large language models still have a tendency to make up incorrect facts and fake citations, or do math wrong. You will be responsible for any inaccurate, biased, offensive, or otherwise unethical content you submit, regardless of whether it originally comes from you or a foundation model. If you use foundation models or LLMs, its contribution must be acknowledged; you will be penalized for using it without acknowledgment.

The university's policy on plagiarism still applies to any uncited or improperly cited use of work by other human beings, or submission of work by other human beings as your own.

## **Communication:**

Moodle will have the basic information on the course, such as the syllabus, and course calendar. But communication will take place on Slack. Slack is a great way to collaborate, ask questions and chat on relevant topics. If you have a question on the course, feel free to Slack me or the TA, and we'll answer as soon as possible. You should also use the platform as a way to communicate and work with each other to try to solve problems. Sign up for the slack channel here:

<https://join.slack.com/t/ec34datascien-hls6144/shared_invite/zt-3mhok01xj-eSAxEOzaxnRmvGMTb3DiSQ>

## **Course Materials:**

Course materials can be accessed on github. We will learn how to use GitHub in this course, but for now, you can go to the repository link (<https://github.com/amichuda/ec34-ds-for-econ>), click on the green "Code" button and click "Download Zip" to download all course materials. Note that if materials are updated, you will need to re-download. That's one of the reasons why learning Git is so useful.

**Schedule and topics:**

| \# | Date | Topic | Assignments | Relevant Folder(s) |
|---------------|---------------|---------------|---------------|---------------|
| 1 | Jan 21 | Getting started with Python 1 |  | `lectures/intro-python` |
| 2 | Jan 26,28 | Getting started with Python 2, Imports, Numpy, loops, vectorization and parallelization 1 |  | `lectures/intro-python`, `lectures/import-and-numpy` |
| 3 | Feb 2,4 | Imports, Numpy, loops, vectorization and parallelization 2, pandas - Cleaning and manipulating tabular data 1 |  | `lectures/import-and-numpy`, `lectures/pandas` |
| 4 | Feb 9,11 | pandas - Cleaning and manipulating tabular data 2, Visualizing Data and Making Visualization Interactive |  | `lectures/pandas`, `lectures/visualization` |
| 5 | Feb 16,18 | Manipulating text, Efficient coding practices | HW1 | `lectures/text-analysis`, `lectures/efficient-coding` |
| 6 | Feb 23, 25 | Web scraping with beautiful soup and using APIs, Manipulating and visualizing spatial data with geopandas | HW1 Due | `lectures/web-scraping`, `lectures/geospatial-analysis` |
| 7 | Mar 2,4 | Version Control, Midterm |  | `lectures/git-workflow` |
| 8 | Mar 9,11 | Spring Break |  |  |
| 9 | Mar 16,18 | Reproducibility, DAGs | Short Project Description | `lectures/dynamic-documents`, `lectures/dags` |
| 10 | Mar 23,25 | Monte Carlo, Regression (RDD, DiD) |  | `lectures/monte-carlo`, `lectures/causal-regression` |
| 11 | Mar 30, Apr 1 | Machine Learning | HW2 | `lectures/machine-learning` |
| 12 | Apr 6, 8 | Neural Networks, Causal Machine Learning | HW2 Due | `lectures/neural-net`, `lectures/causal-machine-learning` |
| 13 | Apr 13,15 | Image Analysis with open-cv, OpenAI and LLMs | HW3 | `lectures/computer-vision`, `lectures/llms` |
| 14 | Apr 20,22 | Maximum Likelihood in Python, Special Topic (TBA) | HW3 Due | `lectures/gmm-mle` |
| 15 | Apr 27,29 | Wrap-up; Group Presentations |  |  |
| 16 | TBD | Final Exam |  |  |
