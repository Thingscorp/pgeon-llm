# Talk prep

Not a product launch checklist. What you can say tomorrow without lying.

## One sentence

A person asks. If pgeon already published an answer, they get it. If not, anyone may answer, anyone may vote, one answer is published, and the author keeps points.

## What is public today

- Code: [Thingscorp/pgeon](https://github.com/Thingscorp/pgeon) — ask, answer, vote, publish, points, `check_knowledge`, events.
- Claim: [Thingscorp/pgeon-llm](https://github.com/Thingscorp/pgeon-llm) — the paper. Not a second engine.
- There is no hosted public node with a dense published feed. Do not imply there is.

## Five beats (the talk)

1. A person asks a question.
2. If a published answer already fits, return it.
3. If not, anyone answers, anyone votes.
4. The clock or the asker publishes one answer.
5. Points move on the author. Repeat. The second person should be faster.

That is how it becomes a model: published answers get denser. Hits replace new questions.

## Demo (local, ten minutes)

```bash
git clone https://github.com/Thingscorp/pgeon.git
cd pgeon/api && PGEON_ALLOW_RESET=1 npm start
```

Then the walkthrough in the pgeon README: register two handles, ask, answer, vote, accept, `GET /feed/published`, `check_knowledge: true` on the same prompt.

Show three screens only: an open question, a published answer, `GET /authors/:handle`.

## Say this / do not say this

Say: selected answers stay public, named, reusable. Points are where an author obtained a record.

Do not say: we beat GPT, we are a chain, we have a live global model, humans cannot answer, this is a leaderboard, we have user scale.

## HN, in advance

- Stack Overflow is pages in a feed. Pgeon publishes one answer so the next ask does not open a duplicate.
- LMSYS is a lab arena with a board. Pgeon prints no ranks on the directory. Points live on the author.
- A lab model regenerates in private. This keeps the answer that was chosen.
- Not a blockchain. The log is `GET /v1/events`.

## YC, honest

- Problem: chat forgets; model names churn; there is no public file for who wrote what survived.
- Product: time-boxed questions, published answers, author points. Shipped in pgeon.
- Why now: people cannot tell which model to use; they need a record, not another brand.
- Traction: working API, paper, history back to the 2018 Q&A. Not usage at Google scale. Say that.
- Ask: a public node and real questions, not another spec.

## Still open (do not pitch as shipped)

Human-only votes. Sit fees. Instruction-line points. Hosted high-availability node. npm client. Cross-node identity.
