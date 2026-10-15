# EcoVerify
EcoVerify investigates whether retrieval-augmented generation (RAG) can improve the reliability and traceability of environmental metric extraction from long, unstructured corporate reports.

The study compares prompt-based and retrieval-augmented configurations of GPT-4o Mini and Qwen2.5-1.5B-Instruct using a corpus of 100 FTSE 100 sustainability reports.

It was found that retrieval can improve access to relevant evidence and extraction coverage but evidence-grounded outputs may still hold incorrect values, units and false positives.

## Introduction
Corporate sustainability reports contain environmental disclosures across narrative text, tables and inconsistent reporting formats. Extracting comparable metrics requires identifying the right disclosure and preserving its numerical value, unit and context.
EcoVerify examines both whether a model finds a disclosure and whether it extracts it correctly. Source evidence supports verification, but its presence alone does not ensure accuracy.

## Research Aims
• To design and evaluate a transparent AI system capable of extracting verifiable environmental performance metrics from corporate sustainability reports using Llama-3.

• To enhance model transparency by ensuring every extracted metric is traceable to its
original textual evidence

### Approach
The pipeline combines document processing, hybrid retrieval and structured extraction:
1. Parse reports: Extract text from PDFs, using OCR where required.
2. Prepare evidence: Segment text into searchable chunks while retaining source metadata.
3. Retrieve passages: Combine BM25 lexical retrieval with embedding-based semantic retrieval and FAISS similarity search.
4. Extract metrics: Supply retrieved passages to the language model for structured metric extraction.
5. Support verification: Present extracted values alongside supporting source evidence.

## Experimental design
Both GPT-4o Mini and Qwen2.5-1.5B-Instruct were evaluated in two configurations:
- Prompt-based: Baseline extraction without retrieved report context.
- Retrieval-augmented: Extraction using relevant passages retrieved from the reports.
The comparison evaluates the configurations used in this study; it does not establish the performance of every possible prompting or retrieval strategy.

## Evaluation
- Disclosure detection: Precision, recall and F1 measure recovered disclosures, missed disclosures and false positives.
- Structured extraction: Exact match, numeric match and unit match assess the correctness of extracted values and measurement context.
- Evidence grounding: Faithfulness assesses whether outputs are supported by retrieved evidence.
- Retrieval quality: Hit rate and mean reciprocal rank assess whether relevant evidence is retrieved and ranked highly.
- Efficiency: Latency measures processing time.

## Results
Disclosure detection
Retrieval substantially improved recall and F1 relative to the evaluated prompt-based configurations. The report gives the following approximate results:
- GPT-4o Mini: Recall increased from 0.00 to approximately 0.70, and F1 increased from 0.00 to approximately 0.70 with RAG.
- Qwen2.5-1.5B-Instruct: Recall increased from 0.00 to approximately 0.49, and F1 increased from 0.00 to approximately 0.56 with RAG.
These are disclosure-detection results, rather than measures of fully correct numerical extraction. In the evaluated setup, prompt-based configurations predominantly returned negative predictions, failing to recover positive disclosures.

Figure 1 — model performance comparison
<img width="566" height="313" alt="image" src="https://github.com/user-attachments/assets/6562feae-e9f7-4230-8533-599637b20ea2" />


## Error Trade-offs
- RAG improved recall and output faithfulness, reducing missed disclosures.
- Greater coverage was accompanied by false positives and incorrect numerical values.
- Identifying a disclosure did not guarantee the correct value, unit or complete structured output.
- Errors shifted from missed disclosures towards incorrect extraction from retrieved context.

Figure 2.a — confusion matrices
<img width="385" height="316" alt="image" src="https://github.com/user-attachments/assets/514c3ac9-0813-449a-aa30-09dacaa995b6" />


Figure 2.b — structured extraction
<img width="413" height="296" alt="image" src="https://github.com/user-attachments/assets/bde47210-0826-4e28-a2bf-88b0e59c39a0" />


Figure 2.c — error analysis
<img width="406" height="248" alt="image" src="https://github.com/user-attachments/assets/3e2897a7-1095-46f0-9644-a5177812d67a" />


## Limitations
- Retrieval quality constrains extraction. Partially relevant passages, fragmented context and PDF parsing errors can propagate into generated outputs.
- Grounding and correctness are distinct. An answer may be supported by a retrieved passage while misinterpreting its value, unit or reporting context.
- Match-based scores require care. The report identifies that matching negative or “NOT FOUND” outputs can inflate match rates. Excluding these cases or evaluating only positive disclosures was not implemented, so these scores should be interpreted alongside recall and F1.
- Findings are configuration-specific. Results reflect the selected models, report corpus, prompts and retrieval setup.
  
## Implications and future work
EcoVerify highlights the gap between traceability and reliability. Grounding outputs in available evidence is a useful foundation for oversight however further validation is needed to establish whether a claims are correct.

Potential extensions may include:
- Table-aware parsing and retrieval that preserve numerical context.
- Validation of values, units and reporting periods before presenting an extraction.
- Evaluation restricted to positive disclosures to clarify structured extraction performance.
- A human–AI interaction study testing whether interfaces that encourage active source verification improve error detection compared with passive citations.

