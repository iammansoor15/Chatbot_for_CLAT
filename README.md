# Personalized CLAT FAQ Chatbot - Approach Documentation

## **Requirements**
1. **Python 3.7 or higher**
2. **spaCy**
3. **rapidfuzz**

---

## **1. Data Creation**
- The FAQ data was manually curated and compiled from the following official and trusted sources:
  - [Careers360 - CLAT FAQs](https://law.careers360.com/articles/clat-faqs)
  - [Consortium of NLUs - CLAT 2025 FAQs](https://consortiumofnlus.ac.in/clat-2025/FAQs.html)
- These sources cover a wide range of topics such as:
  - CLAT eligibility, registration, syllabus, exam dates, and format
  - Cutoffs, seat allotment, and reservation categories
  - Post-exam processes and NLU-specific info
- The extracted question-answer pairs were cleaned and structured into a Python dictionary (`clat_faqs`) to serve as the core knowledge base for the chatbot.

---

## **2. Data Loading**
- The system loads a dictionary `clat_faqs` containing common CLAT-related questions as keys and their answers as values.
- A list of all FAQ keys (`faq_questions`) is created to compare against user input.

---

## **3. Text Preprocessing (Optional but Recommended)**
- Uses **spaCy** to process user input:
  - Lowercase the text  
  - Remove stop words and punctuation  
  - Lemmatize tokens  
  - Extract entities (e.g., "CLAT 2025", "NLSIU", etc.)  
- This step ensures cleaner and more accurate fuzzy matching.

---

## **4. User Input Matching (Fuzzy Search)**
- The user enters a free-form question via CLI.
- `rapidfuzz.process.extractOne()` compares the user input with all FAQ questions using `token_sort_ratio` scoring.
- If the highest score exceeds a threshold (typically 50 or 60), it is considered a match.

---

## **5. Chat Loop with Exit Condition**
- The chatbot runs in a continuous loop until the user types "exit".
- For each input:
  - The chatbot fetches the closest matching FAQ.
  - Returns the corresponding answer from `clat_faqs`.
  - If no good match is found, it asks the user to rephrase.

---

## **6. Limitations & Future Scope**
- **Add synonym support** – Understand variations like "exam schedule" and "test date" as the same intent.
- **Use spaCy NER** – Detect useful info like exam year, college names, or scores from user questions.
- **Load FAQs from a JSON file** – Makes it easier to update FAQs without changing the code.
- **Build a web version** – Convert it into a user-friendly web app using Flask or Streamlit.
- **Allow feedback** – Let users mark helpful/unhelpful answers to improve the bot over time.
