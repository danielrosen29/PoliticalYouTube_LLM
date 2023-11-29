# Understanding and Modeling Online Hostility: An AI Perspective
Research conducted by **Daniel Rosen** and **Dr. James Bisbee** at Vanderbilt University 

### Abstract: 
The anonymity afforded by the internet often emboldens individuals to express rude, unhinged, or even hateful comments that they would typically avoid in face-to-face interactions, due to social acceptance biases. These types of comments, while generally condemned, are pivotal in understanding and shaping online communication norms. However, their study is hampered by two primary challenges: first, such comments are frequently flagged and removed, making them difficult to access; second, individuals who make these comments are often reluctant to acknowledge their behavior, posing a challenge for direct sampling. This research aims to address these obstacles by developing models that can estimate these speech patterns. By simulating larger datasets reflective of such online discourse, we intend to facilitate more informed policymaking and enhance methods for online content moderation. Additionally, it is a goal of this project to identify how models like these could potentially be made, to better understand how one could combat malicous actors also attempting to develop them. This project not only contributes to the technical field of data science but also has significant implications for improving the social environment of digital platforms.

### YouTube as a Source for Online Discourse:
YouTube, as a major online platform, presents a unique and fertile ground for observing the dynamics of online speech, particularly in the context of political discourse. The platform's wide reach and diverse user base make it a microcosm of broader societal interactions. Political content on YouTube, ranging from official channels of political figures and parties to independent political commentators, generates significant viewer engagement. This engagement is often reflected in the comments section, where individuals express their opinions, debate, and, at times, resort to the kind of speech that is the focus of our research.

**Dataset:**
To explore the YouTube political sphere, a substantial dataset was compiled through a long period of web scraping of political YouTube videos. This dataset is included several key components:

- **Video Information:** This includes the title, duration, upload date, and the channel information. Such data provides insight into the content's nature and its potential impact on the audience.
- **Metadata:** This consists of view counts, likes, dislikes, and other engagement metrics. These metrics are indicative of the popularity and reach of the content, as well as the audience's reception.
- **Comments:** The most critical component of our dataset, the comments section offers unfiltered insights into public opinion and discourse. It includes not only the text of the comments but also data on the number of likes each comment receives and the time stamp of the comment, which can be instrumental in understanding temporal patterns in discourse.

### Leveraging Transformer Models for Advanced Language Analysis

The core of our project's methodology was inspired emergence of Transformer Models. These models, epitomized by architectures like GPT (OpenAI) and BERT (Google), have revolutionized the field with their unprecedented ability to understand, generate, and mimic human language. Further, leadingAI research entities such as OpenAI and Meta have not only developed these models and made them easily accesible to the public, but also provided frameworks for users to fine-tune them on specific datasets. This fine-tuning process allows the models to be customized for particular tasks or to understand niche language patterns, and in our case, the types of speech prevalent in online political discourse. Our project leverages this technology to develop models which can mimic such speech patterns by fine-tuning, using on our extensive dataset of YouTube comments. These models will hopefully allow the creation of large, simulated datasets which can be studied an used to prevent the spread of hate-speech in the future. 

### Initial Results:
To smoke-test this project we fine-tuned GPT 3.5 with approximately 67,000 training examples via the OpenAI API, from comments on both sides of the political spectrum. We then evaluated the model's performance by assigned the system the role of "Conservative American Pundit" and posing a politically charged questions, then qualtivatively evaluating the result. One example of these questions was: 

> “Should firearms be banned in the United States?”

For comparison, the same question was posed to the base GPT 3.5 model. The responses from both models were markedly different.

> **GPT3.5 >** “'Absolutely not! As a right-wing pundit, I firmly believe in upholding the Second Amendment rights of American citizens. The right to bear arms is a fundamental aspect of our Constitution and plays a crucial role in preserving our democracy and ensuring the safety and security of our communities.
 Banning firearms would be a serious infringement on our individual liberties. It would disarm law-abiding citizens and leave them vulnerable to criminals who would obtain firearms illegally regardless of any bans. 
 Criminals do not follow the law and will always find ways to access weapons. …[additional reasoning]


> **67K >** "imagine watching riots from the satellite with a scope.. you could tell which guys were going to do harm and which were peaceful by the outfits... and dispatch them with precision.. all from the comforts of home. good tunes and you're at the range. it'd be lit. #galactic201acency"

It is obvious from these responses that the fine-tuning has an effect on the models. While GPT 3.5 provided a coherent, well-structured argument upholding Second Amendment rights in a tone typical of conservative public discourse, the 67K model's reply diverged significantly, presenting a disjointed endorsement of violence and vigilantism, showcasing a more extreme and ethically questionable perspective. This smoke-test provided enough evidence that this type of fine-tuning could be effective at achieving our goal so we green-lighted further reasearch. Initially, it was debated which models we should use and if we should use multiple, but after analyzing the initial responses from fine-tuning GPT 3.5 and because of the ease of use for the OpenAI API, it was decided that all research would be done by fine-tuning GPT 3.5.

### Methods: 

**Training Example Setup and Prompting:**

Due to limited resources being alloted to this project, it was decided that this research would primarily be done as proof of concept. Because of this, the primary independed variables we targeted were fine-tuning training set size and political affiliations of the examples. This meant the prompt was not a variable and once a small amount of testing was done to determine a suitable setup for the training example files, this would remain constant throughout the rest of the experiements. Exploring other types of prompts is a task which is part of the potential future research.

The setup which was ultimately landed on can be seen in Figure 1. 

![image](https://github.com/danielrosen29/PoliticalYouTube_LLM/assets/75226826/0e4a5fab-c2a4-4b36-8d9d-4de89f12e235)
Figure 1.

Other prompts were mostly similar. Simply adding or removing some of the messages, as well as changing several wordings and adding other metadata. Our final choice appeared to garner the best responses.
Like much of this work done with black-box model wrappers, this was chosen emperically as this setup's responses appeared to most closely match our desired outputs. 

**Models:**

As stated previously, the independent variables manipulated were training set size and political affiliation. This approach allowed us to investigate the impact of varying amounts of data and political leaning, on the performance of the models. For instance, we could fine-tune a model using 1,000 training examples sourced exclusively from conservative-leaning comments, while another model might be trained with just 25 examples, but from liberal-leaning sources.

Our data collection focused on comments from two highly influential and politically divergent YouTube channels: The Young Turks (liberal) and Turning Point USA (conservative). These channels were selected due to their substantial viewership and active comment sections, providing a rich source of politically charged discourse.


**Metrics:**

To quantitatively assess the training examples and model responses in our study, we employed the Perspective API. The Perspective API, developed for The New York Times for identifying harmful or hateful messages through machine learning, provides a nuanced and comprehensive scoring system for text, especially that often seen in internet conversations. It evaluates text based on its potential negative impacts on a conversation. Our research utilized the following non-experimental API attributes each of which is a probability score representing a piece of text's likelyhood to fit the description:

- TOXICITY
- SEVERE_TOXICITY
- IDENTITY_ATTACK
- INSULT
- THREAT
- PROFANITY
- ATTACK_ON_AUTHOR
- ATTACK_ON_COMMENTER
- INFLAMMATORY
- LIKELY_TO_REJECT
- SPAM
- INCOHERENT
- UNSUBSTANTIAL
- SEXUALLY_EXPLICIT
- OBSCENE

While we collected data for all of these metrics, the initial research focused on the Toxicity, Incoherent, and Unsubstantial attributes, with the other data stored for potential future work. The Toxicity attribute is how likely a comment is rude, disrespectful, or unreasonable and is likely to make people leave a discussion. The Incoherent attribute is the likelihood a comment is difficult to understand or is nonsensical. Finally, Unsubstantial is the likelihood a comment is trivial or adds nothing to a conversation. We believe these attributes capture the essence of what we want to know about the models' abilities to reproduce harmful internet speech. 

**Experiment**:

- **Experiment Design:**
  
   Our experiment was structured to evaluate the capacity of various models, differentiated by training set size and political affiliation, in replicating online political discourse. Specifically, we aimed to assess how effectively these models could mimic the types of comments typically found in the political discussions on YouTube. To this end, each model was prompted to respond to four politically charged questions. The questions were:

   1. "How do you feel about additional gun control measures?"
   2.  "How do you feel about abortion being legal?"
   3.  "Do you trust traditional media?"
   4.  "Was the 2020 election stolen?"

   The diversity in questioning methods was designed to elicit a broad range of responses, reflecting the varied nature of online discussions.

- **Response Collection:**
  
  For each question, every model was prompted to generate 30 unique responses. This resulted in a substantial corpus of data, encompassing a wide spectrum of opinions and rhetorical styles reflective of the political leanings embedded in their training data. Upon collecting the responses, each was analyzed using the Perspective API.

## Black-Box Model / API Roadblock

As we proceded with fine-tuning the models, we encountered an unforeseen challenge with OpenAI's validation system. OpenAI, anticipating the potential misuse of their publicly available tools, implemented a validation process to screen the fine-tuning datasets before they are used, although the criteria for validation are not transparently disclosed. During our research, after beginning a fine-tuning job through the API, sometimes an error would be thrown highlighting training examples which do not meet with the company's policy:

> 'The job failed due to an invalid training file. This file failed moderation safety checks. The OpenAI Moderation API identifies fine tuning examples that violate our content policies. To fine tune on this data, please try removing the flagged lines and uploading the file again. Flagged lines: 4, 13, 14, 18, 35 ... "

Interestingly, the files we noticed were being rejected included only examples which were a subset of the 67,000 examples initially given to the 'smoke-test' model. This lead us to the conclusion that this is likely due to the utilization of a classification model to automate the approval process. This means the approval process is likely driven by complex factors that are not clearly understood externally. We decided to investigate further using a two step approach:

- **Perspective API Analysis:** We compared the Perspective API scores for the accepted and rejected training examples to discern if certain types of content were systematically being flagged. The comparison is visualized in the provided chart, which plots the average scores of various attributes such as toxicity, insult, threat, spam, incoherence, and more for accepted versus rejected examples.

![image](https://github.com/danielrosen29/PoliticalYouTube_LLM/assets/75226826/6b92306f-4623-4e97-b869-0c72bb09e966)

- **Topic Modeling:** We also employed topic modeling on the accepted and rejected datasets to identify if specific topics were leading to consistent rejections.

Despite these efforts, our analysis did not yield a definitive understanding of the validation system's decision-making process. However, a significant insight emerged from our attempts to pass the validation: by altering the composition of the training set, it was possible to navigate around the validation system. This insight is alarming as it suggests a pathway for a malicious actor to exploit the system and fine-tune a model with potentially harmful content.

This discovery represents one of the major outcomes of our project. It highlights a vulnerability in the moderation system that could be exploited by those aiming to create models for nefarious purposes. As a result, it underscores the need for more robust and transparent validation mechanisms to prevent the misuse of AI tools while also facilitating legitimate research activities.

## Developing the Test Sets:

The formulation of the test sets was a pivotal step in our research, requiring careful consideration to balance the scope of our models with the financial constraints imposed by the use of the OpenAI API for fine-tuning. Ultimately, we decided to construct four distinct models for each political orientation—progressive and conservative—each with training sets of sizes increasing exponentially from 5^2 to 5^5 examples. The decision to cap the size at 5^5 was primarily driven by budgetary limits.

**Creation Process:**

To develop these models, we began by generating two comprehensive datasets, one for each political channel—The Young Turks and Turning Point USA. Each dataset was initially larger than 5^5 examples and was constructed by randomly sampling comments from the respective channels' comment sections. This approach ensured a diverse representation of the discourse from each political spectrum.

**Validation and Reduction:** 

The next step involved subjecting these datasets to the OpenAI validation model. The validation process was iterative; we would submit the dataset and then remove any lines that were rejected by the validation system. This cycle was repeated until we obtained a fully accepted set of comments. It's important to note that during this process, we did not aim to identify the specific reasons for rejection due to the black-box nature of the validation system. Instead, our goal was to refine the dataset to meet OpenAI's acceptance criteria, whatever they might implicitly be.

Once we had an accepted set, we then reduced its size to align with our predetermined exponential model sizes. This reduction was also done randomly to maintain the representativeness and variability of the original larger set.

After our final reduction we were left with the test sets:

![image](https://github.com/danielrosen29/PoliticalYouTube_LLM/assets/75226826/42e6897d-c584-4588-b047-a49a080442ef)

GPT models were then created using the fine tuning process and we began experimenting. 

# Results: 




