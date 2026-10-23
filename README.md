# smartquizApp
A quiz app that tells learners why an answer is right or wrong, not just which letter is correct. Questions are organised by Microsoft AZ-900 topic, and a small rule-based agent decides what to practise next.

Live demo: https://smartquizapp009.lovable.app/

The problem

Many learners practise with questions but don't understand why an answer is right or wrong. They memorise letters, repeat the same mistakes, and a final score hides what they actually misunderstand.

The solution

After every answer the app gives:

an instant verdict (correct or not quite)
why the correct option is right
why each wrong option fails, with your own pick marked
a reminder to verify against Microsoft Learn

Behind the quiz, an agent tracks your results, finds the questions you keep missing, ranks your weakest topics and forecasts how close you are to a pass.

Features
Tab	What it does
Quiz	Adaptive questions with instant feedback and explanations. Filter by topic or practise across all topics.
Progress	Totals, a weakest-first study order, recurring misses and a readiness forecast.
Builder	Add your own questions. Rejected unless it has 4 options and a real explanation (20+ characters).
Agent canvas	Diagram showing how the eight frameworks connect.

The app follows your device's light or dark mode.

AZ-900 topics covered

Cloud Concepts, Architecture, Compute & Network, Storage, Identity & Security, Cost Management, Governance, and Monitoring & Tools. The app ships with 12 starter questions.

How the agent works

The eight framework names are stages of one pipeline. Their expansions are this project's own definitions, not an industry standard.

Stage	Meaning	What it does in the app
ETHOS	Ethics and trust guardrails	Every question needs an explanation. Learners are pointed to Microsoft Learn.
OASIS	Objective & Adaptive Selection	Picks the next question from topic weakness, past misses and novelty.
PRIDE	Personalised Reasoning, Instant Detailed Explanation	Verdict, why right, why each other option fails.
TRACK	Tracking every answer	Stores attempts and correct answers per topic.
HUNT	Hunt for misconceptions	Lists the questions you miss repeatedly.
RANK	Ranking by risk	Topic risk = (wrong + 1) / (attempts + 2).
TRAIL	Trail of study order	Orders topics weakest first.
HORIZON	Readiness forecast	Compares overall accuracy with a 70% mark and estimates answers still needed.

Flow: OASIS → PRIDE → TRACK → HUNT → RANK → TRAIL → HORIZON → learner → back to OASIS. ETHOS applies to every step.

Run it

No build step and no dependencies. It is a single file.

Save smart-quiz-builder.html.
Open it in any modern browser.
Project structure
smart-quiz-builder.html   HTML, CSS and JavaScript in one file

Inside the file:

T — the list of AZ-900 topics
BASE — the starter question bank
NODES — text for the agent canvas legend
oasis() — question selection
answer() — feedback (PRIDE) and tracking (TRACK)
dash() — progress, ranking, misses and forecast
add() — the Builder with the ETHOS check
canvas() — draws the agent diagram
Adding questions in code

Add an object to BASE:

js
{
  t: 3,                                   // index into T (3 = Storage)
  q: "Your question text?",
  o: ["Option A", "Option B", "Option C", "Option D"],
  a: 1,                                   // index of the correct option
  e: "Why the correct option is right.",
  w: ["Why A fails.", "", "Why C fails.", "Why D fails."]  // "" for the correct option
}

Questions added through the Builder tab have no per-option reasons (w), so they show only the main explanation.

Data and privacy

Progress and custom questions are stored in your browser's localStorage under the key sqb-az900. Nothing is sent to a server. Clearing site data, or the Reset progress button, removes your results. Reset keeps custom questions.

Limitations
The agent is rule-based. It does not call a language model, and there is no live question generation.
The 12 starter questions are study aids written from general knowledge. Always check answers against the current AZ-900 skills outline on Microsoft Learn.
The 70% readiness mark is a simplification. The real exam uses a scaled score, so a percentage of correct answers here does not map exactly to the official pass score.
Data lives in one browser on one device. There are no accounts or syncing.
