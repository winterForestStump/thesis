## EDGAR CRAWLER

EDGAR-CRALER is an open-source & optimized toolkit that retrieves key information from financial reports. It can crawl any report found in the SEC EDGAR database, the web repository for all publicly traded companies in the USA. Apart from downloading EDGAR filings like other standard toolkits, EDGAR-CRAWLER can also preprocess and convert them from lengthy and unstructured documents into clean and easy-to-use JSON files.

### Citation:
The following paper provides insights into EDGAR-CORPUS:

[@loukas-etal-2021-edgar](https://aclanthology.org/2021.econlp-1.2)


### There are two code updates to the original `extract_items` script:
* Additional unicode characters text cleaning steps are added
```
python
# Replace special characters with their corresponding substitutions
text = re.sub(r"[\xa0]", " ", text)
text = re.sub(r"[\u200b]", " ", text)
text = re.sub(r"[\x91]", "‘", text)
text = re.sub(r"[\x92]", "’", text)
text = re.sub(r"[\x93]", "“", text)
text = re.sub(r"[\x94]", "”", text)
text = re.sub(r"[\x95]", "•", text)
text = re.sub(r"[\x96]", "-", text)
text = re.sub(r"[\x97]", "-", text)
text = re.sub(r"[\x98]", "˜", text)
text = re.sub(r"[\x99]", "™", text)
text = re.sub(r"[\u2010\u2011\u2012\u2013\u2014\u2015]", "-", text)
```


* All extracted items now are saved under one 'context' key
```
python
def extract_items(self, filing_metadata: Dict[str, Any]) -> Any:
        """
        Extracts all items/sections for a 10-K file and writes it to a CIK_10K_YEAR.json file (eg. 1384400_10K_2017.json)

        Args:
                filing_metadata (Dict[str, Any]): a pandas series containing all filings metadata

        Returns:
                Any: The extracted JSON content
        """

        absolute_10k_filename = os.path.join(
            self.raw_files_folder, filing_metadata["filename"]
        )

        # Read the content of the 10-K file
        with open(absolute_10k_filename, "r", errors="backslashreplace") as file:
            content = file.read()

        # Remove all embedded pdfs that might be seen in few old 10-K txt annual reports
        content = re.sub(r"<PDF>.*?</PDF>", "", content, flags=regex_flags)

        # Find all <DOCUMENT> tags within the content
        documents = re.findall("<DOCUMENT>.*?</DOCUMENT>", content, flags=regex_flags)

        # Initialize variables
        doc_10k = None
        found_10k, is_html = False, False

        # Find the 10-K document
        for doc in documents:
            # Find the <TYPE> tag within each <DOCUMENT> tag to identify the type of document
            doc_type = re.search(r"\n[^\S\r\n]*<TYPE>(.*?)\n", doc, flags=regex_flags)
            doc_type = doc_type.group(1) if doc_type else None

            # Check if the document is a 10-K
            if doc_type.startswith("10"):
                # Check if the document is HTML or plain text
                doc_10k = BeautifulSoup(doc, "lxml")
                is_html = (True if doc_10k.find("td") else False) and (
                    True if doc_10k.find("tr") else False
                )
                if not is_html:
                    doc_10k = doc
                found_10k = True
                break

        if not found_10k:
            if documents:
                LOGGER.info(
                    f'\nCould not find document type 10K for {filing_metadata["filename"]}'
                )
            # If no 10-K document is found, parse the entire content as HTML or plain text
            doc_10k = BeautifulSoup(content, "lxml")
            is_html = (True if doc_10k.find("td") else False) and (
                True if doc_10k.find("tr") else False
            )
            if not is_html:
                doc_10k = content

        # Check if the document is plain text without <DOCUMENT> tags (e.g., old TXT format)
        if filing_metadata["filename"].endswith("txt") and not documents:
            LOGGER.info(f'\nNo <DOCUMENT> tag for {filing_metadata["filename"]}')

        # For non-HTML documents, clean all table items
        if self.remove_tables:
            doc_10k = self.remove_html_tables(doc_10k, is_html=is_html)

        # Prepare the JSON content with filing metadata
        json_content = {
            "cik": filing_metadata["CIK"],
            "company": filing_metadata["Company"],
            "filing_type": filing_metadata["Type"],
            "filing_date": filing_metadata["Date"],
            "period_of_report": filing_metadata["Period of Report"],
            "sic": filing_metadata["SIC"],
            "state_of_inc": filing_metadata["State of Inc"],
            "state_location": filing_metadata["State location"],
            "fiscal_year_end": filing_metadata["Fiscal Year End"],
            "filing_html_index": filing_metadata["html_index"],
            "htm_filing_link": filing_metadata["htm_file_link"],
            "complete_text_filing_link": filing_metadata["complete_text_file_link"],
            "filename": filing_metadata["filename"],
        }

        ###############  <Update> ###############

        # Extract the text from the document and clean it
        text = ExtractItems.strip_html(str(doc_10k))
        text = ExtractItems.clean_text(text)

        positions = []
        # all_items_null = True
        content = ""
        for i, item_index in enumerate(self.items_list):
            next_item_list = self.items_list[i + 1 :]

            # Parse each item/section and get its content and positions
            item_section, positions = self.parse_item(
                text, item_index, next_item_list, positions
            )

            # Remove multiple lines from the item section
            item_section = ExtractItems.remove_multiple_lines(item_section)
            content += item_section.strip() + " "
        
        # Set the 'content' key in the JSON
        json_content["content"] = content.strip()

        return json_content
    
        ###############  </Update> ###############
```
