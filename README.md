# Food Hygiene Analysis for *Eat Safe, Love*
Using MongoDB, PyMongo, and Pandas to evaluate food hygiene ratings data to help journalists and food critics decide where to focus future articles of the UK food magazine *Eat Safe, Love*

![halal_recipe](Resources/halal-iStock.jpg)
- - -
## Project Structure
All project code files can be found in the [Project_Files](Project_Files/) folder.
### Deliverable 1 (Parts 1 & 2): 
A Jupyter notebook containing code that imports the data and sets up and updates the `uk_food` database.  
**Setup and Database Update:** [setup.ipynb](Project_Files/setup.ipynb)
### Deliverable 2 (Part 3):
A Jupyter notebook containing code that performs the exploratory analysis queries in the database.  
**Exploratory Analysis:** [analysis.ipynb](Project_Files/analysis.ipynb)  

You can also find the original json dataset used for this project in the [Resources](Resources/) folder, along with the stock photo used in this README.  In order to import the dataset, please copy the following line of code into a command-line window opened from the [Resources](Resources/) folder:  
`mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json`
- - -

## Background Scenario
The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, *Eat Safe, Love*, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.

### Part 1: Database and Jupyter Notebook Set Up  
1. Import the data provided in the `establishments.json` file from your Terminal.  
    - Name the database `uk_food` and the collection `establishments`.  
    - Copy the text you used to import your data from your Terminal to a markdown cell in your notebook.

2. Confirm that you created the database and loaded the data properly:

3. Assign the `establishments` collection to a variable to prepare the collection for use.

### Part 2: Update the Database
The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the `establishments` collection:

1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:

    ```{
    "BusinessName":"Penang Flavours",
    "BusinessType":"Restaurant/Cafe/Canteen",
    "BusinessTypeID":"",
    "AddressLine1":"Penang Flavours",
    "AddressLine2":"146A Plumstead Rd",
    "AddressLine3":"London",
    "AddressLine4":"",
    "PostCode":"SE18 7DY",
    "Phone":"",
    "LocalAuthorityCode":"511",
    "LocalAuthorityName":"Greenwich",
    "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
    "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
    "scores":{
        "Hygiene":"",
        "Structural":"",
        "ConfidenceInManagement":""
    },
    "SchemeType":"FHRS",
    "geocode":{
        "longitude":"0.08384000",
        "latitude":"51.49014200"
    },
    "RightToReply":"",
    "Distance":4623.9723280747176,
    "NewRatingPending":True
    }
    ```  
2. Find the `BusinessTypeID` for "Restaurant/Cafe/Canteen" and return only the `BusinessTypeID` and `BusinessType` fields.

3. Update the new restaurant with the `BusinessTypeID` you found.

4. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Then, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.

5. Some of the number values are stored as strings, when they should be stored as numbers. Use `update_many` to convert `latitude` and `longitude` to decimal numbers.

### Part 3: Exploratory Analysis
Eat Safe, Love has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Some notes to be aware of while you are exploring the dataset:

 - `RatingValue` refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating. **Note:** This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating.

 - The scores for `Hygiene`, `Structural`, and `ConfidenceInManagement` work in reverse. This means, the higher the value, the worse the establishment is in these areas.

Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.

1. Which establishments have a hygiene score equal to 20?

2. Which establishments in London have a `RatingValue` greater than or equal to 4?

3. What are the top 5 establishments with a `RatingValue` of '5', sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.

- - -
## References
[UK Food Standards Agency](https://www.food.gov.uk/) (2022). UK food hygiene rating data API. [https://ratings.food.gov.uk/open-data/en-GB](https://ratings.food.gov.uk/open-data/en-GB). Contains public sector information licensed under the [Open Government Licence v3.0](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)  
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).
