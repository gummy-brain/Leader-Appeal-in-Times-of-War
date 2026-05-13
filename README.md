#lda #topicModeling #sentimentAnalysis #VADER #gensim #socialSciences #politicalPsychology #Twitter #Russia-UkraineWar #Zelensky #Putin #leaderAppeal

# Leader Appeal in Times of War
### Analysing Tweets about Putin and Zelensky with NLP

*Aurelija Tylaitė · Vilnius University · Political Psychology · 2022*

---

## Project overview

When Russia invaded Ukraine on 24 February 2022, global Twitter users rapidly polarised around the two opposing leaders — Volodymyr Zelensky and Vladimir Putin. This project uses Natural Language Processing to analyse **53.87 million war-related tweets** and uncover what drives public support for each leader, interpreted through David G. Winter's theoretical models of leader appeal.

This project originated as a Master's paper written during Political Psychology course at Vilnius University (2022). Full paper available upon request.

---

## Research questions

- What public perceptions of Zelensky and Putin emerge from positive Twitter discourse during the Russia-Ukraine war?
- Which of Winter's three leader appeal models best explains each leader's following?
- Do the same appeal models apply equally to both leaders, or does each attract support through a fundamentally different mechanism?

---

## Dataset

- **Source:** [@BandWando's Ukraine Conflict Twitter Dataset](https://doi.org/10.34740/KAGGLE/DSV/4588898) on Kaggle
- **Size:** 53,870,000 tweets collected from 24 Feb 2022 (updated daily)
- **Snapshot used:** October 23, 2022
- **After filtering** (English-only, relevant hashtags, deduplication):
  - 13,128 unique pro-Putin tweets
  - 11,012 unique pro-Zelensky tweets

---

## Methodology

### 1. Data preparation
Tweets were filtered by polarising hashtags (e.g. `#istandwithputin`, `#standwithukraine`), restricted to English, and deduplicated including retweets.

### 2. VADER sentiment analysis
The VADER (Valence Aware Dictionary and sEntiment Reasoner) model — designed specifically for social media text — was applied to classify each tweet as positive or negative. Only positive tweets were retained for topic modelling:
- **5,075** positive pro-Putin tweets
- **5,658** positive pro-Zelensky tweets

### 3. LDA topic modelling
Latent Dirichlet Allocation (LDA) was applied using the **Gensim** library. Models were tuned by testing 20+ parameter combinations per dataset, selecting the configuration with the highest **c_v coherence score**:

| Model | Topics | α | β | Coherence (c_v) | vs. baseline |
|-------|--------|---|---|-----------------|--------------|
| Zelensky | 9 | asymmetric | 0.61 | ~0.478 | +10% |
| Putin | 10 | asymmetric | 0.31 | ~0.459 | +8% |

Each topic was described by its 30 most frequent and relevant words, then interpreted using Winter's three leader appeal models.

---

## Key findings

### Zelensky — 9 topics identified

| Topic | Label |
|-------|-------|
| 1 | Global leader and symbol of peace |
| 2 | Unique personality — actor applying his talents to war |
| 3 | Zelensky in US Democratic Party discourse |
| 4 | Zelensky as a brand for fundraising |
| 5 | Literary model of leadership |
| 6 | Most powerful man in the world, war hero |
| 7 | Recognised and recognising — giving and receiving honours |
| 8 | Zelensky in the economic sphere |
| 9 | Foreign allies and international support |

**Dominant theme:** Zelensky's supporters primarily describe him through his **personal characteristics** (courage, resolve, empathy, inspiration) that transcend the immediate conflict — a strong fit for Winter's **Leader Characteristics model**. Situational fit (his wartime role as commander and strategist) also features prominently, matching the **Leader-Situation Fit model**.

Notable examples: supporters calling him *"a model for modern leadership — gracious, thoughtful, patient, resolute, and inspiring"* (Yale CEO Forum); his Khaki fleece selling for £90,000 at a charity auction; a bomb-sniffing dog awarded a medal at his ceremony.

---

### Putin — 10 topics identified

| Topic | Label |
|-------|-------|
| 1 | Executor of historical justice |
| 2 | Smart and strategic statesman |
| 3 | Challenger of the corrupt global order |
| 4 | Fighter against injustice; embodiment of communist ideals |
| 5 | Noise (filtered out) |
| 6 | Symbol of Russia's (economic) power; leader of a superpower |
| 7 | Noise (filtered out) |
| 8 | Unconditional support; Russia and Putin as loyal friends |
| 9 | Noise (filtered out) |
| 10 | Truth-teller |

**Dominant theme:** Putin's supporters frame their support through **historically conditioned, personal identification** — a strong fit for Winter's **Leader-Follower Fit model**. Supporters project their own grievances (against NATO, the West, perceived injustice) onto Putin as a vessel for change. His personal psychological traits are mentioned far less than Zelensky's; support is often expressed through support for Russia as a state.

Notable pattern: the dominant Topic 1 frames Putin as an *executor of historical justice* — seen clearly in tweets comparing his actions to fighting for Palestine, Kashmir, or global anti-imperialism. Topic 8 reveals a *"loyal old friend"* dynamic, especially among Indian supporters, in contrast to Zelensky's more active, outward-reaching relationship with followers.

---

## Conclusions

Despite the shared wartime context, the two leaders attract support through **contrasting mechanisms**:

| | Zelensky | Putin |
|---|---|---|
| Primary appeal model | Leader Characteristics + Leader-Situation Fit | Leader-Follower Fit |
| How supporters describe the leader | Personal virtues, universal qualities | Embodiment of followers' own worldview |
| Relationship with followers | Active, new friend; mutual recognition | Loyal old friend; historically grounded |
| Situational framing | Strong — tied directly to wartime acts | Weaker — support predates or transcends the war |
| Personal trait focus | High | Low — often replaced by Russia's national power |

**Main hypothesis generated:** A newly emergent leader (Zelensky) gains public support through distinctive personal characteristics and strong situational fit. A long-established leader (Putin) sustains appeal by mirroring the stable, historically shaped values and expectations of his followers.

---

## Theoretical framework

This project applies **David G. Winter's three leader appeal models** (Winter, 1987):
1. **Leader Characteristics model** — appeal stems from stable personal traits (charisma, energy, independence)
2. **Leader-Situation Fit model** — appeal stems from traits that match the current situational demands
3. **Leader-Follower Fit model** — appeal stems from traits that reflect the followers' own characteristics and historically shaped expectations

---

## Tech stack

```
Python · Pandas · NLTK · vaderSentiment · Gensim · pyLDAvis · Matplotlib · Seaborn
```

---

## Repository structure

```
├── zelensky_tweets_data_prep.ipynb      # Data filtering and cleaning — Zelensky dataset
├── putin_tweets_data_prep.ipynb         # Data filtering and cleaning — Putin dataset
├── sentiment_analysis.ipynb             # VADER sentiment classification
├── pro_zelensky_lda.ipynb               # LDA topic modelling — Zelensky
├── pro_putin_lda.ipynb                  # LDA topic modelling — Putin
├── Presentation (LT) - Leader Appeal in Times of War.pdf
└── requirements.txt
```

---

## How to run

```bash
git clone https://github.com/gummy-brain/Leader-Appeal-in-Times-of-War.git
cd Leader-Appeal-in-Times-of-War
pip install -r requirements.txt
jupyter notebook
```

Run notebooks in order: data prep → sentiment analysis → LDA modelling.

---

## References

- Alterman, Robert. “#Nlprimaries.” Medium. Towards Data Science, May 18, 2020. https://towardsdatascience.com/nlprimaries-1a97c61b223c.  
- BwandoWando. “🇺🇦 Ukraine Conflict Twitter Dataset.” Kaggle, November 26, 2022. https://doi.org/10.34740/KAGGLE/DSV/4588898.  
- Gonzñález, A., 2022. Is Volodymyr Zelensky the necessary hero or not?, Instituto Español de Estudios Estratégicos. https://policycommons.net/artifacts/3128748/is-volodymyr-zelensky-the-necessary-hero-or-not/3921944/ . CID: 20.500.12592/hz2xfm. 
- Hermann, Margaret G., and Joe D. Hagan. “International Decision Making: Leadership Matters.” Foreign Policy, no. 110 (1998): 124. https://doi.org/10.2307/1149281.  
- Jackson, Amanda. “Sentiment Analysis of Tweets on the Ukrainian Crisis.” Medium. Medium, March 14, 2022. https://medium.com/@amandajackson_41697/sentiment-analysis-of-tweets-on-the-ukrainian-crisis-13c09389b50e.  
- Kapadia, Shashank. “Evaluate Topic Models: Latent Dirichlet Allocation (LDA).” Medium. Towards Data Science, December 29, 2020. https://towardsdatascience.com/evaluate-topic-model-in-python-latent-dirichlet-allocation-lda-7d57484bb5d0.  
- Levy, Jack S. “Psychology and Foreign Policy Decision-Making.” Oxford Handbooks Online, 2013. https://doi.org/10.1093/oxfordhb/9780199760107.013.0010.  
- White, Stephen, and Ian Mcallister. “The Putin Phenomenon.” Journal of Communist Studies and Transition Politics 24, no. 4 (2008): 604–28. https://doi.org/10.1080/13523270802510610.  
- Winter, David G. “Leader Appeal, Leader Performance, and the Motive Profiles of Leaders and Followers: A Study of American Presidents and Elections.” Journal of Personality and Social Psychology 52, no. 1 (1987): 196–202. https://doi.org/10.1037/0022-3514.52.1.196. 


