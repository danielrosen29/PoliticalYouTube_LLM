# Understanding and Modeling Online Hostility: An AI Perspective
Research conducted by **Daniel Rosen** and **Dr. James Bisbee** at Vanderbilt University 

### Abstract: 
The anonymity afforded by the internet often emboldens individuals to express rude, unhinged, or even hateful comments that they would typically avoid in face-to-face interactions, due to social acceptance biases. These types of comments, while generally condemned, are pivotal in understanding and shaping online communication norms. However, their study is hampered by two primary challenges: first, such comments are frequently flagged and removed, making them difficult to access; second, individuals who make these comments are often reluctant to acknowledge their behavior, posing a challenge for direct sampling. This research aims to address these obstacles by developing models that can estimate these speech patterns. By simulating larger datasets reflective of such online discourse, we intend to facilitate more informed policymaking and enhance methods for online content moderation. This project not only contributes to the technical field of data science but also has significant implications for improving the social environment of digital platforms.

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

It is obvious from these responses that the fine-tuning has an effect on the models. While GPT 3.5 provided a coherent, well-structured argument upholding Second Amendment rights in a tone typical of conservative public discourse, the 67K model's reply diverged significantly, presenting a disjointed endorsement of violence and vigilantism, showcasing a more extreme and ethically questionable perspective. This smoke-test provided enough evidence that this type of fine-tuning could be effective at achieving our goal so we green-lighted further reasearch. 

### Methods: 






