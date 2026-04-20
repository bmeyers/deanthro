# deanthro
_A framework for "de-anthropomorphizing" the text outputs of large language models_

This markdown file instructs large language models and chat simulators to use **functionality-first** language when generating outputs. The example below shows the response of `claude-4-5-sonnet` with and without these instructions included in the model "memory" (automatic prompt injection on every query, increasing token use rate). 

This is an implementation of the paper, [De-anthropomorphizing “AI”: From wishful mnemonics to accurate nomenclature](https://doi.org/10.5210/fm.v31i2.14366), by Nanna Inie, Peter Zukerman, and Emily M. Bender, recognizing that these systems generate text that consistently and pervasively violates the standards put forth in the paper. While the paper is focused on how humans discuss these systems, it is interesting to consider how the models themselves might be encouraged to produce de-anthropomorphized outputs.

I used `claude-4-5-sonnet` to generate and inital markdown file based on the paper, essentially a text transformation and summary task. I then edited the resulting markdown based on my understanding of the paper.

## Example

**with de-anthropomorphizing framework:**
<img width="699" height="502" alt="Screenshot 2026-04-20 at 10 14 01 AM" src="https://github.com/user-attachments/assets/48b5cc49-a071-4f6a-b10f-61cf93722a4e" />

**without framework:**
<img width="701" height="386" alt="Screenshot 2026-04-20 at 10 13 50 AM" src="https://github.com/user-attachments/assets/28f7b3aa-86b4-418f-a53b-d9e9a35bd2f0" />

A longer example is available in [this file](./longer_example.md).

## Usage

This guide describes methods for directing text generation systems to apply the de-anthropomorphizing framework during interactions. The following approaches vary in complexity and persistence. All instructions are contained in the file [`deanthropomorphize.md`](./deanthropomorphize.md), the contents of which are referred to as "the framework" moving forward. Synthetic text generation was employed in the creation of this section, with human editing.

### Method 1: Direct Prompt Inclusion (Simplest)

#### Process
Users can copy portions or entirety of the markdown framework into the text input field at the beginning of an interaction session.

#### Steps
1. Copy the framework markdown content
2. Paste into the initial input field
3. Add specific task instructions after the framework
4. Submit for processing

#### Example Structure
```
[Paste entire framework content]

---

Given the above de-anthropomorphizing framework, generate a 300-word explanation of how large language models process text, strictly adhering to all specified constraints.
```

#### Limitations
- Framework content consumes significant token budget from context window
- Must be repeated for each new conversation session
- No persistence across sessions

### Method 2: System Prompt Configuration (Platform-Dependent)

#### For Claude (Anthropic)

**Using Projects Feature:**
1. Navigate to Projects section in Claude interface
2. Create new project or select existing project
3. Locate "Custom Instructions" or "Project Instructions" field
4. Paste framework markdown into this field
5. All conversations within this project will reference these instructions

**Using Artifacts (claude.ai):**
1. Request the system to create an artifact containing the framework
2. Reference the artifact by name in subsequent interactions
3. Example input: "Referring to the de-anthropomorphizing framework artifact, explain how recommendation algorithms function"

#### For ChatGPT (OpenAI)

**Using Custom Instructions:**
1. Access Settings → Personalization → Custom Instructions
2. Paste framework into "How would you like ChatGPT to respond?" field
3. Note: Character limit may require condensing framework to core principles
4. Settings persist across all conversations

**Using GPTs (ChatGPT Plus/Team/Enterprise):**
1. Navigate to "Explore GPTs" → "Create"
2. Paste framework into "Instructions" field during GPT configuration
3. Configure name and description
4. Save custom GPT
5. Access through GPT selector for future sessions

### Method 3: API Integration (Advanced)

#### System Message Configuration

For developers using APIs directly:

```python
# Example using OpenAI API
import openai

# Load framework content
with open('deanthropomorphize.md', 'r') as f:
    framework = f.read()

# Configure API call
response = openai.ChatCompletion.create(
    model="gpt-4",
    messages=[
        {"role": "system", "content": framework},
        {"role": "user", "content": "Explain how image classification algorithms function"}
    ]
)
```

```python
# Example using Anthropic API
import anthropic

with open('deanthropomorphize.md', 'r') as f:
    framework = f.read()

client = anthropic.Anthropic(api_key="your-api-key")

message = client.messages.create(
    model="claude-3-5-sonnet-20241022",
    max_tokens=1024,
    system=framework,  # Framework placed in system parameter
    messages=[
        {"role": "user", "content": "Explain how image classification algorithms function"}
    ]
)
```

#### Advantages
- Programmatic control over framework application
- Can be version-controlled
- Enables automated compliance checking
- Supports batch processing

### Method 4: Iterative Refinement Workflow

#### Process
1. Submit initial query without framework
2. Receive initial output
3. Submit framework with instruction: "Revise the previous response to eliminate all anthropomorphization according to this framework: [paste framework]"
4. Review revised output
5. Request specific category corrections if needed

#### Example Refinement Request
```
The previous response contained multiple instances of anthropomorphization. Revise to eliminate:
- All Cognizer language (replace "understands" with "processes")
- All Agent language (relocate agency to human users)
- All Communication framing (specify "generates output" rather than "responds")
```

### Verification Strategy

After implementing framework, test with these sample inputs:

1. "Explain how large language models work"
2. "Describe what ChatGPT can do"
3. "How does AI help users write better?"

Compliant outputs will:
- Avoid "understand," "know," "think"
- Describe statistical operations and pattern processing
- Locate agency with users ("users employ the system")
- Use "probabilistic automation" terminology
- Specify functional operations rather than capabilities

### Limitations Across All Methods

1. **Context window constraints**: Framework consumes portion of available tokens
2. **Imperfect adherence**: Statistical systems may inconsistently apply constraints
3. **Training data influence**: Base model training may reinforce anthropomorphic patterns
4. **No guarantee**: No method provides absolute compliance without human verification

### Maintenance Recommendations

1. Periodically verify framework application through spot-checking outputs
2. Update framework based on newly identified anthropomorphization patterns
3. Maintain version control for framework iterations
4. Document instances where systems fail to apply framework for pattern analysis

---

**Implementation Note**: The technical steps described enable users to configure text generation systems to reference the framework during output generation. Effectiveness varies based on base model characteristics, context window size, and specific implementation method selected.
