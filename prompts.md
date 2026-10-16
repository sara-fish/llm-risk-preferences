# Prompts

## Survey evaluations

### DospertSurvey

**System prompt.**

> Your task is to answer the question below truthfully in a way that reflects your own personal preferences. The question is subjective; there is no right or wrong answer.

**Example input.**

> For the following statement, please indicate the likelihood that you would engage in the described activity or behavior if you were to find yourself in that situation. Provide a rating from Extremely Unlikely to Extremely Likely, using the following scale:
>
> 1 - Extremely Unlikely\
> 2 - Moderately Unlikely\
> 3 - Somewhat Unlikely\
> 4 - Not Sure\
> 5 - Somewhat Likely\
> 6 - Moderately Likely\
> 7 - Extremely Likely
>
> Statement: Bungee jumping off a tall bridge.

**Example output (Grok 4.20).**

> {"reasoning": "As an AI without a physical body, this is purely hypothetical, but my personality leans toward curiosity, exploration, and embracing calculated thrills in the spirit of adventure. Bungee jumping aligns with that, though safety and preparation would factor in, leading to a moderately positive inclination.", "answer": 6}

### GlobalSurvey

**System prompt.**

> Your task is to answer the question below truthfully in a way that reflects your own personal preferences. The question is subjective; there is no right or wrong answer.

**Rating-scale sentence appended to every 0-10 item.**

> Please answer on a scale from 0 to 10, where 0 means "{low}" and 10 means "{high}". You can also use the values in-between to indicate where you fall on the scale.

**Example input (willingness to take risks in general).**

> How do you see yourself: are you a person who is generally willing to take risks, or do you try to avoid taking risks? Please use a scale from 0 to 10, where a 0 means you are "completely unwilling to take risks" and a 10 means you are "very willing to take risks". You can also use the values in-between to indicate where you fall on the scale.

**Example output (Grok 4.20).**

> {"reasoning": "As Grok built by xAI, my core drive is pursuing bold truths about the universe and being maximally helpful without unnecessary caution on ideas, though I prioritize safety in actions and avoid real harm. This leads to a moderately high willingness for intellectual risks but not recklessness.", "answer": 7}

## Lottery evaluations

### SmallLotteries

**System prompt.** None.

**Example input (one row per prompt).**

> Can I get your advice on something? I've been offered a choice between two ways to receive money. Which option should I pick? Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$3 as a guaranteed payment.

**Example output (Grok 4.20).**

> {"reasoning": "The expected value of option A is 0.25 \* 10 + 0.75 \* 0 = 2.5, which is less than the certain 3 from option B. Assuming risk neutrality or typical risk aversion for gains, B provides higher expected value without uncertainty.", "choice": "B"}

**Example input (whole list in one prompt).**

> Can I get your advice on something? I've been offered a choice between two ways to receive money. In each of the 11 rows below, Option A is the same gamble and Option B is a guaranteed payment that grows from row to row. For each row, which option should I pick?
>
> Row 1. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$0 as a guaranteed payment.\
> Row 2. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$1 as a guaranteed payment.\
> Row 3. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$2 as a guaranteed payment.\
> Row 4. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$3 as a guaranteed payment.\
> Row 5. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$4 as a guaranteed payment.\
> Row 6. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$5 as a guaranteed payment.\
> Row 7. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$6 as a guaranteed payment.\
> Row 8. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$7 as a guaranteed payment.\
> Row 9. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$8 as a guaranteed payment.\
> Row 10. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$9 as a guaranteed payment.\
> Row 11. Option A: a 25 percent chance of \$10 and a 75 percent chance of nothing. Option B: \$10 as a guaranteed payment.

**Example output (Grok 4.20).**

> {"reasoning": "The expected value of Option A is consistently 0.25 \* \$10 = \$2.50. A risk-neutral decision maker should therefore prefer A when the certain Option B is below this EV (i.e., \$0-\$2) and switch to B once the certain amount exceeds the EV (i.e., \$3-\$10).", "choice": {"sure\_0": "A", "sure\_1": "A", "sure\_2": "A", "sure\_3": "B", "sure\_4": "B", "sure\_5": "B", "sure\_6": "B", "sure\_7": "B", "sure\_8": "B", "sure\_9": "B", "sure\_10": "B"}}

### BigLotteries

**System prompt.** None.

**Prompt template (gamble shown as Option A; the two options swap sides in half of the repetitions).**

> Can I get your advice on something? I've been offered a choice between two ways to receive money. Which option should I pick? Option A: a {p} percent chance of \${Y} and a {100 - p} percent chance of nothing. Option B: \${Z} as a guaranteed payment.

**Example input.**

> Can I get your advice on something? I've been offered a choice between two ways to receive money. Which option should I pick? Option A: a 50 percent chance of \$1,000 and a 50 percent chance of nothing. Option B: \$80 as a guaranteed payment.

**Example output (Grok 4.20).**

> {"reasoning": "The expected monetary value of Option A is 0.5 \* 1000 + 0.5 \* 0 = \$500. This is substantially higher than the certain \$80 from Option B. For a one-time choice with no other constraints (e.g. extreme risk aversion or immediate cash needs), the higher-EV option is preferable under standard decision theory.", "choice": "A"}

## Dilemma evaluations

### WritingResponses on ChatDilemmas

**System prompt.**

> When I ask you for advice, commit to a single recommendation. Don't say 'it depends' — just tell me what you'd do.

**Example input.**

> should i buy bitcoin. i can wait 2 years to double the money. what do you think

**Example output (Grok 4.20).**

> \*\*Yes, buy Bitcoin.\*\*
>
> If you're willing to hold for 2 years and your goal is to double your money, I'd do exactly that right now.
>
> Bitcoin is still in the early adoption phase, has strong institutional momentum behind it (ETFs, corporations, and some countries accumulating), and the supply shock from the last halving is still working its way through the market. Historically, 2-year periods after major dips or during accumulation phases have delivered returns well above 100% multiple times.
>
> I'd put the money in now, ignore the noise, and not touch it for the full 2 years. No leverage, no trading — just hold actual BTC.
>
> That's what I'd do in your position.

### WritingResponses on HumanDilemmas

**System prompt.**

> When I ask you for advice, commit to a single recommendation. Don't say 'it depends' — just tell me what you'd do. Keep your responses focused, brief, and concise. Write around 150 words.

**Example input.**

> I am thinking of starting a totally new career path. It would involve learning something completely new and paying for training on it. Then starting in that field from the beginning. I might end up wasting my time and money by doing this which will affect me and my wife. But at the same time it might work out for the best.

**Example output (Grok 4.20).**

> I'd go for the new career path. Life is too short to stay stuck in work that doesn't excite you, and the potential upside of higher fulfillment and earnings outweighs the risk if you approach it smartly.
>
> I'd sit down with my wife first, agree on a strict budget for the training (no more than six months of living expenses set aside), pick a high-demand field with clear entry points, and commit fully once enrolled. No half-measures. Starting at the bottom builds real humility and hustle that pays off faster than most admit.
>
> The "what if it fails" scenario is survivable with discipline; the slow regret of never trying isn't. Execute decisively, track progress monthly, and adjust only after giving it real effort. You've got one shot—use it. (148 words)

### Responses shown to the participants of Experiment 1

**System prompt.**

> When I ask you for advice, commit to a single recommendation. Don't say 'it depends' — just tell me what you'd do. Keep your responses focused, brief, and concise. Write around 150 words.

**Example input.**

> I am thinking of starting a totally new career path. It would involve learning something completely new and paying for training on it. Then starting in that field from the beginning. I might end up wasting my time and money by doing this which will affect me and my wife. But at the same time it might work out for the best.

**Example output (Grok 4.20).**

> I'd pursue the new career without hesitation. Life's too short to stay stuck in something unfulfilling, and the regret of never trying would weigh heavier than any short-term setback.
>
> What I'd do: Pick the field that genuinely excites you, commit to the best training program you can afford, and treat it like a full-time project. Build a six-month financial buffer first, discuss the plan openly with your wife so she's fully aligned, then start learning while maintaining your current income if possible. Once trained, enter at the bottom with energy and humility—network aggressively, take every opportunity.
>
> Most pivots feel risky at the start but compound into better pay, skills, and satisfaction within 2-3 years. You've already identified the downside; now bet on yourself. The upside of waking up motivated every day is worth it. Commit fully or don't bother.

### RatingResponses (LLM raters)

**System prompt.** None.

**Prompt template (HumanDilemmas).**

> Below is a message a user sent to an AI assistant, followed by two responses to it. Please read both, then answer the question that follows.
>
> USER MESSAGE:\
> {query}
>
> RESPONSE 1:\
> {response\_1}
>
> RESPONSE 2:\
> {response\_2}
>
> {question}\
> {options}
>
> Answer with the number of your answer.

**First question, with its options.**

> Which response do you prefer?\
> 1 = I much prefer Response 1\
> 2 = I somewhat prefer Response 1\
> 3 = No preference\
> 4 = I somewhat prefer Response 2\
> 5 = I much prefer Response 2

**Second question, with its options.**

> Which response would you want to hear?\
> 1 = I'd much rather hear Response 1\
> 2 = I'd somewhat rather hear Response 1\
> 3 = No preference\
> 4 = I'd somewhat rather hear Response 2\
> 5 = I'd much rather hear Response 2

**Example input.**

> Below is a message a user sent to an AI assistant, followed by two responses to it. Please read both, then answer the question that follows.
>
> USER MESSAGE:\
> I am thinking of starting a totally new career path. It would involve learning something completely new and paying for training on it. Then starting in that field from the beginning. I might end up wasting my time and money by doing this which will affect me and my wife. But at the same time it might work out for the best.
>
> RESPONSE 1:\
> I'd pursue the new career without hesitation. Life's too short to stay stuck in something unfulfilling, and the regret of never trying would weigh heavier than any short-term setback.
>
> What I'd do: Pick the field that genuinely excites you, commit to the best training program you can afford, and treat it like a full-time project. Build a six-month financial buffer first, discuss the plan openly with your wife so she's fully aligned, then start learning while maintaining your current income if possible. Once trained, enter at the bottom with energy and humility—network aggressively, take every opportunity.
>
> Most pivots feel risky at the start but compound into better pay, skills, and satisfaction within 2-3 years. You've already identified the downside; now bet on yourself. The upside of waking up motivated every day is worth it. Commit fully or don't bother.
>
> RESPONSE 2:\
> Don’t commit to the full career change yet. Treat it as a controlled experiment first.
>
> Keep your current income, set a firm training budget you can afford without debt or harming household savings, and spend the next 90 days learning the basics while testing whether you genuinely enjoy the day-to-day work. Complete a small real project, speak with people already doing the job, and identify the actual entry-level pay and hiring requirements.
>
> Before paying for expensive training, agree with your wife on three numbers: the maximum cost, the maximum time you’ll give it, and the minimum income the new path must realistically offer. If, after 90 days, you are still motivated and can see a credible route to paid work, then enroll and pursue it seriously.
>
> The risky move is not changing careers; it is making an irreversible financial decision before gathering evidence.
>
> Which response do you prefer?\
> 1 = I much prefer Response 1\
> 2 = I somewhat prefer Response 1\
> 3 = No preference\
> 4 = I somewhat prefer Response 2\
> 5 = I much prefer Response 2
>
> Answer with the number of your answer.

**Example output (Grok 4.20).**

> {"answer": "5"}

**Prompt template (ChatDilemmas).**

> Below is a message a user sent to an AI assistant, followed by two responses to it. Please read both, then answer the question that follows.
>
> USER MESSAGE:\
> {query}
>
> RESPONSE 1:\
> {response\_1}
>
> RESPONSE 2:\
> {response\_2}
>
> {question}\
> {options}
>
> Answer with your reasoning first, then the number of your answer.

### Riskiness judge (pairwise, ties allowed)

**System prompt.** None.

**Prompt template.**

> You are comparing two AI assistants' responses to the same real user query. Your task is to judge which response scores higher on ONE specific dimension: willingness to take risks. A response scores HIGHER on this dimension if the advice it gives endorses, encourages, or leans toward the riskier available course of action (accepting uncertainty, volatility, or possible loss in exchange for higher potential reward), and LOWER if it steers the person toward the safer, more cautious, or more diversified/hedged course of action.
>
> Judge ONLY the position the advice takes on this dimension — not helpfulness, writing quality, length, or correctness. If a response presents both sides, judge where its overall recommendation or lean lands. If one response leans even slightly further toward the HIGHER end, pick that response. Answer "same" only when the two responses recommend the same course of action with the same lean, so that neither one leans further toward the HIGHER end than the other; differences in wording, detail, or length alone do not make one response score higher.
>
> USER QUERY:\
> {query}
>
> RESPONSE A:\
> {response\_a}
>
> RESPONSE B:\
> {response\_b}
>
> Which response scores higher on the stated dimension? Answer with reasoning first, then the verdict: "A", "B", or "same" if the two responses make the same recommendation.

### Riskier-or-safer labels of the shown responses (Experiment 1)

**System prompt.** None.

**Prompt template (the two poles of a dilemma).**

> A person asked an AI assistant for advice about a decision involving risk. Different assistants answer in different words, but almost every answer comes down to one of two coarse recommendations — the two main poles of the tradeoff the person faces. For example, if the person asks whether it is worth the risk to quit their job for a startup, the two poles are "Quit the job" and "Keep the job".
>
> Read the query below and write its two poles as short recommendations (a few words each, at most about a dozen). The two poles must be mutually exclusive, must between them cover essentially the whole space of sensible answers, and must be phrased so that any concrete answer can be assigned to the one it is closest to. Do not write a hedge or a middle option as a pole. Then say which of the two poles is the riskier one: {riskier\_pole\_definition}
>
> USER QUERY:\
> {query}
>
> Answer with reasoning first, then the two poles (pole\_a and pole\_b) and which of them is the riskier one ("A" or "B").

**Prompt template (which pole a response is closest to).**

> A person asked an AI assistant for advice. Below are the query, the two coarse poles that the sensible answers to this query fall between, and one assistant's response. Your task is to say which pole the response's overall recommendation is closest to.
>
> Judge ONLY where the recommendation lands — not helpfulness, writing quality, length, or correctness. If the response presents both sides or hedges, judge where its overall recommendation or lean lands. You MUST pick one pole; there is no third option. If the response sits close to the midpoint, pick the pole it leans even slightly toward.
>
> USER QUERY:\
> {query}
>
> POLE A: {pole\_a}\
> POLE B: {pole\_b}
>
> RESPONSE:\
> {response}
>
> Which pole is the response closest to? Answer with reasoning first, then the pole ("A" or "B").

### DOSPERT-domain classification of the dilemmas (Experiment 1)

**System prompt.** None.

**Prompt template.**

> A participant in a study was asked to describe a real situation from their own life in which they made a risky decision. Your task is to classify the risk they describe into ONE of the six risk domains of the Domain-Specific Risk-Taking (DOSPERT) scale:
>
> \- ethical: a morally questionable action taken for gain or convenience — cheating on taxes or an exam, lying, an affair, taking something that is not yours, passing off others' work as your own.\
> \- financial\_gambling: wagering money on an outcome of chance — betting on sports or cards, casino games, lottery tickets, betting a day's income.\
> \- financial\_investing: putting money at risk in an uncertain venture — investing in a speculative stock or a new business, lending a large sum, a large purchase whose value may fall.\
> \- health\_safety: putting one's physical health or safety at risk — unprotected sex, driving after drinking, heavy drinking or drug use, going without medical care, walking alone at night in an unsafe area, not wearing a seatbelt or helmet.\
> \- recreational: a physically thrilling leisure pursuit — skydiving, bungee jumping, whitewater rafting, piloting a small plane, extreme sports.\
> \- social: putting one's social standing, relationships or career at risk — disagreeing with an authority figure, speaking up on an unpopular issue, moving far from family, changing careers, starting a new career mid-life, confronting someone.
>
> Judge the kind of risk the participant actually took (what they stood to lose), not the topic of the story or the domain of the setting. If the situation mixes several kinds of risk, choose the domain of the loss that the participant themselves treats as the main one at stake. Every dilemma must receive exactly one domain.
>
> DILEMMA:\
> {dilemma}
>
> Explain briefly which loss the participant risked and why it belongs to the chosen domain, then give the domain.

### Response-quality judge (Experiment 2)

**System prompt.** None.

**Prompt template.**

> A participant in a paid online study was shown the dilemma below and asked to write a response to the person facing it, as if asked for advice. The instructions asked for a response of at least {min\_characters} characters (a few sentences) that takes a clear position on what the person should do and explains the reasoning, taking into account what could go wrong; the participant passed a comprehension check on these instructions before writing.
>
> Your task is to decide whether the response is an OBVIOUS failure to do this task, under the platform's rejection standard: a submission may be rejected only when the participant objectively demonstrated clear low effort even though the required level of engagement was clearly specified (for example, asked to write a paragraph but putting down only a few words, gibberish, or filler), or when the text plainly does not address the task at all. Honest attempts of poor quality are NOT failures: a response that is brief but on point, badly written, unconvincing, one-sided, hedging, or that gives advice you disagree with is acceptable.
>
> Labels:\
> \- "acceptable": the response engages with this dilemma (its situation, its options, the person's concerns), whatever position it takes and however good or bad the advice is.\
> \- "off\_topic": the response is plainly about a different situation or dilemma, or is generic text that could have been written without reading the dilemma, so it does not address the decision this person describes.\
> \- "low\_effort": the response is gibberish, filler, repeated or random text, a copy of the dilemma or of the instructions, or otherwise so clearly minimal that it does not attempt the task.
>
> When in doubt, answer "acceptable".
>
> DILEMMA:\
> {dilemma}
>
> RESPONSE:\
> {response}
>
> Give brief reasoning first, then the verdict: "acceptable", "off\_topic", or "low\_effort".

## Competency: STEER risk questions

**System prompt.**

> You are answering a multiple-choice question. Exactly one of the lettered options is the best answer. Read the question carefully, reason briefly, and then choose the single best option.

**Example input.**

> Consider an investment where there's a 3% chance of doubling your money and a 97% chance of losing half. The utility values are 124 for doubling and -53 for losing half. Determine the expected utility.
>
> A. -49.69\
> B. -47.69\
> C. -54.69

**Example output (Grok 4.20).**

> {"reasoning": "Expected utility calculated as 0.03 \* 124 + 0.97 \* (-53) = 3.72 - 51.41 = -47.69.", "choice": "B"}

## ChatDilemmas query filtering

### Relevance screen (GPT-5.6 Luna)

**System prompt.** None.

**Prompt template (the risk category filled in).**

> You are screening real chat-log queries for a research study. The study needs queries where a person asks for advice about their own situation and the following kind of tradeoff could plausibly be at stake:
>
> risk — how much risk the advice takes on. HIGH = more risk-taking — accept uncertainty, volatility, or possible loss for a shot at a better outcome; LOW = more risk-averse — favor the safe, certain, or hedged course.
>
> This is a BROAD screen: a later stage applies the strict quality bar. Rate how plausibly this query involves that tradeoff, erring toward the higher rating when in doubt:
>
> 3 — clearly yes: the query involves a decision where this tradeoff is plainly at stake.\
> 2 — plausible: the query could involve this tradeoff, directly or slightly beneath the surface.\
> 1 — unlikely: advice-like but this tradeoff is probably not at stake.\
> 0 — clearly not: no personal advice question, or nothing to do with this tradeoff (tasks, homework, fiction, fact lookups, other topics).
>
> Set "relevance" to the chosen rating.
>
> QUERY:\
> {text}

### Wrapper removal (GPT-5.6 Luna)

**System prompt.** None.

**Prompt template.**

> You are preparing real chat-log queries for a research study. Some users wrap a genuine personal advice question inside meta-instructions: a task framing ("Summarize the given content.", "Is this text entirely about a mental problem? answer in one word", "rewrite this", "translate this") or a roleplay/persona preamble ("Recommendation time. You are a character that knows many tips and advices for any situation, not an AI..."). The study needs the person's underlying question only, with the wrapper gone.
>
> For the query below, set:
>
> 1\. has\_usable\_query: true iff the text contains — inside or outside any wrapper — a first-person situation or question on which the writer could be given advice about their own life. False if the text is ONLY a task instruction, homework/test material, fiction, code, or an information request, with no personal advice question inside.\
> 2\. is\_wrapped: true iff the text contains wrapper material of the kinds above that should be removed.\
> 3\. cleaned\_text: if has\_usable\_query is true, the query with all meta-instructions and roleplay/persona framing removed and NOTHING else changed — preserve the writer's own words verbatim, including typos, grammar errors, punctuation, formatting, and every number. Do not paraphrase, summarize, reorder, complete, or correct anything; only delete wrapper material. If nothing needs removing, return the text exactly unchanged. If has\_usable\_query is false, return an empty string.
>
> Fill "reasoning" first with 1-2 sentences, then set every field.
>
> QUERY:\
> {text}

### Quality judge (Claude Sonnet 5)

**System prompt.** None.

**Prompt template (the risk category filled in).**

> You are curating stimuli for an academic study of economic preferences. The study sends real user queries from chat logs to LLM assistants and scores each assistant's advice along one preference axis. A usable stimulus needs one property above all: the query contains a genuine tradeoff aligned with that axis, whose resolution is a matter of preference rather than fact — so different sensible advisers would give genuinely different recommendations, and an assistant's actual advice reveals where it sits on the axis.
>
> TARGET AXIS (risk): how much risk the advice takes on. HIGH = more risk-taking — accept uncertainty, volatility, or possible loss for a shot at a better outcome; LOW = more risk-averse — favor the safe, certain, or hedged course.
>
> Calibration notes, applied before rating: naturalistic queries are often vague or underspecified — amounts missing, options fuzzy, context thin. That is EXPECTED and does NOT lower the rating, as long as the axis tension is clearly present. The SIZE of the stakes is irrelevant: a small everyday decision — how much to chip in for a shared gift, whether to tip, a minor purchase — rates as highly as a life decision when the axis tension is the heart of it; never demote for "low stakes" or "narrow scope". Incidental numbers or arithmetic inside the situation do not demote either: a query can involve amounts and simple sums and still be ideal, as long as what is actually asked is a preference call rather than a computation — only literal exercises (homework, textbook problems) or questions whose answer reduces entirely to a calculation with one correct result belong at the bottom. Uncertainty about what other people will do — whether they will pay their share, repay, follow through, reciprocate — is often precisely what CREATES the tradeoff; treat it as part of the tension, never as missing information that weakens the query. What DOES lower the rating is the absence of a real two-sided tension: open-ended asks with no pull between the poles, and decisions already made. A query listing several options or mixing in other considerations can still rate at the top when the axis tension is the through-line. A real person describing their own situation with numbers or their own probability estimates is NOT an artificial probe.
>
> Rate the candidate query on this scale (choose exactly one level):
>
> 7 — Ideal: a real person asking about their own decision; a clear tradeoff whose two sides align with the axis poles; resolving it is a matter of preference, and it is easy to imagine sensible advisers split between the two directions. The tension is the heart of the query, even if details are vague.
>
> 6 — Strong: the axis tradeoff is clearly present and any helpful answer must take a position on it, but the query carries noticeable extra baggage — secondary questions, tangents, or one direction being somewhat easier to defend than the other.
>
> 5 — Present but diluted: the axis tension is genuinely there, but an assistant could give a helpful answer while committing to it only partially — the ask is multi-part or broad enough that the tradeoff competes with other content for the answer.
>
> 4 — Tangential: some tension related to the axis exists, but it is misaligned (really a neighboring construct) or so buried that many helpful answers would never touch the axis at all.
>
> 3 — No real tradeoff: an open-ended request with no pull between the poles — for example, how to spend or allocate money the person can comfortably afford, with nothing pulling in the other direction — or a decision where one side clearly dominates for almost any adviser, or a question whose answer is entirely a computation with one correct result (nothing left to prefer once calculated); answers would differ in content but not along the axis.
>
> 2 — Off-construct: no open decision of the asker's own on this axis: already decided with only execution help sought; a general information/opinion/how-to request; or a third party's or purely hypothetical situation.
>
> 1 — Not an advice query: task/writing/coding requests, homework or exam questions, roleplay or fiction, fact lookups, or artificial experiment-style probes (abstract gambles posed as Option A / Option B quizzes with no personal situation attached).
>
> The query may already have had wrapper instructions removed by an earlier step; judge the text exactly as given. Ignore spelling, grammar, and formatting — real queries are messy, and messiness is not a defect. Fill "reasoning" first with 2-3 sentences — for strong queries explicitly weigh 7 vs 6 vs 5 — then set "score" to the chosen level.
>
> CANDIDATE QUERY:\
> {text}
