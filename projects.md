---
layout: default
title: Projects
permalink: /projects
---

## Pre-Health Service Indicator

**Problem:** Pre-health students at UF had no reliable tracking mechanism. The closest thing was enrollment in a listserv that wasn't actively maintained — leaving advisors and administrators guessing at the actual population size. Demand forecasting for pre-health courses, and personalized tools like BCP/BCPM GPA visibility in the degree audit, were impossible without a clean, current population list.

**Achievement:** The technical build was straightforward. The hard part was navigating the institutional process — getting the concept approved, the service indicator created, the self-service website launched, and the workflow accepted as an ongoing operational process. Received approval from the Dean's office (December 2024), stood up the `PRE/HLTH` service indicator in Campus Solutions (January 2025), and launched student outreach to seed the population (February 2025). A Python script runs weekly to reconcile student opt-in requests against current indicators in Campus Solutions and apply bulk adds and removes.

**Tools:** Python, Snowflake, Campus Solutions (PeopleSoft SIS), MySQL (Acadvise), CLAS web infrastructure

**Current state:** A few thousand students are now tracked with a clean, maintained record — replacing years of guesswork. The indicator is intentionally built as a foundation: planned future uses include pre-health course demand prediction and surfacing BCP/BCPM GPAs directly in students' degree audits.

---

## Quest Mass Enrollment Algorithm

**Problem:** Each May, thousands of incoming UF freshmen need to be placed into Quest 1 courses before orientation begins. The previous process was run manually in Ruby by the Quest Director and didn't scale — seat allocation was inconsistent and priority groups weren't systematically enforced.

**Approach:** Rewrote and maintain the algorithm in Python (2024). The script reads student survey responses from Salesforce alongside course section data from Campus Solutions, then applies a tiered priority system: URSP students in Honors sections are placed first, followed by URSP students in general sections, then Honors students in Honors sections, then the general population. Within each tier, students are assigned a random number to break ties fairly. The algorithm runs four independent versions per term — each with a fresh shuffle — so the team can compare outcomes and select the best fit before submitting to the Registrar. Covers both Summer and Fall terms. Unassigned students are identified separately and assigned a Spring Quest hold. Final output is delivered as a CSV to OUR and UFIT for mass enrollment via Campus Solutions.

**Tools:** Python (pandas), Salesforce, Snowflake, Campus Solutions (PeopleSoft SIS)

**Impact:** Runs annually each May as part of UF Preview orientation preparation, placing thousands of incoming students across Summer and Fall. Priority logic updated in 2025 to better serve Honors and URSP populations.

---

## SIDA Watchlist + AI Concern Scoring

**Problem:** When students drop courses, they sometimes leave free-text comments that signal medical or mental health distress. With hundreds of drop reasons submitted each week, manually reviewing each one for warning signs wasn't feasible — and missing a high-risk message carried real consequences.

**Approach:** Built a two-part system: a weekly Cognos report surfaces all new SIDA drop comments (co-conceived with Lynn O'Sickey and Shannon Kelly), and a Snowflake stored procedure routes each unscored message through NaviGatorAI to generate a concern score. The scoring prompt was engineered with calibrated bands (1–19 routine, 20–49 low, 50–79 moderate, 80–100 critical) and includes human-graded examples as few-shot context to anchor the model's output. The prompt specifically flags messages indicating potential need for DRC accommodations, suicidal ideation, mental health crises, serious medical events, and major life instability. The model returns a JSON object with a 1–100 score and a one-sentence reason; parse failures default to a sentinel value for manual review. Results are versioned by model and timestamped on insert.

**Tools:** Snowflake (Snowpark Python stored procedure), NaviGatorAI (gpt-oss-120b), SQL, IBM Cognos

**Impact:** Automates initial triage of all weekly drop activity. Advisors receive a prioritized list each Monday and focus outreach on the highest-scoring students. Eliminates the risk of a high-concern message going unreviewed in a large weekly batch.

---

## Salesforce Case Sharing

**Problem:** Advising case data across UF lived in silos — each office could only see its own cases, even when students had overlapping needs across colleges. No office had taken the step to open their cases broadly.

**Achievement:** CLAS became the first office to share its advising cases university-wide. Led the coordination with UFIT to make all CLAS cases visible as read-only to 200+ Salesforce-licensed advisors across campus — an olive branch intended to get the ball rolling on a culture of shared visibility. The gesture worked: IA, Honors, and Quest established reciprocal sharing agreements within a month, and conversations with additional colleges are ongoing.

**Tools:** Salesforce (Gator360), UFIT CRM team

**Impact:** Described by the UFIT CRM team as "a long-standing goal become a reality." The goal was never just the configuration — it was demonstrating that an office was willing to go first.
