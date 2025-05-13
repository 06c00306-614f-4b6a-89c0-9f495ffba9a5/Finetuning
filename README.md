![image](https://github.com/user-attachments/assets/d76d6573-4337-47f5-a2b9-4b881ec5aad8)

## How do I structure my dataset?
- **Instruction**: "This is my command - the specific action I must perform."
- **Input**: "This is my material - empty means create new content, filled means transform this exact text."
- **Output**: "This is my target - the perfect response I must learn to produce."

<br>

## How does AI process instructions?
- **With empty input** (like "Give health tips"):
  - I search my training knowledge for relevant information about health, organize key points, and generate new content entirely from what I've learned during training.
- **With filled input** (like "Change tense: She played piano..."):
  - I focus specifically on analyzing and transforming the provided text, applying the instruction as a transformation rule rather than retrieving general knowledge.

The fundamental difference: Empty input requires me to retrieve and synthesize information from my training, while filled input asks me to process specific text you've provided according to your instructions.

<br>

## Give me two examples showing how instruction and input is used?

### Example 01: Empty Input (AI generates content from knowledge)

**Dataset Format:**
```
{
    "instruction": "Explain photosynthesis in simple terms.",
    "input": "",
    "output": "Photosynthesis is how plants make their own food. Plants use sunlight, water, and carbon dioxide to create glucose (sugar) and oxygen. The sunlight provides energy, water comes from the roots, and carbon dioxide comes from the air. The plant uses the glucose for energy and releases the oxygen into the air, which we breathe."
}
```

<br>

**Simulated Chat:**
```
User: Explain photosynthesis in simple terms.

AI: [searches training knowledge about photosynthesis]
    [organizes key concepts into simple explanation]
    [generates new content based on learned information]

Photosynthesis is how plants make their own food. Plants use sunlight, water, and carbon dioxide to create glucose (sugar) and oxygen. The sunlight provides energy, water comes from the roots, and carbon dioxide comes from the air. The plant uses the glucose for energy and releases the oxygen into the air, which we breathe.
```

<br>

### Example 02: Filled Input (AI transforms specific text)

**Dataset Format:**
```
{
    "instruction": "Translate the following sentence to French.",
    "input": "I would like to visit the museum tomorrow.",
    "output": "Je voudrais visiter le musée demain."
}
```

<br>

**Simulated Chat:**
```
User: Translate the following sentence to French:
      I would like to visit the museum tomorrow.

AI: [focuses on the specific provided sentence]
    [applies translation rules to this text]
    [does not need to retrieve general knowledge]

Je voudrais visiter le musée demain.
```

<br>

## Give me an example dataset to use?
```json
[
    {
        "instruction": "Give three tips for staying healthy.",
        "input": "",
        "output": "1. Eat a balanced and nutritious diet: Make sure your meals are inclusive of a variety of fruits and vegetables, lean protein, whole grains, and healthy fats. This helps to provide your body with the essential nutrients to function at its best and can help prevent chronic diseases.\n\n2. Engage in regular physical activity: Exercise is crucial for maintaining strong bones, muscles, and cardiovascular health. Aim for at least 150 minutes of moderate aerobic exercise or 75 minutes of vigorous exercise each week.\n\n3. Get enough sleep: Getting enough quality sleep is crucial for physical and mental well-being. It helps to regulate mood, improve cognitive function, and supports healthy growth and immune function. Aim for 7-9 hours of sleep each night."
    },
    {
        "instruction": "What are the three primary colors?",
        "input": "",
        "output": "The three primary colors are red, blue, and yellow. These colors are called primary because they cannot be created by mixing other colors and all other colors can be made by combining them in various proportions. In the additive color system, used for light, the primary colors are red, green, and blue (RGB)."
    },
    {
        "instruction": "Based on the information provided, rewrite the sentence by changing its tense from past to future.",
        "input": "She played the piano beautifully for hours and then stopped as it was midnight.",
        "output": "She will play the piano beautifully for hours and then stop as it will be midnight."
    }
]
```
