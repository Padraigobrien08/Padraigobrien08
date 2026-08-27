<h1 align="center">Padraig O'Brien</h1>
<p align="center"><strong>AI Engineer</strong> — production LLM, RAG &amp; computer-vision systems</p>

<p align="center">
  <a href="https://padraig-obrien.com">Portfolio</a> ·
  <a href="https://www.linkedin.com/in/padraigmobrien/">LinkedIn</a> ·
  <a href="https://padraigobrien00.substack.com/">Substack</a> ·
  <a href="https://x.com/padraigob">X</a>
</p>

---

I started as a **data scientist** — R, notebooks, models that answered a question and then stopped. What interested me was everything that comes *after* the model works, so I taught myself software engineering in the open. The repos below are that process, kept public: each one carries its own reasoning, its own measurements, and its own limitations on the record.

Today I ship LLM, RAG and computer-vision systems at **yieldHUB**, embedded inside a commercial semiconductor analytics platform — owning them end-to-end from ambiguous requirements through to live deployment.

The part I keep coming back to is the layer most demos skip. Not just RAG and agent systems that reach production, but the **evaluation harnesses, regression gates, observability and failure analysis** that tell you whether they still work tomorrow — and say so honestly when they don't.

> **The LLM plans and interprets. Deterministic code computes.**
> Every number my systems report traces back to an artifact you can open.

That's the thread through everything below: robustness, evaluation, and honest reporting of what a system can't do. Each project states its own limitations, and **every figure on this page links to the file that proves it** — same rule the repos hold themselves to.

Next I'm taking that in the direction of research, with an **MSc in Artificial Intelligence at the University of Edinburgh**. [nanogpt-from-scratch](https://github.com/Padraigobrien08/nanogpt-from-scratch) is the run-up to it — it began as a tutorial reproduction, and [the original scripts are still committed](https://github.com/Padraigobrien08/nanogpt-from-scratch/tree/main/legacy) beside the rewrite that replaced them.

### Selected work

#### [nanogpt-from-scratch](https://github.com/Padraigobrien08/nanogpt-from-scratch) · [interactive site](https://www.nanogpt-pob.dev/) · [attention explorer](https://padraigobrien08.github.io/nanogpt-from-scratch/attention/)
From-scratch GPT-2 124M reproduction. RoPE, RMSNorm, SwiGLU, grouped-query attention and a static KV cache, all hand-written and tested against their defining mathematical properties rather than their output shapes.

**3.0503** val loss against a [target fixed before the run](https://github.com/Padraigobrien08/nanogpt-from-scratch/blob/main/docs/reproduction.md) · **39-run** [paired-seed ablation](https://github.com/Padraigobrien08/nanogpt-from-scratch/blob/main/docs/ablations.md) that reports "not a result" when the seeds disagree · **95.1%** [scaling efficiency across 8 GPUs](https://github.com/Padraigobrien08/nanogpt-from-scratch/blob/main/docs/scaling.md) with no NVLink · a benchmark that [found a 30% regression](https://github.com/Padraigobrien08/nanogpt-from-scratch/blob/main/docs/efficiency.md) hiding behind a green test suite

#### [rag-eval-observability](https://github.com/Padraigobrien08/rag-eval-observability) · [live demo](https://pob-rag-chat.xyz/)
RAG evaluation and observability in one deployable repo. Most RAG demos stop at chat; this one closes the loop — change the system, measure the same dataset, see what regressed and where to look in the production trace.

Four retrieval strategies [measured rather than asserted](https://github.com/Padraigobrien08/rag-eval-observability/blob/main/docs/BENCHMARKS.md) — reranking buys +3.8pp Hit@5 for ~5× the latency and ~1000× the cost · a [worked regression](https://github.com/Padraigobrien08/rag-eval-observability/blob/main/backend/eval/case_study/README.md) that a recall-only gate would ship, caught by MRR and blocked in CI · per-stage OpenTelemetry traces, so "slow" becomes "two OpenAI calls, not your retrieval"

#### [auditable-agent-loop](https://github.com/Padraigobrien08/auditable-agent-loop)
An investigation loop that proposes competing explanations, tests each against deterministic analysis, and traces every claim back to the number behind it. Adaptive reasoning is common; *auditable* adaptive reasoning is the part that took the work.

**107 of 107** evidence records linked to the experiment that produced them · a run that [rejected the premise of its own question](https://github.com/Padraigobrien08/auditable-agent-loop/blob/main/frontend/src/lib/demo-static/edgar-margin-vs-growth.json) instead of answering it · the model may write the answer but may not state a figure — one unverified number discards the whole narrative · [agency benchmark](https://github.com/Padraigobrien08/auditable-agent-loop/blob/main/docs/agent/agency-scoreboard.md) where a hard case is only admitted if it defeats the deterministic baseline

#### [strideiq](https://github.com/Padraigobrien08/strideiq) · [live demo](https://strideiq-lemon.vercel.app)
Local-first training intelligence for runners. Deterministic engines compute every metric; the LLM coach orchestrates 44 tools and is not allowed to invent numbers. Ships an MCP server so the same tools work in Claude Desktop.

Runs in the browser with [zero environment variables](https://strideiq-lemon.vercel.app) — no account, no database, no key · forecasts that name their own weakest assumption · [LIMITATIONS.md](https://github.com/Padraigobrien08/strideiq/blob/main/docs/LIMITATIONS.md) separates *implemented*, *unit-tested*, *exercised against the real system* and *proven in use* — and admits the race predictor has been checked against exactly one race, and was 7.5% out

#### [model-failure-lab](https://github.com/Padraigobrien08/model-failure-lab)
CLI that compares two versions of an LLM/RAG system, tells you what got worse, and harvests those failures into a permanent regression dataset. Git-native, fully local, no account.

See it catch a regression [offline in ~30 seconds](https://github.com/Padraigobrien08/model-failure-lab/tree/main/examples/regression_demo) — 4 of 8 cases quietly break · `compare --gate` exits non-zero, shipped as a composite GitHub Action · an [honest comparison table](https://github.com/Padraigobrien08/model-failure-lab#how-it-compares) that tells you when to reach for LangSmith, promptfoo or Ragas instead

#### [Stepwise](https://github.com/Padraigobrien08/Stepwise)
Multimodal RAG that turns tutorial videos into a searchable knowledge base — answers cite the exact step, timestamp, and the screenshot to prove it. Zendesk sidebar app included.

[HyDE retrieval](https://github.com/Padraigobrien08/Stepwise/blob/main/docs/hyde.md) with cross-encoder re-ranking · scene-change frame dedup cuts 40–60% of image tokens without dropping the visual modality · gap detection clusters the questions the library *couldn't* answer and names the tutorial to record next · [eval harness](https://github.com/Padraigobrien08/Stepwise/blob/main/docs/evaluation.md) reporting 52% strict pass, and the analysis showing the gap is corpus coverage rather than ranking

### Stack

**Building blocks I've written by hand** — rotary embeddings, RMSNorm, SwiGLU, grouped-query attention, static KV cache, quantization (int8/int4), speculative decoding, distributed training (DDP, gradient accumulation, 1.54 PFLOP/s across 8 GPUs)

**LLM systems** — agentic loops · RAG (hybrid, HyDE, cross-encoder re-ranking) · structured outputs &amp; tool use · offline eval harnesses and CI regression gates · MCP servers · multi-provider (OpenAI, Anthropic, Gemini)

**Platform** — Python · TypeScript · SQL · FastAPI · Next.js · PostgreSQL/pgvector · ChromaDB · Docker · OpenTelemetry · Prometheus/Grafana

**ML / CV** — PyTorch · anomaly detection · industrial and X-ray imaging

---

<p align="center"><strong>Open to AI / ML Engineer roles — relocating to London after my MSc, and open to remote.</strong><br>
<em>Currently in Edinburgh. Always happy to talk shop.</em></p>
