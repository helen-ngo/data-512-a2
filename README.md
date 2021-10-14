# A2 - Bias in Data Assignment

## Background and Goal
Who is the "president of Japan"? The Google results for that question are not very revealing since Japan's head of state is a prime minster, not a president. In fact, the first result is the Wikipedia article for [Shinzo Abe](https://en.wikipedia.org/wiki/Shinzo_Abe), Japan's longest-serving prime minister, who has now been succeeded by two different people since Abe left office in 2020. While Wikipedia will eventually lead you to the correct answer, how much can it tell you about [Fumio Kishida](https://en.wikipedia.org/wiki/Fumio_Kishida), the current prime minister of Japan? According to the [Wikipedia content assessment](https://en.wikipedia.org/wiki/Wikipedia:Content_assessment) procedures, "[not] a complete picture for even a moderately detailed study."

This leads us to the goal of this assignment, to explore the concept of bias through data on Wikipedia articles - specifically, articles on political figures from a variety of countries. To do this, we combine two datasets:
- A Wikipedia [politicians by country dataset](https://figshare.com/articles/dataset/Untitled_Item/5513449) that was posted on Figshare in 2017. A copy of this dataset, `page_data.csv` can be found in the the `data` folder. The project also includes code, written in the programming language R, that can be used to retreive category and page data from the Wikipedia, so you may explore a different category or more updated collection of political figures.
- The [population data](https://docs.google.com/spreadsheets/d/1CFJO2zna2No5KqNm9rPK5PCACoXKzb-nycJFhV689Iw/edit?usp=sharing) drawn from the world [population data sheet](https://www.prb.org/international/indicator/population/table/) published by the Population Reference Bureau. A copy of this dataset, `WPDS_2020_data.csv` can also be found in the `data` folder. 

Then we use the API endoint from a machine learning service called ORES to estimate the quality of each article. The ORES REST API ([documentation](https://ores.wikimedia.org/v3/#!/scoring/get_v3_scores_context_revid_model)) expects a [revision ID](https://en.wikipedia.org/wiki/Wikipedia:Revision_id), a model and name of the context to find the model. In this analysis, the model and context are `articlequality` and `enwiki`, respecitvely. For this analysis, we are only interested in the `prediction` value that the ORES endpoint returns, which is a article quality score in line with the Wikipedia content assessment procedures, such that from best to worst:
1. FA - Featured article
2. GA - Good article
3. B - B-class article
4. C - C-class article
5. Start - Start-class article
6. Stub - Stub-class article

## Reproducing the Analysis

The `hcds-a2-bias.ipynb` Jupyter notebook includes all the code to run the analysis and produce six totals tables, but references a `data` folder with the two source files mentioned above. To run the analysis directly as-is,

1. Download (and unzip) the ZIP file for this repository, or clone data-512-a2 on your computer by using the following `git` command from the terminal:
```
git clone https://github.com/helen-ngo/data-512-a2
```
2. Navigate to the library directory.
3. Open `jupyter notebook`.
4. Click on the `hcds-a2-bias.ipynb` file then `Cell` > `Run All`.

If you are interested in completing this analysis with an updated Wikipedia *category* by county dataset, you can replace the `page_data.csv ` file in the `data` folder or point the `page_data` variable to the correct file in the second code cell of the notebook.

## Reflection and Implication

Prior to the assignment, I thought that countries with English as the primary language would have politicians with the highest coverage and relative quality. Since we used articles from English edition of Wikipedia and a country's constituents were most likely to care about their own politicians, I thought English-speaking countries would write more and better articles about their populations. Although I had considered how widely English is used around the world, I felt that the bias towards English-primary countries would be prevalent in the totals tables. While my hypothesis may hold for "Geographic regions by relative quality," the results show little evidence that a country's use of English impacts how good its politicians' English Wikipedia articles will be.

Over the course of the data processing and analysis, I discovered that different country delineation and naming between the two primary data sources, Wikipedia politician by country dataset and WPDS_2020_data.csv heavily influenced missing information. Since we excluded countries (and articles) with missing information, this either disproportionately reduces the number of articles in 1) countries with "special administrative regions" (e.g. Hong Kong) and 2) countries that may be recognized differently according to the setting (e.g. "South Korea" vs "Korea, South"). The political bias of the Wikipedia article editors and world population curators may have also played a role in the results of this analysis.

While a researcher could have mapped all the countries between the datasets, so that all the information from the Wikipedia politician by country dataset and WPDS_2020_data.csv could be included, they would still have to consider why some articles did not receive ORES scores. Without understanding the inherent gaps and limitations of the data,  based on my initial assumptions of biases for these datasets, one may conclude that many North Koreans can read/write English. In fact, there is no interaction between North Korea's citizens and the English-speaking world.

Many of the "Top 10 countries by coverage" have English as one of their primary languages, but more importantly, they all have relatively small populations. It follows that every country has an executive branch of government or equivalent, and that the smaller the country, the greater the ratio of politicians to its population. The "Top 10 countries by relative quality," while had larger populations, also had very few number of politician articles. The "Top 10" results showed that smaller countries actually have higher coverage of their politicians and that those Wikipedia articles are relatively better in quality.

Perhaps the bigger takeaway from the results is that most articles on English Wikipedia are not "high-quality." Since Wikipedia is now generally accepted as a place for accurate information, it would be interesting to analyze only the most accesses articles. I would also like to see if we can extrapolate heuristic techniques from this data to identify the quality of articles outside of Wikipedia.


## Project License
Please view the [MIT License](https://github.com/helen-ngo/data-512-a2/blob/main/LICENSE?raw=true) for details.
