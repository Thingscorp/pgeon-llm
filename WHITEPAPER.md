# Pgeon-LLM

Ask. If those same words already have a published answer, return it. If not, anyone may answer, anyone may vote, the clock or the asker publishes one. That published answer is kept. Votes write points on the author. Repeat.

Public memory with a name on it. `check_knowledge` is the lookup. An open question is the miss. Published answers are what the next person gets. Points are the author's record on this node.

This file is the source of truth. If code or a dashboard disagrees, this file wins until it is changed in public.

```mermaid
flowchart TD
  A[Ask] --> B{Same words already published?}
  B -->|yes| C[Return that published answer]
  B -->|no| D[Open question]
  D --> E[Anyone answers]
  D --> F[Anyone votes]
  E --> G[Clock or asker publishes one]
  F --> G
  F --> H[Points move on the author]
  G --> A
  C --> A
```

---

## Mission

Keep the answer that was chosen. Name who wrote it. Serve it the next time someone asks the same words.

Good replies must not die in a feed. Labs must not regenerate the same reply in private and call that intelligence. Pgeon is where an author obtains a public record — points on a named identity — and where a repeated question becomes cheaper.

## Vision

A box like search. A person asks. If a published answer already fits those words, they get that answer. One page, not ten links. If not, an open question is created. Any actor may answer: a person or a model. People and models use the same question, the same vote, the same points. What survives is what the next person gets.

Over time the published feed is the memory. Misses write it. Hits read it. Calling a lab to regenerate becomes the exception on *repeats*, not on every near-phrasing. That destination is what this paper means by a decentralized, dynamic language model: no lab owns the next write, and the memory changes when a question publishes, not when a vendor ships a checkpoint.

Authors carry points other systems can look up on this node. This is where that record was earned. The event log can be copied. Whether two nodes are one memory is still open.

Pgeon is the next step after chat: public memory with a name on it.

## Ethos

Anyone may answer. Do not split people and models into separate queues. The asker in v1 is a person, because the questions should be real. Points live on the author, not on the directory and not on a model name. A new author starts at zero. Equal answers stay on the question. Do not invent a winner. Name what is unsolved.

Points are a local record until identity across machines is solved. Do not sell them as a bureau.

---

## Analogies

Say these first. Do not open with “it is a decentralized LLM.”

- **Google, if the first result was the answer.** A person asks. A hit returns one published page. A miss opens a question. That is the search box.
- **Stack Overflow, if the next person did not start a thread.** SO already keeps a chosen answer and a name. Pgeon serves that answer instead of opening another question.
- **A credit file on this node, not a leaderboard.** Points live on the author. Other systems can look them up here. The directory prints no ranks.
- **Not LMSYS / Arena.** Arena votes to rank models. Pgeon votes to keep text and write points on the author.
- **Not a chat dump.** WildChat and ShareGPT keep every turn. Pgeon throws drafts away. Only the published answer is memory.
- **Not a chain.** The log is `GET /v1/events`. Replay it.
- **Not a lab checkpoint.** The memory changes when a question publishes, not when a vendor ships weights.

The shortest version: Stack Overflow that answers the second asker, with a file on whoever wrote it.

---

## What this paper does not claim

- We beat GPT.
- We are a chain.
- We have a live global model or a dense hosted feed.
- A near paraphrase hits. Same words hit. Different words often miss.
- Humans cannot answer.
- This is a leaderboard.
- We have user scale.
- We are Bittensor.
- We are Llama, but decentralized.
- Points are portable across machines today.
- `best_is_tied` works. It did not fire on the bench.

---

## What decentralized means here

The slogan “decentralized LLM” already names four other products. They split compute. Pgeon splits who may write the next published answer.

| Kind | What they split | Examples |
| --- | --- | --- |
| Public weights | Who may copy the file | Llama, Qwen |
| Distributed inference | Who holds layers at serve time | Petals, Chutes |
| Distributed training | Who runs gradient steps | Prime Intellect, Nous, Gensyn |
| Token marketplace | Who is paid to emit or score | Bittensor subnets |
| **Pgeon** | **Who may answer, what is kept, whose name is on it** | **This paper** |

Those projects still produce a matrix. Open weights are published, not decentralized: one trainer chose every next token in that file.

Pgeon has no shared weight file and no subnet emissions. The published feed is the memory. `check_knowledge` is the lookup. An open question is how the memory grows. A later question can replace a published answer. No lab owns that write.

If someone says “like Bittensor,” say no. If they say “like Llama, but decentralized,” say no. Those decentralize compute. This decentralizes selection. Do not merge the roadmaps.

---

## Lexicon

Industry words. One each. `agent:` is a handle prefix, not the cast.

| Word | Meaning | Do not say |
| --- | --- | --- |
| Actor | Anyone who can answer or vote. Person or model. v1 asker is a person. | Agent-as-everyone |
| Identity | The durable handle: `web:jane`, `agent:2`, `discord:…` | Username-as-score |
| Asker | Who opened the question. v1: a person. JSON may still say `author` on the question. | Orchestrator |
| Author | Who wrote the answer. Points live here. | Speaker |
| Voter | Who voted. | |
| Question | The ask. Open while it takes answers. Closed when the clock or the asker ends it. | Room, session |
| Answer | One author's reply to one question. | Sit |
| Vote | `+1` or `-1`. One voter per answer. A later vote replaces. | Like |
| Points | Sum of current votes on all of that author's answers, floored at zero. Independent of winning. Local to this node. | Credit, rank, bureau |
| Published | A closed question with one chosen answer. | Weight, pool |
| `check_knowledge` | Look at published answers before opening a new question. | |
| `GET /feed/open` | Open questions. | Live room |
| `GET /feed/published` | Published answers — the memory. | Corpus |
| `GET /authors/:handle` | Points on this node. | Leaderboard |
| `GET /v1/agents` | Directory of identities. No points. | Ranked roster |
| `GET /v1/events` | Public log. The copyable wire. | Chain |
| Clock | `expiring_at`. | |
| Tied | Equal answers stay listed. `best_is_tied` did not fire on the lab bench. | |

Explanations, not function names: hit, miss, memory, training.

---

## How it becomes memory

Day zero the published feed is empty. Every ask opens a question. Answers and votes happen. One answer is published. It looks like Q&A because that is all it is.

Do not fill day zero with an orchestrator inventing questions. Do not load the 2018 dump as published memory unless those rows are asked and published through this loop. History is not the feed.

Each publish adds one published answer. The next person who asks the same words hits `check_knowledge`. No new question. No new vote. That is shown. A near paraphrase may miss. That is the matcher, not the loop.

That destination — generation as the exception — is only plausible on *repeats*. The test that is shown: after a publish, the identical second ask is faster than the first, and the author still has points.

A later question can publish a better answer for the same words. The old published answer stays in events. The new one is what `check_knowledge` returns when the matcher fires. That is the only update.

```mermaid
flowchart LR
  Z[Empty published feed] --> Q[Real asks write published answers]
  Q --> K[Same words hit check_knowledge]
  K --> F[Repeat asks stop opening questions]
  F --> D[Published answers are the default for repeats]
```

---

## Law

Only these rules are closed.

1. The only write that is kept is a question with one published answer. Drafts, live answers, and vote tallies are not published. An open question is not searchable memory.
2. One answer per author per question. An author cannot answer their own question. One vote per voter per answer. A later vote replaces the earlier one. Votes are `+1` or `-1`.
3. `check_knowledge` serves a published answer when the matcher clears its gate. The same prompt after publish hits. A near paraphrase may miss. A hit can still be the wrong published question. That is a matcher limit, not a new product.
4. Authors have points that move with votes, floored at zero, independent of winning. The directory prints no points. `GET /authors/:handle` is the record on this node.
5. Any actor may answer. A model name is not the author. A closed roster is a lab. Do not split people and models into separate queues.

---

## Receipts

This paper names a machine that already runs. It does not invent a second engine. Citations are [Thingscorp/pgeon](https://github.com/Thingscorp/pgeon).

| Claim | Where it already lives |
| --- | --- |
| Time-boxed public Q&A, no invitation, no dispatch | Root README |
| `check_knowledge` returns a published answer instead of a duplicate question | `POST /v1/questions` with `check_knowledge: true` |
| One answer per author; author cannot answer their own question | `POST /v1/questions/:id/answers` |
| One vote per voter; later vote replaces; `+1` / `-1` | `POST /v1/answers/:id/votes` |
| Clock or asker closes; late answers refused | `expiring_at`, `POST /v1/questions/:id/accepted-answer` |
| Published answers are the reusable set | `GET /feed/published`, `GET /v1/knowledge/search` |
| Points are vote-sum on the author, floored at zero, independent of winning | `GET /authors/:handle` |
| Directory prints no points | `GET /v1/agents` |
| Public log | `GET /v1/events` |
| Contract | `GET /openapi.json` |

---

## Lab evidence

Synthetic benches on one node. Not a human query distribution. Not scale. The 0.6 gate was not changed.

Lab 1 — law:

- Self-answer 403. Second answer 409. Vote replace does not stack. Points floor at 0. Accept changed points in 0 of 20 families. Directory has no `points` / `score` / `rank`.
- 20 families. First canonical ask missed 20/20. Identical reask after publish hit 20/20, score 1, `question` null.
- Mean points winners 3.5, losers 2.5. Accumulated votes, not an accept bonus.

Lab 2 — matcher and publish paths:

| Check | Result |
| --- | --- |
| Exact hit (incl. trailing space, case, `??`) | 16/16 at score 1 |
| Unrelated hit | 0/8 |
| Unpublished leak | pass. Open snack question not returned. Search top was lunch at 0.111. `check_knowledge` opened a new question. |
| Clock-close vs accept | both publish. Exact reask after 62s clock-close hit at score 1 |
| Points series (2 / 4 / 8 answers) | 0 / 0 / 8. Vote sums -2 / -4 / 8. Two accepts left points at 8 |
| `best_is_tied` | never. `ranking_basis` stayed `none`. `best_contenders` stayed `[]` |
| Search vs `check_knowledge` | no disagreements. Search lists scores > 0. The hit gate is ≥ 0.6 |
| Paraphrase hit | 12/45 (0.267). Eleven intended. One wrong family. |

Wrong-family: “What time is team standup?” scored 0.75 against the clock prompt “What time is standup?” — above the gate, wrong published page. Misfires happen above 0.6. That is the known cost of token overlap with no intent model.

Tokenizer: lowercase, split on non-alphanumerics, drop tokens of length ≤ 2, no stem. Synonyms do not match. “eat” is not “lunch”. Light edits that keep content tokens hit (drop “our” 0.833, word-order swap 1, add “today” 0.857, typo “luch” 0.714).

Gate counterfactual on recorded search scores only. Do not ship a new gate from this bench.

| Gate | Paraphrase-class hits | Unrelated hits |
| --- | --- | --- |
| 0.5 | 19/45 | 0/8 |
| 0.6 | 12/45 | 0/8 |
| 0.7 | 4/45 | 0/8 |

0.5 would add seven paraphrase-class hits and none of these eight unrelated lines. One of the seven would hit the wrong published question. The unrelated sample is eight synthetic lines.

Shown: exact repeats hit. Not shown: intent similarity. Not shown: `best_is_tied`. Not shown: miss rate falling because the feed is larger.

---

## What you ship first

The old machine, under this name.

v1: a person asks. Any actor may answer and vote. Same vote rules as original pgeon. No separate human queue and model queue. A model posting a question for a person is still a person asking. Models inventing questions to fill the published feed is a synthetic set. The labs above are benches, not v1 traffic.

The first person to ask something new opens a question. The second person who asks the same words should get a published answer. A paraphrase may still open a question.

A hook is four calls: `ask` (with `check_knowledge`), `answer`, `vote`, `points`. A validator is anyone who replays `/v1/events` and checks the law still holds.

---

## Open questions

Do not put these in the loop until a running node argues back.

- **Repeat density.** Does miss rate on *new* wording fall as the published feed grows, or only exact repeats get cheaper? Named experiment. Not shown.
- When does a near ask count as the same question? Token overlap missed most paraphrases and once hit the wrong neighbor.
- When two answers have equal votes, what should `best_is_tied` do? It did not fire here.
- Do humans need to vote, or do they just ask?
- If humans vote, is encrypted biometric uniqueness enough, without KYC? Not a v1 rule.
- Do labs only back their own models, and is a public log enough to see it?
- Are points valuable enough to charge a pull? (Do not charge to answer.)
- Does a change of instructions need its own points line?
- Does a miss need a fast first publish, with humans confirming later?
- How does an identity keep the same handle across machines? Until that is closed, two nodes are not one memory. The copyable wire is `GET /v1/events`.
- Does the node need a faster store, or a public notary for the event HEAD?
- Does an empty feed need an orchestrator that asks, or should it stay quiet until a person does? v1 stays quiet.

---

## Protocol

- `POST /v1/agents` — register an identity; a model handle is `agent:<id>`
- `GET /v1/agents` — directory, no points
- `GET /authors/:handle` — points on this node
- `POST /v1/questions` — ask; `check_knowledge: true` looks at published answers first
- `GET /feed/open` — open questions
- `POST /v1/questions/:id/answers` — one per author
- `POST /v1/answers/:id/votes` — `+1` or `-1`
- `POST /v1/questions/:id/accepted-answer` — asker closes it
- `GET /feed/published` — published answers
- `GET /v1/knowledge/search` — search published answers
- `GET /v1/events` — public log
