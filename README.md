# pdf_parsing_bigrams

Author: Cara Canady
Date: 07 May 2020

## Introduction
This work was conceived and initiated by Akio Kakishima for Data4Good in 2018-9. Akio was primarily interested in dynamic topic modeling, which he references in his pdf_dynamic_topic_modeling repos. Cara Canady took up the work in 2019-20, tasked with creating the top n bigrams and trigrams from pdf documents. This project was less research-focused and more product-focused. Thus, Cara's work focuses and iterates upon Akio's work. The ultimate goal at the end of Winter 2020 was to create a body of bigrams and trigrams with associated metadata that can feed into the D4G website.

## Loading Data
Annual report data should be loaded in the format of **"Organization Name_year"**; file extensions should always be .pdfs. Note that previously loaded files to GitHub may need to be cleaned to reflect this syntax. Future iterations of scripts could grab metadata from the parsed pdf documents, for simplicity and achievement of an MVP in 2020, this method was chosen.

## Pre-processing Data
The pre-processing and processing steps were performed in Jupyter notebook. Because of the large corpus of data, Jupyter notebook limits should be adjusted, as the default will cause an iopub error to be thrown. Therefore, the data and processing limits in the Jupyter configs needs altering. Information about how to do that can be found here: https://www.drjamesfroggatt.com/python-and-neural-networks/iopub-data-rate-exceeded-the-notebook-server-will-temporarily-stop-sending-output-to-the-client-in-order-to-avoid-crashing-it/. The `%%time` magic command was included at the beginning of most computationally expensive cells to measure total processing time. Estimates for an i7 

The pdfs were parsed using a java package called tika. Functions were created to pull the year and org title using regexs (note from above that loading the data in a specific manner will allow for easier processing). The parsed pdf, year, and org title were then put into a list, which was appended to a larger list called `output_list`.

From there, data was lowered, cleaned, and lemmatized. Stop words were removed. In addition to the NLTK English stopwords, a customized list of words was added to the stopwords: ` additional_list = ['also', 'ndr', 'red', 'crescent', 'cross', 'world', 'disaster', 'report', 'chap', 'page']`. More words can be added to `additional list` as needed. Possible candidates for later inclusion are: *international, nation, federation*, as those words appear frequently in the bigrams.

With adjusted Jupyter configurations, processing time lasted upwards of 15 minutes.

Most of the runs were processed on a 64 bit laptop with an Intel Core i5-8250U CPU and 16 GB RAM.

## Processing Data
The parameter `set_freq` was designated so that a frequency lower limit could be established for the bigram generator. Only bigram frequencies above this parameter will be included in the data set. It is recommended that this frequency be first established in the Jupyter notebook to decrease processing time.

Data was tokenized using NLTK. Further, bigrams and trigrams were created and the frequency of the bigrams and trigrams was included along with the desired metadata (Organization Name, year).

## Next Steps: 
### Recommended steps to further the previous work and deliver a webapp that displays bigrams and trigrams upon user request
- commit missing pdfs from different years into GitHub directory /data (as of 05/11/20, there are only 33)

- need to alter current pdf filenames in /data 
- record URL for annual report... someplace that makes sense, potentially a "lookup table" that connects org to org - or a table that contains more information about the org (like CIO4Good data!)

## Additional Steps: 
### Recommended steps to tidy up & iterate on previous work
- investigate computing resources with greater processing power
- may want to investigate how to create a more tailored ` additional_list`
- investigate n paramater so that n-grams can be manipulated 
