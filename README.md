# Flask Thesis Search Application  

## Description  
This Flask application allows users to search for theses based on specific queries. It extracts data from a database and uses advanced analysis techniques to provide the most relevant results. The app is also integrated with Mistral to analyze the context of the results and give feedback based on the provided query.  

![Project Logo](./assets/shema_api.png) 

## Features  
- Search for theses by keywords.
- Update the database if the query is new.
- Display similar results based on the query.
- Option to analyze the query with Mistral.
- Supports multiple queries with context-based analysis.


### 1. Clone the repository   
`git clone https://github.com/Avicenne-ctrl/these-explorer-api.git`  


### 2. Install required dependencies  
`pip install -r requirements.txt`    


### 3. Modify the ./scripts/config.ini   
The application uses a config.ini file to manage file paths and other essential parameters. 
- Please provide in the file your personal Mistral API key if you want to use the LLM analysis functionality, by default it's None : `API_KEY = your_api_key`
- No need to adapt ChromeDriver for selenium, use of `chromedriver_autoinstaller`
- You can also change the mistral model if you want, by default : `MISTRAL_MODEL = mistral-large-latest`
- same for the embedder, by default : `MODEL_EMBEDDING = all-MiniLM-L6-v2`
- If you want more result you can modify the number after 'nb=', by default 'nb=100': `PATH_THESES_TAIL = &page=1&nb=10&tri=pertinence&domaine=theses`
- I advise you not to change the other path in the config.ini

### 4. Run the app  
`cd these-scrapping/`  
`python app.py`  

The application uses a config.ini file to manage file paths and other essential parameters. Here's an example structure for the config.ini file:


## Functionalities  
The first functionality on the main page is to search for theses related to a subject that you provide :  
![Project Logo](./assets/first_page.png)  

Then you can filter these theses by key word, and if you have provided your personal API token for Mistral LLM in the ./scripts/config.ini file, you can directly ask Mistral for more information about the theses which correspond to the key word provided.
![Project Logo](./assets/second_page.png)  

And here is the response of Mistral :
![Project Logo](./assets/third_page.png)  

## check for loading  
There is no html loading pages for now, you can only check in the terminal:  
- Loading for the search of theses if new request: 
![Project Logo](./assets/first_loading.png)  
The database will be updating automaticaly

- Loading for the Mistral LLM analysis : 
![Project Logo](./assets/second_loading.png)  


## Explaining concepts  
### 1. Search theses subject
- get the url theses related to a specific subject on theses.fr  
- read all the url to get the metadata : title, resume, author, school...
- update the excel file if new request
- update the vector store if new request
- display the excel filtered on the url request

### 2. Search with key words  
- load the vector store
- call the search function
- display the 10 more related theses

### 3. Mistral analisys
- connect to mistral and give the request


## Raises
- One common raise can be the port of the server if it is already used, you can change it in the ./scripts/config.ini : `PORT_SERVER = 5050`. Usually it's 5000 or 5050.
- Connection error during url theses scrapping on theses.fr due to the chromedriver version

## Files description
- get_url_theses_selenium.py :  
python functions in order to connect to theses.fr and look for theses related to a subject provided. At the end, we have the url for each theses   

- get_metadata_theses_beautiful_soup.py :  
python functions in order to connect to the url returned by get_url_theses_selenium.py and extract metadata on this theses
