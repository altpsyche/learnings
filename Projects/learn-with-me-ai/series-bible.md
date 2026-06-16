# Learn With Me: AI From the Ground Up
### A Graphics Programmer's Path, Taught Through Real-Time Visuals

---

## The Premise

Most of machine learning is fields, gradients, transforms, and noise. A graphics programmer renders exactly those things for a living, which means a large part of this subject is already familiar in a different language. This series treats that overlap as the teaching method. The aim is to learn the material deeply enough to teach it cleanly, to give every concept the best visualization it can have, to leave no gaps in the path from arithmetic to the current frontier, and to teach what actually ships in 2026 rather than what shipped in 2017.

The weight of the series sits deliberately on the episodes that only a graphics and systems background can produce well: convolution as a fragment shader, rotary embeddings as literal rotation, distributed training as a memory and communication problem, the diffusion noise process, the score field, flow matching as straight-line transport, the GPU compute reality, and mechanistic interpretability. The generic from-scratch transformer, which is already taught well elsewhere, is treated as a fast and honest bridge rather than the centerpiece. The differentiated material is where the time goes.

---

## Prerequisites and Scope

This series assumes working fluency in Python and the scientific stack, NumPy moving into PyTorch, which is used from the first build onward and is not taught here. It also leans from Episode 1 on the skill of reading research papers, which is itself worth practicing deliberately rather than assuming.

The following are deliberately out of scope, called out so their absence is a decision rather than an oversight. The classical machine learning breadth of decision trees, ensembles such as random forests and gradient boosting, support vector machines, and clustering is left aside, because the target is deep generative models rather than the full machine learning canon. Graph neural networks are not covered. The operational layer of experiment tracking, deployment pipelines, and MLOps is not covered. These are reasonable next directions, but they are not part of this path.

---

## Visual Honesty

A shader is the right tool for continuous fields and transforms and the wrong tool for discrete, symbolic, or algorithmic content. Forcing a shader onto everything produces visuals that look impressive and teach nothing, and an audience that codes will see through that immediately. So every visual in this series is tagged with the honest medium it deserves, and the tag is a commitment, not a label.

- **[SHADER]** is real-time HLSL on a continuous field or transform, driven by real values produced by your own code wherever possible. This is the hero medium and the reason the series exists. A [SHADER] tag promises the visual is reading genuine numbers, never a hand-faked animation.
- **[PLOT]** is a data visualization or a chart. It is used without apology whenever the content is fundamentally data, such as a loss curve, a scaling law, or an evaluation metric. Dressing a chart up as a shader would be dishonest, so the series does not.
- **[CODE]** is an animated code or algorithm trace. It is used when the content is symbolic and has no natural continuous form, such as the byte pair encoding merge loop. A clear code animation teaches that better than any field ever could.

Many episodes carry a primary medium and a secondary one, and that mix is stated explicitly. The discipline of choosing the right medium per concept is itself part of what makes the visuals good rather than merely pretty.

---

## The Recurring Visual Language

Four shader primitives are built once, in Part 0, and reused for the entire run so that visuals compound rather than restart. The investment in building these well at the start pays back across the whole series, and by the end the most advanced visuals are simply these four primitives recombined and pointed at new data.

| Primitive | Convention | Reused across the series for |
|---|---|---|
| Scalar field | a single consistent color ramp | loss surfaces, probability density, value functions, reward landscapes |
| Vector field | a grid of arrows with consistent scaling | gradients, score functions, flow transport, RL policies |
| Matrix | a heatmap with a fixed color meaning | attention weights, learned weight matrices, linear transforms |
| Trajectory | a path drawn over any field | gradient descent, diffusion and flow sampling, RL rollouts |

The score field in the diffusion episodes is the vector-field primitive aimed at a data distribution. The policy field in the reinforcement learning episodes is the same primitive aimed at a gridworld. Building the four primitives carefully in Part 0 is therefore the single highest-leverage piece of production work in the project.

---

## The Through-Line

Every model in this series, from the first line fit in Episode 6 to the flow-matching transport in Episode 33, is the same loop: define a model, define a loss that measures how wrong it is, and minimize that loss by following its gradient. The series returns to this loop on purpose and names it each time, so that the apparent jump from linear regression to a diffusion transformer is revealed to be the same idea wearing heavier clothing. Holding that line is the thread that makes the whole thing feel like one subject rather than thirty-odd disconnected topics.

**The single rule across every episode:** build it from scratch before touching the library version. The from-scratch build is the episode itself, and the library is a closing footnote that shows how the idea is packaged in practice. Understanding is the product, not working code, and the two are not the same thing.

---

## What Each Episode Ships

Each episode is one piece of work narrated three ways. The from-scratch code is the spine. The visual on altpsyche.dev is the explanation. The blog post and the YouTube video are the written record and the spoken walkthrough of that same work. Producing it as one artifact narrated three ways, rather than three separate efforts, is the only way the cadence survives alongside a demanding job.

Pacing is variable rather than a flat two weeks per episode, because the back half is genuinely heavier than the front. Approximate week ranges are given per module, and the honest total across thirty-three episodes is roughly sixteen to twenty months at a sustainable pace. Treating every episode as equal effort is the most common way a solo technical series collapses around the two-thirds mark, when the easy early episodes have set an expectation the hard later ones cannot meet.

---

# Part 0: Series Setup

Before any teaching happens, the foundation that every later episode depends on gets built once. This is unglamorous and worth doing properly, because every shortcut taken here is paid for repeatedly across the run.

- **Goal.** Build the visual harness and the four primitives so that no later episode spends its time on plumbing instead of on the concept.
- **Tasks.** Standardize the altpsyche.dev shader harness around a shared uniform interface for time, pointer input, and named sliders, so every episode shader plugs into the same controls. Build the scalar-field, vector-field, matrix-heatmap, and trajectory modules as reusable, well-documented shader components. Establish the blog template with a fixed spine of goal, intuition, the math, the visual, the from-scratch code, and the takeaway. Establish the repository template with one folder per episode holding both the code and the shader source. Record a short series introduction that states the premise and the single from-scratch rule so viewers know the contract.
- **Deliverable.** A working visual harness and four solid primitives that the rest of the series reuses without modification.

---

# Module A: Foundations (Episodes 1 to 5, roughly 10 to 12 weeks)

This module builds the mathematical and hardware floor that everything stands on. The temptation is to rush it, and the cost of rushing it is that every later episode becomes a memorization exercise instead of an understanding. The shaders here also establish the visual vocabulary, so the time spent making them beautiful is doubly justified.

## Episode 1: Linear Algebra for ML
Linear algebra is the language the entire field is written in, and the single most useful reframing is that a neural network is a stack of linear maps with simple nonlinear functions wedged between them. Once matrices are seen as transformations of space rather than grids of numbers, most of what follows becomes geometric intuition rather than symbol manipulation.

- **Goal.** See every model as a stack of tensor transforms acting on space.
- **Concepts to master.** Vectors as both points and directions; matrices as transformations; matrix multiplication as the composition of two transformations; the dot product in its two faces, as geometric projection and as a similarity score; norms as length; rank as the dimensionality a transform preserves; the determinant as the factor by which area or volume is scaled; eigenvalues and eigenvectors as the directions a transform leaves pointing the same way; change of basis as looking at the same vector from a different coordinate system; and the realization that matrix multiplication is the atomic operation of all deep learning compute.
- **What to read.** Mathematics for Machine Learning by Deisenroth, Faisal, and Ong, chapters 2 through 4, which is the cleanest single source for this stage. The Matrix Cookbook as a lookup reference rather than a read-through. The 3Blue1Brown series Essence of Linear Algebra, watched for the geometric intuition you will then reproduce in HLSL.
- **The visual [SHADER].** A live matrix acting on a grid mesh, with a slider on each entry, so shear, rotation, and scaling can be felt directly. The determinant is shown by tinting the transformed area according to how much it grew or shrank, and the eigenvectors are drawn as rays that visibly stay on their own line while everything else rotates around them. This single scene becomes the change-of-basis visual reused in later episodes.
- **The build.** Matrix multiplication, the dot product, and transpose by hand, then a power-iteration eigenvector finder, then a small principal component analysis on a toy dataset to show eigenvectors doing real work.
- **Teaching note.** The biggest unlock for most viewers is the dot product wearing two hats at once. Spend time there, because cosine similarity in embeddings and attention scores both rest on it.
- **Video hook.** "Every neural network is one matrix applied over and over. Here is exactly what that does to space."

## Episode 2: Calculus, Gradients, and Autodiff
The dread around backpropagation evaporates the moment it is seen as the chain rule applied mechanically over a graph, which is all it is. This episode builds that graph and runs derivatives backward through it, turning a feared topic into a bookkeeping exercise.

- **Goal.** Understand backpropagation as the chain rule executed over a computational graph, and build the engine that does it.
- **Concepts to master.** Derivatives as local rates of change; partial derivatives as the slope along one axis with the rest held fixed; the chain rule as the rule for composing rates of change; the gradient as the vector of all partials and the direction of steepest ascent; the Jacobian as the gradient generalized to vector outputs; the computational graph as the record of every operation; and the distinction between forward-mode and reverse-mode automatic differentiation, with a clear account of why reverse mode is the right default when there are many inputs and one loss.
- **What to read.** Mathematics for Machine Learning chapter 5. The 3Blue1Brown Essence of Calculus series for intuition. Baydin and colleagues, Automatic Differentiation in Machine Learning, a Survey, 2018, for the mechanism stated precisely.
- **The visual [SHADER] and [CODE].** The shader renders a loss surface as a heightmap with a ball resting on it, and draws the gradient vector at the ball's position pointing uphill, so the negative gradient that training follows is the visible downhill direction. The code trace lights up each node of the computational graph as the backward pass flows through it, so the chain rule is seen propagating, not just described.
- **The build.** A scalar automatic differentiation engine in the style of micrograd, with a Value type that records operations and a backward method that walks the graph in reverse to populate gradients.
- **Teaching note.** Show a wrong gradient first. Let a sign error send the ball uphill, then fix it. Seeing the failure mode cements why the sign and the direction matter.
- **Video hook.** "Backpropagation has a frightening name. It is the chain rule and nothing else, and we are going to build it."

## Episode 3: Probability, Distributions, and Information Theory
Loss functions look arbitrary until they are read as statements about probability and surprise, at which point cross-entropy and the KL divergence stop being formulas to memorize and become things that mean something. This episode gives the information-theoretic vocabulary that recurs in every generative model later.

- **Goal.** Read any loss function and know precisely what quantity it measures.
- **Concepts to master.** Random variables and the distributions they follow; expectation and variance as the center and spread; the Gaussian and Bernoulli as the two workhorses; Bayes theorem as the rule for updating belief on evidence; entropy as the average surprise of a distribution; cross-entropy as the cost of using the wrong distribution to encode the right one; the KL divergence as the gap between the two and why it is never negative; and mutual information as shared content. The payoff is understanding why cross-entropy is the default classification loss and why the KL term appears throughout variational and diffusion models.
- **What to read.** Mathematics for Machine Learning chapter 6. Cover and Thomas, Elements of Information Theory, chapters 1 and 2 as reference. Shannon's 1948 paper skimmed once for the sheer origin of the ideas.
- **The visual [SHADER].** A two-dimensional Gaussian rendered as a soft glow with live sliders for mean and variance, so the distribution can be moved and stretched by hand. Then two distributions shown together with their KL divergence computed live and drawn as the shaded area of mismatch between them, so the abstract number becomes a visible gap that shrinks as the distributions align.
- **The build.** Entropy, cross-entropy, and KL divergence implemented from scratch, with a numerical demonstration that cross-entropy equals entropy plus KL, which makes the relationship concrete rather than asserted.
- **Teaching note.** Tie the KL visual forward explicitly. Tell viewers they will see this exact gap again as the regularizer in a variational autoencoder and inside the diffusion objective, so the investment here is banked.
- **Video hook.** "Cross-entropy loss is not arbitrary. It is measuring surprise. Watch the surprise shrink as the model learns."

## Episode 4: Optimization and Gradient Descent
Training is just optimization, and most training failures are optimization failures in disguise. This episode builds the mental model of a loss landscape and the small family of tricks that get a model down it reliably.

- **Goal.** Know why training works when it works and why it stalls when it stalls.
- **Concepts to master.** The difference between convex and non-convex landscapes and why deep learning lives entirely in the latter; local minima and the more common problem of saddle points and plateaus; gradient descent in its full-batch, stochastic, and mini-batch forms and the tradeoffs between them; momentum as accumulated velocity that powers through flat regions; and the outsized practical effect of the learning rate, which is the single most important hyperparameter in the field.
- **What to read.** Mathematics for Machine Learning chapter 7. Goodfellow, Bengio, and Courville, Deep Learning, chapter 8. Sebastian Ruder's overview of gradient descent optimization algorithms for a survey of the variants.
- **The visual [SHADER].** The loss surface from Episode 2, now hosting several optimizers at once, each released from the same start point and tracing its own colored trajectory down the surface. Plain gradient descent crawls, momentum overshoots and corrects, and different learning rates either diverge off the surface or inch along too slowly, all racing simultaneously so the differences are immediate and visceral.
- **The build.** Stochastic gradient descent and momentum implemented from scratch, run on a deliberately non-convex toy surface with visible traps.
- **Teaching note.** The learning-rate demonstration is the heart of the episode. Show divergence, show crawling, and show the band in between, because nearly every beginner's first failure is a learning rate set wrong.
- **Video hook.** "Why does a model sometimes flatly refuse to learn? I will race four optimizers down the same hill and you will see it happen."

## Episode 5: GPU Compute for Machine Learning
This is the episode almost no machine learning course teaches and the one a profiling background makes uniquely strong. Understanding why a model is slow, and what the hardware is actually doing during a matrix multiply, separates people who can scale a model from people who can only call it. FlashAttention is deliberately deferred to Episode 26, because it is meaningless before attention exists.

- **Goal.** Understand the hardware reality that quietly decides which models are even trainable.
- **Concepts to master.** General matrix multiply, GEMM, as the operation that dominates deep learning runtime; tiling and the memory hierarchy from global to shared memory to registers; arithmetic intensity as the ratio of compute to memory traffic; the distinction between memory-bound and compute-bound kernels; the roofline model as the single diagram that explains where a kernel's performance ceiling comes from; and kernel fusion as the practice of avoiding round trips to slow memory.
- **What to read.** Horace He's essay Making Deep Learning Go Brrrr From First Principles for the conceptual frame. Simon Boehm's walkthrough on optimizing a CUDA matmul kernel for the concrete progression. Kirk and Hwu, Programming Massively Parallel Processors, as the reference text.
- **The visual [SHADER] and [PLOT].** The shader animates GEMM tiling directly, showing tiles of the two input matrices being loaded from slow global memory into fast shared memory and accumulated into the output, with each memory tier given a distinct color so the data movement that dominates real performance becomes visible. The plot is the roofline, placing several kernels on it by their arithmetic intensity so the memory-bound and compute-bound regions are obvious.
- **The build.** A naive matrix multiply kernel and then a tiled one, with the speedup measured and traced back explicitly to reduced memory traffic rather than reduced arithmetic.
- **Teaching note.** This is the episode to lean into your own background openly. The credibility of having shipped GPU profilers is the differentiator, and stating that plainly is what tells the audience why this channel is worth following over a generic one.
- **Video hook.** "Every machine learning course skips this. Let me show you why your transformer is starving the GPU, and how to feed it."

---

# Module B: Classical ML (Episodes 6 to 7, roughly 4 weeks)

Before any neural network, the core loop is established on models simple enough to hold entirely in the head. Everything after this is a more elaborate version of these two episodes, and saying so out loud sets the audience up to recognize the pattern repeating.

## Episode 6: The Learning Loop, Regression From Scratch
This is where the through-line of the whole series is named for the first time. A model, a loss, and a way down the loss is the entire recipe, and seeing it work on a straight line makes every later model less intimidating.

- **Goal.** Internalize the model, loss, minimize loop on the simplest possible model.
- **Concepts to master.** Linear regression as fitting a line by minimizing squared error; logistic regression as bending that idea to classification through the sigmoid; the sigmoid as a squashing function that turns a number into a probability; the decision boundary as the contour where the model is undecided; gradient descent applied to real, interpretable parameters; and the contrast between solving for the answer in closed form with the normal equation versus iterating toward it, which previews why iteration is the only option once models grow.
- **What to read.** An Introduction to Statistical Learning, chapters 3 and 4. Andrew Ng's Machine Learning course, weeks 1 through 3.
- **The visual [SHADER].** Scattered data points in a render target with a fit line that descends toward them as training proceeds, each point tinted by the size and sign of its residual so the error is visible per point. Then the logistic case, where the plane is colored continuously by predicted class probability and the decision boundary emerges for free as the contour where that probability is one half.
- **The build.** Linear and logistic regression written from scratch, with the live parameters of your own training loop driving the shader directly.
- **Teaching note.** Pause on the moment the same gradient-descent loop from Episode 4 is reused here unchanged. That recognition is the point, and it is worth stating that this loop will return for GPT.
- **Video hook.** "This exact loop trains GPT. Once you have seen it work on a line, you have seen it work on everything."

## Episode 7: Generalization, Regularization, Evaluation
A model that scores perfectly on its training data can be worthless, and knowing the difference between learning and memorizing is the skill that separates a practitioner from someone running code they do not understand.

- **Goal.** Learn to tell when a model is genuinely learning versus quietly lying.
- **Concepts to master.** Overfitting and underfitting as the two failure modes; the bias-variance tradeoff as the tension between them; L1 and L2 regularization as penalties that discourage complexity, with L1's tendency toward sparsity and L2's toward small weights; the discipline of separate training, validation, and test sets and why leaking the test set ruins everything; cross-validation as a way to use limited data honestly; and the evaluation metrics beyond accuracy that matter when classes are imbalanced.
- **What to read.** An Introduction to Statistical Learning, chapters 5 and 6. The Elements of Statistical Learning, chapter 7, for the deeper treatment of model assessment.
- **The visual [PLOT] and [SHADER].** The plot shows training loss falling steadily while validation loss falls and then turns back upward, with the gap between them being the visible signature of overfitting, alongside the classic bias-variance U-curve. The shader shows a decision boundary growing visibly more contorted as model complexity rises, so overfitting is not just a number on a chart but a boundary that has clearly started chasing individual noisy points.
- **The build.** L2 regularization and k-fold cross-validation implemented by hand, with the regularization strength swept to show the boundary smoothing out.
- **Teaching note.** The most memorable framing is the model that scores ninety-nine percent and is useless. Open with that paradox and resolve it, because it reframes high training accuracy as a warning sign rather than a success.
- **Video hook.** "Your model scored ninety-nine percent and it is worthless. Here is the exact moment it started memorizing instead of learning."

---

# Module C: Deep Learning From Scratch (Episodes 8 to 12, roughly 12 to 14 weeks)

This module earns the word mastery. By the end of it there is a working neural network, written line by line, that trains reliably, and the viewer knows what to do when it does not. The debugging episode in particular is the one most courses omit and the one that most respects the audience's real experience.

## Episode 8: Neural Nets and Backprop From Scratch
The whole field rests on this one build. Writing a network and its backward pass by hand, with no framework, is the exercise that converts surface familiarity into understanding, and it is non-negotiable for a series built on the from-scratch rule.

- **Goal.** Build a working neural network and its backward pass with no framework whatsoever.
- **Concepts to master.** The artificial neuron as a weighted sum followed by a nonlinearity; layers as stacks of neurons; the forward pass as data flowing through those layers; manual backpropagation as the Episode 2 engine applied to a real network; the common activation functions ReLU, sigmoid, tanh, and GELU and what each is good and bad at; the choice of loss for classification; and a concrete account of why depth lets a network compose simple features into complex ones.
- **What to read.** Michael Nielsen's Neural Networks and Deep Learning, chapters 1 and 2, which has the clearest from-scratch backprop derivation in existence. Karpathy's Zero to Hero, the micrograd and early makemore episodes.
- **The visual [CODE] and [SHADER].** The code trace shows the backward pass flowing through the actual network graph, building on the Episode 2 visual. The shader renders the network's activations as a texture atlas, one tile per neuron, so that as the input is swept, each neuron's region of response lights up and the abstraction of a hidden unit becomes something you can watch react.
- **The build.** Extend the Episode 2 autodiff engine into a small multilayer perceptron, train it on a toy classification dataset, and hand-verify a gradient against a numerical estimate to prove the backward pass is correct.
- **Teaching note.** The numerical gradient check is worth airtime. It is how professionals trust their own backprop, and showing it builds the habit of verification rather than faith.
- **Video hook.** "We are going to build a single neuron, then a network, then watch it learn, every single line by hand."

## Episode 9: Tensor Autograd and Training Deep Networks
There is a hidden rung between a scalar autograd toy and the frameworks everyone uses, and skipping it leaves a permanent gap in understanding. This episode climbs that rung by generalizing the engine to tensors, and then adds the techniques that make deep networks actually trainable.

- **Goal.** Cross from scalar autograd to real tensor autograd, then make a genuinely deep network train.
- **Concepts to master.** Tensor-valued automatic differentiation with broadcasting, which is the real machinery underneath every framework and the piece the scalar engine hid; weight initialization schemes from Xavier and He and why a bad initialization alone can prevent learning; batch normalization and layer normalization as ways to keep activations well-scaled; dropout as a regularizer that prevents co-adaptation; the Adam optimizer and why its per-parameter adaptive rates outperform plain stochastic gradient descent in practice; learning-rate schedules; and residual connections as the idea that let networks go truly deep by giving gradients a clear path backward.
- **What to read.** Ioffe and Szegedy on batch normalization, 2015. Ba, Kiros, and Hinton on layer normalization, 2016. Kingma and Ba on Adam, 2014. He and colleagues on deep residual learning, 2015. Srivastava and colleagues on dropout, 2014.
- **The visual [SHADER] and [PLOT].** The shader draws the network as nodes and edges and animates the magnitude of the real gradient flowing backward through it, colored by size, with a toggle for residual connections so the viewer watches gradients vanish to nothing in a deep plain network and then come back to life the instant the skip connections are switched on. The plot pairs this with loss curves measured with and without each technique so the effect is quantified, not just asserted.
- **The build.** A small tensor-autograd engine with broadcasting, then batch normalization, dropout, and Adam implemented on top of it, with PyTorch introduced only at the very end as the packaged version of what was just built.
- **Teaching note.** The residual-connection toggle is the emotional peak of the episode. Frame the vanishing gradient as the problem that stalled deep learning for years and the skip connection as the deceptively simple fix that broke it open.
- **Video hook.** "Scalar autograd was a toy. Real autograd is tensors and broadcasting, and here is the rung that everybody skips."

## Episode 10: Debugging and the Training Recipe
This episode does not introduce a new architecture, and that is precisely why it matters. The single most useful thing a series can give a beginner is a calm, systematic answer to the moment their loss becomes NaN at two in the morning. Omitting this is a quiet form of negligence.

- **Goal.** Teach the systematic skill of diagnosing a model that will not learn.
- **Concepts to master.** Why a loss goes to NaN and the usual culprits of exploding gradients, bad learning rates, and numerical instability in the loss; the numerically stable softmax and the log-sum-exp trick, whose absence is one of the most common and most mysterious sources of NaN and overflow; vanishing and exploding gradients seen in practice rather than theory; the overfit-a-single-batch test as the fastest sanity check that the model and the training loop are wired correctly; learning-rate finding; how to read the shape of a loss curve as a diagnosis; and a disciplined, ordered recipe for bringing a model up from nothing rather than flailing.
- **What to read.** Andrej Karpathy's essay A Recipe for Training Neural Networks, which is the definitive short text on this and the model for the whole episode.
- **The visual [PLOT] and [CODE].** The plot is a gallery of pathological loss curves, each annotated with what it means and what to change, so the viewer builds a visual diagnostic vocabulary. The code shows a live NaN hunt narrowing down where the instability enters, including a side-by-side of a naive softmax overflowing and the stable version holding, and the overfit-one-batch test passing, which is the moment a broken-feeling project is proven to be fundamentally sound.
- **The build.** Take the working Episode 9 network, deliberately break it five different ways on camera, including an unstable softmax, and fix each one using the recipe, so the audience sees the failures rather than only the successes.
- **Teaching note.** This will likely become the most-rewatched episode in the series, so make it findable and reference it from every later training episode as the place to go when things break. The stable-softmax segment in particular pays off silently every time softmax and cross-entropy appear later.
- **Video hook.** "Your loss just went to NaN at two in the morning. This is the episode you will come back to more than any other."

## Episode 11: Convolutional Networks
For a graphics programmer this is the most natural episode in the early run, because a convolution is a fragment shader, and the realization that years of pixel-shader work was already deep learning in disguise is a genuinely satisfying reframing to give an audience.

- **Goal.** Understand convolution as the shader operation it already is, including the transposed form needed later for generative decoders.
- **Concepts to master.** Convolution as a small kernel swept across an image; the meaning of stride and padding; pooling as spatial downsampling; the receptive field as the region of input a deep feature can see; convolution arithmetic relating input size, kernel, stride, and output; transposed convolution as the upsampling operation that builds the decoder half of U-Nets and generative models; and a clear-eyed look at vision transformers as the architecture that increasingly competes with convolutional networks on images.
- **What to read.** Deep Learning by Goodfellow and colleagues, chapter 9. Dumoulin and Visin, A Guide to Convolution Arithmetic for Deep Learning, 2016, which is the clearest reference for the shapes. Dosovitskiy and colleagues, An Image is Worth Sixteen by Sixteen Words, 2020, for the vision transformer.
- **The visual [SHADER].** Convolution implemented directly as a fragment shader, starting with hand-designed kernels for edge detection, blur, and sharpening so the operation is grounded in something familiar, then a learned-looking kernel sliding across an image with the current receptive field highlighted, and finally transposed convolution shown upsampling a small feature map back up to image resolution.
- **The build.** A convolution layer and a transposed-convolution layer written from scratch, with the learned kernels rendered as images so the viewer sees what the network chose to detect.
- **Teaching note.** Open by writing a blur in HLSL the way the audience already knows, then reveal that this is the exact operation inside a convolutional network. The bridge from familiar to new is the whole pedagogical move.
- **Video hook.** "You have written this exact loop in a pixel shader a hundred times. It turns out you have been doing deep learning all along."

## Episode 12: Sequence Models and Why They Break
This episode exists to make the audience feel a specific pain, because attention is only impressive once the problem it solves has been experienced. A recurrent network that visibly forgets the start of a sentence is the setup that makes the next module land.

- **Goal.** Feel, concretely, the long-range memory problem that attention was invented to solve.
- **Concepts to master.** Recurrent networks as models with a hidden state carried across time; the long short-term memory cell as a gated attempt to preserve that state; backpropagation through time as backprop unrolled across a sequence; the mechanism by which gradients vanish over long sequences and information from early steps decays away; and the resulting hard ceiling on how much context these models can truly hold.
- **What to read.** Hochreiter and Schmidhuber's original long short-term memory paper, 1997. Christopher Olah's Understanding LSTM Networks for the clearest diagrams. Karpathy's The Unreasonable Effectiveness of Recurrent Neural Networks for the intuition and the fun.
- **The visual [SHADER].** The hidden-state vector rendered as a horizontal strip of color that evolves token by token as a real recurrent network reads a sequence, with the influence of early tokens visibly fading from the strip as the sequence grows longer, so the memory leak is something the viewer watches happen rather than reads about.
- **The build.** A character-level recurrent network from scratch, trained until it generates plausible text, then probed until it visibly loses track of context introduced many characters earlier.
- **Teaching note.** End on the unresolved frustration deliberately. Do not fix the problem in this episode. The cliffhanger of a model that cannot remember is what gives the attention episode its payoff.
- **Video hook.** "Before attention, models had a memory leak by design. Watch the beginning of the sentence literally fade out."

---

# Module D: Representations (Episode 13, roughly 2 to 3 weeks)

A single episode, but a pivotal one, because the idea that meaning can live as geometry in a vector space is the conceptual key to attention, retrieval, and the text-to-image conditioning that arrives much later.

## Episode 13: Embeddings and Representation Learning
This is the episode where vectors stop being lists of numbers and start being meanings with directions and distances, which is the mental shift that makes everything from attention to CLIP to retrieval feel inevitable rather than magical.

- **Goal.** Understand vectors as meaning, the single idea underneath everything modern.
- **Concepts to master.** word2vec and its skip-gram training with negative sampling; the embedding space as a learned geometry where nearness encodes similarity; cosine similarity as the natural measure of closeness between meanings; the famous analogy arithmetic where vector operations correspond to semantic relationships; contrastive learning as the broader principle of pulling related things together and pushing unrelated things apart; and CLIP as the model that places images and text into a single shared space, which is exactly the mechanism that will later let a text prompt steer an image.
- **What to read.** Mikolov and colleagues, Efficient Estimation of Word Representations in Vector Space, 2013, and the companion paper on distributed representations of words and phrases. Radford and colleagues on CLIP, 2021.
- **The visual [SHADER].** Embeddings projected to three dimensions and rendered as a rotatable point cloud where semantically related words visibly cluster, with cosine similarity drawn as a field of brightness around a selected word, and the canonical king minus man plus woman analogy animated as actual vectors being added and subtracted in the space.
- **The build.** Train word2vec on a small corpus, then explore the resulting space by querying nearest neighbors and testing analogies, so the geometry is something the viewer can poke at.
- **Teaching note.** Make the forward links explicit. Tell the audience that this same geometry is the shared space that lets a prompt steer an image in the diffusion module, and the search space that powers retrieval in the applied module, so the investment here is banked twice.
- **Video hook.** "Meaning becomes geometry. Once words are directions in space, attention and CLIP and retrieval all stop being mysterious."

---

# Module E: Transformers and LLMs (Episodes 14 to 20, roughly 16 to 19 weeks)

The heart of the modern field. The generic transformer build is kept tight and honest as a bridge, and the differentiated weight is placed on the distributed-training episode, which is squarely a systems problem, the modern-architecture episode, the generation episode, and above all the interpretability episode, which is the most distinctive thing the whole series can offer.

## Episode 14: Attention and the Transformer From Scratch
The hinge of everything modern, and the episode where the magic is meant to evaporate. Once a transformer block has been written by hand and its attention matrix watched lighting up, the rest of the LLM world becomes engineering rather than mystery.

- **Goal.** Build a transformer block from scratch and dissolve the mystique, treating this as a bridge rather than the centerpiece.
- **Concepts to master.** Self-attention as each token deciding how much to attend to every other token; the query, key, and value roles and the lookup metaphor that unifies them; scaled dot-product attention and why the scaling matters for stable gradients; multi-head attention as several attention operations running in parallel subspaces; the position-wise feedforward block; the placement of residual connections and normalization; and causal masking as the mechanism that stops a token from peeking at its own future during language modeling.
- **What to read.** Vaswani and colleagues, Attention Is All You Need, 2017, read closely. Jay Alammar's The Illustrated Transformer for the canonical visuals. Karpathy's Let's build GPT for the from-scratch build.
- **The visual [SHADER].** The attention matrix rendered as a heatmap reading the real weights from your own model, token across one axis and token across the other, with the ability to step through query tokens one at a time and watch which keys light up for each, which is the single clearest explanation of attention that exists.
- **The build.** A complete transformer block from scratch, assembled into a tiny character-level GPT that learns to predict the next token.
- **Teaching note.** Resist the urge to make this the showpiece. Karpathy owns this ground. Build it cleanly, get the audience to the working model quickly, and spend the saved energy on the modern and interpretability episodes that follow.
- **Video hook.** "Attention is a soft lookup table built out of dot products. Here is exactly what each token is looking at."

## Episode 15: Tokenization and the Data Problem
A model never sees text, it sees tokens, and the way text is chopped into tokens quietly shapes what the model can and cannot represent. This episode also makes the unglamorous point that pretraining is overwhelmingly a data problem rather than an architecture problem.

- **Goal.** Respect tokenization as load-bearing and pretraining as mostly data work.
- **Concepts to master.** Byte pair encoding as an algorithm that repeatedly merges the most frequent adjacent pair into a new token; the tradeoffs in vocabulary size between sequence length and embedding-table size; special tokens and their roles; dataset construction and the dataloader; deduplication and cleaning as the work that quietly determines model quality; and the broad principle that data quality tends to dominate architectural cleverness at scale.
- **What to read.** Sennrich, Haddow, and Birch on subword units, 2015, the origin of byte pair encoding for language models. Karpathy's Let's build the GPT Tokenizer.
- **The visual [CODE].** The byte pair encoding merge loop animated step by step, with the most frequent pair in the corpus highlighted and then fused into a single new token, the vocabulary growing entry by entry. This content is symbolic and algorithmic, so it is honestly a code trace and not a shader, and that choice is itself a teaching moment about matching medium to content.
- **The build.** A byte pair encoding tokenizer trained from scratch on a corpus, plus a dataloader that feeds batches to the model.
- **Teaching note.** Show how a rare or made-up word shatters into many tokens while a common word stays whole, and connect that directly to why models sometimes stumble on unusual spellings and numbers.
- **Video hook.** "Models do not see text. They see this. And how the text gets chopped up decides what the model can even think about."

## Episode 16: Pretraining a GPT and Scaling Laws
Training a real, if small, language model end to end, and then confronting the empirical laws that predict capability from scale before a single step of training is run. This is where the abstract becomes a model that actually generates.

- **Goal.** Train a real small language model and understand the scaling rules that govern the field.
- **Concepts to master.** Next-token prediction as the simple objective behind all of it; the full pretraining loop at small scale; scaling laws as the empirical relationships tying loss to parameters, data, and compute; and the compute-optimal frontier that says how to spend a fixed compute budget between making the model bigger and feeding it more data.
- **What to read.** The GPT-2 and GPT-3 papers from Radford and Brown and colleagues for the trajectory. Kaplan and colleagues on scaling laws, 2020. Hoffmann and colleagues, the Chinchilla paper, 2022, for the compute-optimal correction.
- **The visual [PLOT].** Loss plotted against compute on logarithmic axes, with the straight-line scaling relationship emerging as training data accumulates and the Chinchilla compute-optimal point marked. This is fundamentally data, so it is presented honestly as a plot rather than dressed as a shader.
- **The build.** Train a nanoGPT-scale model end to end on a real corpus, logging the genuine loss curve into the visual.
- **Teaching note.** The striking idea to sell here is predictability. A law that forecasts how capable a model will be before it is trained is deeply counterintuitive to most people, and leaning into that surprise makes the episode memorable.
- **Video hook.** "There is a law that predicts how capable a model will become before you train it. Here it is, drawing itself."

## Episode 17: Distributed and Large-Scale Training
The nanoGPT from Episode 16 fits on a single device, and almost nothing real does. This episode covers the entire apparatus that lets a model be trained across many GPUs, which is the most glaring omission in most from-scratch courses and the second place, after the GPU compute episode, where a systems background is a decisive advantage rather than a nice-to-have.

- **Goal.** Understand how a model too large for one device is actually trained across many.
- **Concepts to master.** The memory budget of a training step and the surprising fact that the optimizer states, not the parameters, usually dominate it; data parallelism as replicating the model and splitting the batch; tensor parallelism as splitting individual layers across devices; pipeline parallelism as splitting the network into stages; the ZeRO family and fully sharded data parallelism as ways to shard parameters, gradients, and optimizer states so no device holds the whole model; mixed-precision training in bf16 and fp8 with loss scaling; gradient accumulation as a way to reach a large effective batch on limited memory; gradient checkpointing as trading recomputation for memory; and the collective communication primitives such as all-reduce, with the recognition that interconnect bandwidth, not raw compute, is often the real bottleneck.
- **What to read.** Rajbhandari and colleagues, ZeRO, 2020. Shoeybi and colleagues, Megatron-LM, 2019, for tensor and pipeline parallelism. Huang and colleagues, GPipe, 2018, for pipeline parallelism. Micikevicius and colleagues, Mixed Precision Training, 2017. Zhao and colleagues, PyTorch FSDP, 2023.
- **The visual [SHADER] and [PLOT].** The shader renders the memory budget of a single training step as stacked, colored regions for parameters, gradients, optimizer states, and activations, then shows each region being sharded across a row of devices so the viewer sees exactly what each parallelism strategy splits and what it leaves replicated, with the all-reduce communication drawn as flows between devices. The plot shows memory per device falling as the number of GPUs rises under the different sharding strategies, making the scaling tradeoffs concrete.
- **The build.** Take the Episode 16 model and run it under data parallelism and then fully sharded data parallelism across whatever devices are available, measuring peak memory with and without mixed precision and gradient checkpointing so the savings are real numbers rather than claims.
- **Teaching note.** Lead with the memory budget, because the single most clarifying fact for most people is that Adam's two moments per parameter mean the optimizer states alone can outweigh the model itself, which is why sharding them is the first move. This is the systems-credential episode, so show genuine measurements.
- **Video hook.** "Your nanoGPT fits on one GPU. Real models do not even come close. Here is the machinery nobody shows you."

## Episode 18: Modern LLM Architecture
The transformer from Episode 14 is a 2017 design, and the models that actually ship in 2026 have moved on in specific ways. This episode closes that gap so the series teaches the present rather than the history, and it contains a visual that a graphics audience will find almost unfairly intuitive.

- **Goal.** Close the gap between the original transformer and what is actually deployed today.
- **Concepts to master.** Rotary position embeddings, which encode position by rotating the query and key vectors rather than adding a positional signal; RMSNorm as a simpler and cheaper normalization that has largely displaced LayerNorm in large models; SwiGLU and the family of gated linear unit variants in the feedforward block; grouped-query attention as a way to shrink the memory cost of the key-value cache; the mixture-of-experts pattern that routes each token to a small subset of specialized subnetworks; a look at state space models and Mamba as the leading non-attention alternative for sequence modeling; and a look at how an image enters a language model through a vision-language projection, which is the half of the multimodal story the CLIP episode did not cover.
- **What to read.** Su and colleagues, RoFormer, 2021, for rotary embeddings. Zhang and Sennrich on RMSNorm, 2019. Shazeer on gated linear unit variants, 2020. Ainslie and colleagues on grouped-query attention, 2023. Shazeer and colleagues on the sparsely-gated mixture-of-experts layer, 2017. Gu and Dao, Mamba, 2023, for state space models. Liu and colleagues, LLaVA, 2023, for the vision-language path.
- **The visual [SHADER].** Rotary embeddings shown as exactly what they are, vectors rotating by angles that depend on position and dimension, with each dimension pair rotating at its own frequency, presented side by side with the original sinusoidal positional encoding for contrast. For an audience fluent in rotation matrices this is the most natural visual in the series.
- **The build.** Swap the positional encoding in the Episode 16 model for rotary embeddings and replace LayerNorm with RMSNorm, then measure the effect on training.
- **Teaching note.** This is a second place where the graphics background is a genuine credential. Rotary embeddings are a rotation, and you understand rotations more deeply than most machine learning researchers, so teach them from that strength.
- **Video hook.** "The original transformer is a museum piece. Rotary embeddings encode position as rotation, which you happen to read better than most machine learning researchers."

## Episode 19: Generation, Decoding, and LLM Evaluation
A trained language model is only half of what produces text, because the decoding strategy that turns probabilities into words has an enormous effect on quality. This episode covers that missing half and then teaches how a language model is measured at all.

- **Goal.** Control the quality of generated output and learn to measure a language model.
- **Concepts to master.** Greedy decoding and why it produces dull, repetitive text; sampling with temperature as a way to trade off coherence against diversity; top-k and top-p, or nucleus, sampling as ways to truncate the unlikely tail of the distribution; repetition penalties; the broad truth that much of perceived model quality lives in decoding rather than weights; and then evaluation, with perplexity as the intrinsic measure and a survey of how external benchmarks attempt to measure capability.
- **What to read.** Holtzman and colleagues, The Curious Case of Neural Text Degeneration, 2019, which introduced nucleus sampling. The lm-evaluation-harness and HELM as references for how benchmarking is actually done.
- **The visual [SHADER] and [PLOT].** The shader renders the next-token probability distribution read live from the real model's logits, and reshapes it as the temperature slider moves, sharpening toward a single spike at low temperature and flattening toward uniform at high temperature, while top-p visibly clips the tail. The plot tracks perplexity over training as the intrinsic quality measure.
- **The build.** Implement temperature, top-k, and top-p sampling on the Episode 16 model, then compute perplexity on held-out text.
- **Teaching note.** Demonstrate the same prompt producing wildly different outputs under different settings, with identical weights, to drive home that decoding is a first-class lever and not an afterthought.
- **Video hook.** "Same model, same prompt, completely different output. The weights are only half the story. This is the other half."

## Episode 20: Mechanistic Interpretability
This is the most differentiated episode the series can offer. Interpretability is intensely visual, it is barely taught visually anywhere, and it plays directly to a strength in rendering and spatial thinking. It is also the satisfying payoff of having built the model by hand, because now the audience gets to open it up and look inside.

- **Goal.** Look inside the model that was built and find real, legible structure in it.
- **Concepts to master.** Attention pattern analysis as reading what heads actually do; induction heads as a concrete, discoverable circuit that implements copying and underpins in-context learning; the residual stream as the shared communication channel running through the network; features and the problem of superposition, where a network packs more concepts than it has neurons; sparse autoencoders as a technique for pulling those overlapping features apart into interpretable units; and the circuits perspective that treats a network as composed of discoverable algorithms.
- **What to read.** Olah and colleagues, Zoom In, an Introduction to Circuits, 2020. Elhage and colleagues, A Mathematical Framework for Transformer Circuits, 2021. Olsson and colleagues, In-context Learning and Induction Heads, 2022. Bricken and colleagues, Towards Monosemanticity, 2023, on sparse autoencoders.
- **The visual [SHADER].** Real attention patterns pulled from your own trained model and rendered as heatmaps, with the distinctive diagonal-shifted pattern of an induction head highlighted, and the magnitude of activations across the residual stream shown as a live field. Every value here is read from the actual model, which is what makes it interpretability rather than illustration.
- **The build.** Locate an induction head inside your small GPT and visualize its behavior, then train a tiny sparse autoencoder on a layer's activations and inspect the features it recovers.
- **Teaching note.** This episode should be positioned as the emotional climax of the LLM core. The framing of building a mind and then opening it to watch a single head learn to copy is rare in educational content and worth all the production effort it takes.
- **Video hook.** "We built this model from nothing. Now let me open the skull and show you a single attention head learning to copy."

---

# Module F: Reinforcement Learning (Episodes 21 to 22, roughly 5 to 6 weeks)

Reinforcement learning is placed here, ahead of alignment, so that the reinforcement learning from human feedback episode is not forced to hand-wave the very algorithm it depends on. The narrative arc across these modules is build the model, understand the model, then learn the tool needed to align and to reason.

## Episode 21: RL Foundations
A clean introduction to decision-making under reward, and an episode with one of the most beautiful natural shaders in the whole series, because a value function over a gridworld is a scalar field and a policy is a vector field, which are exactly the primitives already built.

- **Goal.** Understand decision-making under reward from the ground up.
- **Concepts to master.** The Markov decision process as the formal setting of states, actions, and rewards; returns and discounting as the way future reward is valued now; the value function as the expected return from a state; the Bellman equation as the recursive relationship values must satisfy; Q-learning as a method for learning action values without a model of the environment; the exploration versus exploitation dilemma; and a look at the deep Q-network as the bridge from tabular methods to the visual, high-dimensional case.
- **What to read.** Sutton and Barto, Reinforcement Learning, an Introduction, chapters 3 through 6, the standard text. David Silver's reinforcement learning course, lectures 1 through 4. Mnih and colleagues, Playing Atari with Deep Reinforcement Learning, 2013.
- **The visual [SHADER].** A gridworld with each cell colored by its learned value, read from the real Q-table, so that as training proceeds the value of the goal visibly propagates outward across the grid like a spreading tide, with the greedy policy drawn on top as an arrow in each cell pointing the way the agent would go.
- **The build.** Tabular Q-learning on a gridworld, with the live value table and policy driving the heatmap and the arrows.
- **Teaching note.** The propagation of value outward from the reward is mesmerizing and explanatory at once. Let it play out slowly, because watching reward flow backward through space is the intuition the whole field is built on.
- **Video hook.** "Reward flows backward through space until every square knows the way home. Watch it spread."

## Episode 22: Policy Gradients to PPO
This episode reaches the algorithm that powers both robotics and the alignment of language models, which makes it the direct setup for the alignment and reasoning episodes that follow.

- **Goal.** Reach proximal policy optimization, the workhorse behind control, alignment, and reasoning.
- **Concepts to master.** Policy gradients as directly optimizing the policy rather than a value function; the REINFORCE estimator and its high variance; baselines and the advantage function as variance-reduction tools; actor-critic methods that learn a policy and a value estimate together; generalized advantage estimation as the standard way to balance bias and variance in the advantage; and proximal policy optimization with its clipped objective that prevents destructively large policy updates.
- **What to read.** Sutton and Barto, chapter 13. Schulman and colleagues, Proximal Policy Optimization Algorithms, 2017. Schulman and colleagues, High-Dimensional Continuous Control Using Generalized Advantage Estimation, 2015. OpenAI's Spinning Up, the proximal policy optimization section.
- **The visual [SHADER] and [PLOT].** The shader shows the policy's probability distribution over actions shifting as the real advantage estimates update, with the proximal policy optimization clip drawn as a clamped region that visibly prevents the update from stepping too far. The plot tracks reward per episode so the learning curve is grounded.
- **The build.** A policy gradient agent on a simple control task, then a minimal proximal policy optimization implementation.
- **Teaching note.** End by stating plainly that this exact algorithm is what aligns the assistant models people talk to, and is also the basis for training reasoning, and that the next module points it at a language model. That forward pointer is what makes the reinforcement learning detour feel motivated rather than tangential.
- **Video hook.** "This is the algorithm that aligned the model you talk to. Next module, we point it straight at a language model."

---

# Module G: LLM Alignment, Reasoning, and Systems (Episodes 23 to 27, roughly 11 to 14 weeks)

With reinforcement learning in hand, the alignment stack and the reasoning paradigm can be taught honestly, the systems episode finally places FlashAttention where it belongs, and the closing applied episode connects the model to the world.

## Episode 23: Post-Training, Fine-Tuning, and LoRA
Turning a raw base model into something that follows instructions, and doing it cheaply, is the practical heart of how usable models are made today. This episode also contains a clean matrix visual that rewards a linear-algebra audience.

- **Goal.** Turn a base model into one that follows instructions, without retraining the whole thing.
- **Concepts to master.** Supervised fine-tuning on curated instruction data as the first post-training step; the problem of catastrophic forgetting when fine-tuning naively; parameter-efficient fine-tuning as the family of techniques that update only a small part of the model; LoRA specifically, which represents the weight update as the product of two thin low-rank matrices; the low-rank intuition for why this captures most of the useful adaptation at a fraction of the cost; and quantized LoRA as the memory-saving extension that makes fine-tuning large models possible on modest hardware.
- **What to read.** Ouyang and colleagues, the InstructGPT paper, 2022, for the supervised fine-tuning stage. Hu and colleagues, LoRA, 2021. Dettmers and colleagues, QLoRA, 2023.
- **The visual [SHADER].** A weight matrix shown receiving a full-rank update in one panel and a low-rank LoRA update in another, where the two thin matrices multiply to reconstruct an approximation of the full update, so the viewer sees how a small number of parameters can stand in for a large change. This is a matrix-transform visual and a natural fit for the heatmap primitive.
- **The build.** Fine-tune the small model with a from-scratch LoRA implementation, observing how few parameters are actually being trained.
- **Teaching note.** Connect the low-rank idea back to rank from Episode 1. The reason LoRA works is that the useful part of a weight update tends to be low-rank, and that lands far harder for an audience that already understands rank geometrically.
- **Video hook.** "You do not retrain the whole brain. You bolt on two tiny matrices. Here is why that works, geometrically."

## Episode 24: Reward Modeling, RLHF, and DPO
Alignment as optimization against human preference, taught properly now that proximal policy optimization is already understood from Episode 22. This is where the reinforcement learning module first pays off.

- **Goal.** Understand alignment as optimization against preferences, with the underlying algorithm already in hand.
- **Concepts to master.** Reward modeling as learning a scalar reward from human comparisons between outputs; the full reinforcement learning from human feedback loop that uses the reward model and proximal policy optimization to fine-tune the policy; direct preference optimization as a more recent and simpler alternative that optimizes against preferences directly without a separate reward model or reinforcement learning loop; and reward hacking as the failure mode where a policy exploits flaws in the reward model rather than genuinely improving.
- **What to read.** Christiano and colleagues, Deep Reinforcement Learning from Human Preferences, 2017. Ouyang and colleagues, the full InstructGPT paper, 2022. Rafailov and colleagues, Direct Preference Optimization, 2023.
- **The visual [SHADER] and [PLOT].** The shader shows preference pairs assembling into a learned reward landscape and the policy climbing that landscape, driven by real values from a toy setup so the dynamics are genuine. The plot tracks reward-model accuracy and the policy's divergence from its starting point, which is the quantity that has to be kept in check to avoid drifting into nonsense.
- **The build.** Train a tiny reward model on toy preference pairs, implement direct preference optimization, and connect the pieces back to the proximal policy optimization loop from Episode 22.
- **Teaching note.** The framing that resonates is that good is not defined, it is demonstrated. The model is never told what a good answer is, only shown pairs and left to infer the direction, and that indirectness is the conceptual core worth dwelling on.
- **Video hook.** "How do you teach a model what good means? You do not define it. You show it pairs and let it climb."

## Episode 25: Reasoning and Test-Time Compute
This is the development that defines the frontier since 2023, and the matching modernity fix on the training side to the modern-architecture and flow-matching episodes. The reinforcement learning module set it up perfectly, so this is where reward optimization meets reasoning.

- **Goal.** Understand how a model is made to reason by spending compute at inference and by training against verifiable rewards.
- **Concepts to master.** Chain-of-thought as the precursor idea that letting a model write out intermediate steps improves its answers; test-time compute scaling, the empirical finding that more thinking tokens or more sampled attempts buy more capability without changing the weights; reinforcement learning with verifiable rewards, where correctness on math or code is checked programmatically rather than judged by a learned reward model, removing the human-preference bottleneck for any domain with a checkable answer; group relative policy optimization as the reinforcement learning algorithm used in this setting; the train-time versus test-time compute tradeoff; and process reward models that score the reasoning steps rather than only the final outcome.
- **What to read.** Wei and colleagues, Chain-of-Thought Prompting Elicits Reasoning in Large Language Models, 2022. Lightman and colleagues, Let's Verify Step by Step, 2023, on process reward models. Shao and colleagues, DeepSeekMath, 2024, which introduced group relative policy optimization. The DeepSeek-R1 paper, 2025. Snell and colleagues, Scaling LLM Test-Time Compute Optimally, 2024.
- **The visual [PLOT] and [SHADER].** The plot shows accuracy rising as a function of test-time compute, whether measured in reasoning tokens or in the number of sampled attempts, which makes the buy-capability-with-thinking idea concrete. The shader shows a search over reasoning paths with verifiable rewards pruning the wrong branches, or equivalently the policy distribution under group relative policy optimization shifting toward correct reasoning traces, driven by real values on a toy task with checkable answers.
- **The build.** Take the small aligned model, define a tiny task with programmatically checkable answers such as arithmetic, and run a minimal group relative policy optimization loop that rewards a correct final answer, then show accuracy improving and the chains of thought lengthening as the model learns to think before answering.
- **Teaching note.** The conceptual leap to dwell on is that the reward can be a program. For any domain where correctness can be checked, the human-preference bottleneck disappears, which is why reasoning models advanced first in math and code. Frame the train-time versus test-time compute tradeoff clearly, because it is the new axis the field optimizes along.
- **Video hook.** "The model gets smarter by thinking longer. Here is how reasoning is trained, with a reward that is just a correctness check."

## Episode 26: Inference and Systems
Making a trained model fast and cheap to run is the production reality that a tooling background is built for, and it is finally the right moment for FlashAttention, because the audience now understands the attention it accelerates.

- **Goal.** Make a model fast and cheap to serve, with FlashAttention landing where it makes sense.
- **Concepts to master.** The key-value cache as the central trick that makes autoregressive generation efficient by reusing past computation; quantization to eight and four bits and the methods like GPTQ that preserve quality while shrinking the model; knowledge distillation as the standard way a small, cheap, deployable model is trained to imitate a large one; speculative decoding as a way to generate several tokens per expensive step using a small draft model and a verifier; batching and the tension between latency and throughput; and FlashAttention as the IO-aware reformulation of attention that tiles the computation and maintains a running softmax to avoid ever materializing the full attention matrix in slow memory.
- **What to read.** Dao and colleagues, FlashAttention, 2022. Frantar and colleagues, GPTQ, 2022. Dettmers and colleagues, the eight-bit matrix multiplication paper, 2022. Hinton and colleagues, Distilling the Knowledge in a Neural Network, 2015. Leviathan and colleagues, Fast Inference from Transformers via Speculative Decoding, 2022.
- **The visual [SHADER].** The key-value cache shown growing and being reused token by token during generation, speculative decoding shown drafting a run of tokens with the verifier accepting or rejecting them, and the FlashAttention block pattern shown with its running softmax maximum and sum updating per tile, which is now meaningful because the attention it optimizes is fully understood. This is also the natural callback to the GEMM tiling shader from Episode 5.
- **The build.** Add a key-value cache to your model and measure the generation speedup, then implement eight-bit quantization and measure the memory saving.
- **Teaching note.** This is the third episode where the profiling background is a direct credential, and the place to show real measurement rather than asserted speedups, because the audience trusts numbers from someone who clearly measures for a living.
- **Video hook.** "The model is trained. Now make it cheap. This is the part your tooling instincts will eat alive."

## Episode 27: Retrieval and Agents
A model's knowledge is frozen at training time and it cannot act in the world on its own, and this closing applied episode covers the two techniques that fix both, connecting the whole language-model track back to the embedding geometry from Episode 13. This is how models are actually deployed in 2026.

- **Goal.** Connect a frozen model to fresh knowledge and to real actions.
- **Concepts to master.** Retrieval-augmented generation as injecting relevant retrieved text into the context at inference so the model can answer from knowledge it never memorized; the embedding and vector-search machinery underneath it, including chunking, approximate nearest-neighbor indexes such as HNSW, and the direct reuse of the cosine-similarity geometry from the embeddings episode; tool use and function calling as the model emitting a structured call that the surrounding runtime executes; agents as multi-step loops of plan, act, and observe; the ReAct pattern that interleaves reasoning and acting; and the practical problem of managing a limited context window across many steps.
- **What to read.** Lewis and colleagues, Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks, 2020. Malkov and Yashunin, the HNSW paper, 2018, for the index. Yao and colleagues, ReAct, 2022. Schick and colleagues, Toolformer, 2023.
- **The visual [SHADER] and [CODE].** The shader reuses the embedding point cloud from Episode 13, dropping a query vector into the cloud of document vectors and lighting up the nearest neighbors by cosine proximity, driven by real embeddings, so retrieval is seen as a geometric lookup. The code traces an agent loop over a few steps, the model emitting a tool call, the runtime executing it, and the observation feeding back into the next step.
- **The build.** Build a minimal retrieval-augmented system over a small document set using your own embeddings from Episode 13 and a brute-force nearest-neighbor search, then a tiny agent loop with one or two tools the model can call.
- **Teaching note.** The unifying insight is that the weights stay frozen while capability still grows, retrieval adding knowledge at inference and tools adding actions, so the model reaches the world without any retraining. Anchor retrieval explicitly in the cosine geometry the audience already saw in Episode 13.
- **Video hook.** "The model's knowledge is frozen at training. Retrieval and tools are how it reaches the world. Let me wire it up."

---

# Module H: Generative Models and Diffusion (Episodes 28 to 33, roughly 14 to 18 weeks)

The visual high point of the series and the part where a rendering background is the strongest possible advantage, because diffusion is almost entirely about fields, noise, and trajectories. The track is carried all the way to the 2026 frontier so that it matches the modernity of the language-model track rather than stopping at 2022.

## Episode 28: Autoencoders and VAEs
The latent-space idea that latent diffusion stands on, built before the diffusion itself so that the compressed space is already familiar by the time Stable Diffusion is assembled.

- **Goal.** Build the latent-space idea that all of modern image generation depends on.
- **Concepts to master.** The autoencoder as a network that compresses input to a bottleneck and reconstructs it; the variational autoencoder as the probabilistic version that learns a smooth, sampleable latent distribution; the reparameterization trick that makes sampling differentiable so the network can be trained end to end; the latent space as a compressed, navigable representation of the data; and the KL term in the loss, which is the same divergence introduced back in Episode 3, now doing the job of keeping the latent space well-behaved.
- **What to read.** Kingma and Welling, Auto-Encoding Variational Bayes, 2013. Lilian Weng's survey From Autoencoder to Beta-VAE.
- **The visual [SHADER].** A navigable two-dimensional latent space with a cursor the viewer can move through it, the decoded output morphing continuously as the cursor moves, so the abstract notion of a latent space becomes a place you can wander. The reparameterization trick is shown as sampling a noise vector and then shifting and scaling it by the network's predicted mean and variance.
- **The build.** A variational autoencoder trained on MNIST from scratch, with the latent-space walk driving the shader.
- **Teaching note.** Make the explicit promise that Stable Diffusion does not operate on pixels but inside exactly this kind of compressed space, so this episode is laying a foundation that pays off two episodes later.
- **Video hook.** "Stable Diffusion does not work on pixels. It works in this compressed space. Let me build it and walk through it."

## Episode 29: GANs (Optional Flex Episode)
Included for the conceptual lineage and the adversarial idea, and explicitly designated as the episode to cut if the schedule slips, because nothing downstream depends on it.

- **Goal.** Understand the adversarial idea and its place in the generative-model lineage.
- **Concepts to master.** The generator and discriminator as two networks locked in a minimax game; the training dynamics in which each improves against the other; mode collapse as the characteristic failure where the generator produces only a narrow slice of the data; the general instability of adversarial training; and the places the adversarial idea persists today, including perceptual losses and the decoders used in latent diffusion.
- **What to read.** Goodfellow and colleagues, Generative Adversarial Networks, 2014. Radford and colleagues, the deep convolutional GAN paper, 2015.
- **The visual [SHADER].** The generator's output distribution and the discriminator's decision boundary shown chasing each other across a two-dimensional space, with mode collapse rendered as the generated distribution visibly shrinking and collapsing onto a single point.
- **The build.** A small generative adversarial network trained on a two-dimensional toy distribution where the dynamics are easy to watch.
- **Teaching note.** Keep this one lighter and shorter by design, since it is the flex episode. If time is tight, it can be folded into a brief segment of the autoencoder episode instead of a standalone piece.
- **Video hook.** "Two networks fighting. One forges, one detects. Watch them reach a standoff, then watch it collapse."

## Episode 30: Diffusion I, DDPM
The core of diffusion, and the episode where the rendering background pays off most directly, because the forward process is almost literally a noise shader the audience could have written years ago.

- **Goal.** Build the core denoising diffusion model, the part that is already close to a shader.
- **Concepts to master.** The forward process that gradually adds Gaussian noise to an image until it becomes pure static; the reverse process that a network learns to run, removing noise step by step; the noise schedule, the beta and cumulative alpha values that control how much noise is added at each timestep; the training objective, which reduces to predicting the noise that was added; and the U-Net backbone that does the denoising, built from the convolutions and transposed convolutions of Episode 11.
- **What to read.** Ho and colleagues, Denoising Diffusion Probabilistic Models, 2020. Sohl-Dickstein and colleagues, the 2015 nonequilibrium thermodynamics paper that originated the idea. Lilian Weng's What Are Diffusion Models. The Annotated Diffusion Model from Hugging Face for the from-scratch code.
- **The visual [SHADER].** The forward process shown live, with scheduled Gaussian noise added to a texture across timesteps and a slider that scrubs from a clean image all the way to pure static and back, the noise schedule matched exactly to the one the model is trained on so the visual and the math are provably the same thing. This single scene explains diffusion more clearly than any equation.
- **The build.** A small denoising diffusion model trained on MNIST from scratch with a compact U-Net.
- **Teaching note.** Open by writing the forward noising as a shader the audience already knows how to write, then reveal that the entire difficulty of diffusion is teaching a network to run that familiar process in reverse.
- **Video hook.** "Diffusion is just noise, added and then removed. The hard part is teaching a network to run it backward."

## Episode 31: Diffusion II, The Score Field and Samplers
The deepest and most beautiful understanding of diffusion, and the episode that contains the signature visual of the entire series, because the score function is a vector field pointing toward the data and that is precisely the primitive built in Part 0.

- **Goal.** Reach the score-based view, the deepest and most visual way to understand diffusion.
- **Concepts to master.** The score function as the gradient of the log probability density, a vector at every point that says which way is more likely; score matching as the way to learn it; the stochastic differential equation formulation that unifies the discrete steps into a continuous process; the equivalence between the denoising diffusion view and the score-based view; and the family of samplers, from the original stochastic sampler to the faster deterministic DDIM, and the tradeoff between number of steps and sample quality.
- **What to read.** Song and Ermon, Generative Modeling by Estimating Gradients of the Data Distribution, 2019. Song and colleagues, Score-Based Generative Modeling through Stochastic Differential Equations, 2020. Song and colleagues, Denoising Diffusion Implicit Models, 2020.
- **The visual [SHADER].** The score rendered as a vector field over a two-dimensional space, every arrow pointing toward higher data density, with a sample released into the field and shown following the arrows uphill toward a data cluster, and several sampler trajectories overlaid so the difference between stochastic and deterministic paths is visible. This is the most striking visual in the series and the clearest argument for why the rendering angle is the right one.
- **The build.** Implement DDIM sampling on the Episode 30 model and compare the number of steps needed against the original sampler at matched quality.
- **Teaching note.** This is the conceptual summit of the diffusion track. The line that the model learns a force field pointing toward real images, and that sampling is just letting a point fall along it, is the sentence the whole episode is built to earn.
- **Video hook.** "The model learns a force field that points toward real images. Sampling is just letting a point fall along it."

## Episode 32: Diffusion III, Conditioning and Latent Diffusion
The full Stable Diffusion picture, assembled from parts the series has already built, plus the question of how generated images are evaluated at all.

- **Goal.** Assemble the complete latent-diffusion system from existing parts, and learn to evaluate generated images.
- **Concepts to master.** Conditioning as the mechanism that lets an external signal steer generation; cross-attention as the specific way text conditions the image, reusing the attention of Episode 14; classifier-free guidance and the guidance scale that trades prompt adherence against diversity; CLIP as the text encoder, reusing the shared space of Episode 13; latent diffusion as running the whole process inside the compressed space of the variational autoencoder from Episode 28; and the evaluation metrics, the Frechet Inception Distance and the Inception Score, that attempt to quantify generated image quality.
- **What to read.** Rombach and colleagues, High-Resolution Image Synthesis with Latent Diffusion Models, 2022. Ho and Salimans, Classifier-Free Diffusion Guidance, 2022. Ronneberger and colleagues, the U-Net paper, 2015. Heusel and colleagues on the Frechet Inception Distance, 2017. Salimans and colleagues on the Inception Score, 2016.
- **The visual [SHADER] and [PLOT].** The shader shows classifier-free guidance as an extrapolation along the conditioning direction within the score field from the previous episode, with a guidance-scale slider that visibly pulls the sample harder toward the prompt and, pushed too far, shows the artifacts of over-guidance. The plot tracks the Frechet Inception Distance falling as sample quality improves.
- **The build.** Add text conditioning and classifier-free guidance to the diffusion model, then compute the Frechet Inception Distance to put a number on quality.
- **Teaching note.** This is the synthesis episode, so make the callbacks explicit and celebratory. Every component being assembled here, the latent space, the score field, the CLIP text encoder, the cross-attention, was built earlier in the series, and naming that is what makes Stable Diffusion feel earned rather than handed down.
- **Video hook.** "Now we connect every piece, the latent space, the score field, the CLIP text, and the cross-attention. This is Stable Diffusion, built from parts you already made."

## Episode 33: Diffusion IV, Flow Matching and Diffusion Transformers
The episode that carries the diffusion track to the 2026 frontier, matching the modernity given to the language-model track and ending the series on what is current rather than what is historical.

- **Goal.** Bring the diffusion track up to the current frontier of image and video generation.
- **Concepts to master.** Why the field moved beyond the wandering, curved trajectory of the original diffusion process; flow matching and rectified flow as approaches that learn a near-straight transport from noise to data, allowing far fewer sampling steps; the diffusion transformer, which replaces the U-Net backbone with a transformer and scales better, now powering state-of-the-art image and video models; and how the most recent systems combine rectified flow with a transformer backbone.
- **What to read.** Lipman and colleagues, Flow Matching for Generative Modeling, 2022. Liu and colleagues, the rectified flow paper, 2022. Peebles and Xie, Scalable Diffusion Models with Transformers, 2023, for the diffusion transformer. Esser and colleagues, the Stable Diffusion 3 paper on scaling rectified flow transformers, 2024.
- **The visual [SHADER].** The defining contrast of the modern era shown directly, the curved and noisy sampling path of the original diffusion process beside the near-straight transport path of flow matching, both drawn as trajectories over the same field, side by side, which is the clearest possible visual argument for why the field moved on.
- **The build.** Implement a minimal flow-matching trainer and compare its sampling path and the number of steps it needs against the denoising diffusion model from Episode 30.
- **Teaching note.** Ending the series here is deliberate. Closing on the current frontier, with a visual that makes the reason for the shift obvious, leaves the audience standing at the present edge of the field rather than two years behind it.
- **Video hook.** "The original diffusion process takes a wandering path to an image. The frontier learned to walk straight. Here is both, racing."

---

## Timeline

| Module | Episodes | Approximate weeks |
|---|---|---|
| Setup | Part 0 | 1 |
| A: Foundations | 1 to 5 | 10 to 12 |
| B: Classical ML | 6 to 7 | 4 |
| C: Deep Learning | 8 to 12 | 12 to 14 |
| D: Representations | 13 | 2 to 3 |
| E: Transformers and LLMs | 14 to 20 | 16 to 19 |
| F: Reinforcement Learning | 21 to 22 | 5 to 6 |
| G: Alignment, Reasoning, and Systems | 23 to 27 | 11 to 14 |
| H: Diffusion | 28 to 33 | 14 to 18 |

The honest total across thirty-three episodes is roughly sixteen to twenty months at a sustainable cadence. The distributed-training, diffusion, and from-scratch-pretraining episodes are month-long efforts in their own right and are budgeted as such rather than pretended to be two-week pieces.

---

## Production Notes

The series only works if the from-scratch code and the shader are treated as a single artifact that is then narrated three ways, because producing code, a shader, a blog, and a video as four separate efforts on every episode is not survivable alongside a full-time role. Each [SHADER] tag is a standing promise that the visual is driven by real values from your own code rather than a hand-faked animation, and keeping that promise is what gives the channel its credibility with an audience that codes. The right medium is chosen per concept rather than forced, so a continuous field gets a shader, data gets a plot, and a symbolic algorithm gets a code trace, and that discipline is part of what makes the visuals genuinely good. Building a buffer by batch-producing the lighter early foundation episodes before publishing banks weeks against the much heavier back half. Episode 29 on generative adversarial networks is the single designated cut if the schedule comes under pressure. And the four primitives from Part 0 are extended rather than rebuilt across the run, so that by the time the score field appears in Episode 31 it is simply the vector-field primitive aimed at a data distribution, and the early investment compounds all the way to the end.
