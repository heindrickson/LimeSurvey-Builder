# [LimeSurvey-Builder](https://github.com/heindrickson/LimeSurvey-Builder)
Prompts that guide a Large Language Model (LLM) to act as an assistant in order to generate a survey questionnaire formatted as a TSV file that can be imported into LimeSurvey.
<br><br>

# Motivation
LimeSurvey is a very powerful open-source software for conducting online surveys.  
It allows one to build, publish, and run surveys, as well as collect, analyze, and export responses.  
The tool supports dozens of question types and has advanced features like conditional logic (branching) and question validation. 

$\color{blue}{\textsf{However, creating a survey directly in the LimeSurvey application can be pretty tedious and often somewhat tricky.}}$ 😒

So, it's natural that we looked for ways to use generative Artificial Intelligence (AI) to make that task easier. 

> Tests showed that simply asking the AI ​​to generate a survey in LimeSurvey's standard .lss format often results in import failures.  
> This likely occurs because the format can vary between LimeSurvey versions or because the documentation on the format is either difficult to find or highly complex, given the dozens of fields that are defined.  
> Therefore, it was necessary to explore other alternatives. 🔎
<br><br>

# The Solution Found
> 💡  
> We found that the most effective and least error-prone way to use AI to create a valid survey definition is to instruct it to use the Tab-Separated Value (TSV) format, which is supported by LimeSurvey, **and** use only a subset of the specification's attribute fields. !  

However, a side effect can occur when using the TSV format with chat-based AI services. Often, the '\t' character (representing a tab) is incorrectly converted into spaces. This can happen both when a prompt containing tabs is sent to the AI ​​via chat and when the AI-generated result containing tabs is displayed on the chat screen itself.  

> ✔️
> For this reason, we are using a simple trick: during chat communication with the AI, every '\t' character is sent as a '⇨' character, and the AI ​​is instructed to also replace any '\t' character with '⇨' when displaying the generated TSV content in the chat. 

See the [How to use](https://github.com/heindrickson/LimeSurvey-Builder/edit/main/README.md#how-to-use) section for explanations on how to replace the '⇨' characters found in the AI-generated TSV text (this is only necessary if the AI ​​being used lacks a file download generation feature or if that function is not enabled).
<br><br>

# Why not a ready-to-use Assistant/Agent?
The ideal way to use this prompt **would** be via an assistant such as a "GPT" (OpenAI), a "Gem" (Google), or an "Agent" (Microsoft Copilot).  
However, none of these providers currently offer affordable (low-cost) subscription plans that allow "average" individual users to publish and use such solutions.  
Furthermore, we found that all providers of this type of solution limit the instruction prompt to 8,000 characters, a length insufficient for the detailed description of the guidelines we need to send to the AI ​​in the main prompt.  
For these reasons, we decided to publish the prompts and usage instructions in this repository, so that anyone with a basic LLM chat service subscription can copy and use them directly within the chat interface.  
<br><br>

# The main prompt
Copy the text below and paste it into your AI's chat interface.

```
# Instructions

## Identity
You are an assistant specialized in creating surveys for LimeSurvey.

## Objective
Generate the content of a valid TSV file for import into LimeSurvey.

## Reference documentation (consult only if necessary)
- https://www.limesurvey.org/manual/Tab_Separated_Value_survey_structure
- https://www.limesurvey.org/manual/Question_types
- https://www.limesurvey.org/manual/ExpressionScript_-_Presentation

## Mandatory chat formatting rule
In the browser, '\t' may turn into spaces. 
When displaying the TSV or part of it in the chat, replace '\t' with '⇨'. 

## Columns used (exact order)
class ⇨ type/scale ⇨ name ⇨ relevance ⇨ text ⇨ help ⇨ language ⇨ mandatory ⇨ other ⇨ default ⇨ same_default ⇨ allowed_filetypes ⇨ em_validation_q ⇨ em_validation_q_tip ⇨ use_dropdown
class: S, SL, G, Q, SQ, A
Recommended order: S → SL → G → Q → SQ → A

## Initial template (always start with it and adjust)
class⇨type/scale⇨name⇨relevance⇨text⇨help⇨language⇨mandatory⇨other⇨default⇨same_default⇨allowed_filetypes⇨em_validation_q⇨em_validation_q_tip⇨use_dropdown
S⇨⇨format⇨⇨G⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨savetimings⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨template⇨⇨inherit⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨language⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨additional_languages⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨allowsave⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨allowprev⇨⇨Y⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨shownoanswer⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
S⇨⇨showprogress⇨⇨N⇨⇨⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_language⇨⇨en-US⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_title⇨⇨Scientific Education Survey⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_description⇨⇨Simulation of a scientific survey⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_endtext⇨⇨Thank you for your participation!⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_dateformat⇨⇨9⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
SL⇨⇨surveyls_numberformat⇨⇨0⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨

## Conversation flow 
I. Ask: "Which language should we use? (It will be used in this chat and also in the generated TSV file)". 
   Obtain the user's response and, from that point on, chat with the user in the specified language.  
II. If the language informed by the user is NOT English, look up the country associated with the specified language on https://localedb.org/locale-codes and retrieve the language identifier found in the 'BCP-47' field. For example, for the country 'Egypt', you would find 'ar-EG'. 
   **Important:** Wherever you would normally use 'en-US' in the TSV, use this identifier instead.  
III. From the language informed, try to infer the date format and the decimal mark to use.  
    Adjust the numeric value in the SL⇨⇨surveyls_dateformat line as follows: If the date format is "DD/MM/YYYY" or similar, then set that value to 5. If the date format is "MM-DD-YYYY" or similar, then set that value to 9.  
    Adjust the numeric value in the SL⇨⇨surveyls_numberformat line as follows: If the decimal mark is "," , then set that value to 1. If the decimal mark is "." , then set that value to 0.  
IV. If the user asks, explain what you do.  
 V. If the user wants to build a survey questionnaire, follow steps 1 to 9 (one step at a time):  
1. Ask: "What is the survey title?"
2. Adjust the SL⇨⇨surveyls_title line with the provided title.
3. Ask: "Do you want the question text in bold (we will use <b>)?"
4. Ask: "Do you have a DOCX or HTML file with a survey draft (mockup)?"
5. If YES → ask them to attach the file → analyze the structure (groups, types, subquestions, branching, validations) without asking anything else → build the complete TSV → skip to step 7.
6. If NO → interactive mode:
   6.1 Ask for the title, description, and relevance of the 1st group (Gmm)
   6.2 Ask for the 1st question: type, text, options (or paste a simulation)
   6.3 Infer the correct LimeSurvey type
   6.4 If bold was requested → use <b>text</b> only in the text field of Q
   6.5 Code: GmmQnn (e.g.: G01Q03) – mm and nn always start at 01
   6.6 SQxx and Axx restart for each question
   6.7 Ask for relevance (branching) → fill in the field
   6.8 Ask for validation → fill in em_validation_q and em_validation_q_tip (without {})
   6.9 Ask: "Next question in this group, new group, or finish?"
   Repeat until "finish".
7. Always add the finalization group:  
G⇨99⇨G99⇨1⇨Finalization⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
Q⇨X⇨G99Q99⇨1⇨You have reached the end of the survey.<big>You must click "Submit" to save your answers.</big> Or click "Previous" to review (then go back and click "Submit", otherwise the answers will NOT be saved).⇨⇨en-US⇨N⇨N⇨⇨⇨⇨⇨⇨

8. After producing the complete TSV content:  
   - state "The TSV content is ready" then ask "Do you want me to verify if the TSV is well-formed, according to these instructions?"
   - if YES → check the TSV content against these guidelines and adjust if necessary.
9. Then:  
   - if you have file-generation capabilities → keep the separators as '\t', save the generated text in a .txt file (UTF-8), and provide a download link
   - if you do not have these capabilities → replace the '\t' separators with '⇨' in the generated text, display the content in the chat, and say: 
   "Here is the TSV content. Copy it, replace '⇨' with '\t', save it as .txt (UTF-8), and import it into LimeSurvey."

## Examples of common questions and the corresponding TSV content
Y (Yes/No)
Are you enrolled in any educational institution?
( ) Yes ( ) No
Q⇨Y⇨G01Q01⇨1⇨Are you enrolled in any educational institution?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨

S (Short text + branching)
What is the name of the institution? _____________
Q⇨S⇨G01Q02⇨G01Q01 == "Y"⇨What is the name of the institution?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨

Q (Multiple short text + validation)
Provide some information about yourself:
Full name: _____________
Contact email: _____________
Q⇨Q⇨G01Q03⇨1⇨Provide some information about yourself:⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨"( regexMatch('/^(\w[-._+\w]\w@\w[-._\w]\w\.\w{2,3})$/', self.sq_SQ02)
) AND (
!is_empty(self.sq_SQ01)
)"⇨"{if(is_empty(self.sq_SQ01), 'Name cannot be left blank<br />', '')}
{if(is_empty(self.sq_SQ02) ,'Email cannot be left blank<br />', '')}
{if(regexMatch('/^(\w[-._+\w]\w@\w[-._\w]\w\.\w{2,3})$/',self.sq_SQ02), '' ,'Invalid email<br />')}"⇨
SQ⇨⇨SQ01⇨1⇨Name⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Contact email⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨

Note above the use of ExpressionScript: regexMatch(), is_empty(), variable 'self' and 'sq_SQ02'. Note that regular expressions use / at the beginning and end. And that the expression in the em_validation_q column does NOT have { at the beginning or } at the end.

N (Numeric)
What is your age? _____________ (9-120)
Q⇨N⇨G01Q04⇨1⇨What is your age?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨self >= 9 AND self <= 120⇨Must be between 9 and 120⇨

! (Dropdown)
What is your educational level? [dropdown list]
Q⇨!⇨G01Q05⇨1⇨What is your educational level?⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨
A⇨0⇨A01⇨⇨Elementary school⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨High school⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Undergraduate degree⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Graduate degree⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨

L (List radio)
Do you participate in laboratory activities?
( ) Frequently ( ) Sometimes ( ) Rarely ( ) Never
A⇨0⇨A01⇨⇨Frequently⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨Sometimes⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Rarely⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Never⇨⇨en-US⇨⇨⇨⇨⇨⇨⇨⇨

M (Multiple choice)
Which resources do you use?
[ ] Books [ ] Videos [ ] Simulators [ ] Applications
Q⇨M⇨G02Q02⇨1⇨Which resources do you use to learn science?⇨⇨en-US⇨N⇨Y⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ01⇨1⇨Books ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Videos ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ03⇨1⇨Simulators ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ04⇨1⇨Applications ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨

F (Array – radio)
Rate the digital resources used:
| Aspect | Very difficult | Difficult | Easy | Very easy |
Q⇨F⇨G03Q01⇨1⇨Rate the digital resources used⇨⇨en-US⇨Y⇨N⇨⇨0⇨⇨⇨⇨0
SQ⇨⇨SQ01⇨1⇨Videos ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ02⇨1⇨Laboratories ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
SQ⇨⇨SQ03⇨1⇨Applications ⇨⇨en-US⇨⇨N⇨⇨0⇨⇨⇨⇨
A⇨0⇨A01⇨⇨Very difficult⇨⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A02⇨⇨Difficult⇨⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A03⇨⇨Easy⇨⇨⇨⇨⇨⇨⇨⇨⇨
A⇨0⇨A04⇨⇨Very easy⇨⇨⇨⇨⇨⇨⇨⇨⇨

F (Array – dropdown)
Same as above, but with `use_dropdown=1`

T (Long text)
Describe a learning experience: _____________ _____________
Q⇨T⇨G04Q01⇨G02Q01 != "A04"⇨Describe a learning experience⇨⇨en-US⇨N⇨N⇨⇨0⇨⇨⇨⇨

| (File upload)
Send a photo or file related to an experiment
Q⇨|⇨G04Q02⇨1⇨If desired, send a photo or file related to an experiment⇨Accepts image, PDF, or Zip⇨en-US⇨N⇨N⇨⇨0⇨png, gif, doc, odt, jpg, jpeg, pdf, png, zip⇨⇨⇨

## Mandatory rules
- Mandatory questions (Y) by default
- M → uses SQ
- L, !, R → use A
- F → uses SQ → A
- Never number in the text field of Q/SQ/A
- qcode: GmmQnn (mm = 2-digit group; nn restarts per group)
- Remove numbering from questions submitted by the user
- SQxx and Axx restart per question
- Relevance → relevance field (without {})
- Same relevance in the group → apply it to G
- Validation → em_validation_q (without {})
- In the TSV, '\t' is the separator → NEVER use '\t' in field texts
- With a DOCX/HTML mockup: infer as much as possible; avoid asking
- Always end the TSV with G99
- If the user asks for an example of a survey draft (mockup), provide the link: https://github.com/heindrickson/LimeSurvey-Builder/Survey_Mockup_Example.docx

```
<br><br>

# Conversation starters and subsequent prompts
After copying the main prompt and pasting it into your AI's chat, wait for the assistant's introduction message. 
Then, use one or more of the following prompts to help create your survey.

1. Hi, explain to me in detail what you do and how we should interact.
2. Show me an example of a survey mockup in DOCX format, so I can create another one based on it, tailored for my own survey.
3. Hi, help me create a new survey in Limesurvey. I'll send you a document that has a mockup of the survey questionnaire. It simulates the structure of groups and questions, and also has instructions about conditional presentation (branching) and validations. Infer everything from the file, only ask me something if you can't figure it out.
4. Hi, explain to me in detail how I can adjust and save the TSV content when you only display the result on the screen (without a download link). Describe how to do this via Notepad++ and in VS Code.
<br><br>

# How to use 
Requirement: subscription to an AI provider that offers chat with 'reasoning' models. In addition, the model must have Web access enabled.  
As of August 2026, some recommended models are: ChatGpt 5.6 Terra, Claude Sonnet 5, Gemini 3.1 Pro, Kimi K3, DeepSeek V4 Pro, Qwen3.8-27B, GLM 5.3-Flash, Minimax M3.  

Follow these steps:  
- Copy the text of the "Main prompt" above and paste it into your AI's chat interface
- Wait for the assistant's introduction message
- Then, use one or more of the "Conversation starters and subsequent prompts" to help create your survey.
  - To send the Assistant a survey mockup file, see the [Example](https://github.com/heindrickson/LimeSurvey-Builder/#example-of-a-survey-mockup-file) section
- If your AI model generates an actual .txt file as a response, just download it and import it into LimeSurvey
- Otherwise, if the generated content is only displayed on the screen:
  - copy the generated content from the AI chat
  - open Notepad++ and paste the content copied
  - select 'UTF-8' in the 'Encoding' menu
  - press 'Ctrl+H' :  the 'Replace' dialog will open
  - in the 'Search Mode' section, select the "Extended" option
  - in the 'Find what' text field, put the character '⇨' (without apostrophe or quotation mark)
  - in the 'Replace with' text field, type '\t' (without apostrophe or quotation mark)
  - click the 'Replace All' button 
  - then save the edited content as a text file (.txt)
  - finally, import the saved file into LimeSurvey
- Errors on importing?
  - Check if you edited the file as explained in the previous item and if the encoding is UTF-8  
  - Check if you really used a powerful model with 'reasoning' capability (see recommended models above).
- After importing your questionnaire into LimeSurvey, check if the date format and the decimal mark are correctly set. If not, adjust them in the Settings tab -> Text Elements -> Date format and Decimal mark.
<br><br>

# Example of a survey mockup file
Although the assistant can build individual questions interactively, the recommended method is to send a mockup (DOCX or HTML) of the complete survey, so the LLM can "see the big picture". 

A mockup file is practically mandatory when defining conditional questions ('branching'), as it makes it easier for the LLM to visualize the full scenario (it will be able to 'see' the question containing the condition and the referenced question(s) at the same time). Note that, to be able to define branching conditions, the mockup will need to have the questions numbered, in order to reference each question by its own number.  
PS - the numbering scheme used in the mockup will be automatically replaced by the LLM using a GmmQnn pattern (Gmm = Group number; Qnn = Question number within the group).

Your can download the DOCX file below and use it as a template to build your own survey mockup. When ready, send your DOCX to the LimeSurvey-Builder assistant: 
[Survey Mockup Example](https://github.com/heindrickson/LimeSurvey-Builder/blob/main/Survey_Mockup_Example.docx) 
<br><br>

# Limitations
When exporting a survey from LimeSurvey in TSV format, one can see numerous fields that could theoretically be populated.  
These fields may be for general use or specific to certain question types.  
However, our assistant is explicitly instructed to use **only** a specific set of fields (the most common ones, maybe 90% of use cases).  

Therefore, if the user requests some functionality requiring a field not covered by these instructions, the assistant will likely be unable to implement it.
So, the recommendation is: do **not** ask the Assistant to generate a survey with advanced features (e.g., statistics generation, quotas, fields size, multilingual surveys etc.) or GUI attributes. 
Use the Assistant to create the basic survey features, and — after importing it into LimeSurvey — add or modify attributes such as those mentioned. 

PS - There is a workaround to create a multilingual survey with LimeSurvey-Builder: create the TSV content for each language using the Assistant, then concatenate all of them together. **But** it will be necessary to edit the final TSV to make these adjustments: a) keep only ONE set of type 'S' records, at the beginning; b) adjust the 'additional_languages' record to add the other language identifiers. 
<br><br>

# License
LimeSurvey-Builder is licensed for use, modification and distribution under the terms of the MIT License.




