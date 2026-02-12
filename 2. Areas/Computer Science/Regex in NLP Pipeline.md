**Tags:** #concept #nlp
**Related:** [[Regular Expressions (Regex)]], [[NLP Preprocessing]]

## Definition
In an NLP pipeline, regular expressions are used in the early stages to clean and structure raw text before it is passed to statistical or neural models.

## Usage in Pipeline
Regular expressions typically appear in:

1. **Data Cleaning**: Removing HTML tags, noise, or irrelevant metadata (e.g., removing `<p>` tags).

2. **Preprocessing**: Normalizing whitespace, dates, or prices into a standard format.
   
3. **Feature Preparation**: Extracting specific identifiers (emails, URLs, IDs) or protecting certain tokens from being broken during tokenization.

### Python Implementation
In Python, this is primarily handled by the `re` module:
```python
import re

text = "<p>Pay €1,249.50 now</p>"
clean_text = re.sub(r'<[^>]+>', '', text) # Removes tags
price = re.search(r'€[\d,.]+', text).group() # Extracts price
```

## Significance
Regex represents the point at which text stops being prose and starts becoming an object of computation. While models like Transformers are powerful, they often presuppose clean, normalized data, making regex a foundational "pipeline protection" tool.
