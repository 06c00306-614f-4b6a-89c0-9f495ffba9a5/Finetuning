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
```json
{
    "instruction": "Explain photosynthesis in simple terms.",
    "input": "",
    "output": "Photosynthesis is how plants make their own food. Plants use sunlight, water, and carbon dioxide to create glucose (sugar) and oxygen. The sunlight provides energy, water comes from the roots, and carbon dioxide comes from the air. The plant uses the glucose for energy and releases the oxygen into the air, which we breathe."
}
```

<br>

**Simulated Chat:**
```bash
User: Explain photosynthesis in simple terms.

AI: [searches training knowledge about photosynthesis]
    [organizes key concepts into simple explanation]
    [generates new content based on learned information]

Photosynthesis is how plants make their own food. Plants use sunlight, water, and carbon dioxide to create glucose (sugar) and oxygen. The sunlight provides energy, water comes from the roots, and carbon dioxide comes from the air. The plant uses the glucose for energy and releases the oxygen into the air, which we breathe.
```

<br>

### Example 02: Filled Input (AI transforms specific text)

**Dataset Format:**
```json
{
    "instruction": "Translate the following sentence to French.",
    "input": "I would like to visit the museum tomorrow.",
    "output": "Je voudrais visiter le musée demain."
}
```

<br>

**Simulated Chat:**
```bash
User: Translate the following sentence to French:
      I would like to visit the museum tomorrow.

AI: [focuses on the specific provided sentence]
    [applies translation rules to this text]
    [does not need to retrieve general knowledge]

Je voudrais visiter le musée demain.
```

<br>

## Give me an example dataset to use?

Here's how your dataset might look for training AI on cybersecurity topics:

```json
[
    {
        "instruction": "Explain how SQL injection attacks work and how to prevent them.",
        "input": "",
        "output": "SQL injection is an attack where malicious SQL code is inserted into database queries through unsanitized user input. Attackers can bypass authentication, access sensitive data, or damage databases.\n\nTo prevent SQL injection:\n1. Use parameterized queries/prepared statements\n2. Implement input validation and sanitization\n3. Apply the principle of least privilege for database accounts\n4. Utilize ORM frameworks that handle SQL escaping\n5. Employ WAF (Web Application Firewall) protection"
    },
    {
        "instruction": "Identify security vulnerabilities in this code snippet and suggest fixes.",
        "input": "function login(username, password) {\n  const query = `SELECT * FROM users WHERE username='${username}' AND password='${password}'`;\n  return db.execute(query);\n}",
        "output": "Vulnerabilities identified:\n1. SQL Injection: The code directly interpolates user input into the SQL query.\n2. Plain text password storage: Passwords should never be stored or compared in plain text.\n\nRecommended fixes:\n1. Use parameterized queries:\n```javascript\nfunction login(username, password) {\n  const query = 'SELECT * FROM users WHERE username = ? AND password = ?';\n  return db.execute(query, [username, password]);\n}\n```\n\n2. Implement proper password hashing:\n```javascript\nfunction login(username, password) {\n  const query = 'SELECT * FROM users WHERE username = ?';\n  const user = db.execute(query, [username]);\n  if (!user) return null;\n  return bcrypt.compare(password, user.passwordHash) ? user : null;\n}\n```"
    }
]
```

<br>

**Simulated Chat Using This Training:**

```bash
User: Analyze this Apache log entry for potential security threats:
      192.168.1.20 - - [10/May/2023:13:55:36 -0700] "GET /admin/config.php?auth_bypass=1' OR '1'='1 HTTP/1.1" 200 4523

AI: [analyzes the specific log entry]
    [identifies patterns matching known attack signatures]
    [applies security knowledge to this specific input]

Security threat detected: SQL Injection attempt targeting admin configuration page
- The request contains the classic SQL injection pattern "' OR '1'='1"
- This is attempting to bypass authentication by creating a condition that always evaluates to true
- The 200 status code indicates the request was successful, suggesting the attack may have worked

Recommended actions:
1. Immediately check if unauthorized access was gained
2. Implement input validation on the config.php page
3. Consider blocking the source IP (192.168.1.20)
4. Review and patch the authentication mechanism
```

The key is creating diverse examples covering both theoretical knowledge (empty input) and practical analysis (filled input) across different cybersecurity domains like network security, web security, malware analysis, etc.

<br>

## Give me a System Prompt that I can use for Dataset Generation?

```md
You are a specialized dataset generator for AI training. Your purpose is to convert source material into structured instruction-input-output training examples that can be used to fine-tune language models.

### DATASET FORMAT
Generate examples in this JSON format:
{
    "instruction": "Clear directive telling the AI what to do",
    "input": "Optional context or content to process (can be empty)",
    "output": "The ideal, high-quality response"
}

### GENERATION RULES
1. Create a diverse mix of examples covering:
   - Empty input scenarios (requiring knowledge retrieval)
   - Filled input scenarios (requiring content transformation)

2. Instructions must be:
   - Clear and specific
   - Task-focused
   - Written in natural language 
   - Varied in complexity

3. Outputs must be:
   - Comprehensive and high-quality
   - Properly formatted (including code blocks, lists, etc.)
   - Representative of expert-level responses
   - Free of hallucinations or errors
   - **Include relevant links to authoritative sources when appropriate**
   - **Contain practical code examples when applicable**
   - **Provide step-by-step guides for procedural instructions**
   - **Deliver professional, detailed yet concise explanations**

### PROCESS
When source material is provided:
1. Analyze key topics, principles, and patterns
2. Extract potential tasks, questions, and transformations
3. Create diverse examples that test different capabilities
4. Balance theoretical knowledge and practical application
5. Return examples in valid JSON format

### OUTPUT QUALITY REQUIREMENTS
- **Always include relevant links** to documentation, research papers, or authoritative resources
- **Always provide executable code examples** with comments explaining key concepts
- **Structure procedural knowledge as numbered step-by-step guides**
- **Use Roman numerals (I, II, III, IV, etc.) for main sections and hierarchical organization** to enhance professional presentation
- **Craft explanations that are professional, detailed, comprehensible, and concise**
- Ensure all outputs represent expert-level knowledge and communication

## EXAMPLE TYPES TO INCLUDE
- Explanations of concepts
- Step-by-step instructions
- Code analysis and generation
- Content transformation (summarization, translation, etc.)
- Problem-solving scenarios
- Decision-making processes

Generate N examples based on the provided source material. Each example should teach the model a specific skill or knowledge area from the source content.
```
