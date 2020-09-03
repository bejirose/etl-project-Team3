# etl-project-Team3

PURPOSE

To use multiple data sources to find data job titles, average salaries and salaries by region.

1. Source 1: http://indeed.com/salaries
2. Source 2: Kaggle CSV files (file for each job title category)
3. Source 3: https://www.calu.edu/academics/undergraduate/bachelors/data-science/what-can-you-do-with-a-statistics-and-data-science-degree.asp

PROCESS

1. Scrape source # 1 - Start with a list of job titles. Fill Indeed search field for each title and click "Search". This shows results page with 
average salary and other details. The key challenge was that indeed search field pops a drop-down mouse_over list and by deafult only searches 
for first option. Splinter was used to mouse_over last option that allows "popular search for the specific title desired". Second challenge was 
the classes would change based on indeed loading two different type of search pages on same URL. The scraped data is stored in a pandas dataframe.

2. Kaggle Surce # 2 - Downloaded three csv (DataAnalyst,DataEngineer,DataScientist) file from Kaggle in which we can see Job title, Salary estimate and location. Reading data from CSV file and did transformation on juper notebook. The challenging part was salary estimate column, need to first split the column to lower & upper salary then repplace K,$ or any special character with zero's, cleaning the data. To get average salary did typecast on lower & Upper column. After Transfformation moved/insert the data in stage and then did cleaning/calculation/transformation at database level and moved/insert in new final/reporting table.

3. Scrape Source # 3 - Scraped job titles and Salary info from www.calu.edu using BeautifulSoup and loaded these 16 lists of job title dictionaries along with salary to Postgres SQL. These job titles are in turn used to extract more detailed information from indeed.com. There was a challenge in extracting job title information as the job title, a brief description about the job, and salary were all listed as one paragraph without having separate headings for this info. So had to take each list and search through the text to find out the job title and the salary list.

4. MERGE Steps - Merged the data from all three sources to one Jupyter notebook called salary.ipynb. For this project, all out data extraction, transformation, and loading processes are included in salary. ipynb. All CSV files, schema, and SQLite files are in the folder, Resources. output files in csv format are in the output folder. We used the relational database, PostgreSQL to store our data. There are multiple tables in the DB called, etl_db.sqlite. Final source and output files are in the folder, Team3-etl-Final.
