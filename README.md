# Simple ETL process with KNIME

1. [Business Understanding](#Business-Understanding)
2. [Data Understanding](#Data-Understanding)
3. [Data Preparation](#Data-Preparation)
4. [Modeling](#.Modeling)
5. [Evaluation](#Evaluation)
6. [Deployment](#Deployment)
7. [Final Workflow](#Final-Workflow)

## Business Understanding

In this project, we use movie rating records from grouplens.org as the dataset. Processes that could be applied to this data are as follows:

1. Best recommended movie
2. 10 best recommended movies
3. Rated movies

## Data Understanding

    MovieLens 20M movie ratings. Stable benchmark dataset. 20 million ratings and 465,000 tag applications applied to 27,000 movies by 138,000 users. Includes tag genome data with 12 million relevance scores across 1,100 tags. Released 4/2015; updated 10/2016 to update links.csv and add tag genome data. 

The data is consist of several csv files. The files are as follows:

1. tag.csv:
    * userId
    * movieId
    * tag
    * timestamp

1. rating.csv
    * userId
    * movieId
    * rating
    * timestamp

1. movie.csv
    * movieId
    * title
    * genres

1. link.csv
    * movieId
    * imdbId
    * tmbdId

1. genome_scores.csv
    * movieId
    * tagId
    * relevance

1. genome_tags.csv
    * tagId
    * tag

## Data Preparation

1. load the dataset using File Reader

    ![nodefilereader]
    ![conffilereader]

2. add userid and timestamp fields to the data.

    ![nodeaddfields]

3. split the data to take the first 20 rows

    ![noderowsplitter]

4. rate the splitted 20 row and let the rest unrated

    ![nodesrating]
    ![rate]

5. convert the table data into spark using table to spark

    ![nodetabletosparkrated]
    ![nodetabletosparkunrated]

6. read rating.csv and convert to spark

    ![nodecsvtospark]

7. split the data from csv to spark randomly using spark partitioning

    ![nodesparkpartitioning]

## Modeling

1. concate the partitioned spark and 20 rated movies from table to spark using spark concatenate

    ![nodesparkconcate]

2. create a model from the concatenated data using Spark collaborative filtering learner

    ![nodesparkmodel]
    ![model]

## Evaluation

1. evaluate the model using spark predictor

    ![nodesparkpredictor]
    ![pred1]

2. remove data with missing value(s)

    ![nodesparkmissingvalue]

3. score the evaluation result using scorer

    ![nodesparkscorer]
    ![score]

## Deployment

Display the predicted value using following flow.

![displayflow]
![recommend]

## Final Workflow

![finalworkflow]

## Comparing Csv to Spark vs File Reader

in order to compare those nodes, we need to add them to the flow and set the input csv to rating.csv

![compare1]
![compare2]

and the time compare result is as follow:

![compare3]

it shows that file reader take longer time to finish than csv to spark

[conffilereader]: ./img/conffilereader.png "conffilereader"
[displayflow]: ./img/displayflow.png "displayflow"
[nodeaddfields]: ./img/nodeaddfields.png "nodeaddfields"
[nodecsvtospark]: ./img/nodecsvtospark.png "nodecsvtospark"
[nodefilereader]: ./img/nodefilereader.png "nodefilereader"
[noderowsplitter]: ./img/noderowsplitter.png "noderowsplitter"
[nodesparkconcate]: ./img/nodesparkconcate.png "nodesparkconcate"
[nodesparkmissingvalue]: ./img/nodesparkmissingvalue.png "nodesparkmissingvalue"
[nodesparkmodel]: ./img/nodesparkmodel.png "nodesparkmodel"
[nodesparkpartitioning]: ./img/nodesparkpartitioning.png "nodesparkpartitioning"
[nodesparkpredictor]: ./img/nodesparkpredictor.png "nodesparkpredictor"
[nodesrating]: ./img/nodesrating.png "nodesrating"
[nodetabletosparkrated]: ./img/nodetabletosparkrated.png "nodetabletosparkrated"
[nodetabletosparkunrated]: ./img/nodetabletosparkunrated.png "nodetabletosparkunrated"
[nodesparkscorer]: ./img/nodesparkscorer.png "nodesparkscorer"
[rate]: ./img/rate.png "rate"
[pred1]: ./img/pred1.png "pred1"
[pred2]: ./img/pred2.png "pred2"
[model]: ./img/model.png "model"
[score]: ./img/score.png "score"
[recommend]: ./img/recommend.png "recommend"
[finalworkflow]: ./img/finalworkflow.png "finalworkflow"
[compare1]: ./img/compare1.png "compare1"
[compare2]: ./img/compare2.png "compare2"
[compare3]: ./img/compare3.png "compare3"
