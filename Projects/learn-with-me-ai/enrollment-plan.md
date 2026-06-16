# Enrollment Plan: Courses Mapped to the Bible
### A sequenced, bottom-to-top route through existing courses, paired with the from-scratch series

---

## How to Use This

The courses below are scaffolding, not a substitute. The from-scratch build in each episode is still the real work, and the right pattern is to take the relevant course early in a module to get the concepts and the framework fluency, then spend the rest of the module building the thing by hand. Wherever a course would let you skip the build, do not let it.

Pick one primary course per slot rather than stacking redundant ones. The supplements are there if a topic does not land, not as a checklist.

On cost. The free spine of this plan is strong enough to stand on its own: Karpathy, fast.ai, Hugging Face, the Stanford and UCL lecture recordings, and 3Blue1Brown together cover most of the path. The paid Coursera courses mainly help with structure and accountability in the early math and classical-ML stretch. If you do use a Coursera subscription, subscribe only when you reach the modules that need it, Modules A and B, and cancel once you move into the free-heavy middle, because everything from Module C onward is largely free.

---

## The Sequence, Bottom to Top

### Module A, Foundations (Episodes 1 to 5)
- **Math, Episodes 1 to 4. Primary:** Mathematics for Machine Learning specialization, Imperial College London, on Coursera. Three courses covering linear algebra, multivariate calculus, and PCA. Paid subscription, structured.
- **Supplement, free and strongly recommended:** 3Blue1Brown's Essence of Linear Algebra and Essence of Calculus on YouTube. This is the visual intuition you will be reproducing in HLSL, so watch it regardless of the paid course.
- **GPU compute, Episode 5.** No clean single course exists, which is expected since this is your differentiator. Closest structured option is NVIDIA's Deep Learning Institute Fundamentals of Accelerated Computing with CUDA. In practice most people learn this from Simon Boehm's matmul blog, Horace He's writing, and the Programming Massively Parallel Processors lectures rather than a course.
- **Gap the bible fills:** the GPU compute episode has no real course equivalent.

### Module B, Classical ML (Episodes 6 to 7)
- **Primary:** Andrew Ng's Machine Learning Specialization, Stanford and DeepLearning.AI, on Coursera. The canonical starting point and the cleanest teaching of the model-loss-minimize loop. Paid subscription.
- **Alternative:** the IBM Machine Learning Professional Certificate you found. It sits exactly here, is solid and hands-on, but is library-first and does not reach transformers, diffusion, or systems. Choose it only if you prefer IBM's lab style over Ng's conceptual grounding. Do not take both.
- **Maps cleanly,** since this module is the most course-friendly in the whole plan.

### Module C, Deep Learning From Scratch (Episodes 8 to 12)
- **Primary, free, and the heart of the match:** Andrej Karpathy's Neural Networks Zero to Hero on YouTube. This is the closest thing in existence to the from-scratch philosophy of the bible, building backprop and a GPT by hand. Treat it as required.
- **Structured supplements:** Andrew Ng's Deep Learning Specialization on Coursera for breadth, or fast.ai's Practical Deep Learning, which is free, excellent, and top-down.
- **Debugging, Episode 10.** No course teaches this. Use Karpathy's essay A Recipe for Training Neural Networks, which is the definitive short text.
- **Gap the bible fills:** the debugging and training-recipe episode has no course equivalent.

### Module D, Representations (Episode 13)
- **Primary, free:** the embeddings and tokenization opening of Hugging Face's LLM Course. Covers the vector-as-meaning idea hands-on.
- **Supplement, free:** the early lectures of Stanford CS224N, Natural Language Processing with Deep Learning, on YouTube, which cover word vectors with academic depth.

### Module E, Transformers and LLMs (Episodes 14 to 20)
- **Primary, free:** Hugging Face's LLM Course for the hands-on transformer, tokenization, and fine-tuning material, plus Karpathy's Let's build GPT and Let's build the GPT Tokenizer, which map almost one to one onto Episodes 14 and 15.
- **Depth supplement, free:** Stanford CS224N full lecture set on YouTube.
- **Distributed training, Episode 17.** No good single course, which again validates including it. Best structured free material is Hugging Face's Ultra-Scale Playbook writeup and their parallelism documentation, with the DeepSpeed and PyTorch FSDP docs as practical references.
- **Modern architecture, Episode 18.** No course is current enough. Learn rotary embeddings, RMSNorm, grouped-query attention, Mamba, and mixture of experts from the papers named in the bible.
- **Interpretability, Episode 20.** No course. Use the ARENA curriculum, which is the closest thing to a structured interpretability course and is free, plus Neel Nanda's and Anthropic's published material.
- **Gaps the bible fills:** distributed training, modern architecture, and interpretability all lack course equivalents.

### Module F, Reinforcement Learning (Episodes 21 to 22)
- **Primary, free and hands-on:** Hugging Face's Deep RL Course, which is modern and practical.
- **Theory supplement, free:** David Silver's UCL Reinforcement Learning lectures on YouTube.
- **For the PPO episode, free:** OpenAI's Spinning Up in Deep RL as the practical text.

### Module G, Alignment, Reasoning, and Systems (Episodes 23 to 27)
- **Alignment, Episodes 23 and 24, free:** Hugging Face's RLHF and DPO writeups, supplemented by the InstructGPT and DPO papers themselves.
- **Reasoning, Episode 25.** No course worth enrolling in exists yet. The field moved faster than any curriculum, so learn it from the chain-of-thought, DeepSeek-R1, GRPO, and test-time-compute papers named in the bible.
- **Inference and systems, Episode 26, free:** the FlashAttention, GPTQ, and speculative decoding papers, plus Hugging Face and vLLM documentation for the practical side.
- **Retrieval and agents, Episode 27, free:** the RAG and ReAct papers, plus any current Hugging Face or LangChain-style tutorial for the wiring, though the concepts matter more than the framework.
- **Gap the bible fills:** the entire reasoning and modern-systems frontier lacks course coverage.

### Module H, Generative Models and Diffusion (Episodes 28 to 33)
- **Primary, free and the clear winner:** Hugging Face's Diffusion Models Course, which builds diffusion hands-on and matches Episodes 30 through 32 closely.
- **Depth supplement, free:** fast.ai's From Deep Learning Foundations to Stable Diffusion, which builds from scratch.
- **VAE, Episode 28:** covered in passing by the above, with Lilian Weng's survey as the reference.
- **Flow matching and diffusion transformers, Episode 33.** No course. Learn from the flow matching, rectified flow, DiT, and Stable Diffusion 3 papers named in the bible.
- **Gap the bible fills:** the modern flow-matching and DiT frontier lacks course coverage.

---

## Master Sequence Table

| Order | Bible module | Episodes | Primary course | Format |
|---|---|---|---|---|
| 1 | A: Foundations, math | 1 to 4 | Mathematics for ML, Imperial, Coursera, plus 3Blue1Brown | Paid plus free |
| 2 | A: Foundations, GPU | 5 | No course, NVIDIA DLI CUDA plus blogs | Mixed |
| 3 | B: Classical ML | 6 to 7 | Andrew Ng Machine Learning Specialization, Coursera | Paid |
| 4 | C: Deep Learning | 8 to 12 | Karpathy Zero to Hero, plus fast.ai | Free |
| 5 | D: Representations | 13 | Hugging Face LLM Course, embeddings section | Free |
| 6 | E: Transformers and LLMs | 14 to 20 | Hugging Face LLM Course plus Karpathy GPT, CS224N | Free |
| 7 | F: Reinforcement Learning | 21 to 22 | Hugging Face Deep RL Course plus David Silver | Free |
| 8 | G: Alignment, Reasoning, Systems | 23 to 27 | Papers plus Hugging Face writeups | Free, no course |
| 9 | H: Diffusion | 28 to 33 | Hugging Face Diffusion Course plus fast.ai | Free |

---

## The Honest Pattern

The bottom two-thirds of the bible, roughly Modules A through F, is well served by existing courses: Coursera for early structure, then Karpathy, fast.ai, and Hugging Face for the from-scratch depth and the modern hands-on material. The top third, distributed training, reasoning, alignment, interpretability, flow matching, and the GPU and visual angles throughout, has almost no course coverage and is learned from papers and writeups. That gap is precisely what the series is built to fill, so the absence of courses there is a feature of the opportunity rather than a problem with the plan.

## A Note on the Free-Only Route

If you skip Coursera entirely, the path still holds. Replace the Imperial math specialization with 3Blue1Brown plus the Mathematics for Machine Learning book, and replace Andrew Ng's Coursera courses with fast.ai and the free lecture recordings. Everything from Module C onward is already free in this plan, so the only thing a subscription buys you is structure and graded accountability in the first two modules.
