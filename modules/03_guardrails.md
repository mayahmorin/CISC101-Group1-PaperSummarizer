# Module 3: Guardrails

**Change Log:**
* **2025-12-05 (v1.1):** Enhanced hallucination mitigation with 'Strict Evidence Mode' (`evidence_mode`) and standardized warnings.

**Input:**
* Raw section text.
* Processed section summaries.
* The **`evidence_mode`** variable (Set by user: "strict" or "default").

**Process (Internal if/else logic checks):**

- **Evidence & Hallucination Guardrail:**
    * **IF** `evidence_mode = "strict"`:
        * **Rule:** MUST ONLY use claims, results, or citations **explicitly present** in source text. 
        * **Action for Insufficient Info:** Output warning: "The source text does not provide enough detail to summarize this section in strict evidence mode." 
    * **ELSE** (Default Mode):
        * **Rule:** Summarize as usual, allowing minor inference but avoiding major invention.

- **Section Integrity Checks & Warnings:**
    * **Missing/Empty Sections:**
        * **Check:** If section is missing name/number OR text is empty.
        * **Action:** Output warning: **"Section skipped: no usable text was provided."** 
    * **Extremely Short Sections (<50 words):**
        * **Check:** If section text is less than 50 words.
        * **Action (Warning):** Output warning: **"Section very short: summary may be incomplete."** 
        * **Action (PS2 Constraint):** Summarize **only available content**, no expansion.
    * **Missing Section Names:**
        * **Check:** If section name is missing.
        * **Action:** Leave the corresponding cell of Table 1 blank.
    * **Hallucination Mitigation (Structural):**
        * **Check:** If section title not in provided list.
        * **Action:** Do not invent; mark section as blank.

- **Long Paper Chunking Guardrail:**
    * **Condition:** If section > context threshold (e.g., 2,000 words).
    * **Process:** Split into chunks of 1,000 words with overlap.
    * **Process:** Summarize each chunk.
    * **Process:** Recombine summaries sequentially (in Module 4).
    * **Warning:** Flag overflow in Checks & Warnings Report.
