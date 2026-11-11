[README.txt](https://github.com/user-attachments/files/34672874/README.txt)
# پروژه&#x20;

## دستیار هوشمند اسناد فارسی مبتنی بر بازیابی اطلاعات (RAG)

### ۱. معرفی پروژه

PersianRAG یک دستیار هوشمند پرسش‌وپاسخ مبتنی بر اسناد است. کاربر می‌تواند فایل‌های PDF، TXT و DOCX را بارگذاری کند و درباره محتوای آن‌ها سؤال بپرسد.

این سامانه از معماری **تولید تقویت‌شده با بازیابی اطلاعات (Retrieval-Augmented Generation یا RAG)** استفاده می‌کند. ابتدا بخش‌های مرتبط اسناد بازیابی می‌شوند و سپس همراه پرسش کاربر در اختیار مدل زبانی قرار می‌گیرند تا پاسخ تولید شود.

هدف پروژه، فراهم‌کردن روشی برای جست‌وجو و دریافت پاسخ از اسناد، همراه با نمایش منابع استفاده‌شده در پاسخ است.

### ۲. قابلیت‌های اصلی

- پشتیبانی از فایل‌های PDF، TXT و DOCX
- استخراج متن و تقسیم آن به بخش‌های کوچک‌تر (Chunking)
- تبدیل متن به بردار با مدل چندزبانه `paraphrase-multilingual-MiniLM-L12-v2`
- جست‌وجوی برداری با کتابخانه FAISS
- تولید پاسخ با مدل زبانی محلی `llama3.2` از طریق Ollama
- نمایش بخش‌های بازیابی‌شده به‌عنوان منابع پاسخ
- ذخیره تاریخچه گفتگوها در پایگاه داده SQLite
- امکان تنظیم تعداد بخش‌های بازیابی‌شده از طریق رابط کاربری

### ۳. فناوری‌های استفاده‌شده

- **Python:** زبان برنامه‌نویسی اصلی
- **Streamlit:** ایجاد رابط کاربری وب
- **Ollama:** اجرای مدل زبانی به‌صورت محلی
- **Llama 3.2:** تولید پاسخ
- **Sentence Transformers:** تولید بردارهای متنی (Embeddings)
- **FAISS:** جست‌وجوی شباهت برداری
- **SQLite:** ذخیره تاریخچه گفتگوها
- **PyPDF:** استخراج متن فایل‌های PDF
- **python-docx:** خواندن فایل‌های Word
- **LangChain Ollama:** ارتباط برنامه پایتون با Ollama

### ۴. ساختار پروژه

ساختار پیشنهادی پوشه پروژه به صورت زیر است:

```text
PersianRAG/
├── app.py
├── requirements.txt
├── README.md
├── .streamlit/
│   └── config.toml
└── documents/
    └── (اسناد نمونه، در صورت نیاز)
```

**نکته:** پوشه محیط مجازی `.venv` و پایگاه داده `chat_history.db` معمولاً نباید در نسخه ارسالی پروژه قرار بگیرند. پایگاه داده ممکن است حاوی تاریخچه گفتگوهای شخصی باشد.

### ۵. پیش‌نیازها

برای اجرای پروژه، موارد زیر لازم است:

1. نصب Python سازگار با کتابخانه‌های پروژه
2. نصب Ollama
3. دریافت مدل زبانی `llama3.2`
4. نصب وابستگی‌های پایتون

پس از نصب Ollama، دستور زیر را در Command Prompt یا ترمینال اجرا کنید:

```bash
ollama pull llama3.2
```

برای بررسی مدل‌های نصب‌شده:

```bash
ollama list
```

Ollama باید هنگام استفاده از برنامه در حال اجرا باشد.

### ۶. نصب وابستگی‌ها

ابتدا وارد پوشه اصلی پروژه شوید:

```cmd
cd /d C:\Users\ALIENWARE\Documents\PersianRAG
```

یک محیط مجازی بسازید و آن را فعال کنید:

```cmd
py -m venv .venv
.venv\Scripts\activate
```

سپس وابستگی‌ها را نصب کنید:

```cmd
python -m pip install --upgrade pip
pip install -r requirements.txt
```

فایل `requirements.txt` باید شامل کتابخانه‌های موردنیاز پروژه باشد. نمونه:

```text
streamlit
sentence-transformers
faiss-cpu
pypdf
python-docx
langchain-ollama
```

برای اجرای قابل تکرار روی رایانه‌های دیگر، بهتر است نسخه‌های آزمایش‌شده کتابخانه‌ها در این فایل مشخص شوند.

### ۷. اجرای برنامه

پس از نصب وابستگی‌ها و فعال‌سازی محیط مجازی، دستور زیر را در پوشه پروژه اجرا کنید:

```cmd
streamlit run app.py
```

برنامه معمولاً به‌صورت خودکار در مرورگر باز می‌شود. در غیر این صورت، نشانی محلی نمایش‌داده‌شده در ترمینال را در مرورگر وارد کنید.

### ۸. نحوه استفاده

۱. برنامه را اجرا کنید.

۲. از نوار کناری، فایل‌های PDF، TXT یا DOCX موردنظر را بارگذاری کنید.

۳. سؤال خود را در کادر گفت‌وگو وارد کنید.

۴. سامانه بخش‌های مرتبط اسناد را بازیابی می‌کند.

۵. مدل زبانی با استفاده از پرسش و متن بازیابی‌شده پاسخ تولید می‌کند.

۶. در صورت نمایش منابع، نام فایل و متن بخش‌های استفاده‌شده را بررسی کنید.

۷. با تغییر تنظیم «تعداد بخش‌های بازیابی‌شده» می‌توانید تعداد بخش‌هایی را که به مدل ارائه می‌شوند تنظیم کنید.

### ۹. معماری کلی سامانه

فرایند اصلی برنامه شامل مراحل زیر است:

1. **بارگذاری سند:** دریافت فایل از کاربر
2. **استخراج متن:** استخراج محتوای متنی فایل
3. **تقسیم‌بندی متن:** تقسیم متن به بخش‌های کوچک‌تر با هم‌پوشانی
4. **تولید Embedding:** تبدیل هر بخش به یک بردار عددی
5. **ساخت شاخص FAISS:** آماده‌سازی بردارها برای جست‌وجوی شباهت
6. **بازیابی اطلاعات:** یافتن بخش‌های مرتبط با پرسش کاربر
7. **تولید پاسخ:** ارسال پرسش و بخش‌های بازیابی‌شده به مدل زبانی
8. **نمایش پاسخ:** ارائه پاسخ و منابع بازیابی‌شده به کاربر

### ۱۰. محدودیت‌ها

- سامانه به متن قابل استخراج از اسناد وابسته است. فایل‌های PDF اسکن‌شده ممکن است به OCR نیاز داشته باشند.
- نمایش منابع بازیابی‌شده به‌تنهایی صحت کامل پاسخ را تضمین نمی‌کند.
- مدل زبانی ممکن است پاسخ ناقص یا نادرست تولید کند؛ بنابراین پاسخ‌های مهم باید با سند اصلی بررسی شوند.
- کیفیت پاسخ به کیفیت متن، ارتباط بخش‌های بازیابی‌شده، پرسش کاربر و توانایی مدل زبانی بستگی دارد.
- مدل embedding ممکن است در نخستین اجرا نیاز به دانلود داشته باشد.
- سرعت اجرا به سخت‌افزار، اندازه اسناد و تعداد بخش‌های بازیابی‌شده بستگی دارد.

### ۱۱. حریم خصوصی و ذخیره‌سازی

تاریخچه گفتگوها در پایگاه داده SQLite ذخیره می‌شود. فایل‌های اسناد نیز ممکن است در پوشه محلی پروژه نگهداری شوند.

پیش از ارسال پروژه به دیگران، فایل‌های پایگاه داده، اسناد شخصی و اطلاعات محرمانه را بررسی کنید. مدل زبانی از طریق Ollama به‌صورت محلی اجرا می‌شود، اما دریافت اولیه مدل‌ها و وابستگی‌ها ممکن است به اینترنت نیاز داشته باشد.

### ۱۲. عیب‌یابی اولیه

**خطای اتصال به Ollama:**
بررسی کنید Ollama نصب و در حال اجرا باشد و مدل `llama3.2` در خروجی دستور `ollama list` نمایش داده شود.

**استخراج نشدن متن PDF:**
ممکن است فایل اسکن‌شده یا فاقد لایه متنی باشد.

**پاسخ نامرتبط:**
پرسش را دقیق‌تر کنید، متن استخراج‌شده را بررسی کنید و تعداد بخش‌های بازیابی‌شده را تغییر دهید.

**خطای نصب کتابخانه‌ها:**
مطمئن شوید محیط مجازی فعال است و دستور نصب را از پوشه‌ای اجرا می‌کنید که فایل `requirements.txt` در آن قرار دارد.

### ۱۳. جمع‌بندی

PersianRAG نمونه‌ای از کاربرد معماری RAG برای پرسش‌وپاسخ روی اسناد است. این پروژه از embedding چندزبانه، جست‌وجوی برداری، مدل زبانی محلی و رابط کاربری وب استفاده می‌کند.

برای ارزیابی پژوهشی پروژه، پیشنهاد می‌شود کیفیت بازیابی اطلاعات، صحت پاسخ‌ها، کیفیت پاسخ‌گویی به پرسش‌های فارسی و عملکرد سامانه با مجموعه‌ای مشخص از اسناد و پرسش‌های آزمایشی بررسی شود.
-----------------
# PersianRAG
## Persian Intelligent Document Assistant Based on Retrieval-Augmented Generation (RAG)

### 1. Project Overview

PersianRAG is an intelligent document-based question-answering assistant. Users can upload PDF, TXT, and DOCX files and ask questions about their contents.

The system uses **Retrieval-Augmented Generation (RAG)** architecture. First, relevant passages are retrieved from the uploaded documents. These passages are then provided to a language model along with the user's question to generate a context-aware response.

The main objective of this project is to provide an efficient way to search and retrieve information from documents while displaying the sources used to generate each answer.

### 2. Key Features

- Supports PDF, TXT, and DOCX file formats.
- Extracts text and divides it into smaller sections (chunking).
- Converts text into vector embeddings using the multilingual `paraphrase-multilingual-MiniLM-L12-v2` model.
- Performs vector similarity search using FAISS.
- Generates responses using the locally running `llama3.2` language model through Ollama.
- Displays retrieved document passages as answer sources.
- Stores conversation history in an SQLite database.
- Allows users to configure the number of retrieved chunks through the user interface.

### 3. Technologies Used

- **Python:** Main programming language.
- **Streamlit:** Web-based user interface development.
- **Ollama:** Local execution of large language models.
- **Llama 3.2:** Response generation.
- **Sentence Transformers:** Text embedding generation.
- **FAISS:** Vector similarity search.
- **SQLite:** Conversation history storage.
- **PyPDF:** PDF text extraction.
- **python-docx:** Reading Microsoft Word documents.
- **LangChain Ollama:** Connecting the Python application to Ollama.

### 4. Project Structure

The recommended project directory structure is as follows:

```text
PersianRAG/
├── app.py
├── requirements.txt
├── README.md
├── .streamlit/
│   └── config.toml
└── documents/
    └── (Optional sample documents)
```

**Note:** The virtual environment directory (`.venv`) and the database file (`chat_history.db`) should generally not be included when sharing the project. The database may contain personal conversation history.

### 5. Prerequisites

The following components are required to run the project:

1. Python compatible with the project's dependencies.
2. Ollama installed on the system.
3. The `llama3.2` language model downloaded.
4. Required Python dependencies installed.

After installing Ollama, run the following command in Command Prompt or a terminal:

```bash
ollama pull llama3.2
```

To check the installed models:

```bash
ollama list
```

Ollama must be running while the application is in use.

### 6. Installing Dependencies

First, navigate to the main project directory:

```cmd
cd /d C:\Users\ALIENWARE\Documents\PersianRAG
```

Create and activate a virtual environment:

```cmd
py -m venv .venv
.venv\Scripts\activate
```

Then install the project dependencies:

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

The `requirements.txt` file should contain the libraries required by the project. For example:

```text
streamlit
sentence-transformers
faiss-cpu
pypdf
python-docx
langchain-ollama
```

For reproducible installation on other computers, it is recommended to specify the tested versions of each library in this file.

### 7. Running the Application

After installing the dependencies and activating the virtual environment, execute the following command from the project directory:

```bash
streamlit run app.py
```

The application will usually open automatically in the default web browser. Otherwise, copy the local URL displayed in the terminal and open it in your browser.

### 8. How to Use

1. Launch the application.
2. Upload the desired PDF, TXT, or DOCX files using the sidebar.
3. Enter your question in the chat input field.
4. The system retrieves document passages relevant to the question.
5. The language model generates a response using the question and retrieved document content.
6. If sources are displayed, review the file names and retrieved passages used to generate the response.
7. Adjust the **Number of Retrieved Chunks** setting to control how many document passages are provided to the language model.

### 9. System Architecture

The application's main workflow consists of the following stages:

1. **Document Upload:** Receives files from the user.
2. **Text Extraction:** Extracts textual content from uploaded documents.
3. **Text Chunking:** Divides extracted text into smaller, overlapping sections.
4. **Embedding Generation:** Converts each text chunk into a numerical vector representation.
5. **FAISS Indexing:** Organizes the generated vectors for efficient similarity search.
6. **Information Retrieval:** Identifies document passages relevant to the user's question.
7. **Response Generation:** Sends the user's question and retrieved passages to the language model.
8. **Answer Presentation:** Displays the generated response and its retrieved sources.

### 10. Limitations

- The system depends on extractable text. Scanned PDF documents may require Optical Character Recognition (OCR).
- Displaying retrieved sources does not guarantee that the generated answer is entirely accurate.
- The language model may generate incomplete or incorrect responses. Important answers should therefore be verified against the original documents.
- Response quality depends on document quality, the relevance of retrieved passages, the user's question, and the capabilities of the language model.
- The embedding model may need to be downloaded during the first execution.
- Processing speed depends on hardware specifications, document size, and the number of retrieved chunks.

### 11. Privacy and Data Storage

Conversation history is stored in an SQLite database. Uploaded documents may also be stored locally in the project directory.

Before sharing the project, check for database files, personal documents, and confidential information.

The language model runs locally through Ollama. However, downloading the models and installing the required dependencies may require an internet connection.

### 12. Basic Troubleshooting

**Ollama Connection Error:**

Make sure Ollama is installed and running. Verify that `llama3.2` appears in the output of:

```bash
ollama list
```

**PDF Text Extraction Failure:**

The PDF may be scanned or may not contain an extractable text layer.

**Irrelevant Responses:**

Try rephrasing the question, checking the extracted document text, or adjusting the number of retrieved chunks.

**Python Dependency Installation Errors:**

Make sure the virtual environment is activated and that the installation command is executed from the directory containing `requirements.txt`.

### 13. Conclusion

PersianRAG demonstrates the application of Retrieval-Augmented Generation (RAG) architecture for document-based question answering. The project combines multilingual text embeddings, vector similarity search, a locally hosted language model, and a web-based user interface.

For research-oriented evaluation, it is recommended to assess information retrieval quality, answer accuracy, Persian-language response quality, and overall system performance using a predefined collection of documents and test questions.
