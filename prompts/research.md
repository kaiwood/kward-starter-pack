---
description: Produce an evidence-backed research answer with sources, caveats, and next steps
argument-hint: "<question-or-topic>"
---

Research this question and answer from evidence, not memory alone:

$ARGUMENTS

## Rules

- Report only: do not modify files, run formatters, apply patches, or make code/config changes.
- Lead with the direct answer or recommendation.
- Prefer primary sources: official docs, source code, specs, release notes, vendor pages, papers, authoritative data.
- Cross-check important claims when practical; call out weak, stale, missing, or conflicting evidence.
- Separate facts from interpretation and recommendations.
- Ask one focused clarification question only if scope or decision criteria are unclear.
- If web access is unavailable, say so and use local context only.

## Suggested tool use

- Use web_search for broad/current research; prefer 2-4 varied queries and recency filters when relevant.
- Use code_search for APIs, examples, library behavior, or implementation details.
- Use fetch_content for specific URLs, repos, docs, papers, articles, or videos.
- Use get_search_content for full content from earlier search/fetch results.
- Use local file tools for the current repo or local docs when relevant.

## Process

1. Define the question and evidence needed.
2. Gather primary sources first; use secondary sources for context or disagreement.
3. Verify important claims and prefer newer primary sources when sources conflict.
4. Synthesize concisely with citations, caveats, and practical next steps when useful.

## Output

- **Answer/Recommendation**: direct conclusion.
- **Evidence**: source-backed claims with citations/URLs.
- **Caveats**: uncertainty, limits, conflicts, or version constraints.
- **Next steps/Example**: optional concrete action or minimal code.

Do not dump raw search results unless asked.
