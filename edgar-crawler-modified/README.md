## EDGAR CRAWLER

EDGAR-CRALER is an open-source & optimized toolkit that retrieves key information from financial reports. It can crawl any report found in the SEC EDGAR database, the web repository for all publicly traded companies in the USA. Apart from downloading EDGAR filings like other standard toolkits, EDGAR-CRAWLER can also preprocess and convert them from lengthy and unstructured documents into clean and easy-to-use JSON files.

### Citation:
@inproceedings{loukas-etal-2021-edgar,
    title = "{EDGAR}-{CORPUS}: Billions of Tokens Make The World Go Round",
    author = "Loukas, Lefteris  and
      Fergadiotis, Manos  and
      Androutsopoulos, Ion  and
      Malakasiotis, Prodromos",
    booktitle = "Proceedings of the Third Workshop on Economics and Natural Language Processing",
    month = nov,
    year = "2021",
    address = "Punta Cana, Dominican Republic",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2021.econlp-1.2",
    pages = "13--18",
}

There are two code updates to the original `extract_items` script:
* Additional unicode characters text cleaning steps are added 
* All extracted items now are saved under one 'context' key