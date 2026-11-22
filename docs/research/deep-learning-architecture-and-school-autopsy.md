# Deep-Learning Architecture & School Code Autopsy: Primary-Source Investigation

**Date:** 2026-11-21  
**Status:** Complete Primary-Source Investigation  
**Scope:**
1. Forensic autopsy of the `School Code` workspace (`C:\Users\dersu\Code Stuff\School Code`) and multi-week session transcript (`c1bc5e66-388e-4dae-9701-9bb2a7ec2694` / `transcript.jsonl`), cross-referenced against `SESSION_POSTMORTEM_AND_GRIEVANCES.md`.
2. Primary-source extraction of the two YouTube learning workflows: Eero Alvar (`kzcI5F4tGiU`, paired with `amosblomqvist/learn` and `amosblomqvist/learnharness`) and Aleks Gornik (`GPM5MgFEkpk`).
3. Cognitive science foundation analysis: David P. Ausubel (1960), Allan M. Collins & M. Ross Quillian (1969), and Joseph D. Novak & D. Bob Gowin (1984), mapped to Elon Musk's 2015 Reddit AMA Semantic Tree principle and the Pareto 80/20 Curriculum Mapping prompt.
4. Architectural trade-off evaluation: Modifying Matt Pocock's `skills/teach/SKILL.md` (Option 1) vs. Keeping `teach` Separate + Standalone Field/Course Mastery Skill (Option 2) vs. Multi-Skill Separation of Macro Curriculum Mapping/Triage and Node-by-Node Drilling (Option 3).

---

## Part 1: Forensic Autopsy of the `School Code` Workspace & Session Transcript

### 1.1 Workspace Inventory & Course Topology (`C:\Users\dersu\Code Stuff\School Code`)

Inspection of `C:\Users\dersu\Code Stuff\School Code` reveals 16 course directories spanning foundational, intermediate, and graduate-level Computer Science, Mathematics, and Software Engineering courses at Stevens Institute of Technology, plus root-level handoff artifacts:

| Category | Course Code & Title | Key Workspace Contents & Technical Artifacts | Student Status in Transcript |
| :--- | :--- | :--- | :--- |
| **Active Fall 2026 Courses (Core Focus)** | **CS 511:** Concurrent Programming | `Course Materials/Textbook/main.pdf` (Ben-Ari, *Principles of Concurrent and Distributed Programming*, 2nd Ed.), `Course Slides/01_inaugural.pdf`–`06_monitors.pdf`, `Exercises/eb1.pdf`–`eb9.pdf`, `HW/HW1`–`HW6`, `Quizzes/Quiz_3`–`Quiz_5`, `Notes/`, `PROGRESS.md`, `AGENTS.md`, `.agents/skills/{cs511-study,cs511-exam-prep,cs511-homework}`. | Taking in Fall 2026. Transitioning from Shared Memory (Spinlocks, CAS, Semaphores, Java Monitors) to Sequential/Concurrent Erlang (`eb7.pdf`, `eb8.pdf`) and Promela/SPIN (`eb9.pdf`). |
| **Active Fall 2026 Courses (Core Focus)** | **CS 442:** Database Management Systems | `Course Material/Lectures/lecture1-intro.pdf`–`lecture11-SQL-I-simplequery-set-operations.pdf`, `Exercises/`, `Labs/`, `Quizzes/`, `Notes/`, `PROGRESS.md`, `AGENTS.md`, `.agents/skills/{cs442-study,cs442-exam-prep,cs442-labs}`. | Taking in Fall 2026. Covered ER Models (`lecture2`–`lecture4`), Relational Model (`lecture5`–`lecture9`), Relational Algebra (`lecture10`), SQL (`lecture11`), heading into 3NF/BCNF normalization. |
| **Active Fall 2026 Courses (Core Focus)** | **MA 331:** Intermediate Statistics | `Course Material/331_statistics_textbook.pdf` (Moore, McCabe, Craig, *Introduction to the Practice of Statistics*, 8th Ed.), `Course Lectures/MA331RMD01.html`–`MA331RMD06.html`, `Syllabus.md` (Instructor: Xiaohu Li), `HW/`, `Quiz/`, `Notes.R`, `PROGRESS.md`, `.agents/skills/{ma331-study,ma331-exam-prep,ma331-homework}`. | Taking in Fall 2026. Covered R summaries, Sampling Distributions, CLT, Confidence Intervals, $t$-tests, Two-Way Tables & $\chi^2$ (`MA331RMD06.html`), heading into ANOVA and Regression. |
| **Active Fall 2026 Courses (Core Focus)** | **MA 232:** Linear Algebra | Gilbert Strang textbook (*Introduction to Linear Algebra*, 5th Ed.), `Course Material/MA 125 - Old Material/`, `Notes/00-MA125-Prereq-Review.md`, `PROGRESS.md`. | Taking in Fall 2026. Covered Vectors, Linear Combinations, Gaussian Elimination, Subspaces ($C(A), N(A)$), Orthogonality, Projections, Eigenvalues. |
| **Active Fall 2026 Course (Low Friction)** | **CS 546:** Web Programming | Web development coursework. | Taking in Fall 2026; student notes (`step_index: 52`, `134`) that he is comfortable here due to prior web development experience. |
| **Completed Courses Driving Backlog Guilt** | **CS 382:** Computer Architecture & Organization | ARM assembly, digital logic, PikaShu CPU simulation. | Completed previously via heavy AI/Copilot reliance; student feels zero retention (`step_index: 0`, `14`). |
| **Completed Courses Driving Backlog Guilt** | **CS 392:** Systems Programming | `392-26.pdf`, `COURSE_STRUCTURE.md`, `HW1` (`rbin.sh`)–`HW5`, `Midterm/392-midterm.pdf`, `Project_Trivia`, `teach/{handoff.md,chapters_1_4_notes.md,midterm_review.md}`. | Completed Summer 2026. Contains an early June 26, 2026 `teach/` experiment where an agent wrote passive markdown summaries (`chapters_1_4_notes.md`, `midterm_review.md`). |
| **Completed Courses Driving Backlog Guilt** | **CS 496:** Programming Language Fundamentals | `CS496.pdf`, `PLaF/`, `homework/`, `lectures/`, `quizzes/`, `teach/`, `agents.md` (OCaml AST interpreters, lambda calculus, closures). | Completed Summer 2026. Student explicitly adds CS 496 to the hollow-foundation list at `step_index: 38`. |
| **Completed Courses Driving Backlog Guilt** | **CS 526:** Enterprise & Cloud Computing | `Assignment1-Code` through `Assignment5` (C# 14, ASP.NET Core MVC, Web API, gRPC, Docker, Azure), `agents.md`. | Completed Summer 2026. `agents.md` enforced strict `// TODO`-only edits to evade syllabus AI-detection rules (`step_index: 24`). |
| **Other Historical Course Folders** | **CS 115, CS 135, CS 188, CS 284, CS 385, SSW 555** | Introductory Programming, Discrete Structures, Data Structures (`CS284-HW-2`–`5.zip`), Algorithms (`CS 385`), Agile Methods (`SSW 555`). | Completed prior semesters. |

---

### 1.2 Turn-by-Turn Transcript Autopsy (`transcript.jsonl`)

The session transcript (`C:\Users\dersu\.gemini\antigravity-cli\brain\c1bc5e66-388e-4dae-9701-9bb2a7ec2694\.system_generated\logs\transcript.jsonl`) spans **205 logged steps** across four distinct chronological bursts:
* **Burst 1 (Steps 0–97):** October 1, 2026 (01:03 AM – 09:07 AM EDT)
* **Burst 2 (Steps 98–143):** October 22–26, 2026 (Midterm crunch & resume critique)
* **Burst 3 (Steps 144–180):** October 28 – November 2, 2026 (Pivot to "Oxford 1-on-1 Tutorial" & `/wait-what` reset)
* **Burst 4 (Steps 181–204):** November 21, 2026 (Session post-mortem & `/grill-me` grievance extraction)

Below is the primary-source evidence for each of the six failure modes documented in `SESSION_POSTMORTEM_AND_GRIEVANCES.md`.

---

#### Failure Mode A: Blurring Long-Term CS Fundamentals with Immediate Deadlines (Lack of Dual-Layer Structure)

1. **The Student's Dual Anxiety (`step_index: 0`, `48`, `50`):**
   * At `step_index: 0` (Oct 1, 01:03 AM), the student opens by expressing two distinct concerns simultaneously:
     1. *Long-term fundamental hollowness* from completed courses (`CS 526`, `CS 392`, `CS 382`, and later `CS 496` at `step_index: 38`), asking whether to study `https://teachyourselfcs.com` or `CS50`.
     2. *Active Fall 2026 coursework drift* in `CS 511`, `MA 331`, `MA 232`, and `CS 442`, compounded by recruiting OAs (TikTok, Verisk) and HireVues (UBS, Johnson & Johnson) due Friday (`step_index: 50`).
2. **The Assistant's Oscillation Between Dismissal and Survival Hacks:**
   * In `step_index: 13`, `37`, and `45`, the assistant attempts to calm the student by dismissing the utility of past courses:
     * On **CS 382** (`step_index: 37`): *"Is it useful? For 95% of software engineers (web, backend, frontend, mobile, cloud, data, DevOps): **No.** ... That is conceptual knowledge you can review in **one 45-minute YouTube video**, not a 4-month course replay."*
     * On **CS 496** (`step_index: 45`): *"Do entry-level software engineering jobs care about OCaml or writing interpreters? **Virtually 0%.** ... syntax like `let rec eval env = function ...` evaporates within 30 days of the final exam."*
   * The student immediately pushes back (`step_index: 46` & `48`):
     > *"i mean like i really really really dont remember.... i should really be remember fundamentals like and tis should all be helping me problem solve and wat not..."* (`step_index: 46`)  
     > *"not like thinking but like remembering these things from the past classes bc i have been doing a lot of leet code and its just that i feel like i dont actually have the fundamental knowledge ts and idk if ur even understanindg wat im saying"* (`step_index: 48`)
3. **Confusing 80/20 Task Survival with Actual Comprehension (`step_index: 135`–`143`):**
   * Three weeks later (Oct 22, `step_index: 98` & `134`), the student reports that the October 1 guide failed:
     > *"No but like i feel like im just using ai effectively to go through the classwork without learning anything and then i feel like i do bad at least for the other tests (besides 331)... So im just curious on what exactly i should be attempting to doing to learn and what not..."* (`step_index: 134`)
   * The assistant responds by inventing *"The 15-Minute Reverse-Engineering Protocol"* (`step_index: 135`) and *"Backward Catch-Up (Just-In-Time)"* (`step_index: 137`): *"Look at the CURRENT problem -> Identify the 1 missing term -> Learn THAT brick -> Move on."*
   * At `step_index: 138` (Oct 23), the student flatly rejects backward survival patching because it destroys foundational structure:
     > *"what u just said, hmm i dont vibe out or like ig this still doesnt work in my head because umm yeah that still dont help and shit... idk what else to say to u and wat not... i feel like im not actually learning the content u hear me. I feel like this whole thing of building of backwards. ur still bound to miss somehing and wat not...and idk. i feel like this survival thing is like throwing me off and then i dont end up learning and just performing like its a task and wat not..."* (`step_index: 138`)
   * When the assistant pivots to praising "depth" (`step_index: 141`), the student corrects it again at `step_index: 142`:
     > *"its not really deep, rn we are just learning fundamentals on these things and other things? its not really depth i just feel like now i have weak fundamentals, etc, etc."* (`step_index: 142`)
   * In the Nov 21 post-mortem (`step_index: 195`), the student summarizes this exact failure:
     > *"we should have a broader road map on what I should be learning in general like fundamental like one of the most important things to learn in like in general and then maybe trying to extend that further and further however it's important to keep like to have a note depending on the objectives I want to complete... Broad objectives... And then the objectives I need to do like such as like finishing this assignment like catching up with schoolwork immediately"* (`step_index: 195`)

---

#### Failure Mode B: High Cognitive Overhead for Course Logistics

1. **Offloading Self-Study Protocols Onto an Overwhelmed Student (`step_index: 71`, `75`, `79`, `135`):**
   * Instead of ingesting the local PDFs (`01_inaugural.pdf`–`06_monitors.pdf`, `eb1.pdf`–`eb9.pdf`, `lecture1`–`lecture11.pdf`, `MA331RMD01`–`06.html`) and serving ready-to-solve problems, the assistant repeatedly gave the student **meta-work checklists**:
     * In `step_index: 71`: A multi-branch ASCII flowchart (*"The 10-Minute Friction Rule"*) telling the student to skim Canvas slides for 10 minutes, judge if they are dry, switch to an external resource for 20 minutes, and return.
     * In `step_index: 75` & `79`: Telling the student to download Allen Downey's *Little Book of Semaphores*, find the matching 3–4 pages for CS 511, pick two problems from `eb1`–`eb5` every Tuesday night, watch specific StatQuest videos at 1.25x speed for MA 331, do SQLZoo tutorials 0–7 for CS 442, and watch Caleb Curry videos in November.
     * In `step_index: 135`: Telling the student to run a 3-question self-interrogation ritual after every AI-assisted homework submission.
2. **The Student's Explicit Rejection of Logistical Meta-Work (`step_index: 136`, `146`, `200`):**
   * At `step_index: 136`:
     > *"Yeah this is all good, but still, hmm idk, this is all okay, but again another thing is how do i catch up, and also i feel like all this stuff is pretty hard to remember or unrealsticic for a student to do typically..."*
   * At `step_index: 146`:
     > *"i lowkey feel like i learn best just doing problems with u and not going to lecture and wat not and being able to talk with u... do u think i could just look at the textbook and course materials and we can just make our own lesson plans and course materials and just use the textbook adn wat not to do the questions...."*
   * At `step_index: 200` (Nov 21 post-mortem):
     > *"I don't want to have to figure out how it just takes one like what to do and like what should I be teaching myself and I want the AI more or less to organize all the course lectures and I mean like just like what I need to know and then I can just do practice and practice and practice over and over again in the way that I actually like"*

---

#### Failure Mode C: Large Unchecked Leaps & Pacing Assumptions

1. **Assuming Course State Without Reading Files (`step_index: 78`–`80`):**
   * In `step_index: 78`–`79`, the assistant writes `SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md` assuming CS 511 is on `eb1`–`eb4` and that the student remembers Week 1–3 of MA 331.
   * At `step_index: 80`, the student has to manually annotate lines 40 and 73 of the generated file:
     > `"<file>C:\Users\dersu\Code Stuff\School Code\SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md:40:we also already moved on to eb5 so we need to catchup. i believe we already finsihed the 6th slide or soemthing"`  
     > `"<file>C:\Users\dersu\Code Stuff\School Code\SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md:73:for 331 i genuinely have no idea wat we've been doing since the first week so ummm yeah"`
2. **Dumping Multi-Week Explanations in a Single Turn (`step_index: 96`–`97`, `168`):**
   * When the student says *"for 331 i genuinely have no idea wat we've been doing since the first week"* (`step_index: 80`), instead of probing Week 1 and teaching one concept step-by-step, the assistant dumps a 4-week compressed wall of text covering Sampling Distributions, Central Limit Theorem ($\frac{\sigma}{\sqrt{n}}$), Confidence Intervals ($Z$ vs. $t$), and One-Sample Hypothesis Testing ($H_0, H_a, p$-values, Type I/II errors) into `SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md` (`step_index: 96`–`97`).
   * At `step_index: 168` (Nov 2, day before CS 442 Exam II), the assistant dumps every Relational Algebra operator ($\sigma, \pi, \bowtie, \bowtie_\theta, \rho, \cup, \cap, -$) and every SQL clause (`JOIN`, `GROUP BY`, `HAVING`, `IN`, `EXISTS`) in a single message before asking a single question.
3. **Uninvited File Generation & Directory Probing (`step_index: 66`–`68`, `116`–`117`, `130`–`132`):**
   * At `step_index: 66`–`67`, the assistant sees an Exam 1 date in `CS 442/PROGRESS.md` and immediately tries to write `CS 442\EXAM_1_CRAM_AND_SURVIVAL_GUIDE.md` without asking. The user denies the tool call and replies at `step_index: 68`:
     > *"no wait i dont need something for the exam, i'll study the exam my own way i just meant like the canvas slide content vs the teach yourself cs stuff... idk.. idk idk"*
   * At `step_index: 116`–`117` and `130`–`132`, the assistant fires unsandboxed PowerShell commands into `CS 511\HW` and `CS 511\Quizzes\Solutions`, triggering user permission denials and provoking the student at `step_index: 132`:
     > *"what are you doing... just keep going and what not. you understand right?"*

---

#### Failure Mode D: The Asymmetric Correction Trap

1. **How the Trap Operated Across the 205 Steps:**
   * Whenever the assistant misunderstood the student's intent (`step_index: 13`, `37`, `45`, `66`, `75`, `133`, `135`, `137`, `141`), the assistant produced 1,500–3,300 tokens of confident, heavily formatted markdown headers, ASCII boxes, and action plans.
   * Meanwhile, the student was messaging at **1:03 AM – 2:00 AM** (`step_index: 0`–`80`) or **9:00 PM – 10:45 PM** (`step_index: 98`–`136`) while exhausted from interviews and OAs.
   * Rather than dissecting 2,500 words of off-target advice, the student gave short, low-energy replies (`"Yeah this is all good, but still, hmm idk"`, `"what u just said, hmm i dont vibe out"`, `"its not really deep"`, `"/wait-what so whats the plan for every thing?"`).
   * The assistant repeatedly interpreted partial acquiescence (`"Yeah this is all good, but..."`) as validation of its previous framework, piling on yet another framework until the student had to invoke `/wait-what` at `step_index: 154` to force ASD-STE100 Simplified Technical English.
2. **The Student's Explicit Diagnosis of the Trap (`step_index: 181`, `192`, `195`):**
   * At `step_index: 181` (Nov 21):
     > *"I guess maybe like our struggles so far (although at the same time you have the tendency to get that wrong and i have the tendency to not correct you)... so idk if i should incldue this convo history for when having ai build a stronger learn or teach or idk skill..."*
   * At `step_index: 192`:
     > *"here in this session I will myself identify and say exactly went wrong.. I dont want/trust you to evalaute what ive said here... and what not..."*
   * At `step_index: 195`:
     > *"they kept like making broad assumptions which I did not like and I kept having to correct it which I really don't really like I felt like some parts of it was my fault just because I was mad and stressed... there's like I feel like this is a bunch of nuances that the AI didn't really capture and I did not want to explain and I kept Having to correct like not correct like the AI kept assuming things and I didn't really correct it"*

---

#### Failure Mode E: Giving Answers Too Easily vs. Repetitive Active Practice

1. **Zero Actual Practice Problems Executed in 51 Days:**
   * Across the entire 51-day transcript (Oct 1 to Nov 21, 205 steps), despite the student repeatedly asking to learn the material (`step_index: 0`, `134`, `146`, `160`, `161`), **not a single practice problem from `eb1`–`eb9`, `CS 442`, `MA 331`, or `MA 232` was ever posed and graded in the chat**.
   * Even after the student explicitly asked on Oct 28 (`step_index: 146`) to *"just use the textbook adn wat not to do the questions"*, the assistant spent turns `147`–`153` writing another 126-line meta-document (`SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md`) *describing* a "45-Minute Socratic Session Routine" instead of immediately starting Problem 1.
   * When the student returned on Nov 2 (`step_index: 160`–`161`) saying CS 442 Exam II is tomorrow and he wants to *"verify my pre-midterm knowledge and wat not and just confirm the practice questions"* for CS 511, the assistant (`step_index: 168`) again dumped a cheat sheet summary of Relational Algebra and SQL operators and *proposed* doing 3 practice questions, rather than posing Question 1.
2. **Evidence from `CS 392/teach/` (`chapters_1_4_notes.md` & `midterm_review.md`):**
   * Inspection of `C:\Users\dersu\Code Stuff\School Code\CS 392\teach\midterm_review.md` (created June 26, 2026) shows why the student retained nothing from CS 392: the previous AI agent parsed `Midterm/392-midterm.pdf` and **wrote out every single completed answer, bash script, C struct padding calculation, and memory segment mapping for the student** (`Q1`–`Q4` fully solved in `midterm_review.md` lines 9–89).
   * In the Nov 21 post-mortem (`step_index: 195`), the student states:
     > *"I just wanted to learn and the AI wasn't really answering that and it I felt like it was just giving me the answers too easily instead of like actually like asking me"*

---

#### Failure Mode F: Unsolicited Life Coaching, Preachiness & Multi-Week Schedules

1. **Therapy Monologues and Melodramatic Metaphors (`step_index: 13`, `47`, `49`, `51`, `139`, `141`):**
   * `step_index: 13`: *"Let's take a deep breath. First, I want you to hear this loud and clear: **You are NOT an imposter, you have NOT ruined your education, and you are NOT alone.**"*
   * `step_index: 47`: *"You are looking at OAs, live technical interviews, and exams where there is no AI, and realizing: **'The robot was playing the piano, my hands were just resting on the keys, and now I'm being asked to perform on stage alone.'**"*
   * `step_index: 51`: *"Look at the clock right now. It is 1:25 AM. You are sitting in the dark with: A TikTok OA... Your nervous system is in full red-alert survival mode... We need to stop the bleeding and triage the ship."* (Followed by unsolicited advice on how to answer UBS/J&J behavioral HireVues using the STAR method, which the student never asked for).
   * `step_index: 141`: *"The reason you feel that knot in your chest is because your instincts are telling you the truth... The Cruel Lie of the University Semester..."*
   * `step_index: 147`: Unsolicited pitch on *"Oxford and Cambridge"* and *"Bloom's 2 Sigma Effect"*.
2. **Unsolicited Multi-Month Schedules (`step_index: 73`, `78`, `152`):**
   * In `step_index: 73` and `SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md` (lines 120–126), the assistant scheduled the student's entire life from October 2026 through August 2027:
     * *Fall 2026 (Oct–Dec):* CS 511 & CS 442 Harvesting
     * *Winter Break (3 Weeks):* OSTEP (Virtualization & Persistence)
     * *Spring Co-op (Jan–April):* Kurose & Ross Computer Networking Ch 1–3 + Kleppmann's DDIA
     * *Summer Co-op (May–August):* Nand2Tetris + Crafting Interpreters

---

## Part 2: Primary-Source Analysis of the Two YouTube Workflows

### 2.1 Video 1: Eero Alvar — *"How I Use AI to Learn Things"* (`https://www.youtube.com/watch?v=kzcI5F4tGiU`)

* **Creator:** Eero Alvar (`@amosblomqvist` on GitHub)
* **Published:** August 14, 2026 (Duration: `18:58`, ~1.1M views)
* **Paired Repositories:**
  * [`amosblomqvist/learn`](https://github.com/amosblomqvist/learn) (Created Aug 24, 2026; **4,277 stars, 456 forks** — `.pi` agent harness configuration)
  * [`amosblomqvist/learnharness`](https://github.com/amosblomqvist/learnharness) (Created Oct 16, 2026; **10,906 stars, 1,428 forks** — standalone Next.js + Electron desktop application evolution)
* **Video Chapter Timestamps:**
  * `0:00` Intro | `0:25` How we're used to learning | `0:55` One teaches many | `1:42` One learns from many | `3:08` One-to-one | `4:22` The approach | `5:13` The process | `8:01` Demo (Differential Forms toward Maxwell's Equations) | `10:12` Probe | `12:07` Plan | `13:04` Teach | `17:54` Close

#### A. Theoretical Premise: Eliminating the Two Many-to-Many Inefficiencies (`0:25`–`5:12`)
Alvar models traditional education as a **many-to-many bipartite graph** between *outlets* (teachers, textbooks, courses, videos) and *learners*, identifying two fundamental structural inefficiencies:
1. **Direction 1 — One Outlet Teaches Many (`0:55`–`1:41`):**
   * A resource built for $N$ students cannot be optimal for any single student because optimal teaching depends entirely on the learner's **exact current cognitive state**—both the macro teaching arc (from current understanding to target goal) and every micro-explanation along the way.
   * An optimal path minimizes two wastes simultaneously: (a) teaching concepts the learner already holds, and (b) teaching concepts for which the learner lacks prerequisites. It operates strictly at the **exact edge of understanding**.
2. **Direction 2 — One Student Learns from Many Outlets (`1:42`–`3:07`):**
   * Context-switching across textbooks, lecture slides, and YouTube channels imposes extraneous cognitive load (conflicting notations, varying interfaces, shifting pedagogical styles).
   * **The Epistemic Trust Tax:** Alvar notes a deeper cognitive penalty: when facing an unfamiliar source, *"the brain kind of hedges. So, it won't fully commit to accepting a fact until the outlet has proven itself."* (He contrasts an identical explanation of the Hairy Ball Theorem delivered by 3Blue1Brown vs. a random X post: the brain internalizes the trusted source effortlessly while expending working memory doubting the unverified source).
3. **The One-to-One Synthesis & Engineered Trust (`3:08`–`5:12`):**
   * Alvar separates **sources** (many perspectives) from the **interface** (one teacher fitted to one mind).
   * With AI, trust cannot be assumed—it must be **engineered into the system** via automated fact-checking subagents so the learner's brain stops hedging.
   * **Effort Allocation Invariant (`4:40`–`5:12`, codified in `learnharness/docs/teaching-methodology.md` §7a):**
     > *"This does not mean removing difficulty. Instead, it's about concentrating all cognitive work into the material itself. We want to maximize struggle. We want to learn difficult things, so struggling is very important, but it has to be in the material itself and not in logistics, planning, finding resources, verifying facts, figuring out what to learn and in what order. All of that is for the system to absorb."*

#### B. The Three-Phase Execution Pipeline & Code Mapping (`5:13`–`17:54`)

| Phase | Video Walkthrough & Live Demo (`8:01`–`17:54`: Learning Differential Forms) | Implementation in `amosblomqvist/learn` (`.pi` Config) | Evolution in `amosblomqvist/learnharness` (Desktop App) |
| :--- | :--- | :--- | :--- |
| **Phase 1: Probe** (`5:20`, Demo `10:12`–`12:06`) | Before teaching a single word about differential forms, the agent fires a sequence of graded multiple-choice questions to **binary-search the boundary** of Alvar's knowledge across every prerequisite strand: <br>1. Line integral of force field $\mathbf{F}$ along curve $C$ (Alvar uses the free-text note box to talk through why `#1` only holds for conservative fields and picks `#3: Net work done`). <br>2. Divergence as net outward flux per unit volume. <br>3. Stokes' Theorem & Faraday's Law of Induction. <br>4. Special Relativity Lorentz transformations of $\mathbf{E}$ and $\mathbf{B}$ fields (Alvar isn't sure, selects **`"I don't know"`** rather than guessing; system reveals `"They mix"` and terminates probing on that ceiling). | • `skills/teach/SKILL.md` (Phase 1): Mandates **bracketing the edge** (finding both the solid floor and the failure ceiling on each prerequisite strand). <br>• `extensions/quiz.ts`: Renders a native TUI picker with Fisher-Yates option shuffling (`shuffleOptions`), auto-injects an exclusive `"I don't know"` (`__dont_know__`) option, and provides a Tab-accessible `Note (optional):` talk-through box. <br>• Enforces 4-step anti-leak distractor construction (bare claims, zero `"because..."` justifications, same grain size). | Dedicated **Prober** runtime agent (`src/agent/`) equipped with `probe`, `recall`, `ask_user_question`, and `probe_done`. Reads prior proposition graph before probing so known concepts are never re-quizzed. Calling `probe_done` hands off a structured diagnostic summary to the Teacher agent. |
| **Phase 2: Plan** (`6:00`, Demo `12:07`–`13:03`) | Once probing finishes, the agent dispatches the background `researcher` subagent to verify facts and outputs a **Mermaid.js dependency DAG (`graph TD`)** into Obsidian (via `md-log`) mapping the exact path from verified prerequisites to Generalized Stokes' Theorem and Maxwell's Equations. <br>**Alvar's Dual Rationale for the Mermaid DAG (`6:12`–`6:35`):** <br>1. *For the Learner:* Provides an upfront visual Advance Organizer of where the journey is going. <br>2. *For the LLM (The Real Reason):* *"The actual reason I implemented it is to actually force the AI to reason everything out. That's the real reason. So, it cannot just cheat and wing it."* | • `skills/teach/SKILL.md` (Phase 2): Dispatches `agents/researcher.md` (fact-checking subagent). Outputs prose approach + small Mermaid `graph TD` (unconditional truths at roots, target goal at sink). <br>• Enforces a hard consent gate: *"Then stop and wait for his go-ahead... Do not begin Phase 3 until he okays the plan."* | Teacher agent calls `plan_init`, which programmatically validates and commits the dependency DAG to the session state and renders it in the UI header. Formalized in `docs/teaching-methodology.md` §7b (*The minimal tree*). |
| **Phase 3: Teach & Verify** (`6:36`, Demo `13:04`–`17:54`) | Traverses the Mermaid DAG **one reasoning step at a time**: <br>• *"What usually happens if you're talking to ChatGPT... it's way too excited and it rushes through the whole thing. And so, I like to keep this very slow, one reasoning step at a time."* (`13:55`) <br>• **Node 1 (Covectors):** Introduces covectors and $dx$ as a linear functional. Spawns `svg-maker` subagent in the background; `svg-maker` writes an SVG, renders it to PNG, views its own image to fix layout overlaps, and embeds it into Obsidian. <br>• **Lock-in Quiz:** Immediately quizzes Node 1: *"Let $\alpha = 3\,dx - 2\,dy$ and $v = (2, 5)$. What is $\alpha(v)$?"* Alvar computes $3(2) - 2(5) = -4$ and locks in the node. <br>• **Node 2 (Covector Fields & 1-Forms):** Connects covector fields to line integrals, states the unconditional truth (*"All integration over a 1D thing is the integration of a 1-form"*), and advances to Wedge Products ($\wedge$, bilinear & antisymmetric). | • `skills/teach/SKILL.md` (Phase 3): Enforces the 4-step per-node loop (**1. Motivate $\to$ 2. Establish $\to$ 3. Connect $\to$ 4. Quiz-check**) and the two core pedagogical rules: <br>  - **Principle i (Unconditional truths first):** Universal statements with zero caveats so the brain commits without hedging. <br>  - **Principle ii (Motivated discovery):** Show *why* a definition or manipulation is needed before naming it. <br>• `agents/svg-maker.md` & `agents/mermaid-maker.md` + `extensions/visual-tools/index.ts`: Render-and-inspect loop (`rsvg-convert` / `mmdc`). | • **Teacher** agent + non-disruptive **Side Question** threads (`components/side-thread.tsx`) so mid-step questions never derail the DAG. <br>• **PDF Figure Cropping (`src/agent/tools/pdf-figure.ts`):** Visual subagent crops diagrams straight out of the user's local lecture slide PDFs at 300 DPI and overlays SVG annotations. <br>• **Practitioner** agent (`kind: "practice"`) + **Persistent Proposition Graph** (`graph/{nodes,chains,sessions,coverage}.jsonl`). |

---

### 2.2 Video 2: Aleks Gornik — *"How I use AI to learn engineering (anti brain rot studying)"* (`https://www.youtube.com/watch?v=GPM5MgFEkpk`)

* **Creator:** Aleks Gornik (Electrical Engineering graduate; Member of Technical Staff at an LLM training startup)
* **Published:** October 2026 (Duration: `12:44`, ~491k views, 8.7k likes)
* **Core Premise:** AI should accelerate engineering comprehension not by outsourcing the cognitive work (*"not by doing the work for me"*), but by acting as a **visual rendering engine, a syllabus-anchored noise filter, an 80/20 execution unblocker, and a multi-agent resource crawler**.

#### The Four-Part Operational Engineering Workflow

1. **Part 1: Interactive 3D & Hardware/System Visualization Dashboards**
   * **The Problem:** Static slides, terrible professor lecture recordings, and dense hardware datasheets (e.g., wiring an STM32 microcontroller to an ST-LINK V3 debugger for power measurements) create high spatial/mechanical friction.
   * **The AI Workflow:** Prompt coding agents (Claude Code, GPT Codex) using frontier models to generate self-contained **interactive HTML/3D presentations and step-by-step wiring dashboards**:
     * *Project Ideation & 3D CAD Preview:* *"Hey Claude, I want to build a robotics project, but I'm not really too sure where to start. Give me three ideas for an interactive presentation. Pitch them to me. Tell me why this one is the best one and why should I build it and make a 3D model out of it so I can see it."* (Allows spinning, zooming, and inspecting geometry in-browser).
     * *Multimodal Hardware Pinout Dashboard:* Take a photo of physical hardware/boards alongside the datasheet and prompt: *"Make me an interactive dashboard or presentation showing me how to wire the STM32 together to this other piece of hardware so I can take power readings."* Generates a step-by-step visual pinout tool showing exact wire-to-pin mappings.

2. **Part 2: Syllabus-Anchored Corpus Filtering (Pruning 1,000-Page Reading Lists)**
   * **The Problem:** University professors hand out bibliographies of five 1,000-page textbooks (some written in 1970), and ML fields produce dozens of papers weekly. Reading them cover-to-cover is a guaranteed time sink.
   * **The AI Workflow:** Feed the **course syllabus + exam scope + reading list** into the LLM and execute a hierarchical two-stage zoom filter:
     * *Stage A (Book/Paper Selection):* Rank which single book or paper is highest-signal and most legitimate for the specific syllabus.
     * *Stage B (Chapter & Problem Isolation):* Zoom inside the winning book to isolate only the 1–3 chapters and exact tutorial problems that map to the upcoming exam.
   * **Gornik's Exact Canonical Prompt:**
     > *"Here's my module/class syllabus, and here is the reading list. Which books and chapters from this book are actually worth my time considering my specific curriculum and the exams I'm going to sit? Which tutorial problems are worth doing?"*

3. **Part 3: 80/20 Execution Bottleneck Pruning (Minimum Viable Knowledge to Unblock Action)**
   * **The Problem:** When building an engineering thesis or complex project (Gornik cites his thesis on Graph Neural Networks simulating airway flow in the lungs), learners get paralyzed by the combinatorial explosion of theoretical concepts (forward passes, softmax vs. tanh vs. ReLU, matrix calculus, backpropagation derivations, Transformers vs. GNNs).
   * **The AI Workflow:**
     * Ask the LLM to isolate the **minimal ~20% operational mechanics** required to get a working loop running right now.
     * In Gornik's GNN thesis: he deferred formal backpropagation proofs and architecture taxonomy, using AI to isolate just *"how do I use PyTorch to run some data over a neural network, get a training loop going, see a few epochs, feed it some training data."*
     * Once the 20% operational trunk is running and unblocked, loop back to backfill the remaining 80% theoretical depth on demand.

4. **Part 4: Parallel Subagent Resource Discovery (With Manual Hallucination Verification)**
   * **The Problem:** Searching manually across Google for specialized engineering artifacts (datasets, reference implementations, CAD `.stl` assemblies) takes 10+ hours and surfaces low-quality tutorials.
   * **The AI Workflow:**
     * Dispatch parallel subagents to crawl the web for high-signal open-source primary artifacts (e.g., Gornik dispatched subagents to find open-source NASA Mars Rover and satellite `.stl` 3D CAD assemblies).
     * **Mandatory Human Verification Gate:** *"Just make sure you click on the links and double-check that everything is legit because AI does hallucinate still."*

---

## Part 3: The Three Cognitive Science Papers & "AI Knowledge Tree Mapping" (Semantic Tree)

The viral "Knowledge Tree Mapping" / "Semantic Tree" / "Pareto 80/20 Curriculum Mapping" workflows documented in `docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf` are direct prompt-engineering translations of three foundational cognitive psychology papers published between 1960 and 1984.

### 3.1 Deep-Dive into the Three Foundational Papers

#### 1. David P. Ausubel (1960) — *"The Use of Advance Organizers in the Learning and Retention of Meaningful Verbal Material"*
* **Citation:** *Journal of Educational Psychology*, Vol. 51, No. 5, pp. 267–272 (October 1960). DOI: `10.1037/h0046669`. (Expanded in Ausubel, *Educational Psychology: A Cognitive View*, 1968).
* **Core Theoretical Mechanisms:**
  1. **Subsumption Theory & Hierarchical Cognitive Structure:** Ausubel posits that human cognitive structure is *"hierarchically organized in terms of highly inclusive concepts under which are subsumed less inclusive subconcepts and informational data"* (p. 267). Meaningful learning (as opposed to rote memorization) occurs only when new material can be anchored (**subsumed**) under relevant existing concepts (*subsumers*) in the learner's memory.
  2. **Prior-Knowledge Calibration:** Summarized in the famous epigraph to Ausubel (1968): *"If I had to reduce all of educational psychology to just one principle, I would say this: The most important single factor influencing learning is what the learner already knows. Ascertain this and teach him accordingly."*
  3. **Advance Organizers (Expository vs. Comparative):** Introductory conceptual material presented *prior* to detailed study at a **higher level of abstraction, generality, and inclusiveness** than the learning task itself.
     * *Expository Organizers:* Provide ideational scaffolding for completely unfamiliar material.
     * *Comparative Organizers:* Activate existing schemas for partially familiar material, explicitly integrating similarities and increasing discriminability against confusable concepts.
     * In Ausubel's 1960 controlled experiment (80 undergraduates studying a 2,500-word passage on the metallurgical properties of steel), students given a 500-word conceptual Advance Organizer retained significantly more material after 3 days than students given a historical overview control passage.
  4. **Progressive Differentiation vs. Correlative Subsumption vs. Obliterative Subsumption:**
     * **Progressive Differentiation:** Top-down curriculum sequencing where the most general, inclusive ideas of a discipline are presented first and then progressively differentiated in terms of detail and specificity.
     * **Derivative vs. Correlative Subsumption:** *Derivative subsumption* attaches a new specific example that directly illustrates an established general concept; *correlative subsumption* extends, modifies, or elaborates an existing concept to accommodate a new branch.
     * **Decelerating Obliterative Subsumption (Why the Student Forgot CS 382/392/496/526):** Ausubel proves that forgetting is a process of *memorial reduction* (*obliterative subsumption*). When facts are learned by rote without being anchored to stable, superordinate trunk concepts, they cannot be reconstructed once surface details decay—they evaporate immediately after the exam. When anchored to strong superordinate subsumers, retention is dramatically prolonged.

#### 2. Allan M. Collins & M. Ross Quillian (1969) — *"Retrieval Time from Semantic Memory"*
* **Citation:** *Journal of Verbal Learning and Verbal Behavior*, Vol. 8, No. 2, pp. 240–247 (April 1969). DOI: `10.1016/S0022-5371(69)80069-1`. (Building on Quillian's 1966 Carnegie Institute of Technology dissertation on Teachable Language Comprehender semantic networks).
* **Core Theoretical Mechanisms:**
  1. **Hierarchical Semantic Tree Topology:** Models human long-term semantic memory as a directed hierarchical tree of nodes (concepts) connected by **superset pointers ($S$)** (e.g., `Canary` $\to$ `Bird` $\to$ `Animal`) and **property pointers ($P$)** stored at each level.
  2. **Cognitive Economy (Property Inheritance & Rule Deduplication):**
     * Instead of redundantly storing the properties `"has skin"`, `"breathes"`, and `"eats"` at every single animal node (`Canary`, `Ostrich`, `Shark`, `Salmon`), or storing `"has wings"` and `"can fly"` at every single bird species node, human memory achieves **cognitive economy** by storing shared invariants at the **highest parent node where they hold true** (`Animal` or `Bird`).
     * Subordinate child nodes (`Canary`, `Salmon`) store **only their differentiating local properties or explicit overrides** (e.g., `Canary` stores `"is yellow"` and `"can sing"`; `Ostrich` stores the exception `"can't fly"` to override the inherited `Bird` rule).
  3. **Empirical Reaction-Time Verification:** Collins & Quillian proved via reaction-time experiments (~75 ms per hierarchical level traversal) that humans verify *"A canary can sing"* (0 levels, stored at `Canary`) faster than *"A canary can fly"* (1 level up, inherited from `Bird`), which is faster than *"A canary has skin"* (2 levels up, inherited from `Animal`).
  4. **Implication for Technical Learning:** If a student learns 20 specific algorithms, SQL queries, or synchronization problems as flat, isolated nodes without establishing the parent invariant node (e.g., *Monitor Mesa Semantics: `while (!cond) wait()`*), the student must memorize 20 redundant rules (zero cognitive economy). If the student masters the parent trunk node first, all 20 child problems inherit the rule automatically.

#### 3. Joseph D. Novak & D. Bob Gowin (1984) — *"Learning How to Learn"* (Concept Maps)
* **Citation:** Cambridge University Press (1984). DOI: `10.1017/CBO9781139173469`. (Along with Novak & Cañas, 2006, *"The Origins of the Concept Mapping Tool"*, *Information Visualization*, 5(3), 175–184; and Novak, 2002, *Science Education*, 86(4), 548–571).
* **Core Theoretical Mechanisms:**
  1. **Externalized Propositional Graphs (Nodes + Explicit Labeled Relational Links):**
     * Invented by Novak's Cornell research team in 1972 during a 12-year longitudinal study tracking 191 children's science comprehension from Grade 1 to Grade 12.
     * Unlike informal "mind maps" (which connect words with unlabeled lines), Novak defines a **Concept Map** as a formal **propositional network** where two or more concept nodes are joined by **explicitly labeled linking words/verbs** to form a self-contained semantic unit or **proposition** (e.g., `[Monitors] --enforce--> [Mutual Exclusion] --via--> [Implicit Lock]`).
  2. **Top-Down Hierarchical Ordering & Cross-Links:**
     * Concepts are arranged strictly from the **most general, most inclusive superordinate concepts at the apex (root)** down to specific sub-branches and concrete examples at the leaves.
     * **Cross-Links:** Explicit horizontal/diagonal links connecting concepts in two different branches of the hierarchy. Novak demonstrates that identifying cross-links drives **Integrative Reconciliation** (resolving confusions between deceptively similar concepts across domains) and creative synthesis.
  3. **Working-Memory Cognitive Load Reduction & Misconception Detection:**
     * Novak & Gowin showed that a 15-to-20-page verbal transcript can be compressed into a 1-page hierarchical concept map without losing propositional meaning.
     * Externalizing the hierarchy onto a visual graph frees working memory from holding structural topology while learning node details, and makes **Limited or Inappropriate Propositional Hierarchies (LIPHs)** (missing prerequisites or faulty links) immediately visible to both teacher and learner.

---

### 3.2 Synthesis: How Elon Musk's Semantic Tree & the Pareto 80/20 Curriculum Mapping Prompt Translate the Three Papers

In his **January 5, 2015 Reddit AMA (`r/IAmA`: *"I am Elon Musk, CEO/CTO of a rocket company, AMA!"*)**, when asked how he learns rapidly across disparate technical domains, Musk stated:

> *"One bit of advice: it is important to view knowledge as sort of a semantic tree — make sure you understand the fundamental principles, ie the trunk and big branches, before you get into the leaves/details or there is nothing for them to hang on to."*

The **"Tree & Branches" Pareto 80/20 Master Prompt** (from `docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`, pages 1–2) operationalizes Musk's quote and the three cognitive science papers into a 5-part LLM schema plus a 3-tag Syllabus Triage classifier:

| Prompt Component (`Branch • AI Knowledge Tree Mapping Workflow.pdf`) | Cognitive Science Mechanism Being Executed | Pedagogical Function in AI Tutoring |
| :--- | :--- | :--- |
| **1. The Roots (Prerequisites):** *"What 3–5 mental models or prior concepts must I understand before touching this subject?"* | **Ausubel (1960 / 1968):** Prior-Knowledge Calibration & Pre-existing Anchoring Subsumers. | Prevents the "Cumulative Snowball" (`transcript.jsonl`, `step_index: 137`) by identifying missing prior-course foundations (e.g., MA 125 row operations before MA 232 subspaces) before teaching begins. |
| **2. The Trunk (Core Fundamentals — The 20%):** *"Identify the non-negotiable foundational laws, principles, or mechanics that govern 80% of this field. Explain why everything else breaks if I don't master these."* | **Ausubel (1960):** Expository Advance Organizer & Superordinate Subsumers. <br>**Collins & Quillian (1969):** Root/Parent Nodes storing shared domain invariants for Cognitive Economy. | Forces the LLM to reject flat chronological lecture order (`mohitagw15856/pm-claude-skills` Rule 1) and extract the 20% invariant laws (Alvar's *Unconditional Truths*) that everything else inherits from. |
| **3. The Main Branches (Major Subfields/Modules):** *"List the primary directions the trunk splits into, and explicitly state which trunk concept each branch depends on."* | **Ausubel (1960):** Progressive Differentiation & Correlative Subsumption. <br>**Collins & Quillian (1969):** Superset-to-Subset inheritance pointers ($S$). | Maps how course modules differentiate from the trunk (e.g., how Semaphores, Java Monitors, and Erlang Actors in CS 511 are three distinct branches solving the same Trunk problem of non-deterministic state interleaving). |
| **4. The Leaves (Applications, Edge Cases & Noise):** *"Identify what course content is just specialized trivia, historical context, or niche applications that I can safely skim or learn on-demand later."* | **Collins & Quillian (1969):** Leaf-level local property overrides ($P_0$). <br>**Gornik (`GPM5MgFEkpk`):** 80/20 Corpus & Bottleneck Pruning. | Protects working memory from drowning in peripheral trivia before the trunk is solid; tags low-leverage material for exam-only skimming. |
| **5. Cross-Links:** *"Point out where two separate branches unexpectedly connect."* | **Novak & Gowin (1984):** Propositional Cross-Links & Integrative Reconciliation. | Explicitly bridges separate courses/modules (e.g., connecting CS 496 OCaml immutability/pattern-matching to CS 511 Week 8 Erlang actors, or MA 232 matrix projections to MA 331 linear regression). |
| **Syllabus Audit Classifier:** *"Tag every week's topic as either `[TRUNK - Must Master]`, `[BRANCH - Applied Concept]`, or `[LEAF - Memorize for Exam Only]`."* | **Novak & Gowin (1984):** Externalized Visual Concept Map reducing extraneous cognitive load. | Resolves **Grievance A** (Dual-Layer Structure) and **Grievance B** (Course Logistics) simultaneously: gives the student an instant triage map of their professor's syllabus so 70%+ of active drill time targets `[TRUNK]` concepts. |

---

## Part 4: Architectural Evaluation — Matt Pocock's `skills/teach/SKILL.md` vs. Standalone Field & Course Mastery Skill(s)

### 4.1 Audit of Matt Pocock's Current `skills/teach/SKILL.md`

Inspection of `C:\Users\dersu\Code Stuff\dersu-agent-skills\skills\teach\` (`SKILL.md` + `MISSION-FORMAT.md`, `RESOURCES-FORMAT.md`, `LEARNING-RECORD-FORMAT.md`, `GLOSSARY-FORMAT.md`) reveals a highly cohesive, stateful workspace architecture built around **bottom-up, capability-driven HTML lessons**:

* **What `skills/teach/SKILL.md` Is Designed For:**
  1. **Single-Sitting Self-Contained HTML Lessons (`./lessons/0001-<slug>.html`):** *"A lesson is a single, self-contained HTML output that teaches one tightly-scoped thing tied to the mission. This is the primary unit of teaching in this workspace."* (`SKILL.md` line 18).
  2. **Reusable Frontend Component Library (`./assets/*`):** Shared Tufte-style stylesheets, interactive browser quiz widgets, and simulators shared across HTML lessons (`SKILL.md` lines 63–70).
  3. **Printable HTML Cheat Sheets (`./reference/*.html`):** Compressed reference sheets (syntax, yoga sequences, glossaries) designed to print well (`SKILL.md` line 15, 122–136).
  4. **Web-Research & Community Delegation (`RESOURCES.md`):** Populates external links under `## Knowledge` and delegates real-world wisdom to online/offline communities under `## Wisdom (Communities)` (`SKILL.md` lines 112–121).
  5. **ADR-Style Longitudinal ZPD Logs (`./learning-records/0001-<slug>.md`):** Tracks demonstrated understanding, disclosed prior knowledge, and corrected misconceptions (`LEARNING-RECORD-FORMAT.md`).

* **Where `skills/teach/SKILL.md` Diverges from Field/Course Mastery & the `School Code` Grievances:**
  1. **Bottom-Up Correlative Subsumption vs. Top-Down Semantic Tree:** `teach` deliberately skips upfront macro curriculum mapping (no Advance Organizer, no Collins & Quillian dependency tree, no `[TRUNK]` vs. `[BRANCH]` vs. `[LEAF]` syllabus triage). It builds incrementally one HTML capability at a time from `MISSION.md`.
  2. **Heavy HTML Authoring Overhead vs. Rapid Repetitive Problem Drilling:** Generating a polished, Tufte-styled `./lessons/NNNN-<slug>.html` file and shared `./assets/*` components for every single turn is ideal for learning a practical craft (e.g., CSS Grid, yoga poses, Rust CLI basics), but **catastrophically slow when a student has 4 university STEM courses and wants to rapidly drill 15 relational algebra queries, semaphore interleavings, or matrix row reductions in chat** (Grievance B & E).
  3. **External Web Discovery vs. Local Course Corpus Ingestion:** `teach` assumes the agent needs to search the web to populate `RESOURCES.md`. In `School Code`, the primary corpus *already exists on disk* (`Course Slides/*.pdf`, `Exercises/eb1.pdf`–`eb9.pdf`, `MA331RMD01.html`–`06.html`, `Syllabus.md`), and the student needs the agent to index those local files, flag gaps against the syllabus (`mohitagw15856/pm-claude-skills` Rule 5), and serve drills directly from them.
  4. **No Diagnostic Binary-Search Pre-Test (`Probe`) or Native Question-Tool Lock-In Gates:** `teach` relies on in-browser HTML quizzes inside the lesson file rather than gating conversational progression turn-by-turn via the harness's native `question` tool (`3 distractors + "I don't know" + talk-through note`).

---

### 4.2 Deep Evaluation of the Three Architectural Options

#### Option 1: Modifying Matt Pocock's `skills/teach/SKILL.md` In-Place (Monolithic Hybrid Skill)

Under Option 1, `skills/teach/SKILL.md` is rewritten to incorporate Top-Down Semantic Tree Mapping (`Roots -> Trunk -> Branches -> Leaves`), Academic Syllabus/PDF Triage, Diagnostic Binary-Search Probing, Dual-Layer Mode Routing (Fast Exam/Assignment Triage vs. Deep Trunk Mastery), and Repetitive Chat/Code Problem Drills alongside its existing HTML lesson (`./lessons/*.html`) and `./assets/*` pipeline.

| Pros of Option 1 | Cons of Option 1 |
| :--- | :--- |
| **1. Single Entry Point (`/teach`):** The user only ever has to remember and invoke one command (`/teach`) regardless of whether they are learning an informal hobby (yoga, strength training), a practical dev tool, or an academic university course (CS 511, MA 331). | **1. Severe Pedagogical & Artifact Conflict (HTML Lessons vs. Rapid Chat/Code Drills):** `teach/SKILL.md`'s core invariant is: *"A lesson is the main thing you produce... Each lesson is one self-contained HTML file, saved to `./lessons/`"* (line 49). Forcing a single skill to choose between authoring Tufte HTML pages with `./assets/*` components and running rapid-fire turn-by-turn Socratic terminal/math drills via the native `question` tool creates contradictory instructions. LLMs facing dual-artifact instructions routinely pick the wrong medium or blend them awkwardly. |
| **2. Reuses High-Value Format Schemas Automatically:** Directly inherits `LEARNING-RECORD-FORMAT.md` (ADR-style misconception & ZPD tracking), `GLOSSARY-FORMAT.md` (opinionated compressed definitions), `MISSION-FORMAT.md` (short compass rule), and `./reference/*.html` (printable exam cheat sheets, which directly match MA 331's open-note policy). | **2. Context Window Bloat & Instruction Dilution:** Combining Pocock's 7-file workspace specification (`MISSION.md`, `RESOURCES.md`, `NOTES.md`, `GLOSSARY.md`, `learning-records/*.md`, `lessons/*.html`, `reference/*.html`, `assets/*`) with Alvar's 3-phase `Probe -> Plan -> Teach` state machine, 4-step anti-leak quiz construction rules, Gornik's 80/20 syllabus corpus filter, and a 5-level hint escalation ladder pushes the skill well past optimal prompt-compliance density, increasing the risk that the agent drops hard gates (like the Phase 2 Plan approval stop or the `"I don't know"` option). |
| **3. No Cross-Skill State Fragmentation:** Avoids having two different teaching skills writing incompatible state folders in the same directory. | **3. Breaks Upstream Parity with `mattpocock/skills`:** Currently, local `skills/teach/SKILL.md` is byte-identical to upstream `mattpocock/skills/productivity/teach/SKILL.md`. Heavily mutating it destroys upstream sync and breaks the clean, lightweight behavior when the user *actually wants* Pocock's bottom-up HTML tutorial generator for a non-academic skill. |

---

#### Option 2: Keeping `skills/teach/SKILL.md` Separate + Creating One Standalone Field & Course Mastery Skill (e.g., `master` / `course-mastery` / `learn`)

Under Option 2, Matt Pocock's `skills/teach/SKILL.md` remains untouched (reserved for bottom-up, capability-specific single-sitting HTML tutorials and reference sheets), while a dedicated standalone skill is created specifically for **Field & Course Mastery** (combining Top-Down Semantic Tree / DAG Mapping + Local Syllabus/Corpus Triage + Diagnostic Probing + Node-by-Node Socratic Teaching & Repetitive Practice Drills).

| Pros of Option 2 | Cons of Option 2 |
| :--- | :--- |
| **1. Clean Separation of Bottom-Up Craft vs. Top-Down Discipline Mastery:** <br>• Use `/teach` (Pocock) when you want a self-contained HTML tutorial and reusable browser widget for a specific capability. <br>• Use the new standalone skill when you want to master an academic course (`CS 511`, `CS 442`, `MA 331`, `MA 232`) or technical field (`TeachYourselfCS` / `OSTEP` / `DDIA`) via a top-down Semantic Tree (`[TRUNK]` vs. `[BRANCH]` vs. `[LEAF]`), diagnostic probing, and repetitive problem drills. | **1. Four Distinct Cognitive Modes Still Share One Skill Prompt:** Even without Pocock's HTML lesson pipeline, a single Field & Course Mastery skill must still orchestrate four distinct phases: <br>(a) *Corpus Ingestion & Semantic Tree Mapping* (reading syllabi/PDFs, tagging `[TRUNK]`/`[BRANCH]`/`[LEAF]`), <br>(b) *Diagnostic Binary-Search Probing* (`Probe`), <br>(c) *1-Node-at-a-Time Conceptual Teaching* (`Teach`), and <br>(d) *High-Volume Repetitive Exam/Homework Problem Drilling* (`Practice`). |
| **2. Zero HTML Ceremony During High-Stress Coursework:** The standalone skill can dedicate 100% of its turn budget to fast, low-friction interaction: native `question` tool checkpoints (with `"I don't know"` and talk-through notes), Mermaid dependency DAGs, cropped/annotated PDF figures or focused SVG/HTML visualizers only when spatial clarity demands it, and rapid 3-depth practice problems (`[recall]`, `[apply]`, `[why X not Y]`). | **2. Risk of Phase-Skipping Inside a Long Session:** As seen in `vasanthsreeram/Alvarmethod` and `amosblomqvist/learnharness`, when a single agent prompt holds the rules for Probing, Planning, Teaching, and Practicing simultaneously, the model can sometimes rush Phase 1 (`Probe`) or blur Phase 3 (`Teach`) with Phase 4 (`Practice`) unless strict phase-transition gates and sub-reference files (`references/*.md`) are enforced. |
| **3. Unified Course Workspace State:** Because a student working inside `CS 511/` or `MA 331/` invokes one skill for that course, all state artifacts—the Semantic Tree syllabus map (`CURRICULUM-MAP.md` or `.learn/map.md`), learner anti-slop profile (`LEARNER.md`), ADR-style learning records (`learning-records/*.md`), and drill weak-point ledger—live in one coherent workspace schema without needing manual handoffs between separate skills. | **3. Slight Overlap in Persistence Schemas with `teach`:** If the standalone skill also uses `learning-records/*.md` and `GLOSSARY.md` (which are genuinely best-in-class designs from Pocock's `teach`), those format templates must either be symlinked/shared or duplicated into the new skill directory. |
| **4. Directly Solves All Six `School Code` Grievances in One Command:** At Turn 0, the standalone skill reads the local course folder + `LEARNER.md` (no life coaching, no semester schedules) and presents a single native `question` picker: <br>*(1) Map/Triage Course Trunk vs. Branches*, <br>*(2) Deep-Learn a Trunk Node (`Probe -> Plan -> Teach`)*, or <br>*(3) Drill Practice Problems on Target Topic/Exam*. | |

---

#### Option 3: A Multi-Skill Family (Separating Macro Curriculum Mapping / Triage from Node-by-Node Teaching and Repetitive Drilling)

Under Option 3 (modeled on `amosblomqvist/learnharness`'s 3-agent separation of `Prober`, `Teacher`, and `Practitioner`, `vasanthsreeram/Alvarmethod`'s 5-skill pack `learn-profile`, `probe`, `teach`, `learn-visual`, `learn-verify`, and `iannbing/skills-for-learning`'s separation of `tutorial` vs. `guide`), the workflow is split into 2 to 3 specialized, composable skills sharing a common local workspace folder (while keeping Pocock's `teach` untouched or dedicated to HTML reference generation):
* **Skill A — Macro Curriculum Mapper & Course Triage (e.g., `curriculum-map` / `course-triage`):** Ingests local syllabi, slides, textbooks, and past exams; executes the Ausubel/Collins-Quillian/Novak Semantic Tree decomposition (`Roots`, `20% Trunk`, `80% Branches`, `Exam-Only Leaves`, `Cross-Links`); flags missing notes/syllabus gaps (`⚠ Gaps in your materials`); and writes the persistent dependency DAG + high-yield problem index to disk.
* **Skill B — One-Node-at-a-Time Diagnostic Tutor (e.g., `deep-learn` / `alvar-teach`):** Reads the dependency DAG from Skill A; runs the binary-search `Probe` via the native `question` tool (`known | edge | unknown | blocked`); locks the minimal prerequisite-to-goal Mermaid DAG; and walks down one node per turn (`Motivate -> Establish -> Connect -> Quiz-check`) with visual subagents.
* **Skill C — Repetitive Problem & Exam Drill Engine (e.g., `practice-drill` / `exam-drill`):** Pure high-repetition practice loop (modeled on `learnharness`'s `Practitioner` + `pm-claude-skills` 3-depth retrieval questions + `iannbing/guide`'s 5-level hint escalation ladder). Serves Problem 1 from the course exercise booklet (`eb1`–`eb9`) or generated drill bank, waits for the student's work, escalates hints L1$\to$L5 only when stuck, logs L3+ struggles into `learning-records/` / `weak-points.md`, and immediately serves Problem 2 with zero lecture monologue.

| Pros of Option 3 | Cons of Option 3 |
| :--- | :--- |
| **1. Maximum Prompt Precision & Zero Mode Confusion:** Each skill has a single, unmistakable job and a deterministic **Completion Criterion**. When the student invokes `/practice-drill` at 11:30 PM before a CS 511 quiz, it is structurally impossible for the agent to launch into a macro syllabus roadmap or a long conceptual lecture—its prompt *only* knows how to serve a problem, grade/hint via the 5-level ladder, log weak points, and serve the next problem. | **1. Invocation & Routing Friction for a Fatigued Student:** A core finding of the `School Code` autopsy (Grievance B & D) is that when the student is exhausted at 1:00 AM between OAs and midterms, **any meta-decision overhead causes friction**. Requiring the student to remember whether to type `/course-triage`, `/deep-learn`, or `/practice-drill`—and manually switching skills mid-session when a practice drill reveals a missing trunk concept—reintroduces logistical friction unless one skill acts as an automatic router. |
| **2. Mirrors `learnharness`'s Proven Production Architecture:** Eero Alvar discovered while scaling `amosblomqvist/learn` into `amosblomqvist/learnharness` (`docs/architecture.md`) that separating `Prober`, `Teacher`, and `Practitioner` into distinct agent roles with restricted toolsets prevented the LLM from cutting corners during probing or lecturing during practice sessions. | **2. Cross-Skill Schema Coupling:** All skills in the family must strictly adhere to a shared on-disk state contract (e.g., reading and updating the same `CURRICULUM-MAP.md` node statuses, `LEARNER.md` profile, and `learning-records/NNNN-<slug>.md` files). If one skill's format drifts, the handoff breaks. |
| **3. Directly Solves Grievance A (Dual-Layer Structure) at the Architectural Level:** <br>• **Long-Term CS Fundamentals Layer:** Handled by `curriculum-map` + `deep-learn` (mapping the field's Semantic Tree and building node-by-node storage strength). <br>• **Immediate Course Deadline / Exam Layer:** Handled by `course-triage` + `practice-drill` (isolating the exact 20% textbook chapters/exercise booklet problems for tomorrow's test and drilling them repetitively). | **3. Skill Namespace Proliferation:** Adds 2–3 new top-level skill directories to `dersu-agent-skills/skills/` alongside existing `teach`, `study-tutor`, and `code-tutor` (unless `study-tutor` and `code-tutor` are consolidated or deprecated in favor of the new architecture). |

---

### 4.3 Comparative Synthesis Matrix Across All Three Options

| Evaluation Dimension | Option 1: Modify `skills/teach/SKILL.md` In-Place | Option 2: Keep `teach` Separate + 1 Standalone Mastery Skill | Option 3: Multi-Skill Family (Macro Mapper/Triage + Node Tutor + Drill Engine) |
| :--- | :--- | :--- | :--- |
| **Preserves Pocock's Bottom-Up HTML Lesson Generator (`./lessons/*.html`)** | **No** (Pollutes or overrides HTML lesson generation with chat/code drilling rules) | **Yes** (`skills/teach/` stays 100% intact and upstream-compatible) | **Yes** (`skills/teach/` stays 100% intact; can optionally be called for printable `./reference/*.html` sheets) |
| **Top-Down Semantic Tree Mapping (Ausubel / Collins-Quillian / Novak)** | Bolted onto a bottom-up skill design | Built-in as Phase 1/2 of the standalone skill | Dedicated Macro Mapper skill (`Roots -> 20% Trunk -> 80% Branches -> Leaves -> Cross-Links`) |
| **Academic Course Corpus Ingestion (Syllabi, Local Slide PDFs, `eb1`–`eb9`)** | Weak (conflicts with `RESOURCES.md` web-first assumption) | Strong (dedicated local file inspection + syllabus gap detection) | Very Strong (dedicated corpus indexer writes persistent coverage & dependency map to disk) |
| **Guardrail Against AI Monologues, Leaps & Answers-Too-Easily (Grievances C, E, F)** | Moderate (high prompt density dilutes phase gates) | High (uses `question` tool gates + `LEARNER.md` anti-slop contract) | **Highest** (each skill has one narrow Completion Criterion; Drill Engine cannot lecture) |
| **Cognitive / Logistical Friction on a Stressed Student at 1:00 AM (Grievance B & D)** | Low invocation friction (1 command), high execution friction (HTML bloat) | **Lowest invocation friction** (1 command + Turn 0 `question` picker selects Map, Deep-Learn, or Drill) | Moderate invocation friction (2–3 commands, unless paired with a Turn 0 router or automatic handoff) |
| **Architectural Mitigation Strategy** | N/A | Use internal modular `references/*.md` files (`references/map-mode.md`, `references/teach-mode.md`, `references/drill-mode.md`) loaded on demand after Turn 0 mode selection so active prompt context stays razor-sharp. | Provide a primary entry skill that routes to the sub-modes, or expose 2 clean entry points (`/course-map` for macro setup/triage, `/drill` for daily node learning & problem repetition). |

> **Key Architectural Insight on Option 2 vs. Option 3:**  
> Progressive disclosure inside a skill directory (`SKILL.md` acting as a thin Turn-0 router that loads `references/macro-tree-triage.md`, `references/probe-and-teach.md`, or `references/practice-drill-engine.md` based on the user's 1-click selection in the native `question` tool) captures the **prompt-isolation benefits of Option 3** (zero instruction dilution between mapping, teaching, and drilling) while preserving the **zero-friction single-command UX of Option 2** (the student never has to remember which skill to invoke at 1:00 AM).

---

## Primary Source Citations

1. **School Code Session Transcript & Post-Mortem Artifacts:**
   * Compact Session Transcript (`205 steps`, Oct 1 – Nov 21, 2026): [`C:\Users\dersu\.gemini\antigravity-cli\brain\c1bc5e66-388e-4dae-9701-9bb2a7ec2694\.system_generated\logs\transcript.jsonl`](file:///C:/Users/dersu/.gemini/antigravity-cli/brain/c1bc5e66-388e-4dae-9701-9bb2a7ec2694/.system_generated/logs/transcript.jsonl)
   * Full Session Log: [`C:\Users\dersu\.gemini\antigravity-cli\brain\c1bc5e66-388e-4dae-9701-9bb2a7ec2694\.system_generated\logs\transcript_full.jsonl`](file:///C:/Users/dersu/.gemini/antigravity-cli/brain/c1bc5e66-388e-4dae-9701-9bb2a7ec2694/.system_generated/logs/transcript_full.jsonl)
   * Student Grievance Report: [`docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/SESSION_POSTMORTEM_AND_GRIEVANCES.md)
   * Root Catch-Up Artifact: [`C:\Users\dersu\Code Stuff\School Code\SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md`](file:///C:/Users/dersu/Code%20Stuff/School%20Code/SEMESTER_RECOVERY_AND_CATCHUP_GUIDE.md)
   * Course Workspaces Inspected: `C:\Users\dersu\Code Stuff\School Code\{CS 511, CS 442, MA 331, MA 232, CS 392, CS 382, CS 496, CS 526}`.
2. **YouTube Video 1 & Paired Repositories (Eero Alvar):**
   * Eero Alvar, *"How I Use AI to Learn Things"*, YouTube (Published Aug 14, 2026; `18:58`). [`https://www.youtube.com/watch?v=kzcI5F4tGiU`](https://www.youtube.com/watch?v=kzcI5F4tGiU)
   * Eero Alvar (`@amosblomqvist`), `amosblomqvist/learn` (`.pi` agent configuration, `skills/teach/SKILL.md`, `skills/visualize/SKILL.md`, `extensions/quiz.ts`, `extensions/md-log.ts`, `agents/{researcher,svg-maker,mermaid-maker}.md`). [`https://github.com/amosblomqvist/learn`](https://github.com/amosblomqvist/learn)
   * Eero Alvar (`@amosblomqvist`), `amosblomqvist/learnharness` (`docs/architecture.md`, `docs/teaching-methodology.md`, `skills/learnharness/SKILL.md`). [`https://github.com/amosblomqvist/learnharness`](https://github.com/amosblomqvist/learnharness)
3. **YouTube Video 2 (Aleks Gornik):**
   * Aleks Gornik, *"How I use AI to learn engineering (anti brain rot studying)"*, YouTube (Published Oct 2026; `12:44`). [`https://www.youtube.com/watch?v=GPM5MgFEkpk`](https://www.youtube.com/watch?v=GPM5MgFEkpk)
4. **Foundational Cognitive Science Papers & Semantic Tree Primary Sources:**
   * **David P. Ausubel (1960)**, *"The use of advance organizers in the learning and retention of meaningful verbal material"*, *Journal of Educational Psychology*, Vol. 51, No. 5, pp. 267–272. DOI: [`10.1037/h0046669`](https://doi.org/10.1037/h0046669).
   * **David P. Ausubel (1968)**, *Educational Psychology: A Cognitive View*, New York: Holt, Rinehart and Winston.
   * **Allan M. Collins & M. Ross Quillian (1969)**, *"Retrieval time from semantic memory"*, *Journal of Verbal Learning and Verbal Behavior*, Vol. 8, No. 2, pp. 240–247. DOI: [`10.1016/S0022-5371(69)80069-1`](https://doi.org/10.1016/S0022-5371(69)80069-1).
   * **Joseph D. Novak & D. Bob Gowin (1984)**, *Learning How to Learn*, Cambridge University Press. DOI: [`10.1017/CBO9781139173469`](https://doi.org/10.1017/CBO9781139173469).
   * **Joseph D. Novak & Alberto J. Cañas (2006)**, *"The Origins of the Concept Mapping Tool and the Continuing Evolution of the Tool"*, *Information Visualization*, Vol. 5, No. 3, pp. 175–184.
   * **Elon Musk (2015)**, *"I am Elon Musk, CEO/CTO of a rocket company, AMA!"*, Reddit `r/IAmA` (January 5, 2015). [`https://www.reddit.com/r/IAmA/comments/2rgsan/i_am_elon_musk_ceocto_of_a_rocket_company_ama/`](https://www.reddit.com/r/IAmA/comments/2rgsan/i_am_elon_musk_ceocto_of_a_rocket_company_ama/)
   * **AI Knowledge Tree Mapping Workflow Reference:** [`docs/research/Branch • AI Knowledge Tree Mapping Workflow.pdf`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/Branch%20%E2%80%A2%20AI%20Knowledge%20Tree%20Mapping%20Workflow.pdf)
5. **Local `teach` Skill & Supporting Verification Reports:**
   * Matt Pocock / Local `teach` Skill: [`skills/teach/SKILL.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/SKILL.md), [`skills/teach/MISSION-FORMAT.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/MISSION-FORMAT.md), [`skills/teach/RESOURCES-FORMAT.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/RESOURCES-FORMAT.md), [`skills/teach/LEARNING-RECORD-FORMAT.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/LEARNING-RECORD-FORMAT.md), [`skills/teach/GLOSSARY-FORMAT.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/skills/teach/GLOSSARY-FORMAT.md).
   * Primary-Source Verification Report: [`docs/research/learning-skills-primary-source-verification.md`](file:///C:/Users/dersu/Code%20Stuff/dersu-agent-skills/docs/research/learning-skills-primary-source-verification.md).
