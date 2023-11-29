# DE Maintenance of SAP Metal Prices Automation
**Note: This project was developed for our Germany purchasing team during my tenure at Phoenix Contact USA. As the code is not shareable, its purpose is to explain the project and demonstrate the process behind my solution.**


## Project Summary
This project aims to automate the data collection of metal prices from german websites [westmetall.de](https://www.westmetall.com/de/markdaten.php), [jeners.com](https://www.jeners.com/ticker.html), and [agosi.de](https://www.agosi.de/ek/ek.php).

The automation will then store the collected data in the DE Metal Prices Excel file, which is stored by year and organized by month and year. The automation will then log into SAP using the bot operator SAP RPA credentials to access transaction MEK1 to maintain pricing and validity periods for the following SAP condition types during the specified periods:

- Processed Daily
  - GAU2-Goldpreis
  - GAG2-Silberpreis
  - GCU2-akt. DEL incl. 1% Bz
- Processed at the First of Each Month
  - GLM2-LME officials

The condition type GCU2 pricing must include a 1% increase. All daily recorded pricing within the Excel Spreadsheet and SAP will be recorded in EUR currency format at a pricing unit of 100 KG. The pricing recorded monthly within SAP will be recorded in USD currency format at a pricing unit of 1000 KG.
Exception handling will need to account for the possibility that the metal pricing may not have been updated on the website. The automation will need to log a warning, continue processing, and will need to generate an Email notification to the responsible users to address the issue. The automation will need to alert the responsible users of any errors that occur during processing. Upon successful completion of automation, an Email will be generated to the responsible users. Operators will require access to UiPath Orchestrator to view the progress of automation tasks, address processing errors, schedule tasks, and stop automation in the event of an error. The level of permissions will be defined by the Active Directory group they belong to.


## High Level As-Is Process

| Step     | Description 
| :---: | :--- |
| 1 | Open [westmetall.de](https://www.westmetall.com/de/markdaten.php) and copy-paste all metal prices into an Execl file |
| 2 | Open [jeners.com](https://www.jeners.com/ticker.html) and copy-paste Zinc metal price into an Execl file |
| 3 | Open [agosi.de](https://www.agosi.de/ek/ek.php) and copy-paste Gold and Silver metal prices into an Execl file |
| 4 | Log into SAP and enter all collected prices into their respective SAP condition types |


## High Level Solution
- Developed a Python script for web scraping (utilized Selenium and Beautiful Soup) and integrated it into UiPath using the Invoke Python Method activity.
- Stored the collected data in an Excel file organized by year and month, ensuring accuracy and proper formatting.
- Used UiPath's SAP Automation activities to log in to SAP and access the MEK1 transaction.
- Implemented exception handling within the combined UiPath-Python automation to manage cases where the web scraping process encountered errors or if the website data wasn't updated.
- Logged warnings or errors and generated email notifications to notify responsible users in case of issues.
- Provided operators access to UiPath Orchestrator for monitoring automation tasks, addressing processing errors, and controlling task scheduling based on their Active Directory group permissions.

This extended solution combined the power of UiPath for orchestrating the overall automation process with the capabilities of Selenium and Beautiful Soup for efficient and accurate web scraping from German websites, enriching the data collection process for metal prices.
