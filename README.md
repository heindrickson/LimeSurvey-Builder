# SurveyBuilder4LimeSurvey
Prompt to instruct an LLM to act as an assistant in order to generate the definition of a questionnaire (survey) that can be saved as a TSV file and imported into LimeSurvey. 
<br><br>

# Motivation
LimeSurvey is a very powerful open-source software for conducting online surveys. It allows you to build, publish, and run surveys, as well as collect, analyze, and export responses.  
The tool supports dozens of question types and has advanced features like conditions, logical branching and question validation.

However, creating a survey directly in the LimeSurvey app can be pretty tedious and often somewhat tricky.  
So, it's natural that we looked to use prompts with generative AI to make thata task easier.  
We found that the most effective way to get AI to create a valid survey definition is to instruct it to use the Tab Separated Value format, supported by LimeSurvey. 
<br><br>

# Why not an Assistant/Agent?
The ideal way to use this prompt WOULD be via an assistant such as "GPT" (OpenAI), "Gem" (Google), or "Agent" (Microsoft Copilot).  
However, none of these providers currently offer affordable (low-cost) subscription plans that allow individuals to publish this type of LLM-based application.  
For this reason, we have decided to publish the prompt and basic instructions in this repository, so that anyone with a basic LLM chat subscription can copy and use the prompt directly in the chat interface.  
<br><br>

# The prompt

<br><br>


# How tu use

<br><br>


# Conversation starters and other possible subsequent prompts
1. Hi, explain to me in detail what you do and how we should interact.
2. Show me an example of a survey mockup in DOCX format, so I can create another one based on it, tailored for my own survey.
3. Hi, help me create a new survey in Limesurvey. I'll send you a document that has a mockup of the survey questionnaire. It simulates the structure of groups and questions, and also has instructions about conditional presentation (branching) and validations. Infer everything from the file, only ask me something if you can't figure it out.
4. Hi, explain to me in detail how I can adjust and save the TSV content when you only display it on the screen (without a download link). Describe how to do this via Notepad++ and in VS Code.
<br><br>


# Example of a survey mockup

<br><br>


