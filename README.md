EcoVerify is a research project exploring whether retrieval-augmented generation (RAG) improves the reliability and traceability of environmental metric extraction from long, unstructured corporate reports. Developed as a final-year undergraduate project at Keele University, it compares prompt-based and retrieval-augmented configurations of GPT-4o Mini and Qwen2.5-1.5B-Instruct.
The key finding was that access to evidence improves extraction coverage but evidence grounding does not guarantee correctness.

# Research question
How does retrieval augmentation affect the accuracy, completeness and faithfulness of LLM-based environmental metric extraction?
Approach
The study uses a corpus of 100 FTSE 100 sustainability reports and a modular pipeline:
1. Extract report text from PDFs, using OCR where required.
2. Segment text into searchable chunks with source metadata.
3. Combine BM25 lexical retrieval with embedding-based semantic retrieval and FAISS similarity search.
4. Supply relevant passages to the language model for structured metric extraction.
5. Present extracted values with supporting source evidence for verification.


# Evaluation
Model	Prompt-based	Retrieval-augmented
GPT-4o Mini	Baseline extraction	Extraction using retrieved report context
Qwen2.5-1.5B-Instruct	Baseline extraction	Extraction using retrieved report context

Evaluation covers disclosure detection, precision, recall, F1, exact match, numeric match, unit match, faithfulness, retrieval hit rate, mean reciprocal rank and latency.

# Results
- Retrieval improved recall and output faithfulness relative to the evaluated prompt-based configurations.
- Improved coverage was accompanied by false positives and incorrect numerical values.
- Correctly identifying a disclosure did not necessarily produce the correct value, unit or complete structured output.
- Source-linked outputs remained vulnerable to parsing errors, fragmented context and ambiguous retrieved passages.



A proposed human–AI interaction study would compare passive citation presentation with interfaces that encourage active source verification. It would examine error detection and reliance on AI-generated outputs. This extension has not yet been evaluated.
d Qwen2.5-1.5B-Instruct.
