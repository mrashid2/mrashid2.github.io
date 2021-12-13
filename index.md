# Research Paper Analysis
## Md. Hasanur Rashid

### Context & Motivation

Nowadays, there has been an influx of people trying to publish research papers at big conferences. It has been a cumbersome process for the reviewers to go through all the text to better understand the context of the work that the authors are trying to convey. I want to use the product of this project to make the review of the research paper easier for the reviewers.

### Overview

The project mainly consists of three important features.

#### Abstract Data Extraction

The authors typically provide the critical result in the abstract field. I want to find the texts in the description that match the result reported in the abstract.

![image](https://user-images.githubusercontent.com/73667373/145758162-9baf53c0-deb5-4ad5-b71e-0f7331ac7ea5.png)

#### Citation Correlation

I want to find the text that is associated with a specific citation in the description text of the research paper. For example, if a user inputs 1 for the citation field, it will pull up what the citation is as well as the associated text in the description.

![image](https://user-images.githubusercontent.com/73667373/145758425-88fd806e-6779-468b-ab2e-e694e90bca96.png)

#### Figure And Table Details Collation

I want to collect the text for a certain figure or table from user input. The following image shows the collected text for the user if the user inputs 2 in the field of Table.

![image](https://user-images.githubusercontent.com/73667373/145758471-385355e3-4a35-414f-8316-119e6c0f13ad.png)

### Implementation Approach

Although initially the project was intended to run on Amazon EMR cluster, I decided to implement the project on Google Colab due to credit issue with Amazon Educate account. Using colab has its own set of benefits. First of all, it's free of cost, the develoment is hassle free, and the flexibility is more than enough to implement this project.

![image](https://user-images.githubusercontent.com/73667373/145764325-047698a1-4d66-48c6-9d00-7348cfc9049f.png) ![image](https://user-images.githubusercontent.com/73667373/145763747-f61f56b7-8e6b-4681-8988-ee35d9d82943.png)

I have set up my own Spark cluster and Hadoop FS on runtime with the state-of-the-art software release versions of both. I have also implemented necessary code to monitor spark jobs through UI which looks like following.

<img width="1280" alt="Screen Shot 2021-12-13 at 1 07 53 AM" src="https://user-images.githubusercontent.com/73667373/145761258-34cc2673-4edb-4712-b760-119ef188f121.png">

### Algorithms

I have used SparkContext Parallelize module to load the pre-processed data into RDD. The RDDs are then used to create dataframe. To match pattern, I have custom built REGEX pattern that would match the pattern we observed in common paper. Based on the pattern, we would then output the dataframe filtered by the REGEX pattern.

To get the best match of the user queried text, I have used fuzzy string matching algorithm that would provide us with the suggestions of the best matched sentences from the text.

### Tools

I have utilized an online tool (https://pdftotext.com/) to convert the pdf files of research papers into text files. I have used **ngrok** to tunnel localhost output so I could monitor the Spark jobs and debug if necessary.

![image](https://user-images.githubusercontent.com/73667373/145763884-55e81683-45df-4f3f-bafd-b6ec2aeb9225.png)

I have **Natural Language Toolkit, NLTK** to preprocess the data so we could load sentences in the datframe. Moreover, I have used the approximate string matching algorithm that is implemented through the library of **FuzzyWuzzy**.

![image](https://user-images.githubusercontent.com/73667373/145763437-37ac1cbc-e2c6-4be4-abb6-9bf5efe4064c.png)

### Datasets

Since my implementation has no correlation with the quantity of the data, I have chosen to experiment with only text file of five research papers. The five research papers have significant variations in content which are sufficient enough to prove the efficacy of our proposed and implemented features.

### Results

Following are the sinppets of the results that were collected after different features of my project.

#### Citation Lookup
![Screen Shot 2021-12-13 at 2 01 18 AM](https://user-images.githubusercontent.com/73667373/145766817-ebc68ae1-ac27-447b-ad8f-1f9b0aee6c1e.png)

##### Table Lookup
![Screen Shot 2021-12-13 at 2 02 26 AM](https://user-images.githubusercontent.com/73667373/145766922-455ea6d9-f5f8-465c-8969-397967ef6ece.png)

#### Figure Lookup
![Screen Shot 2021-12-13 at 2 04 03 AM](https://user-images.githubusercontent.com/73667373/145767173-b5742ac2-2d4d-4c17-ba86-5919b3976877.png)

#### Fuzzy Text Match
![Screen Shot 2021-12-13 at 2 04 50 AM](https://user-images.githubusercontent.com/73667373/145767214-e0b398a8-ffd1-4b76-863e-edd8de08d8c7.png)

### Evaluations

The evaluation is qualitative evaluation, not the quantative evaluation. The citation, table, and figure lookup modules all were able to properly locate relevant text from the data and represent to the user. However, the fuzzy text match algorithm hyperparametrs need to be tweaked and the input needs to be thoughtful to get the best outcome from the approximate text match module.

### Achievements

#### Will Achieve

1. Process pdf data to text data. (**Implemented**)
2. Load text data in RDD or Dataframe.(**Implemented**)
3. Complete appropriate regex pattern matching.(**Implemented**)
4. Do above for at least one research paper in the dataset.(**Implemented**)

#### Likely, Will Achieve

1. Based on the matched pattern, extract the sentence or paragraph from the text.(**Implemented**)
2. Do above for multiple papers in the dataset.(**Implemented**)

#### Ideally, Will Achieve

1. Be able to implement fuzzy string matching and from there properly extract the intended text.(**Implemented**)
2. Do above for all the research papers in the dataset.(**Implemented**)
