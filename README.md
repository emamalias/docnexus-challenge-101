# docnexus-challenge-101
Search engine for medical conferences.

### The challenge
Extract data from different sources for medical conferences.
Build a system to extract and index data from hundreds of thousands of medical conferences, including websites, PDFs, and session details.

These 2 websites have the names of all the Conferences:
- https://www.symplur.com/healthcare-hashtags/conferences/
- https://www.astellas.com/me/system/files/pre-approved_global_congress_list_2023_website.pdf

It would then need to search and find the sites and scrape the conference websites for session details and speakers, and extract structured data from unstructured sources like PDFs. It should also handle inconsistent formats, especially PDFs, to accurately parse and extract key information.

Goal is to build a fast, intuitive search engine allowing users to filter by session, speaker, year and topic across conferences. Design a system that can manage and update data from a massive, constantly growing dataset.

### Stacks (open source)
- **Back-end**: Laravel
- **Front-end**: NextJS
- **Database**: PostgreSQL
- **Search Engine**: Meilisearch
- **Crawling/Scraping**: Puppeter
- **Data Parsing**: Unstract

### The design solution

1. Data Collection Pipeline
   - Website Crawling & Scraping:
     - Use **Puppeter** tool for web scraping. These tool can crawl websites listed on the sources you provided (**Symplur** and **Astellas**) and extract relevant links.
     - Extract structured data such as session **titles**, **dates**, **speakers**, and **topics** directly from HTML content.
   - PDF or other documents (screenshot, images) Parsing:
     - PDFs and other documents will have inconsistent formats, so we will use machine learning model **Unstrack** to extract and organize unstructured data (like speaker names, session details, etc.) into a structured format.
3. Data Storage & Indexing
   - Database Design:
     - Use a relational database (like PostgreSQL or MySQL) for structured data
     - Create tables for conferences, sessions, speakers, and topics.
     - Store PDFs and related documents in a file store (e.g., Amazon S3) and link them to the database for easy access.
   - Search & Indexing:
     - Use a search engine **MeiliSearch** to index the data and enable fast, full-text search capabilities.
     - Ensure indexing captures all possible filters: session name, speaker, year, topic, and keywords.
   - Search Engine & Filtering
     - TODO
4. System Management and Updates
   - Real-time Updates:
     - Implement a scheduling system (e.g., Apache Airflow or Celery) to automatically check for new conferences and update the database when new information is available.
     - This system should also handle re-indexing in Elasticsearch/MeiliSearch as the dataset changes.
   - Error Handling & Monitoring:
     - Track failed crawls and parsing issues, especially for PDFs with complex layouts, by implementing logging and monitoring (using Prometheus or Elasticsearch Kibana dashboards).
     - Set up alerts for when scraping rules break due to website structure changes.
5. Data Cleaning & Normalization
   - Normalize names of speakers, topics, and other recurring data points (e.g., different spellings of the same topic).
   - Implement a rule-based system or a machine learning model to auto-detect and correct inconsistencies in the data.
6. Scalability Considerations
   - To handle large volumes of data and frequent updates:
     - Use distributed scraping to speed up data collection (e.g., via AWS Lambda or containerized scraping with Kubernetes).
     - Scale your database and storage system (e.g., AWS RDS with read replicas and S3 for files).
   - Load Balancing: If many users are expected, use load balancers to distribute traffic efficiently and maintain a fast experience.
7. User Interface
   - Design an intuitive front-end interface that allows users to:
     - Perform advanced searches with filters.
     - View detailed conference, session, and speaker information.
     - Download or preview attached PDFs or related documents.


