# ITU Timetable Scheduler + Batch Advisor Bot
## Beginner-Friendly Claude Development Roadmap
### Course: Introduction to AI — ITU Fall 2026

---

# 1. Sab se pehle: Project ko samjho

Tumhara project 2 major parts par based hoga:

### Part A — ITU Timetable Scheduler

User apni batch/section select karega aur usay uski **latest timetable** nazar aayegi.

Example:

```text
Select Batch: CE25
Select Section: A

Monday
09:00 - 11:00   Introduction to AI
11:00 - 12:00   Digital Logic Design
01:00 - 02:00   Linear Algebra

Tuesday
...
```

User different batches/classes ka timetable bhi dekh sakega.

### Part B — Batch Advisor AI Bot

Student bot se natural language mein questions pooch sakega.

Examples:

```text
"Can I take DSA next semester?"

"Is OOP a prerequisite for DSA?"

"What courses can I take if I have not passed OOP?"

"Which classes do I have tomorrow?"

"What is the prerequisite of this course?"

"Can I take this course with my current completed courses?"
```

Bot available university/course data ko use karke answer dega.

---

# 2. IMPORTANT: Claude ko kaise use karna hai

Tum beginner ho, isliye **Claude ko ek hi prompt mein poora project generate karne ko mat kehna**.

Agar tum bolo:

> "Make my complete ITU timetable app"

to Claude bohat saara code ek saath generate kar sakta hai aur phir tumhe samajh nahi aayega ke kya ho raha hai.

Instead:

```text
Plan
↓
Setup
↓
Data
↓
Backend
↓
Timetable
↓
Bot
↓
AI integration
↓
Testing
↓
UI polish
↓
Deployment
```

Har phase complete karo.

**Golden Rule:**

> Claude se code lo, lekin har important code ko samjho bhi.

Har phase ke baad Claude se bolo:

> "Ab mujhe is code ko beginner level par Roman Urdu mein explain karo. Har file ka purpose aur important functions samjhao."

---

# 3. Project ka Recommended Architecture

Tumhara app roughly is tarah kaam karega:

```text
                    USER
                      |
                      v
               Streamlit Web App
                      |
          +-----------+-----------+
          |                       |
          v                       v
   Timetable Section       Batch Advisor Bot
          |                       |
          v                       v
   Timetable Database       AI / RAG Layer
          |                       |
          |                 +-----+------+
          |                 |            |
          |              Course Data  Timetable Data
          |                 |
          +--------+--------+
                   |
                   v
             Answer / Display
```

Simple words mein:

- Timetable data app ke paas stored hoga.
- Course/prerequisite data bhi stored hoga.
- User timetable dekhega.
- User bot se question poochega.
- Bot relevant data retrieve karega.
- AI us data ki basis par answer banayega.
- Bot ko unknown information invent nahi karni chahiye.

---

# 4. Pehle Scope Freeze Karo

Project ko unnecessarily huge mat banao.

## Version 1 — Minimum Working Project

Pehle ye banao:

- Batch selection
- Section/class selection
- Timetable display
- Course information
- Prerequisite information
- Basic advisor bot
- Search/filter
- Updated data load
- Clean UI

## Version 2 — AI Features

Baad mein:

- Natural language questions
- RAG/retrieval
- Course eligibility checking
- Timetable-aware questions
- Conversation history

## Version 3 — Advanced Features

Agar time bache:

- Admin data update
- Automatic timetable conflict detection
- Personalized student profile
- Semester planning
- Course recommendation based on prerequisites
- Notifications
- Export timetable

**Pehle Version 1 complete karo.**

---

# 5. Technology Stack

Recommended beginner-friendly stack:

| Part | Technology |
|---|---|
| Language | Python |
| UI | Streamlit |
| Data | JSON / CSV |
| Data processing | Pandas |
| AI | Gemini API / Claude API / another available LLM |
| Version Control | Git + GitHub |
| Development Assistant | Claude |
| Optional later | SQLite |

Start with JSON/CSV.

Database pehle din se mat lagao jab tak zaroorat na ho.

---

# 6. Folder Structure

Claude ko ye structure follow karne ko bolo:

```text
itu-timetable-advisor/
│
├── app.py
├── requirements.txt
├── README.md
├── .env
├── .gitignore
│
├── data/
│   ├── timetable.json
│   ├── courses.json
│   ├── prerequisites.json
│   ├── teachers.json
│   └── batches.json
│
├── services/
│   ├── timetable_service.py
│   ├── course_service.py
│   └── advisor_service.py
│
├── ai/
│   ├── chatbot.py
│   ├── prompts.py
│   └── retrieval.py
│
├── utils/
│   ├── data_loader.py
│   └── validators.py
│
└── tests/
    ├── test_timetable.py
    ├── test_courses.py
    └── test_advisor.py
```

Claude se folder structure generate karwao.

---

# 7. PHASE 0 — Claude Project Setup

Claude mein apna **Project** create karo.

Project ka naam:

```text
ITU Timetable Scheduler & Batch Advisor
```

Claude Project ke instructions mein ye basic instruction rakho:

```text
You are my coding mentor and development assistant.

I am a complete beginner in software development.

I am building an AI-powered ITU Timetable Scheduler and Batch Advisor for my Introduction to AI course.

Do not generate the entire project at once.

Help me build it phase by phase.

Use Python and Streamlit.

Whenever you provide code:
1. Explain what the code does.
2. Explain where the file belongs.
3. Explain how the code connects to the rest of the project.
4. Tell me how to test it.
5. Explain important code in beginner-friendly Roman Urdu.
6. Do not introduce advanced technologies unless necessary.
7. Do not silently change the architecture.
8. If information is missing, ask me instead of inventing ITU data.

I want to understand my own project because I may have to explain it in a viva.
```

---

# 8. PHASE 1 — Collect and Understand Your Data

Tumhare paas already ITU timetable data hai.

Sab se pehle data ko clean structure mein convert karna hai.

## Timetable data

Example:

```json
{
  "batch": "CE25",
  "section": "A",
  "day": "Monday",
  "start_time": "09:00",
  "end_time": "11:00",
  "course": "Introduction to AI",
  "teacher": "Ms Hira Yaseen",
  "room": "A-101"
}
```

## Course data

```json
{
  "course_code": "CS201",
  "course_name": "Data Structures",
  "credit_hours": 3,
  "prerequisites": ["Programming Fundamentals", "OOP"]
}
```

## Batch data

```json
{
  "batch": "CE25",
  "section": "A",
  "semester": 3
}
```

---

# 9. Claude Prompt — Data Conversion

Claude ko apna timetable data upload karke ye prompt do:

```text
I have uploaded my ITU timetable data.

Do NOT write the whole application yet.

First analyze the data.

Tell me:
1. What information is present?
2. What information is missing?
3. What structure should I use for my app?
4. Which data should be stored in timetable.json?
5. Which data should be stored in courses.json?
6. Which data should be stored in prerequisites.json?
7. Identify duplicate or inconsistent entries.
8. Do not invent missing ITU information.

Then propose a clean JSON schema for each file.

Explain everything in beginner-friendly Roman Urdu.
```

---

# 10. PHASE 2 — Data Loader

Ab Python mein data load karna hai.

Goal:

```text
JSON
 ↓
Python
 ↓
Application
```

Claude ko bolo:

```text
Now create a simple Python data loading system.

Create:
utils/data_loader.py

It should load:
- timetable.json
- courses.json
- prerequisites.json
- batches.json

Keep the code beginner-friendly.

Do not add a database yet.

Explain every important part in Roman Urdu.

Then create a small test script to confirm that all data loads correctly.
```

## Done condition

Terminal mein application/data loader successfully data read kare.

---

# 11. PHASE 3 — Timetable Backend

Ab timetable search system banao.

Required functions:

```text
get_all_batches()
get_sections(batch)
get_timetable(batch, section)
get_teacher_schedule(teacher)
get_course_schedule(course)
```

Claude prompt:

```text
Build the timetable service.

Create:
services/timetable_service.py

Functions should allow me to:
- get all batches
- get sections
- get timetable for a batch and section
- filter by day
- find a teacher's schedule
- find a course's schedule

Use the JSON data we already created.

Do not build the UI yet.

Explain the logic in Roman Urdu.
```

---

# 12. PHASE 4 — Timetable UI

Ab Streamlit UI banao.

First simple UI:

```text
ITU Timetable Scheduler

Batch:
[ CE25 ▼ ]

Section:
[ A ▼ ]

[ Show Timetable ]
```

Result:

```text
MONDAY

09:00 - 11:00
Introduction to AI
Ms Hira Yaseen
Room A-101

11:00 - 12:00
DLD
Sir XYZ
Room B-202
```

Claude prompt:

```text
Now build the first Streamlit UI for my timetable scheduler.

Requirements:
- Batch dropdown
- Section dropdown
- Day filter
- Timetable display
- Clean beginner-friendly interface

Use the existing timetable_service.py.

Do not add AI yet.

Do not change the data architecture.

Explain app.py in Roman Urdu after generating it.
```

---

# 13. PHASE 5 — Make the Timetable Visually Good

Once functionality works, improve UI.

Possible layout:

```text
+--------------------------------------+
|       ITU TIMETABLE SCHEDULER        |
+--------------------------------------+

Batch       Section       Semester
CE25        A             3

----------------------------------------

Monday

09 ┃ AI
11 ┃ DLD
13 ┃ Linear Algebra
15 ┃ Free

----------------------------------------
```

Do not spend hours on design before the functionality works.

---

# 14. PHASE 6 — Course Information System

Now add course information.

Student should be able to search:

```text
Search Course:
[ Data Structures ]

Course Code: CS201
Credit Hours: 3

Prerequisites:
- Programming Fundamentals
- OOP
```

Claude prompt:

```text
Build a course information service.

It should allow:
- search course by code
- search course by name
- show credit hours
- show prerequisites
- show course details

Use courses.json and prerequisites.json.

Do not add AI yet.

Keep it simple.
```

---

# 15. PHASE 7 — Build the Batch Advisor WITHOUT AI First

This is VERY important.

Pehle normal rule-based advisor banao.

Example:

```text
Student completed:
Programming Fundamentals

Question:
Can I take Data Structures?

System checks:

DSA prerequisites:
- Programming Fundamentals
- OOP

Student has:
- Programming Fundamentals

Missing:
- OOP

Answer:
You are missing OOP.
```

Iska matlab bot ka basic brain pehle deterministic hoga.

---

# 16. Why Rule-Based First?

Agar tum directly LLM ko bolo:

> "Can I take DSA?"

LLM guess kar sakta hai.

Better architecture:

```text
Student Question
      ↓
Retrieve ITU Data
      ↓
Check Actual Rules
      ↓
LLM Explains Result
```

Yani:

**LLM = explanation**

**Your data/rules = source of truth**

Ye project ko zyada reliable banata hai.

---

# 17. PHASE 8 — Advisor Logic

Create:

```text
services/advisor_service.py
```

Possible functions:

```text
check_prerequisites()
get_missing_prerequisites()
can_take_course()
get_course_requirements()
```

Claude prompt:

```text
Create a beginner-friendly advisor service.

It should determine whether a student can take a course based on:
- completed courses
- prerequisite courses
- course data

Do not use an LLM yet.

The result should contain:
- eligible: true/false
- missing prerequisites
- explanation

Write tests for:
1. All prerequisites completed
2. One prerequisite missing
3. Multiple prerequisites missing
4. Course with no prerequisite
```

---

# 18. PHASE 9 — Add the AI Advisor

Ab AI introduce karo.

Architecture:

```text
Student Question
       ↓
Question Understanding
       ↓
Relevant Data Retrieval
       ↓
Rule / Data Check
       ↓
LLM
       ↓
Natural Language Answer
```

Example:

Student:

> "Can I take DSA next semester?"

System:

```text
Student courses
+
DSA prerequisites
+
Academic rules
       ↓
Advisor logic
       ↓
Result
       ↓
LLM explains result
```

---

# 19. AI ko Directly Decision Maker Mat Banao

Bad architecture:

```text
Student
 ↓
LLM
 ↓
"Yes, you can take DSA"
```

Better:

```text
Student
 ↓
Retriever
 ↓
ITU Data
 ↓
Prerequisite Checker
 ↓
Actual Result
 ↓
LLM Explanation
```

This reduces hallucination.

---

# 20. PHASE 10 — Retrieval / RAG

Agar tumhara course project AI concepts show karna chahta hai, RAG add kar sakte ho.

Basic RAG:

```text
Question
   ↓
Find relevant ITU information
   ↓
Retrieve course/timetable data
   ↓
Give retrieved information to LLM
   ↓
Generate answer
```

Example:

```text
Question:
"What is the prerequisite of DSA?"

Retriever finds:

DSA
Prerequisites:
OOP
Programming Fundamentals

LLM:
"According to the provided ITU data..."
```

Start with simple keyword/search-based retrieval.

Vector databases aur embeddings ko tabhi add karo jab tum samajh jao ke zaroorat kyun hai.

---

# 21. Claude Prompt — AI Advisor

```text
Now integrate an LLM into my existing Batch Advisor.

IMPORTANT:

The LLM must NOT invent ITU academic rules.

The application should first retrieve relevant data and perform deterministic checks.

Then the LLM should explain the verified result naturally.

For example:

User:
"Can I take DSA?"

Application:
1. Identify DSA.
2. Retrieve prerequisites.
3. Check student's completed courses.
4. Determine missing prerequisites.
5. Give the result to the LLM.
6. LLM explains the result.

If the required ITU information is unavailable, the bot must say that it does not have enough information.

Do not make unsupported claims.

Keep the architecture simple and explain it in Roman Urdu.
```

---

# 22. PHASE 11 — Timetable Questions in the Bot

Ab bot timetable bhi understand kare.

Examples:

```text
"What classes do I have tomorrow?"

"When is AI class?"

"Who teaches DLD?"

"What room is my AI class in?"

"Do I have any class on Friday at 11?"
```

Flow:

```text
Question
 ↓
Identify intent
 ↓
Retrieve timetable
 ↓
Answer
```

---

# 23. PHASE 12 — Combine Everything

Final app tabs:

```text
🏠 Home

📅 Timetable

📚 Courses

🤖 Batch Advisor

🔎 Search

ℹ️ About Project
```

### Timetable

Batch → Section → Day → timetable

### Courses

Search course → details → prerequisites

### Advisor

Ask question → retrieve data → verify → AI explanation

---

# 24. PHASE 13 — Updated Timetable Feature

Tumhara original requirement "updated timetable" hai.

Isliye data update mechanism zaroor rakho.

Simple version:

```text
data/
    timetable.json
```

Jab new timetable aaye:

```text
Replace/update JSON
        ↓
App automatically reads latest file
```

Better version:

```text
Last Updated:
29 September 2026
```

UI mein show karo:

```text
Timetable Last Updated: 29 Sep 2026
```

Agar admin UI banana ho to baad mein add karo.

---

# 25. PHASE 14 — Validation

Data galat hua to bot bhi galat answer dega.

Isliye validation banao.

Check:

- Course code valid?
- Teacher exists?
- Batch exists?
- Room exists?
- Time valid?
- Duplicate class?
- Prerequisite course exists?

Claude prompt:

```text
Create validators for my ITU data.

Check:
- missing fields
- duplicate entries
- invalid course references
- invalid batch references
- invalid teacher references
- invalid time values

Show clear error messages.

Do not modify data automatically.
```

---

# 26. PHASE 15 — Testing

Minimum tests:

### Timetable

```text
CE25 + A
→ correct timetable
```

### Course

```text
DSA
→ correct prerequisites
```

### Advisor

```text
All prerequisites complete
→ eligible
```

```text
Prerequisite missing
→ not eligible
```

### Unknown question

```text
"Who won the World Cup?"
→ bot should say this is outside its available ITU data
```

---

# 27. PHASE 16 — Security

API keys code mein directly mat likhna.

BAD:

```python
api_key = "AIza........"
```

Use `.env`:

```text
GEMINI_API_KEY=your_key_here
```

And `.gitignore`:

```text
.env
```

GitHub par API key kabhi upload mat karna.

---

# 28. PHASE 17 — Use Claude Correctly

Claude ke saath development ka best workflow:

```text
1. Explain
2. Plan
3. Generate small piece
4. Run it
5. Test it
6. Fix errors
7. Explain
8. Commit to Git
9. Move to next phase
```

Har baar complete project regenerate mat karwana.

---

# 29. Claude ko Error Dete Waqt

Sirf ye mat bolo:

```text
code doesn't work
```

Instead:

```text
I ran the application and got this error:

[paste full error]

Here is the relevant file:

[paste file/code]

Do not rewrite the entire project.

First explain:
1. What caused the error?
2. Which file is responsible?
3. What is the smallest fix?

Then provide the corrected code.
```

---

# 30. Claude se Code Samajhne ka Prompt

Har important feature ke baad:

```text
Now act as my tutor.

Explain the code you just created in beginner-friendly Roman Urdu.

Explain:
1. What each file does
2. What each important function does
3. How data flows through the program
4. Why we used this approach
5. What would break if we removed this part
6. Which parts I should understand for my viva

Do not explain every obvious syntax detail.
Focus on the actual logic.
```

---

# 31. Git Workflow

Har completed phase ke baad Git commit:

```text
Phase 0:
setup project

Phase 1:
add timetable data

Phase 2:
add timetable service

Phase 3:
add Streamlit timetable

Phase 4:
add course service

Phase 5:
add advisor logic

Phase 6:
add AI advisor
```

Agar Claude ka change break ho jaye to previous working version par wapas ja sakte ho.

---

# 32. Suggested Development Order

FOLLOW THIS ORDER:

```text
PHASE 0
Project setup
        ↓
PHASE 1
Clean ITU data
        ↓
PHASE 2
Data loader
        ↓
PHASE 3
Timetable service
        ↓
PHASE 4
Timetable UI
        ↓
PHASE 5
Course information
        ↓
PHASE 6
Rule-based advisor
        ↓
PHASE 7
AI advisor
        ↓
PHASE 8
Timetable questions
        ↓
PHASE 9
Validation
        ↓
PHASE 10
Testing
        ↓
PHASE 11
UI polish
        ↓
PHASE 12
Demo + report
```

---

# 33. Minimum Viable Product (MVP)

Agar deadline close hai, pehle ye complete karo:

```text
✓ ITU timetable data
✓ Batch/section selection
✓ Timetable display
✓ Course information
✓ Prerequisites
✓ Rule-based eligibility checker
✓ AI Batch Advisor
✓ Basic search
✓ Clean Streamlit UI
```

Ye working product ban jayega.

Uske baad:

```text
+ RAG
+ advanced personalization
+ admin panel
+ analytics
+ timetable conflict detection
```

---

# 34. AI / Introduction to AI Course Concepts

Tumhare project mein ye AI concepts clearly demonstrate ho sakte hain:

### Knowledge Representation

ITU courses, prerequisites, batches, teachers and timetable ko structured data mein represent karna.

### Search / Retrieval

Relevant timetable/course information retrieve karna.

### Constraint Reasoning

Prerequisite conditions aur timetable constraints check karna.

### Generative AI

LLM natural language answer generate karta hai.

### RAG

LLM ko relevant ITU data provide karke grounded answer generate karwana.

### AI Reliability

System verify karta hai ke AI ka answer actual data se supported hai ya nahi.

---

# 35. Original CSP Idea ko kaise use karna hai

Tumhari existing project plan mein CSP solver bhi hai.

Us plan ke mutabiq timetable generation ko CSP ke through model kiya gaya hai:

```text
Variables
Domain
Hard Constraints
Backtracking
MRV
Forward Checking
AC-3
```

Ye project ka advanced extension ho sakta hai.

Lekin tumhare current app ka primary purpose:

```text
Existing ITU timetable
        ↓
Students ko accessible banana
        +
Batch Advisor
```

Agar instructor specifically timetable GENERATION maangta hai, tab CSP module add karo.

Agar instructor ko sirf timetable scheduler/viewer + advisor dikhana hai, to pehle existing timetable retrieval system complete karo.

---

# 36. CSP Extension — Later

Agar add karna ho:

```text
Course sessions
      ↓
Variables
      ↓
Possible time/room slots
      ↓
Constraints
      ↓
Backtracking
      ↓
MRV
      ↓
Forward Checking
      ↓
AC-3
      ↓
Valid timetable
```

Is feature ko existing app ke:

```text
Admin / Generate Timetable
```

section mein rakha ja sakta hai.

---

# 37. Final App Architecture

Recommended final structure:

```text
                    ITU APP
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
   Timetable        Courses       Batch Advisor
        |              |              |
        |              |         +----+----+
        |              |         |         |
        |              |       Rules      LLM
        |              |         |         |
        +--------------+---------+---------+
                         |
                         v
                    ITU DATA
                         |
               +---------+---------+
               |         |         |
          Timetable   Courses   Prerequisites
```

---

# 38. Final Demo Flow

5–7 minute demo:

## Step 1

Open app.

Show:

```text
ITU Timetable Scheduler
```

## Step 2

Select:

```text
Batch → CE25
Section → A
```

Show timetable.

## Step 3

Ask:

```text
"When is my AI class?"
```

Bot retrieves timetable data.

## Step 4

Ask:

```text
"What are the prerequisites for DSA?"
```

Bot retrieves course information.

## Step 5

Ask:

```text
"Can I take DSA if I have passed Programming Fundamentals but not OOP?"
```

System checks actual prerequisites.

Bot explains the result.

## Step 6

Ask an unsupported question.

Show that the system does not invent information.

## Step 7

Show:

```text
Last Updated:
29 September 2026
```

Explain that timetable data can be updated without changing the application code.

---

# 39. What You Should NOT Do

Do NOT:

- Ask Claude to build everything at once.
- Copy code without understanding it.
- Put API keys in GitHub.
- Let the LLM invent university rules.
- Hard-code every timetable answer into Python.
- Start with advanced databases unnecessarily.
- Spend too much time on UI before functionality.
- Add RAG/vector databases before understanding basic retrieval.
- Change frameworks midway without a reason.

---

# 40. Your First Claude Prompt

This is the FIRST prompt you should give Claude:

```text
I want to build my Introduction to AI course project.

Project:
ITU Timetable Scheduler + Batch Advisor Bot.

I am a complete beginner in software development, so I need you to act as my coding mentor.

I have an existing project plan and ITU timetable data.

IMPORTANT:
Do not build the whole project at once.

First help me understand the project architecture.

My app should eventually:
1. Let users select their ITU batch and section.
2. Show their updated timetable.
3. Allow users to search courses.
4. Show course prerequisites.
5. Have a Batch Advisor chatbot.
6. Answer questions such as:
   - Can I take this course?
   - What are its prerequisites?
   - What classes do I have?
   - When/where is a course?
7. Use actual provided ITU data as the source of truth.
8. Use an LLM to explain answers naturally.
9. Never let the LLM invent university information.

I want to use:
- Python
- Streamlit
- JSON/CSV initially
- Git/GitHub
- An LLM API for the advisor

First do ONLY these things:

1. Analyze my project requirements.
2. Explain the complete architecture in beginner-friendly Roman Urdu.
3. Explain how data will flow through the application.
4. Propose the folder structure.
5. Explain what we should build first, second, third, etc.
6. Tell me what NOT to build yet.
7. Create Phase 0 only.

Do NOT write the complete application yet.

After that, wait for me to say "continue".

I want to understand the project while building it, because I will need to explain it in my Introduction to AI course presentation/viva.
```

---

# 41. Golden Rule

Tumhara target sirf:

> "Claude se app banwana"

nahi hona chahiye.

Target hona chahiye:

> **"Claude ki help se app khud samajhte hue banana."**

Best workflow:

```text
You
 ↓
Understand requirement
 ↓
Claude
 ↓
Small implementation
 ↓
You run it
 ↓
You test it
 ↓
Claude explains/fixes it
 ↓
You understand it
 ↓
Git commit
 ↓
Next feature
```

Isi workflow se tum project bhi bana loge aur viva mein architecture bhi explain kar sakoge.
