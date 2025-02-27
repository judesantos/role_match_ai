# Job Search Assistant

## Overview
The Job Search Assistant is an intelligent job-matching application that utilizes **Azure OpenAI (AzureChatOpenAI)** and **CrewAI** to analyze resumes, search for job postings, and rate job opportunities. The application integrates job search APIs like **Jooble** and **Glassdoor** to retrieve job listings and provides structured evaluations based on user-submitted resumes and job preferences.

## Features
- **Resume Analysis**: Extracts and processes key information from uploaded resumes.
- **Job Search API Integration**: Fetches job listings from **Jooble** and **Glassdoor**.
- **AI-Powered Job Matching**: Uses **CrewAI agents** to analyze job postings and match them to resumes.
- **Company Evaluation**: Retrieves and rates companies based on relevant factors.
- **Flask Web API**: Accepts job search parameters such as keywords, job location, and resume files.
- **Structured JSON Output**: Provides well-formatted results for easy integration.

## Tech Stack
- **Backend**: Python, Flask
- **AI Models**: Azure OpenAI (AzureChatOpenAI)
- **Orchestration**: CrewAI
- **Job Search APIs**: Jooble, Glassdoor
- **Data Processing**: Python, Pandas

## Project Structure
```
├── README.md
├── data
│   ├── resumes
│   │   └── Professional Resume - 2025.docx.txt
│   ├── sample_jobs.json
│   ├── sample_result.json
│   └── sample_resume.txt
├── environment.yml
├── requirements.txt
├── src
│   ├── agent.py          # CrewAI agents for job search & evaluation
│   ├── config
│   │   ├── agents.yml    # Configuration for AI agents
│   │   └── tasks.yml     # Task definitions for job search & rating
│   ├── main.py          # Main execution script
│   ├── models
│   │   └── models.py    # AI model configurations
│   ├── services
│   │   ├── jooble.py    # Jooble API integration
│   │   └── search_jobs.py # Job search functions
│   ├── tasks.py         # Job-related task execution
│   └── utils
│       ├── parser.py    # Resume parsing utilities
│       └── utils.py     # Helper functions
└── web
    ├── app.py          # Flask Web API
    ├── static
    │   └── css
    │       └── styles.css
    └── templates
        ├── index.html   # Search input page
        └── results.html # Job search results page
```

## Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/judesantos/job_search_assistant.git
   cd job-search-assistant
   ```
2. **Set up the Miniconda environment**:
   ```bash
   conda env create -f environment.yml
   conda activate job-search-assistant
   ```
3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
4. **Set up environment variables**:
   - Create a `.env` file in the root directory and use `.env.development` as a guide. Add the following entries:
     ```
     SERPER_API_KEY=<signup_for_a_free_serper_api_key>

     JOOBLE_HOST=<signup_for_a_free_jooble_api_key>
     JOOBLE_API_KEY=<the_jooble_api_key>

     AZURE_OPENAI_ENDPOINT=<the_azure_openai_endpoint_in_your_azure_account>
     AZURE_OPENAI_KEY=<the_azure_openai_key_in_your_azure_account>
     OPENAI_API_VERSION=<the_openai_api_version_in_your_azure_account>
     ```

## Usage
### Running the Web API
```bash
python -m web.app
```
Access the web app at: [http://127.0.0.1:5000](http://127.0.0.1:5000)

### Running Job Search & Rating via CLI
```bash
python src/main.py --resume data/resumes/sample_resume.txt --keywords "Software Engineer" --location "New York"
```

## API Endpoints
### 1. **Upload Resume & Search Jobs**
   - **Endpoint:** `/search`
   - **Method:** `POST`
   - **Parameters:**
     - `resume` (file)
     - `keywords` (string)
     - `location` (string)
   - **Response:** JSON object containing job listings and ratings.

### 2. **Fetch Job Search Results**
   - **Endpoint:** `/results`
   - **Method:** `GET`
   - **Response:** JSON object with job listings and evaluations.

## JSON Output Format
```json
{
  "jobs": [
    {
      "id": "12345",
      "location": "New York",
      "title": "Software Engineer",
      "company": "TechCorp",
      "description": "Exciting opportunity for a software engineer...",
      "provider": "Glassdoor",
      "url": "https://example.com/job12345",
      "rating": 9,
      "rating_notes": "Matches skills and experience closely.",
      "company_rating": 8,
      "company_notes": "Well-rated company with growth opportunities."
    }
  ]
}
```

## Future Enhancements
- **Add more job search sources (LinkedIn, Indeed, etc.)**
- **Improve AI matching using deep learning models**
- **Enhance Flask UI for better user experience**

## Contributors
- **Your Name** ([@yourgithub](https://github.com/yourgithub))

## License
This project is licensed under the MIT License.

