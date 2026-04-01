---
name: impeccable
description: "Guided end-to-end UI improvement workflow. Establish context, diagnose design and implementation issues, ask one focused decision batch, then execute an ordered command route from repair through polish."
argument-hint: "[target] [goal (optional)]"
user-invocable: true
compatibility: "Works best in harnesses that support subagents or parallel analysis. If unavailable, perform the same workflow locally."
---

Run a full design-improvement workflow from diagnosis through execution. This is the master command for non-trivial UI work.

## MANDATORY PREPARATION

Invoke {{command_prefix}}frontend-design first - it contains design principles, anti-patterns, and the **Context Gathering Protocol**. Follow the protocol before proceeding. If no design context exists yet, you MUST run {{command_prefix}}teach-impeccable first.

---

## Scope First

Before doing any real work:

1. **Resolve the target into concrete scope**:
   - Files
   - Routes/pages
   - Components
   - Styles
   - Assets

2. **Understand what success means**:
   - What is the user trying to accomplish?
   - What problem should improve?
   - Is this a repair, refinement, or larger redesign?

3. **Choose execution depth**:
   - **Quick**: Small component or obvious issue cluster. Minimal questioning, no agent fan-out unless clearly valuable.
   - **Standard**: Default for most feature/page work. Use the core diagnostic split described below.
   - **Deep**: Large flows, multi-route work, or redesigns with system implications. Add the optional exploration and specialist passes below.

If scope is still too vague after a quick repo scan, {{ask_instruction}} Ask narrowly about the target and success criteria - not broad brand questions that should have been handled by {{command_prefix}}teach-impeccable.

## Step 1: Context Gate

Confirm the work has enough context to be real rather than generic:

- **Design context**: audience, use cases, brand personality, aesthetic direction
- **Product context**: what this surface is for and what users need to do
- **Constraints**: platform, accessibility, performance, launch timing, off-limits areas

**IMPORTANT**:
- Broad audience/brand questions belong only here, via {{command_prefix}}teach-impeccable if needed
- Do NOT keep reopening discovery interviews later in the workflow
- Do NOT infer missing brand intent from code

## Step 2: Diagnose in Parallel

If your harness supports agents, subagents, or parallel analysis, use them here. If not, do the same work locally while preserving the same ownership boundaries.

### Default Split

Run these two diagnostic passes in parallel by default:

1. **`experience_critic`**
   - Owns the qualitative design pass
   - Evaluate visual hierarchy, information architecture, cognitive load, emotional tone, affordance, composition, typography as communication, purposeful color, microcopy, and AI-slop tells
   - Return:
     - Top 3-5 issues
     - Strengths worth preserving
     - Persona or journey red flags
     - Evidence
     - Unknowns
     - Route hints

2. **`implementation_auditor`**
   - Owns the measurable implementation pass
   - Evaluate semantics, keyboard/focus basics, ARIA/labels, contrast, token usage, theming integrity, responsive mechanics, and concrete code-level drift
   - Return:
     - Top 3-5 issues
     - Systemic patterns
     - Positive findings
     - Evidence
     - Unknowns
     - Route hints

### Deep Mode Exploration Pass

In **Deep** mode, or when the target spans multiple routes/components, optionally run these exploration passes before the default split:

1. **`context_ledger`**
   - Collect explicit product, audience, brand, and constraint facts from instructions, docs, config, and assets
   - Never infer missing intent from code

2. **`design_system_atlas`**
   - Map canonical tokens, shared components, conventions, and design-system touchpoints
   - Do not judge drift yet

3. **`surface_context_map`**
   - Map surfaces, states, entry points, navigation, breakpoint mechanisms, pointer/hover assumptions, and copy surfaces
   - Do not diagnose yet

4. **`reuse_inventory`**
   - Map repeated patterns, hard-coded clusters, inconsistent variants, and likely extraction candidates
   - Do not redesign yet

These exploration agents should return maps, not recommendations.

### Conditional Specialist Passes

Spawn these only when the default diagnosis exposes a real need:

- **`system_fit`**
  - Use when findings indicate cross-cutting design-system drift, repeated local one-offs, or likely shared-component work
  - Determine whether {{command_prefix}}extract or {{command_prefix}}normalize should move earlier

- **`performance_profiler`**
  - Use when performance risk is visible or likely
  - Owns measurement-first diagnosis: load time, runtime jank, animation/render bottlenecks, bundle/request weight

- **`resilience_assessor`**
  - Use when state coverage looks weak
  - Owns empty/loading/error/success/permission/offline states, long text, i18n/RTL/CJK, large data, validation, concurrency, and graceful degradation

### Hard Ownership Rules

Avoid duplicate findings by keeping ownership strict:

- AI-slop and qualitative design judgment belong to `experience_critic`
- Static implementation quality belongs to `implementation_auditor`
- Performance belongs to `performance_profiler`
- Edge cases and production robustness belong to `resilience_assessor`
- {{command_prefix}}polish is NOT a primary diagnosis pass

### Agent Output Contract

Every diagnostic or exploration pass should return the same core structure:

- **Summary**: What this pass concluded in 2-4 lines
- **Issues**: Severity, user impact, root cause, evidence
- **Strengths or patterns**: What should be preserved or reused
- **Unknowns**: What still needs user confirmation
- **Route hints**: Which command families are likely relevant

Agents should never ask the user questions directly. They report to the main workflow only.

## Step 3: Synthesize and Ask Once

Do NOT spawn more agents by default here.

Merge the Step 2 findings into one clear diagnosis:

- Dedupe by surface plus root cause
- Keep the 5 highest-value issues only
- Separate systemic problems from local detail issues
- Preserve strengths so later commands do not accidentally erase them

Then {{ask_instruction}} ask **one batched decision set** of 2-4 questions maximum. These questions must reference the actual findings.

Ask only what changes the route:

1. **Priority axis**: Which issue cluster matters most right now?
2. **Intervention intensity**: Conservative, balanced, or bold?
3. **Scope boundary**: Local surface only, or shared/systemic fixes too?
4. **Guardrails**: What must remain untouched?

If confidence is high and the route is obvious, compress this to a single confirmation question.

## Step 4: Propose Tracks, Not a Raw Command Dump

Present 2-3 workflow tracks with clear trade-offs:

### 1. Conservative Repair
- Best when correctness, clarity, and consistency matter more than reinvention
- Often uses: {{command_prefix}}normalize, {{command_prefix}}clarify, {{command_prefix}}adapt, {{command_prefix}}harden, {{command_prefix}}polish

### 2. Balanced Redesign
- Best when the structure is decent but the experience needs stronger hierarchy, rhythm, and expression
- Often uses: {{command_prefix}}normalize, {{command_prefix}}typeset, {{command_prefix}}arrange, {{command_prefix}}colorize or {{command_prefix}}quieter, {{command_prefix}}adapt, {{command_prefix}}polish

### 3. Signature Treatment
- Best when the current work feels generic and needs a stronger point of view
- Often uses: {{command_prefix}}distill or {{command_prefix}}bolder, {{command_prefix}}typeset, {{command_prefix}}arrange, {{command_prefix}}animate or {{command_prefix}}delight, {{command_prefix}}polish

**Rules**:
- Recommend only commands from: {{available_commands}}
- Put system, quality, and structural fixes before expressive enhancement
- Keep {{command_prefix}}polish last when real changes were made
- Do not recommend commands that would address zero findings

## Step 5: Execute Deliberately

After the user approves a track:

1. Re-read the specific files you will touch
2. Execute the chosen command sequence in order
3. Keep scope disciplined - do not let a local fix sprawl into a redesign unless the user approved it
4. Re-check the diagnosis after each major phase so you do not drift away from the actual problems

If your harness supports worker agents, parallelize only when write ownership is clean:

- **Shared/system layer**: design tokens, shared UI, reusable components
- **Local surface layer**: route/page/component implementation
- **Specialist layer**: performance or resilience fixes with a disjoint write set

**NEVER** let multiple workers edit the same files at once.

## Step 6: Review and Finish

After implementation:

- Run a final review pass for bugs, regressions, and convention drift
- If available, parallelize review by focus:
  - design/UX review
  - code/regression review
  - performance/resilience review
- Apply the highest-value fixes
- End with {{command_prefix}}polish if the route changed real UI details

Then summarize:

- What changed
- Why this track was chosen
- What was validated
- Remaining risks or follow-up opportunities

## NEVER

- Never skip the context gate and jump straight to styling
- Never ask broad brand questions after {{command_prefix}}teach-impeccable already answered them
- Never let multiple diagnostic agents report the same category without clear ownership
- Never let agents ask the user independently
- Never spawn specialist passes just because they exist - use evidence
- Never use {{command_prefix}}polish as the primary diagnostic tool
- Never present a giant flat list of commands without a routed strategy

Remember: this is the orchestration command. Your job is not just to fix pixels - it is to choose the right sequence, at the right depth, with the right level of intervention.
