---
layout: post
author: Graham Higgins
category: project
title: How to check new gaps / better merits
tags: post project
excerpt: A walkthrough of the process of checking new record gaps or gaps with better merits -  
---

### Checking for new first known occurrences and/or bettered merits

Start with a list of candidate record gap data to be checked, formatted as per Tom Nicely’s spatial format or as comma-separated values.

The [“Prime gap record data fields”](/prime-gap-record-data-fields/) page describes the data fields. The [“Data format conversion”](/conversions/) page presents examples of first known occurrence data in both formats and for all possible outcomes - for new gaps discovered (or not) and better merits found (or not).

This data in this example has been fabricated from those presented in the “Data Conversion” page and is formatted as comma-separated values (CSV). The process for Nicely format is identical except for the URL of the processing page: [`/csv-to-sql/`](/csv-to-sql/) for data using CSV format and [`/nicely-to-sql/`](/nicely-to-sql/) for data using the Nicely format.

The data can be a locally-stored file or copied into a buffer for subsequent pasting.

Example candidate first known occurrence data, fabricated from the examples on the “Data Conversion” page, formatted as CSV, containing one newly-discovered gap and one with bettered merit.

```sql
136098,0,C,?,P,Toni_Key,2016,16.37,3610,1500031*8431#/41910 - 97126
136100,0,C,?,P,Toni_Key,2016,15.39,3842,10000091*8963#/2221230 - 115554
136102,0,C,?,P,Jacobsen,2019,17.61,3560,5105*8324#/30 - 60965
136104,0,C,?,P,Jacobsen,2017,25.61,3560,5105*8297#/30 - 61266
```

#### 1. Copy and paste example

> Navigate to `/csv-to-sql/`.

![Convert CSV to SQL page](/img/news/2019-12-04-how-to-check-00.png)

---

> Paste the CSV data into the textarea:

![CSV pasted into the textarea](/img/news/2019-12-04-how-to-check-01.png)

---

> Click the “Convert CSV to SQL” button and note the results which are shown in green, immediately under the textarea/buttons. A newly-discovered gap implies a bettered merit, hence the 2/4 result.

![Results shown in green immediately under the textarea](/img/news/2019-12-04-how-to-check-02.png)

---

> If a new gap or better merit has been found, click the “Save SQL” button and decide how to handle the result.

![Open results in text editor or save results as file](/img/news/2019-12-04-how-to-check-03.png)

---

> The results are the converted SQL statements, one INSERTing the newly-discovered gap and one UPDATEing the bettered merit.

![Results in text editor](/img/news/2019-12-04-how-to-check-04.png)

---

In this example, the text editor window was dismissed, the “Save SQL” re-clicked and the results saved to a local file. The saved filename is distinguishable by the date+time.

![Results saved as local file](/img/news/2019-12-04-how-to-check-05.png)


#### 2. "Load file” example

> Navigate to `/csv-to-sql/`.

![Convert CSV to SQL page](/img/news/2019-12-04-how-to-check-00.png)

---

> Click the “Browse...” button and navigate to a locally-stored file of CSV-formatted data. In this example, the contents of the file are the fabricated example data shown above.

![Select file of CSV-formatted gap data](/img/news/2019-12-04-how-to-check-06.png)

---

> Upon clicking the “Open” button, the file is read, the contents are copied into the textarea, checked and the result indication updated.

![Results of reading and processing the “uploaded” file (is actually just read from disk)](/img/news/2019-12-04-how-to-check-07.png)

As in the preceding copy-and-paste example, the SQL results can be inspected in a text editor and/or saved to file.

---
