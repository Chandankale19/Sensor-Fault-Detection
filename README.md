## Wafer Fault Detection

#### Problem Statement:
    
    Wafer (In electronics), also called a slice or substrate, is a thin slice of semiconductor,
    such as a crystalline silicon (c-Si), used for fabricationof integrated circuits and in photovoltaics,
    to manufacture solar cells.
    
    The inputs of various sensors for different wafers have been provided.
    The goal is to build a machine learning model which predicts whether a wafer needs to be replaced or not
    (i.e whether it is working or not) nased on the inputs from various sensors.
    There are two classes: +1 and -1.
    +1: Means that the wafer is in a working condition and it doesn't need to be replaced.
    -1: Means that the wafer is faulty and it needa to be replaced.
  
#### Data Description
    
    The client will send data in multiple sets of files in batches at a given location.
    Data will contain Wafer names and 590 columns of different sensor values for each wafer.
    The last column will have the "Good/Bad" value for each wafer.
    
    Apart from training files, we laso require a "schema" file from the client, which contain all the
    relevant information about the training files such as:
    
    Name of the files, Length of Date value in FileName, Length of Time value in FileName, NUmber of Columnns, 
    Name of Columns, and their dataype.
    
#### Data Validation
    
    In This step, we perform different sets of validation on the given set of training files.
    
    Name Validation: We validate the name of the files based on the given name in the schema file. We have 
    created a regex patterg as per the name given in the schema fileto use for validation. After validating 
    the pattern in the name, we check for the length of the date in the file name as well as the length of time 
    in the file name. If all the values are as per requirements, we move such files to "Good_Data_Folder" else
    we move such files to "Bad_Data_Folder."
    
    Number of Columns: We validate the number of columns present in the files, and if it doesn't match with the
    value given in the schema file, then the file id moves to "Bad_Data_Folder."
    
    Name of Columns: The name of the columns is validated and should be the same as given in the schema file. 
    If not, then the file is moved to "Bad_Data_Folder".
    
    The datatype of columns: The datatype of columns is given in the schema file. This is validated when we insert
    the files into Database. If the datatype is wrong, then the file is moved to "Bad_Data_Folder."
    
    Null values in columns: If any of the columns in a file have all the values as NULL or missing, we discard such
    a file and move it to "Bad_Data_Folder".
    
#### Data Insertion in Database
     
     Database Creation and Connection: Create a database with the given name passed. If the database is already created,
     open the connection to the database.
     
     Table creation in the database: Table with name - "Good_Data", is created in the database for inserting the files 
     in the "Good_Data_Folder" based on given column names and datatype in the schema file. If the table is already
     present, then the new table is not created and new files are inserted in the already present table as we want 
     training to be done on new as well as old training files.
     
     Insertion of file in the table: All the files in the "Good_Data_Folder" are inserted in the above-created table. If
     any file has invalid data type in any of the columns, the file is not loaded in the table and is moved to 
     "Bad_Data_Folder".
     
#### Model Training
    
     Data Export from Db: The data in a stored database is exported as a CSV file to be used for model training.
     
     Data Preprocessing: 
        Check for null values in the columns. If present, impute the null values using the KNN imputer.
        
        Check if any column has zero standard deviation, remove such columns as they don't give any information during 
        model training.
        
     Clustering: KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters 
     is selected


## Create a file "Dockerfile" with below content

```
FROM python:3.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT [ "python" ]
CMD [ "main.py" ]
```

## Create a "Procfile" with following content
```
web: gunicorn main:app
```

## to create requirements.txt

```buildoutcfg
pip freeze>requirements.txt
```

## initialize git repo

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin <github_url>
git push -u origin main
```

## create a account at AWS & Launch AWS Elastic BeanStack Service

<a href="https://aws.amazon.com/free/?trk=09863622-0e2a-4080-9bba-12d378e294ba&sc_channel=ps&s_kwcid=AL!4422!3!453325184854!e!!g!!create%20aws%20account&ef_id=Cj0KCQiA6rCgBhDVARIsAK1kGPLl4E7ZoYROgjWPIjydpma24S9tUsPAL_szVEdc4-dkfy7_OKrzQS4aAiGJEALw_wcB:G:s&s_kwcid=AL!4422!3!453325184854!e!!g!!create%20aws%20account">AWS Free Tier</a>

## setup your project as per Documentation on AWS

<a href="https://aws.amazon.com/elasticbeanstalk/"> Setup project </a>

## Access the Project through web link

```
http://cdacwafer-env.eba-2s9pyepj.ap-south-1.elasticbeanstalk.com/
```


## to update the modification

```
git add .
git commit -m "proper message"
git push 
```

## Thank You

    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
     
    
     
    
