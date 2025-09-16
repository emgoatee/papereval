# Pediatric Surgery Paper Evaluation Tool

A Streamlit app that **scores and ranks research articles** for pediatric surgery using a weighted composite of five factors:

- **Relevance** — keyword match score.
- **Journal quality (NHI)** — **Normalized H-Index** by journal with fuzzy matching for journal names.
- **Recency** — higher scores for newer publication years.
- **Study design** — fuzzy-matched design keywords mapped to evidence-level scores.
- **Statistical strength** — lowest p-value mentioned in the abstract mapped to a score.

The tool ingests an Excel file of articles and computes a **Total Score** per row to help you triage literature quickly.

## Usage

1. Place support files in `resources/`:
   - `resources/normalized_h_index.xlsx`
   - `resources/keyword_relevance.xlsx`
2. Run:
   ```bash
   pip install -r requirements.txt
   streamlit run app.py
   ```
3. Upload an Excel file with columns: `Title`, `Abstract`, `Publication Year`, `Journal`.
4. Review the scored table in the app.

## Dependencies

Key Python libraries used (see requirements.txt):
- streamlit – interactive web interface
- pandas – data manipulation
- openpyxl – Excel file handling
- PyPDF2 – PDF parsing support
- python-docx – Word report generation
- fuzzywuzzy + python-Levenshtein – fuzzy keyword matching

## Notes

- Journal names are fuzzily matched to improve robustness; unmatched journals default to **NHI = 0** (a warning is shown).
- Missing years default **Recency = 3**; missing abstracts default **p-value score = 5** and **Study Design = 0**.
- All text fields are coerced to string to prevent errors on NaNs.

## Project Structure

```
.
├── app.py                    # Main Streamlit app
├── requirements.txt          # Python dependencies
├── resources/
│   ├── normalized_h_index.xlsx   # Journal-level Normalized H-Index data
│   └── keyword_relevance.xlsx    # Keyword → relevance weight mapping
└── README.md                 # Project documentation
```

## License

This project is licensed under the [MIT License](LICENSE).
