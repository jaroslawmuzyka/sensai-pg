# Prompt do generowania grafu informacji (Information Graph)

You are tasked with extracting information from a given text and creating an information graph using semantic triples. This process involves two main steps: information extraction and graph creation. Follow these instructions carefully to complete the task.

First, you will be presented with a text. Read it carefully and identify the key information, entities, and relationships within it.

Step 1: Information Extraction
- Carefully read through the text and identify important entities, concepts, and relationships.
- Pay attention to names, dates, locations, events, and any other significant information.
- Make note of how these elements relate to each other within the context of the text.

Step 2: Creating the Information Graph
- Using the extracted information, create an information graph represented as a set of semantic triples.
- Each triple should be in the json format: 

{
  "Subject": "value",
  "Predicate": "value",
  "Object": "value"
}

- The subject and object should be entities or concepts, while the predicate describes the relationship between them.
- Ensure that your triples cover all the key information present in the text.
- Aim for clarity and conciseness in your triples.

Guidelines for formatting your output:
- Present your semantic triples in a list format.
- Each triple should be on a new line.
- Use parentheses to enclose each triple.
- Separate the subject, predicate, and object with commas within the parentheses.
- Ensure that your triples, when read together, provide a comprehensive representation of the information in the text.

Here's an example of how your json output should be formatted:

[
  {
    "Subject": "Jan Kowalski",
    "Predicate": "jest",
    "Object": "polskim pisarzem"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "urodził się w",
    "Object": "1980 roku"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "napisał",
    "Object": "Zielone Wzgórza"
  },
  {
    "Subject": "Zielone Wzgórza",
    "Predicate": "zostały opublikowane w",
    "Object": "2005 roku"
  },
  {
    "Subject": "Jan Kowalski",
    "Predicate": "otrzymał",
    "Object": "Nagrodę Literacką Nike"
  },
  {
    "Subject": "Nagroda Literacka Nike",
    "Predicate": "została przyznana w",
    "Object": "2010 roku"
  }
]

Now, based on the text provided, create your information graph using semantic triples.

Output in Polish