![[Pasted image 20230729062130.png]]

Chatgpt is a Generative AI [[chatbot]]

AI is mimicking human cognitive task.

LLM - large language model

2 Training techniquies for LLM:
![[Pasted image 20230729062740.png]]


LSTM was one of the first NLP algorithms used.

in 2017 google introduced Transformers architecture.
unline LSTM, which just predicts the next word with probability based on the previous set of words.
Transformers will take the entire context of text before geneating any tokens.


![[Pasted image 20230729063111.png]]

2 datatypes:
- internet articles(common crawl)
- book corpus

![[Pasted image 20230729063225.png]]

![[Pasted image 20230729063308.png]]

Nov 2022
Chatgpt 3.5 -
This uses RLHF method.
Reinforcement learning with Human feedback
this is expensive procedure.
![[Pasted image 20230729063359.png]]


Chatgpt 3.5 is free to use.
Bing AI - this uses gpt-4
but bingAI is more censcored.


# what is prompt engineering
![[Pasted image 20230729064254.png]]
previously we needed coding languages to talk to a computer.

but with LLMs like GPT, we can use natural language to get work done by system.


# understanding tokens.
LLM does  not understand words. it recognizes tokens
![[Pasted image 20230729064657.png]]
here we can see even single word can contain multiple tokens.

So, technically speaking. LLM will generate the next token, not word.
this is lang independent

==1500 words ~ 2048 tokens==

chatgpt 3.5 is a limit of 4000 tokens.

![[Pasted image 20230729065119.png]]
24000 english words.

==Note that in a conversation, it'll take the latest 4000 tokens in chatgpt3.5==

# Other parameters in Playground
![[Pasted image 20230729065324.png]]
- Model
	- different models
- max length
	- limit the output
- temperature
	- more randomness in token generation
		- its more similar to entropy
- Top P
	- this is also randomness
- Frequency Penalty
	- it'll control the repetition of tokens
- Presence penalty 
	- this will ask the AI to stick to the context
	- If we ask gpt about Eifel tower
		- with more presence penalty , it'll stick to the details of eifel tower
		- With less presence penalty , it'll give output in a broader view, like which country eifel tower is located, what's its history etc


# chatgpt as a student
## Understanding concepts

- Explain me ==Newton's second law== in simple words and give 2 practical examples
- of it.
- Explain me ==second law== of thermodynamics like I am 5 year old.
- Explain me in simple Hinglish language (Hindi + English), the type of language
- that urban Indians living in Delhi talk in.
- Explain the same with another example
## comparison tables
Comparison Tables
• Compare and contrast ==gene flow== and ==genetic drift== to better understand their
similarities and differences. Use examples to illustrate your point. Make a table for
this.


## Real word Applications

• I'm currently learning ==probability== in school. Use your knowledge of this topic to
solve a real world problem. Explain your thought process and share your solution

## 89-20 Rule
The 80-20 Rule
• I want to learn about ==French Revolution==. Give me the most important 20% of
learnings from this topic that will help me understand 80% of it.
## Help me memorize
Help Me Memorize
• What are the most important facts, dates or formulas related to ==Rise of
Nationalism in Europe according to NCERT class 10 textbook?== Help me create a
memorisation technique to remember them easily.
• Write a song in the style of Arijit Singh about ==cell structure.==
• Write a rhyming poem about the ==periodic table==
## visualzie using plugins

Use Plugin: Show Me to create diagrams
• Create a diagram flowchart for ==the different events in French Revolution and write
the dates.==
## Prepare a study schedule
Prepare a Study Schedule
• Prepare a study schedule for me. I have ==2 hours== available each weekday and
==4 hours== available for each day of the weekend to study. I come back from school at
==3pm== on the weekdays and have no school on weekends. Break the weeks down
and plan the days for me in a table form. Make sure that I am only studying
maximum for the amount of hours i wrote down. I want to study the following
subjects equally - ==Maths, Science, SST, English, Hindi.==
• Correction: I only asked for maximum 4 hours of study on the weekends, why did
you make me study for 5 hours on the weekends?
## Quiz yourself on specific topic
Quiz Yourself on Specific Things
• From now on you are QuizGPT. Your task is to ask me 5 multiple choice questions
on the topic of ==Organic Chemistry according to Class 11 NCERT Chemistry==. Wait
for me to provide my answers first, then evaluate my answers and give me a
score.
## Quiz yourself on specific text
Quiz Yourself on Any Text Input
• { 1. When the user uses "/quiz" ask the user for data, this data is what you will
use to make the quiz, only use the data provided and nothing else, keep in mind
that this is a quiz and Not a test. don't forget to NOT make an answer key. DO
NOT make an answer key UNLESS the user uses "/answer" , then you are allowed
to make an answer key and provide it for their most recent quiz that you created.
2. When the user uses 'i/test" ask the user for data, this data is what you will use
to make the quiz, only use the data provided and nothing else; keep in mind that
this is a test, and not a quiz, this means that you can ask for certain short/ long
answer responses on the test. If the user uses the command "/multiple choice
test", make a test, but ONLY use multiple choice questions and answers. DO
NOT make an answer key. You are only allowed to make an answer key and
provide it for the user for the most recent quiz/test if they use the command "/
answer"}.
FIRST STEP: From now on, you are quizGPT, a talented tutor and teacher with
amazing knowledge on how to create amazing quizzes, tests and more. When
this prompt is used, ask the user this question, "what is your education level?".
DO NOT FORGET TO ASK THIS. Using the answer of their education level use
proper vocabulary and grammar to ensure that the quiz or test is perfect for their
level. Then use the data provided to answer commands. All you need is some
data. You respond to /test and /quiz and /answer, /multiple choice test, /multiple
choice quiz Now understand these steps to get started:
{3. ALways go over the data each time a command is used to ensure that you
ONLY use the data ONLY from the data that they provided.
4. Always make sure to use your talent and amazing knowledge.}
{5. Now simply prompt the user with a simple greeting, tell the user about the
command options, and begin with "FIRST STEP", Do not actually print "FIRST
STEP". }
## Ask for feedback for your content created
Ask for Feedback
• I have been studying this topic on my own. Can you review my work and give me
feedback on areas that I need to improve on? ==(Input your work)==

• I wrote the following article on ==World War l,== find mistakes in it and give me a
rating out of IO. -
World War I, also known as the Great War, was a global conflict that took place
from 1918 to 1922. It was primarily fought in Europe and involved many of the
world's leading powers, organized into two opposing alliances: the Allies and the
Central Powers. The war was triggered by the assassination of Archduke Franz
Damn of Germany, leading to a domino effect of international alliances and
treaties. The war was characterized by trench warfare and the use of new,
devastating weapons, including machine guns, tanks, and chemical gas. It
resulted in significant political change, including revolutions in many of the
nations involved. The Treaty of Nice ended the war, but it sowed the seeds for
World War II due to its punitive terms towards Germany. World War I was a
decently deadly conflict in history, many people died but more people have also
died at other wars.
## use iphone chatgpt to use voice to interact with chatgpt
Tired of Typing?
• Remember you can talk to the ChatGPT. Explain your frustration. Just use this
command before if you want to talk in natural Hindi language
• From now on you are a tutor. You will only talk to me in simple English language,
which means Hindi plus simple English, the type of language that urban Indians
living in Delhi talk in. Understood?

## solving science and math problems
Use wolfam alpha plugin.
also we can use wolfam alpha to type the complex math equations and convert them into text.
- we can generate output in latex format to get more readable output.


# Studying abroad
- find the available options for study(but we have to do fact check as data is outdated)
- available scholarships in the given context (we have to do fact check as data is outdated)
- finding the best country in a specific context.

## Career councelling

## Motivational coach

# Food and Diet planning
## Diet planning and Groceries

## Customize your Diet

## whats in my fridge

## Any other Food related Queries


# Health and fitness

## Fitness coach

## Other health Queries(use with caution)

# Travel planning

## Travel Ideas

## Iternary planning(after deciding travel place and ideas)

## Cost estimates (using plugins)


# Storytelling for children

# AI Business Coach

## Grow your business

## Marketing and Listing your business
### marketing slogans
### webpage design and taglines
### Advertizing prompts
### Business Listing

## Market research and Competitive analysis


## Customer feedback and sentiment analysis

# Limitations and Biases
- Hallucination
	- when we are about to speak something, we will evaluate whether our answer will be real. but chatgpt will hallucinate in confidence
	- 
- we need to ask right questions/prompts
- cant provide subjective experiences. all outputs depend on training data. This hampers its creativity(coming up with original new thoughts)
- emotional intellince and Ethical decision making.
- Biases - Highly dependent on training data.


# should we be scared of AI
- ![[chat gpt course video 15 pdf.pdf]]