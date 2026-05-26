---
title: Projects
permalink: /projects
---

## Close2Grad

**Problem:** When UF students miss three consecutive semesters, they're marked "discontinued" and can't re-enroll without a formal process. Many of these students were within reach of graduation, a few courses away, but had simply lost momentum and never returned. Others had completed the degree without formal certification and simply needed a system audit. No systematic process existed to identify them and reach back out.

**Approach:** With assistance from the Provost's Office, built a reporting system in the SIS to surface discontinued CLAS students close to completing their degree requirements. The CLAS Undergraduate Graduation Coordinator conducts personalized outreach: emails, phone calls, check-ins and works through whatever is in the way: re-enrollment paperwork, holds, financial obstacles. The data identifies who to contact; the human relationship moves them to act.

**Tools:** Snowflake, Campus Solutions (PeopleSoft SIS)

**Impact:** Since launching, the program has identified and contacted 38 discontinued students. 13 have graduated. Featured in [Ytori magazine (Spring/Summer 2025)](https://news.clas.ufl.edu/close2grad/).

> "I'm grateful to have a data coordinator and a graduation coordinator, who can find the time to work together to make progress like this. First and foremost for the students, of course, but writ large it helps the university achieve its goals of getting students their degrees."  
> — Former Associate Dean, College of Liberal Arts and Sciences

---

## Pre-Health Service Indicator

**Problem:** Pre-health students at UF had no reliable tracking mechanism. The closest thing was enrollment in a mailing list that wasn't actively maintained leaving advisors and administrators guessing at the actual population size. Demand forecasting for pre-health courses, and personalized tools like BCP/BCPM GPA visibility in the degree audit, were impossible without a clean, current population list.

**Achievement:** The technical build was straightforward. The hard part was navigating the institutional process: getting the concept approved, the service indicator created, the self-service website launched, and the workflow accepted as an ongoing operational process. Received approval from the Dean's office (December 2024), stood up the `PRE/HLTH` service indicator in Campus Solutions (January 2025), and launched student outreach to seed the population (February 2025). A Python script runs weekly to reconcile student opt-in requests against current indicators in Campus Solutions and apply bulk adds and removes.

**Tools:** Python, Snowflake, Campus Solutions (PeopleSoft SIS), MySQL (Acadvise), CLAS web infrastructure

**Impact:** Over 2500 students are now tracked with a clean, maintained record replacing years of guesswork using various methods such as membership in a mailing list or enrollment in a few majors. The indicator is intentionally built as a foundation: planned future uses include pre-health course demand prediction and surfacing BCP/BCPM GPAs directly in students' degree audits.

> "A game-changer for our ability to support students, especially as first-year pre-health advising responsibilities are transferred to departments, given that over 70% of biology majors aspire to health professions."  
> — Biology Advisor, College of Liberal Arts and Sciences

> "This system has already proven invaluable in allowing our office to proactively reach and guide students more effectively."  
> — Assistant Director of Pre-Health Advising, College of Liberal Arts and Sciences

---

## Quest Mass Enrollment System

**Problem:** Each May, thousands of incoming UF freshmen need to be placed into Quest 1 courses before orientation begins. The previous process was written in Ruby and enrollment was done manually.

**Approach:** Wrote a Query-Based Update (QBU) in Campus Solutions that allowed bulk enrollment based on a CSV file. Subsequently, rewrote and maintained the algorithm in Python (2024). The script reads student survey responses from Salesforce alongside course section data from Campus Solutions, then applies a tiered priority system. Within each tier, students are assigned a random number to break ties fairly. The algorithm runs multiple independent versions per term, each with a fresh shuffle, so the team can compare outcomes and select the best fit before submitting to the Registrar. Covers both Summer and Fall terms. Unassigned students are identified separately and assigned a Spring Quest hold. Final output is delivered as a CSV to OUR and UFIT for mass enrollment via Campus Solutions via previously engineered QBU.

**Tools:** Python (pandas), Salesforce, Snowflake, Campus Solutions (PeopleSoft SIS)

**Impact:** Runs annually each May as part of UF Preview orientation preparation, placing 3000 incoming students across Summer and Fall. Priority logic updated in 2025 to better serve special populations of students. Automatic registration based on student preference saves time in the registration appointment during the second day of orientation.

---

## SIDA Watchlist + AI Concern Scoring

**Problem:** When students drop courses, they sometimes leave free-text comments that signal medical or mental health distress. With hundreds of drop reasons submitted each week, manually reviewing each one for warning signs wasn't feasible and missing a high-risk message carried real consequences.

**Approach:** Built a two-part system: a weekly Cognos report surfaces all new SIDA drop comments (co-conceived with academic advisors), and a Snowflake stored procedure routes each unscored message through NaviGatorAI to generate a concern score. The scoring prompt was engineered with calibrated bands (1–19 routine, 20–49 low, 50–79 moderate, 80–100 critical) and includes human-graded examples as few-shot context to anchor the model's output. The prompt specifically flags messages indicating potential need for DRC accommodations, suicidal ideation, mental health crises, serious medical events, and major life instability. The model returns a JSON object with a 1–100 score and a one-sentence reason; parse failures default to a sentinel value for manual review. Results are versioned by model and timestamped on insert.

**Tools:** Snowflake (Snowpark Python stored procedure), NaviGatorAI (gpt-oss-120b), SQL, IBM Cognos

**Impact:** Automates initial triage of all weekly drop activity that totals thousands per term. Advisors receive a prioritized list each Monday and focus outreach on the highest-scoring students. Eliminates the risk of a high-concern message going unreviewed in a large weekly batch.

---

## Salesforce Case Sharing

**Problem:** Advising case data across UF lived in silos where each office could only see its own cases, even when students had overlapping needs across colleges. No office had taken the step to open their cases broadly.

**Achievement:** CLAS became the first office to share its advising cases university-wide. Led the coordination with UFIT to make all CLAS cases visible as read-only to 200+ Salesforce-licensed advisors across campus serving as an olive branch intended to get the ball rolling on a culture of shared visibility. The gesture worked: IA, Honors, and Quest established reciprocal sharing agreements within a month, and conversations with additional colleges are ongoing.

**Tools:** Salesforce (Gator360), UFIT CRM team

**Impact:** Described by the UFIT CRM team as "a long-standing goal become a reality." The goal was never just the configuration, but rather it was demonstrating that an office was willing to go first.  

> "He has created a model for how large and small advising units can and should adopt specific technologies to improve how they interact with and serve students."  
> — IT Manager, UF Information Technology

---

## CLAS Registration Dashboard

**Problem:** Department leaders across CLAS needed regular enrollment counts: how many majors, minors, and certificate students are in their department right now. Cognos could answer the question but required enough technical skill that most leaders came to me for one-off requests instead, creating a bottleneck for routine headcount questions.

**Approach:** Built Snowflake views to aggregate current enrollment data by major, minor, and certificate across CLAS departments, then connected them to a Power BI dashboard built for a non-technical leadership audience. The dashboard refreshes automatically on a regular schedule so current counts are always available without a data request.

**Tools:** Snowflake, Power BI

**Impact:** Eliminated a recurring category of ad hoc data requests. Department leaders across CLAS now have self-service access to enrollment counts: no ticket required.

---

## Campus-Wide Reporting

**Problem:** Two recurring gaps in campus reporting: standard waitlist counts obscured true unmet course demand, and advisors without dedicated data support had no way to do bulk student lookups across multiple courses. A colleague described checking grades for her ~70 students one by one, a manual process with no scalable alternative for offices without a local data professional.

**Unique Waitlist Demand Reporting:** Built a report in Cognos using Snowflake views that separates waitlisted students into two groups: those already enrolled in the course (seeking a preferred seat) and those not enrolled at all (needing a seat). UF data governance restrictions prevented sharing it directly with the broader advising community, so I requested that UFIT replicate it in their infrastructure using my code and logic.

**Bulk Student-Course Lookup:** Brought the bulk lookup need to UFIT and worked with them to define and build a report through Enterprise Analytics that accepts multiple course IDs and student UFIDs at once, returning results in a single query instead of one-by-one manual checks.

**Tools:** Snowflake SQL, IBM Cognos, UFIT Enterprise Reports

**Impact:** Both reports are now available campus-wide through UFIT Enterprise Analytics and accessible to the full advising and registration community without requiring a local data contact to fulfill requests. A pattern: when a colleague surfaces a problem that no one else has the position or access to fix, I route it to the right institutional partner and get it built for everyone.
