# Client review: Larkspur disruption-care agent

**To:** Room 2  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-17 11:29

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. agent.py build_tools(): the search_alternatives description is the 6-character string "search".**

The scan puts search_alternatives at 6 characters. The other eight descriptions run from 71 to 445 characters. hold_seat is at 73 and send_confirmation at 71. Your agent.py has no diff against the template, so this entry is unchanged and it is the only text Claude has for choosing that tool.

Run python3 run.py --show-tools and paste the search_alternatives entry as it prints.

**2. agent.py run_agent(): the loop appends text_of(response) as the assistant turn, so no tool_use blocks go back into messages.**

Inside the while loop, messages gets {"role": "assistant", "content": text_of(response)}, then a user message of tool_results carrying tool_use_id values. The assistant turn holds a text string and none of the blocks those ids belong to. Your diff is empty, so this is the loop as shipped.

Run python3 run.py K7PQ2M --trace and paste the turn-by-turn trace for the first two tool calls.

**3. agent.py run_agent(): answer is assigned before each follow-up client.messages.create call, and the final response is never read.**

answer = text_of(response) runs inside the loop, ahead of the next call. The last response, the one that ends the loop, is never passed to text_of. A conversation that needs no tools returns the initial value "". Nothing in your diff touches this.

Run python3 run.py --all --trace and paste the final answer text printed for each booking shape.

**4. agent.py MAX_TOOL_CALLS is 8 and the loop tests turns < MAX_TOOL_CALLS, with no run of this agent committed.**

The scan finds no readout-trace.json and no evals/cases.json. The PITCH.md Number: line is empty. The cap of 8 counts model turns. Nobody has shown how many turns a rebooking with hold_seat, check_policy, issue_voucher and send_confirmation uses.

Run python3 run.py --all --trace and paste the totals footer.

**5. agent.py run_agent(): MODEL is imported from support and every turn sends thinking adaptive, nine schemas, and TONE_ADDENDUM at 0 characters.**

The scan finds no cache_control anywhere in agent.py. Each client.messages.create call re-sends runtime_preamble() + SYSTEM_PROMPT and all nine tool schemas, one of them 6 characters. The cost and wrong-answer rates of this configuration have no figure in the repository, and the search_alternatives description would be the same under any model name.

Run python3 run.py --tool-tax and paste its output.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (226 lines)`
- `PITCH.md`
- `TEAM.md`
- given files that differ from the shipped pack: `verify.py`, `eval_harness.py`, `bench.py`, `readout.py`, `setup.py`, `pod_sync.py`, `run.py`, `review.py`, `support/__init__.py`, `support/client.py`, `support/data.py`, `support/models.py`, `support/tools.py`, `support/trace.py`, `support/offline.py`, `support/mock_backend.py`, `support/mcp_client.py`, `support/mcp_server.py`, `support/mcp_selftest.py`, `support/access.py`, `support/keyscan.py`, `support/review.py`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
