## About the files
- [sec_master_scrap_v2.ipynb](data/sec_master_scrap_v2.ipynb) notebook creates a csv file with all 10-K filings from January 1999 until September 2023 containing following columns:cik_number, company_name, form_id, date, file_ur.
- [10k_text_extraction.ipynb](data/10k_text_extraction.ipynb) contains code for text extraction from the 10K filings
- [10-K_sec_filings_ver2.csv](data/10-K_sec_filings_ver2.csv) is a resulting csv file with all 10-K filings from January 1999 until September 2023 containing following columns:cik_number, company_name, form_id, date, file_ur.
- [10k_10examples_text_corpus.csv](data/10k_10examples_text_corpus.csv) is a resulting csv file with 10 examples of text extraction from the 10K filings

## Examples
- [HTML 10-K filing representation](https://www.sec.gov/Archives/edgar/data/1008586/000095015207003118/l25295ae10vk.htm). This is the most conviniet format for people to read reports
- [TXT represenattion]([data/txt_example.txt](https://raw.githubusercontent.com/winterForestStump/thesis/main/data/txt_example.txt)). This format will be used while embedding.


## About 10-K SEC filings
The 10-K offers a detailed picture of a company’s business, the risks it faces, and the operating and financial results for the fiscal year. Company management also discusses its perspective on the business results and what is driving them. Most U.S. public companies are required to produce a 10-K each year and file it with the U.S. Securities and Exchange Commission (SEC). (Non-U.S. public companies usually file their annual reports with the SEC on different forms.) SEC rules require that 10-Ks follow a set order of topics.

The company writes the 10-K and files it with the SEC. Laws and regulations prohibit companies from making materially false or misleading statements in their 10-Ks. Likewise, companies are prohibited from omitting material information that is needed to make the disclosure not misleading. In addition, the Sarbanes-Oxley Act requires a company’s CFO and CEO to certify the accuracy of the 10-K. The SEC neither writes the 10-K nor vouches for its accuracy. The SEC sets the disclosure requirements – the topics that all companies must cover in their 10-Ks, and how the information should be presented.

The SEC staff reviews 10-Ks to monitor and enhance companies’ compliance with the requirements. Both the SEC and the staff also provide interpretive advice about the disclosure requirements. The SEC staff reviews 10-Ks and may provide comments to a company where disclosures appear to be inconsistent with the disclosure requirements or deficient in explanation or clarity. The Sarbanes Oxley Act requires the SEC to review every public company’s financial statements at least once every three years. The SEC staff may review the 10-Ks of certain companies more frequently. All 10-Ks filed with the SEC are available to the public on the SEC’s EDGAR website. Most companies also post their 10-Ks on their own websites.
