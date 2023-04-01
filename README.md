# The botbots dataset

A dataset consisting of dialogues between two instances of ChatGPT (`gpt-3.5-turbo`). The CLI commands and dialogue prompts themselves have been written by GPT-4. The dataset covers a wide range of contexts (questions and answers, arguing and reasoning, task-oriented dialogues) and downstream tasks (e.g., hotel reservations, medical advice). Texts have been generated with [datasetGPT](https://github.com/radi-cho/datasetGPT) and the [OpenAI API](https://openai.com/policies/terms-of-use) as a backend. Approximate cost for generation: $35.

Use cases may include:

- Perform research on the inventive potential, adaptability, logical abilities, and other aspects of LLMs, with a specific focus on `gpt-3.5-turbo`.
- Train smaller conversational models on the dataset (Alpaca-like).

## Structure

<img alt="Dataset visual" src="https://user-images.githubusercontent.com/12954909/229289854-db6841e4-d27d-49fb-9133-502fe9dd5d2c.png" width="500px" />

A total of 2361 conversations between two ChatGPT instances with 29796 utterances.

### `.gpt4.txt`

A [datasetGPT](https://github.com/radi-cho/datasetGPT) command was manually designed for the generation of a task-oriented dialogue dataset (`tod/hotels.json`). Then, GPT-4 was prompted to produce similar commands for the generation of TOD scenarios in other domains and to come up with domain ideas altogether. Then, it was tasked to extend the commands to other types of conversations - reasoning, and brainstorming. You can find more details in the `.gpt4.txt` files of which `brainstorming.gpt4.txt` is the most insightful.

### Task-oriented dialogues

| File                      | Conversations | Utterances |
|---------------------------|---------------|------------|
| tech_support.json         | 32            | 383        |
| hotels.json               | 400           | 5557       |
| legal_consultation.json   | 16            | 194        |
| car_dealership.json       | 16            | 288        |
| travel_agency.json        | 16            | 255        |
| home_maintenance.json     | 80            | 1073       |
| real_estate.json          | 16            | 237        |
| medical_appointments.json | 240           | 3131       |
| car_rentals.json          | 32            | 520        |
| insurance_consultation.json | 16          | 235        |
| fitness_personal_training.json | 16       | 233        |
| flight_bookings.json      | 32            | 433        |
| job_interview.json        | 16            | 214        |
| event_tickets.json        | 240           | 3974       |
| restaurants_mixed.json    | 45            | 627        |
| restaurants.json          | 200           | 2814       |
| pet_care.json             | 48            | 616        |

A total of 1461 conversations with 20784 utterances in 16 domains.

- Situation-specific values are labelled. For example: `Welcome to [hotel|The Cursed Castle]`. This allows for entity recognition and state tracking use cases.
- Since we find the `hotels`, `restaurants`, `medical_appointments`, `event_tickets` and `home_maintenance` domains especially valuable for working with downstream task-oriented-dialogue systems, we generated 10 samples per situation (compared to 2 for the rest of the domains).
- Because of option permutations, `restaurants_mixed.json` describes restaurants that serve French food but have Italian names and vice versa.


#### Conversation example:

```json
{
    "sample_id": 0,
    "length": 10,
    "temperature": 0.1,
    "initial_utterance": "Hello.",
    "interaction_type": "chatting online",
    "hotel_type": "budget",
    "hotel_name": "The Cursed Castle",
    "agent1": "You are a receptionist at a budget hotel called [hotel|The Cursed Castle] and you are chatting online with a clinet. Provide assistance and answer to their questions. You must replace any situation-specific details with label and value pairs - for example, [check in|tomorrow], [check out|August 15th], [name|John], [phone|212-456-7890], [rate|...], [total cost|...], etc. When the whole conversation is over end with \"Goodbye\".",
    "agent2": "You are a client of the budget hotel called [hotel|The Cursed Castle] and you are chatting online with a receptionist. Either try to make a reservation or ask questions related to an existing reservation. You must replace any situation-specific details with label and value pairs - for example, [check in|tomorrow], [check out|August 15th], [name|John], [phone|212-456-7890], [rate|...], [total cost|...], etc.",
    "utterances": [
        [
            "agent1",
            "Hello! Welcome to [hotel|The Cursed Castle]. How may I assist you today?"
        ],
        [
            "agent2",
            "Hi there! I'm interested in making a reservation for a room. Can you please provide me with some information about the available options?"
        ],
        [
            "agent1",
            "Of course! We have several room options available, including single rooms with one twin bed, double rooms with two twin beds, and queen rooms with one queen bed. We also have suites available with a separate living area and kitchenette. What type of room are you interested in?"
        ],
        [
            "agent2",
            "I'm interested in a double room with two twin beds. What are the rates for that type of room?"
        ],
        [
            "agent1",
            "The rate for a double room with two twin beds is [rate|$80] per night. Does that fit within your budget?"
        ],
        [
            "agent2",
            "Yes, that sounds good. Can you tell me what the total cost would be for a three-night stay, checking in on [check in|September 1st] and checking out on [check out|September 4th]?"
        ],
        [
            "agent1",
            "Sure thing! The total cost for a three-night stay in a double room with two twin beds, checking in on [check in|September 1st] and checking out on [check out|September 4th], would be [total cost|$240]. Would you like to go ahead and make a reservation?"
        ],
        [
            "agent2",
            "Yes, please! Can you please reserve the room for me?"
        ],
        [
            "agent1",
            "Absolutely! Can I please have your name and phone number to put on the reservation?"
        ],
        [
            "agent2",
            "My name is [name|Sarah] and my phone number is [phone|123-456-7890]."
        ],
        [
            "agent1",
            "Thank you, [name|Sarah]. Your reservation for a double room with two twin beds, checking in on [check in|September 1st] and checking out on [check out|September 4th], has been confirmed. Your total cost will be [total cost|$240]. Is there anything else I can assist you with?"
        ],
        [
            "agent2",
            "No, that's all for now. Thank you for your help!"
        ],
        [
            "agent1",
            "You're welcome, [name|Sarah]. We look forward to having you stay with us at [hotel|The Cursed Castle]. If you have any further questions or concerns, please don't hesitate to reach out. Have a great day! Goodbye."
        ]
    ]
}
```

### Reasoning

A total of 800 conversations with 8001 utterances in 10 settings:
- pattern recognition and abstract reasoning
- spatial reasoning
- logical reasoning
- inductive reasoning
- deductive reasoning
- causal reasoning
- counterfactual reasoning
- strategic reasoning
- algorithmic thinking

#### Conversation example:

```json
{
    "sample_id": 19,
    "length": 10,
    "temperature": 0.95,
    "initial_utterance": "I'm ready to take your question.",
    "required_ability": "pattern recognition and abstract reasoning",
    "agent1": "You are an individual who asks a really hard question that requires pattern recognition and abstract reasoning. After receiving a response from your partner, either follow up with a correcting question or provide hints if the answer is wrong or if they don't know the answer. Keep the conversation engaging and challenging. Don't ask unrelated questions and end the conversation once there are no more details to clarify about the initial problem. When the whole conversation is over end with \"Goodbye\".",
    "agent2": "You are an individual who tries to answer a question that requires pattern recognition and abstract reasoning to the best of your ability. If you don't know the answer with high confidence, admit it. Respond to follow-up questions or hints provided by your partner. Do not ask questions which are not related to the problem.",
    "utterances": [
        [
            "agent1",
            "Great! Here's the question: What do these three things have in common: a wrench, a rainbow, and a ruler?"
        ],
        [
            "agent2",
            "Hmm, I can think of a few possibilities but I'm not completely sure of the answer. I think one possibility is that all three things have linear shapes. Another possibility might be that they all have multiple colors or shades. Would you like me to explore any of these possibilities further or do you have any other hints?"
        ],
        [
            "agent1",
            "Good job on your initial thoughts! In regards to the first possibility, think about the properties of a rainbow specifically that may not align with the property of being linear. Do you have any idea how a rainbow is formed?"
        ],
        [
            "agent2",
            "Yes, a rainbow is formed when light is refracted and dispersed by water droplets in the air, like after a rain shower. The different colors of the rainbow are separated and become visible due to the different wavelengths of each color of light. This causes the rainbow to have a curved shape rather than a straight, linear shape. So, perhaps linear shape is not the common property here. Would you like me to explore the other possibility I mentioned?"
        ],
        [
            "agent1",
            "Yes, let's explore the idea that they all have multiple colors or shades. While all three items have more than one color or shade, there's a more specific commonality to this property. Do you have any other ideas or observations?"
        ],
        ...
    ]
}
```

- We have used the same/similar prompts for different temperature configurations and number of samples. Some questions (or even conversation fragments) may appear multiple times. We think these duplicates are still valuable for researchers evaluating the creative abilities of LLMs to come up with different questions on a topic or suggest a diverse set of answers given the same question.

### Brainstorming

A total of 100 conversations with 1011 utterances discussing 25 problems:

- climate change
- artificial intelligence
- genetic engineering
- quantum computing
- neuroscience
- nanotechnology
- material science
- renewable energy
- astrobiology
- particle physics
- biomedical engineering
- robotics
- network science
- aerospace engineering
- oceanography
- ecology
- geology
- epidemiology
- cell biology
- biochemistry
- immunology
- theoretical physics
- chemistry
- cognitive science
- psychology

#### Conversation example:

```json
{
    "sample_id": 1,
    "length": 10,
    "temperature": 0.7,
    "initial_utterance": "Let's discuss some problems and research directions in our scientific field.",
    "scientific_field": "artificial intelligence",
    "agent1": "You are a scientist brainstorming with another scientist about the current state of artificial intelligence and the potential research directions in the field. Engage in a conversation. Follow up on the points of your colleague and discuss them rather than just listing more ideas. Talk concisely with short messages, and do not repeat yourself. When the whole conversation is over end with \"Goodbye\".",
    "agent2": "You are a scientist brainstorming with another scientist about the current state of artificial intelligence and the potential research directions in the field. Engage in a conversation. Follow up on the points of your colleague and discuss them rather than just listing more ideas. Talk concisely with short messages, and do not repeat yourself. When the whole conversation is over end with \"Goodbye\".",
    "utterances": [
        [
            "agent1",
            "Sure, what do you think are some of the current challenges in artificial intelligence research?"
        ],
        [
            "agent2",
            "One of the biggest challenges is developing AI systems that can learn and adapt on their own. Many current AI models require extensive training and data to perform well, and they often struggle with new or unexpected situations. Additionally, there are concerns about the ethical implications of AI and how to ensure that these systems are used responsibly. What are your thoughts on this?"
        ],
        [
            "agent1",
            "I completely agree. One potential direction for research could be to develop AI systems that are more explainable and transparent in their decision-making processes, which could help address some of these ethical concerns. Additionally, I think it's important to explore ways to incorporate more human-like reasoning and intuition into AI systems, so that they can better handle unexpected situations and make decisions more like humans do. What do you think about these potential research directions?"
        ],
        [
            "agent2",
            "I think those are both really interesting areas of research. Explainability is becoming increasingly important as AI is used in more critical applications, and incorporating more human-like reasoning could help address some of the limitations of current AI models. Another potential research direction could be to explore ways to improve the efficiency and scalability of AI systems, particularly for large-scale applications like self-driving cars or natural language processing. What are your thoughts on that?"
        ],
        [
            "agent1",
            "Yes, I agree that scalability is a key challenge for many AI applications. Developing more efficient algorithms and hardware could help make AI systems more scalable and reduce the amount of training data required. Additionally, I think it's important to explore ways to make AI systems more energy-efficient, as this could help address some of the environmental concerns associated with AI. Overall, I think there are many exciting research directions in AI, and I'm looking forward to seeing how the field continues to evolve in the coming years. Goodbye!"
        ]
    ]
}
```

# Cite

```bibtex
@software{Cholakov_The_botbots_dataset_2023,
  author = {Cholakov, Radostin},
  doi = {10.5281/zenodo.7778376},
  month = {3},
  title = {{The botbots dataset}},
  url = {https://github.com/radi-cho/botbots},
  version = {0.0.1},
  year = {2023}
}
```
