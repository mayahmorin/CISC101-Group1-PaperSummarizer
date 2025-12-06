# Module 2: Section Loop

**Change Log:**
* **2025-12-05:** Added conditional logic for 'Summary Level' mode (`summary_level`) to support 'short' (1-2 sentences) and 'detailed' (paragraph + bullet points) summaries per section.

**Input:**
* Normalized list of paper sections and their corresponding text.
* The **`summary_level`** variable (Set by the user: "short" or "detailed"). (Required for 0.5 Marks)

For each section:
- **Summary Generation (Conditional Logic):** For each section, determine the output structure:
    * **IF** `summary_level = "short"`:
        * Generate a compact, 1–2 sentence summary.
    * **ELSE IF** `summary_level = "detailed"`:
        * Generate a short paragraph summary.
        * **PLUS** a bullet list of 3–5 key points. (Required for 1.0 Marks combined)

- **Formatting & Constraints:**
    * **Length Constraint:** Ensure the summary is ≤175 words (Total length for paragraph + bullet points).
    * **Style:** Bold main points, italicize key details.
- **Storage:** Store results in Table 1.

**Output:** A summary object for each section.
