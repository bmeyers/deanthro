# deanthro
_A framework for "de-anthropomorphizing" the text outputs of large language models_

This markdown file instructs large language models and chat simulators to use **functionality-first** language when generating outputs. Below shows the response of `claude-4-5-sonnet` with and without these instructions included in the model "memory" (automatic prompt injection on every query, increasing token use rate). 

This is an implementation of the paper, [De-anthropomorphizing “AI”: From wishful mnemonics to accurate nomenclature](https://doi.org/10.5210/fm.v31i2.14366), by Nanna Inie, Peter Zukerman, and Emily M. Bender.

I used `claude-4-5-sonnet` to generate and inital markdown file based on the paper, essentially a text transformation and summary task. I then edited the resulting markdown based on my understanding of the paper.

**with de-anthropomorphizing framework:**
<img width="699" height="502" alt="Screenshot 2026-04-20 at 10 14 01 AM" src="https://github.com/user-attachments/assets/48b5cc49-a071-4f6a-b10f-61cf93722a4e" />

**without framework:**
<img width="701" height="386" alt="Screenshot 2026-04-20 at 10 13 50 AM" src="https://github.com/user-attachments/assets/28f7b3aa-86b4-418f-a53b-d9e9a35bd2f0" />
