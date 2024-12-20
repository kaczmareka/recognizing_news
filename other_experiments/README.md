# TUTAJ TO SIĘ UPDATE SPORY PRZYDA!!!
i sprawdzenie czy w tym folderze wszystkie pliki są ok

# Recognizing Selected Features in the News Text

This repository includes materials created during work on the paper `Recognizing Selected Features in the News Text`. It includes demonstrating scenario of the created pipeline, prepared data and codes used to run all experiments related to the work.

## Real-world scenario considered in this work

[Actaware Inc.](https://actaware.com) is developing an application allowing users to scan products and learn about their producers and the values they represent. During registration for the app, users select values that are important to them, e.g. environment, animal care, or human and employee rights, as can be seen on the screenshot below. Next, when scanning the products, users receive producer scores, based on this “value compass”. In the application, producers’ actions are evaluated based on news articles. 

![Screenshot from application](../img/app_value_compass.png)

This work aimed to create a solution that can match the content of the news to predefined categories (from the “value compass”): human and employee rights, diversity, equity and inclusion, environment, animal care, corporate transparency, business involvement, political and religious views, and other. Next, the developed solution should establish the sentiment of the considered articles.

Here, to address article categorization, state-of-the-art methods, i.e. KeyBERT, GPT-3.5-turbo, and GPT-4o-mini, have been tested during experiments. Similarly, for sentiment analysis, BERT- and GPT models, along with a novel graph-based solution, have been tried. 

In this context, the contributions of the work are as follows: 
(a) evaluating the dataset provided by Actaware and enhancing part of it with annotations of categories and sentiment (see directory `data`),
(b) introducing evaluation methods, including performance metrics and addressing sustainability, resources, cost and explainability, 
(c) experimental evaluation of the performance of possible approaches to text news categorization and establishing their sentiment, 
(d) proposing a comprehensive solution using state-of-the-art (as of Fall 2024) tools.

### Solution

![Solution Plan](../img/solution_pipeline.jpg)

The final pipeline consists of two parts: categories recognition and sentiment analysis. For both parts various approaches were tested, but for the final solution, categories are recognized using GPT-4o-mini model, whereas sentiment is found using ensemble of two models: RoBERTa and graph-based solution. The output of the solution includes article, company name, category and sentiment, as can be seen below.
![Final output](../img/final_results.jpg)

## Requirements

To run the solution, installed conda is recommended.

```
conda create -n env_actaware python=3.10.12
conda activate env_actaware
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```
and run notebook `Final_pipeline.ipynb`. Please be aware, that you need to provide your own OpenAI API key in `src\config.py` file to run the solution.

For running notebooks with experiments, please find more details described in `notebooks_with_experiments`.

For reproducing our work, please relate to `other_experiments` directory. Please be aware that in might be necessary in some cases to update the paths to some of the dependencies, in case you want to run any of the experiments.

## Example usage

To run the final version of the presented work, please look on `Final_pipeline.ipynb` notebook. 

## Structure of the repository
* `data` - directory with most of the data needed to run `final_pipeline.ipynb`. The only file too big to store on GitHub is the original Actaware Inc data, which should be downloaded from [here](https://drive.google.com/file/d/1WNaTt7WLZjqp6-JyS9kj7XVsVG6v59N9/view?usp=sharing) and moved to `data` folder.
* `img` - directory with all images needed for `README.md`.
* `notebooks_with_experiments` - directory containg notebooks for the experiments conducted during this work.
* `other_experiments` - resources related to our other approaches, including incident recognition part.
* `results_of_experiments` - directory with the results from conducted experiments.
* `src` - directory with source files to run `Final_pipeline.ipynb` file.
* `actaware_data_preprocessing.ipynb` - notebook with proposed preprocessing of original data from Actaware Inc. The proprocessing does not include labelling of chosen subsets of the data.
* `Final_pipeline.ipynb` - notebook with final pipeline, proposed as the solution for the problem.
* `requirements.txt` - what libraries needs to be installed to run final pipeline. For running experiments, additional requirements are mentioned in the appropriate directory.

## Authors

Title: Recognizing Selected Features in the News Text

Authors: 
- Agata Kaczmarek (agata.kaczmarek@pw.edu.pl), Faculty of Mathematics and Information Science, Warsaw University of Technology, Warsaw, Poland
- Filip Tobolewski, Actaware Inc., Concord, California, US
- Maria Ganzha (maria.ganzha@pw.edu.pl), Faculty of Mathematics and Information Science, Warsaw University of Technology, Warsaw, Poland
- Marcin Paprzycki (marcin.paprzycki@ibspan.waw.pl), Systems Research Institute Polish Academy of Sciences, Warsaw, Poland
- Anna Wróblewska (anna.wroblewska1@pw.edu.pl), Faculty of Mathematics and Information Science, Warsaw University of Technology, Warsaw, Poland


## Structure of the repository
* `notebooks` - directory containg notebooks and files that are more tidy than `work_in_progress` :)

## Current plan and setup

![Solution Plan](img/solution_plan.png)

To recognize incidents the topic modeling model BERTopic is used. Performance is measured by metrics: TopicDiversity, mean diversity in topics and Coherence. 

* Coherence metrics - measure how the top-k words in the topic relate to each other
* Significance metrics - aim at discovering high-quality and junk topics based on document-topic and topic-word distributions
* Diversity metrics - measure diversity of words in topics

For sentiment analysis three models are being compared: BERT, RoBERTa and graph based solution. The metric to compare them is balanced accuracy, measured on dataset similar to ACTAWARE (https://www.kaggle.com/datasets/hoshi7/news-sentiment-dataset).

### Future work

1. Add significance and probably similarity metrics for topic modeling.
2. Define what means "best results" for this part - any suggestions, which metrics are more important and makes more sense?
3. Check other models and compare to BERTopic.
4. Find best setup (including hyperparameters) for topic modeling.
5. Solve issues with BERT and RoBERTa regarding input tokens.
6. Find best configuration (including hyperparameters) for sentiment analysis.

## Current results for topic modeling 

Diversity parameter: 0.5, coherence metric: c_npmi, TopicDiversity: 0.7886792452830189, mean diversity in topics: 1.0, coherence score: 0.034461948245713726, KL background: 2.534053223796575, KL vacuous: 2.4354541148173947.

Diversity parameter: 0.2, coherence metric: c_npmi, TopicDiversity: 0.7061320754716981, mean diversity in topics: 0.9001286449399674, coherence score: 0.09791122425972787, KL background: 2.534053223796575, KL vacuous: 2.3216755782442813.

Diversity parameter: 0.05, coherence metric: c_npmi, TopicDiversity: 0.680188679245283, mean diversity in topics: 0.8406534503232632, coherence score: 0.11335504226096892, KL background: 2.534053223796575, KL vacuous: 2.3040921834697.

Sample topic:

[('hamas', 0.03437410007487483),
 ('terrorist', 0.01593485845474893),
 ('antisemitism', 0.01382230042677843),
 ('jews', 0.012036425841046161),
 ('civilians', 0.007678645589811692),
 ('staff', 0.007132417021782438),
 ('attacks', 0.0069416562088209215),
 ('bbcs', 0.005977607178207836),
 ('editorial', 0.005890806183172142),
 ('simpson', 0.005484746849865494)]

For given text (part of it is shown below):

The BBC is being urged to drop singer Olly Alexander as its entrant for Eurovision after it emerged he signed a letter calling Israel an 'apartheid regime'. The Years And Years frontman, 33, was unveiled as next year's candidate for the UK during the Strictly Come Dancing final, which aired on the BBC on Saturday. But he now faces having that role stripped from him after he signed a letter from LGBT charity Voices4London which described Israel as an 'apartheid regime' which is trying to 'ethnically cleanse' Palestine. The statement, which was published on October 20, almost two weeks after Hamas' October 7 attack, also says that Israel has 'terrorised' Palestinian people and there is now a 'genocide' taking place 'in real time'.[...]


## Current results for sentiment analysis

![Twitter_results](img/results_sentiment_twitter.png)
![News_result](img/results_sentiment_news.png)
![overlap_results](img/results_methods_comparison_overlap.png)
