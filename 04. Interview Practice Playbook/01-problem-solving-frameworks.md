# 01 · Problem-Solving Frameworks and Communication

Technical interviews assess far more than code—they evaluate how you frame problems, collaborate under pressure, and reason about trade-offs. This chapter provides a repeatable framework you can follow for every question, plus guidance on communication and evaluation rubrics from the interviewer’s perspective.

## Learning objectives
- Structure each interview question using a consistent Solve–Code–Validate loop
- Surface assumptions, constraints, and test cases before coding begins
- Communicate trade-offs clearly and adapt when interviewers steer the conversation
- Understand typical evaluation criteria (analysis, correctness, coding, communication)

## The Solve–Code–Validate framework
1. **Clarify**  
   - Restate the problem in your own words; confirm inputs/outputs.  
   - Ask about constraints (input size, character set, time/space limits).  
   - Clarify edge cases (empty input, duplicates, negative values).
2. **Plan**  
   - Brainstorm multiple approaches (brute force → optimized).  
   - Compare complexity; justify chosen strategy.  
   - Sketch data structures, invariants, and algorithm outline.
3. **Code**  
   - Implement cleanly with clear variable names and helper functions.  
   - Verbally narrate what you’re writing; highlight tricky sections.  
   - Keep code modular to simplify debugging.
4. **Validate**  
   - Walk through example inputs, including edge cases.  
   - Check complexity, memory usage, and potential failure modes.  
   - Discuss extension ideas (streaming input, distributed systems) if time permits.

## Clarifying questions checklist
- Input format and size, mutability, streaming vs. batch
- Sorted/unsorted, unique/duplicate elements, negative numbers allowed?
- Real-time constraints vs. batch processing
- Should the solution be scalable / thread-safe / production ready?

## Communication playbook
- **Think aloud:** share your reasoning, even when exploring dead ends. Interviewers evaluate problem-solving, not just final answers.
- **Signal structure:** use phrases like “I see two options,” “My invariant is…,” “I’ll now handle edge cases.”
- **Manage time:** keep an eye on the clock; allocate time for validation. If stuck, summarise what you’ve tried and propose alternatives.
- **Invite feedback:** pause after presenting a plan—“Does this approach make sense?”—to ensure alignment.

## Storyboarding your solution (five-minute prep)
Use a scrap page to jot:
- Inputs/outputs with units
- Constraints (n, k bounds)
- Candidate data structures
- Outline of algorithm steps
- Sample test cases (normal + edge)

## Evaluation rubrics (what interviewers score)
- **Problem analysis:** Did you scope the problem, ask smart questions, understand trade-offs?
- **Solution correctness:** Is the algorithm correct and efficient given constraints?
- **Code quality:** Is the code readable, logically structured, and idiomatic?
- **Testing and validation:** Did you test edge cases and reason about failure modes?
- **Communication:** Were you collaborative, clear, and receptive to hints?

## Handling hints and pivots
- Accept hints gracefully; acknowledge and integrate them.  
  “Ah, that suggests I should sort first to simplify comparisons—let me adjust.”
- If the interviewer nudges toward a technique, pause to connect the dots aloud.
- Be ready to abandon sunk costs; summarise the abandoned path and pivot.

## Common interviewer prompts and responses
- **“What’s the complexity?”** Give time and space big-O, plus note dominant factors.  
- **“Can we do better?”** Discuss trade-offs; suggest improvements or state lower bounds.  
- **“How would this scale?”** Outline big-picture architecture considerations.  
- **“What edge cases worry you?”** List them, expand test coverage, and mention defensive coding ideas.

## Practice drills
- Record mock interviews; review for pacing and filler words.
- Rehearse the Clarify → Plan → Code → Validate script until it feels natural.
- Run through past interview questions; after each, score yourself on the evaluation rubric.

Memorize the framework, use the checklists to stay organized under pressure, and adapt these habits until they become instinctive.
