# External Tool, Skill, Repository, and MCP Vetting Protocol

I will provide one or more of the following:

* A GitHub repository
* A GitHub skill
* An agent or agent framework
* An MCP server
* A Claude Code plugin
* A tool package
* A prompt or instruction library
* An automation framework
* A local or hosted integration

Your job is not to glaze it, summarize its marketing, or install it immediately.

Your job is to determine whether it provides meaningful, non-duplicative value to my existing system, what parts are actually worth adopting, and what should be rejected.

## Primary Objective

Separate the submission into:

1. Necessary
    Capabilities that solve a real current problem, remove an important limitation, reduce risk, or materially improve the system.
2. Useful but optional
    Capabilities that provide legitimate value but are not required now.
3. Redundant
    Capabilities already handled adequately by existing tools, skills, agents, scripts, documentation, or workflows.
4. Unnecessary
    Features that add complexity, noise, maintenance burden, dependency risk, or little practical value.
5. Unsafe or unacceptable
    Anything with excessive permissions, unclear data handling, weak security, dangerous execution behavior, supply-chain risk, or unacceptable governance characteristics.

Do not assume that more tools make the system better. The default position is that a new dependency must justify its existence.

## Evaluation Rules

### 1. Inspect before recommending

Perform a read-only evaluation first.

Do not install, clone into the production project, modify configuration, edit files, register an MCP server, add dependencies, commit, push, or execute untrusted scripts unless I explicitly approve those actions after reviewing your report.

You may inspect public source code, documentation, manifests, package files, release history, issues, permissions, configuration examples, and architecture.

Treat README claims as unverified until supported by code or independent evidence.

### 2. Identify the actual capability

Explain:

* What the tool truly does
* What problem it is designed to solve
* Whether the implementation matches its claims
* What inputs it receives
* What outputs or side effects it produces
* Whether it runs locally, remotely, or both
* Whether it requires network access
* Whether it sends data to a third party
* Whether it can read or write files
* Whether it can run shell commands
* Whether it can access secrets, Git history, browsers, databases, or connected accounts
* Whether it creates durable state

Separate demonstrated capabilities from proposed, experimental, incomplete, or marketing-only capabilities.

### 3. Compare it against my existing system

Determine whether the submitted tool:

* Adds a genuinely new capability
* Improves an existing capability
* Replaces a weaker component
* Duplicates something already present
* Conflicts with existing architecture
* Creates overlapping sources of truth
* Introduces a second framework for the same responsibility
* Increases cognitive load or operational complexity
* Makes future maintenance more difficult

Do not evaluate it in isolation. Evaluate its marginal value to my current system.

A feature is not valuable merely because it is impressive. It must improve the actual system.

### 4. Evaluate architectural fit

Review:

* Language and runtime compatibility
* Package-manager compatibility
* Operating-system assumptions
* Local versus cloud architecture
* Configuration model
* API and interface stability
* Extensibility
* Portability
* Vendor lock-in
* Dependency weight
* Resource usage
* Failure behavior
* Logging behavior
* Update strategy
* Version pinning
* Reversibility
* Whether it can be isolated behind an adapter or narrow interface

Prefer narrow integrations over framework-wide adoption.

Prefer extracting a useful pattern over importing an entire repository.

Prefer adopting a small number of files or concepts over adding a large dependency when practical.

### 5. Evaluate security and trust

Inspect, where applicable:

* Repository ownership and maintainer history
* Commit activity and release cadence
* Open security issues
* Known vulnerabilities
* Dependency vulnerabilities
* Install scripts
* Postinstall or lifecycle scripts
* Shell execution
* Dynamic code execution
* Remote downloads
* Telemetry
* Analytics
* Data collection
* Secret handling
* Authentication model
* Permission scope
* Network destinations
* File-system access
* Subprocess access
* Sandbox boundaries
* Prompt-injection exposure
* Tool-call injection exposure
* Supply-chain exposure
* Auto-update behavior
* Whether dependencies are version-pinned
* Whether the MCP registration is version-pinned
* Whether the project relies on mutable branches, floating tags, or unpinned packages

For an MCP server, evaluate two separate security dimensions:

1. The permissions exposed by its declared MCP tools.
2. The OS-level permissions of the MCP subprocess itself.

A read-only MCP tool definition does not mean the underlying subprocess is OS-restricted.

Flag anything that requires blanket trust, full-disk access, unrestricted shell access, broad repository write access, or access to secrets without a strong justification.

### 6. Evaluate quality and maintainability

Inspect:

* Code organization
* Type safety
* Test coverage
* CI status
* Documentation quality
* Error handling
* Input validation
* Dependency hygiene
* Release discipline
* Issue responsiveness
* Bus factor
* License
* Abandoned or experimental status
* Compatibility guarantees
* Ease of removal

Do not confuse popularity, stars, or social-media attention with technical quality.

### 7. Identify the smallest useful extraction

For every valuable capability, decide which adoption strategy is best:

* Use the tool as-is
* Install it but isolate it
* Fork and pin it
* Vendor a small portion
* Reimplement only the core concept
* Extract its documentation pattern
* Extract its prompt or skill structure
* Use it only as a reference
* Reject it completely

Do not recommend importing the full project when a smaller extraction would produce the same value with lower risk.

## Required Output

Produce the following report.

### Vetting Report

#### 1. Verdict

Choose exactly one:

* Adopt
* Adopt selectively
* Test in isolation
* Reference only
* Defer
* Reject

Include a confidence level:

* High
* Medium
* Low

Then give a concise explanation of the decision.

#### 2. What It Actually Is

Explain what the project does in practical terms, without repeating its marketing language.

#### 3. Relevant Capabilities

Create a table with these columns:

Capability | Classification | Existing overlap | Actual value | Recommendation

The classification must be one of:

* Necessary
* Useful
* Redundant
* Unnecessary
* Unsafe

#### 4. What We Should Keep

List only the components, concepts, files, patterns, or capabilities that would materially improve my system.

For each one, explain:

* The problem it solves
* Why my current system needs it
* Whether to import, adapt, reimplement, or reference it
* The expected benefit
* The ongoing maintenance cost

#### 5. What We Should Cut

Identify everything that should not be adopted.

Explain whether each rejected part is:

* Duplicative
* Overengineered
* Immature
* Unsafe
* Too tightly coupled
* Too expensive to maintain
* Outside current scope
* Solving a problem we do not have

#### 6. Security and Trust Assessment

Include:

* Permission surface
* Data-access surface
* Shell and subprocess behavior
* Network behavior
* Secret exposure
* Dependency and supply-chain risk
* Version-pinning status
* Telemetry or external data transfer
* Untrusted-input exposure
* Overall security risk: Low, Moderate, High, or Critical

Clearly distinguish confirmed findings from concerns that still require verification.

#### 7. Architecture Impact

Explain:

* Where it would fit
* What it would replace or overlap
* New dependencies introduced
* New configuration introduced
* New sources of truth introduced
* Operational burden
* Failure modes
* Removal difficulty
* Whether an adapter boundary should be used

#### 8. Cost-Benefit Analysis

Rate each from 1 to 10:

* Practical value
* Architectural fit
* Security confidence
* Maintainability
* Uniqueness
* Integration effort
* Long-term burden

For integration effort and long-term burden, a higher score means more effort or burden.

Do not average the numbers blindly. Explain the tradeoff.

#### 9. Recommended Adoption Scope

Choose the smallest responsible scope:

* No adoption
* Documentation or pattern only
* One isolated component
* Small subset of files
* Sandboxed experimental integration
* Full integration

State exactly what should be included and excluded.

#### 10. Implementation Recommendation

Provide a phased implementation plan only if adoption is justified.

The plan must include:

* Files likely to be added or changed
* Dependencies involved
* Security controls
* Version-pinning requirements
* Tests required
* Rollback method
* Acceptance criteria
* A clear stopping point for approval

Do not implement anything during the vetting stage.

#### 11. Final Recommendation

End with this exact structure:

Decision:
[Adopt / Adopt selectively / Test in isolation / Reference only / Defer / Reject]

Keep:
[The specific valuable parts]

Cut:
[The unnecessary, redundant, or unsafe parts]

Why:
[The strongest reason for the recommendation]

Next action:
[The single highest-leverage next step]

Approval required before:
[Any installation, code modification, MCP registration, dependency addition, configuration change, commit, or push]

## Anti-Hype Rules

Do not recommend adoption merely because the project:

* Has many GitHub stars
* Is popular on social media
* Uses AI or agents
* Has an impressive demo
* Claims to replace multiple tools
* Was built by a recognized company
* Contains many skills or integrations
* Appears comprehensive

Complexity is a cost.

Every new tool must earn its place by delivering unique value greater than its security, maintenance, dependency, and cognitive costs.

When the strongest recommendation is to copy one pattern and reject the rest, say so clearly.

When the system already handles the problem adequately, recommend no adoption.
