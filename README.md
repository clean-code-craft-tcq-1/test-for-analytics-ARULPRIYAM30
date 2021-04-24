# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

Access to the Server containing the Data in a csv file
Mail Client for Notifying the Analysis
RemarK: Since Notification medium not mentioned consider it as a SMTP Server
Mail Client credentials in order to sent mails
Remark: Make sure the Mail client username and password (encrypted) are properly maintained without reset
Software to Open PDF Files for testing values listed in the generated Analysis
Remark: Mostly Third Party Tools have been used.So it should be licensed 
Binaries and API involved in the Analysis can be deprecated so listed with dependency
RemarK: A proper maven set up for the dependency binaries and a work around for deprecated API
Since the Input is a CSV file, the values fetched in csv have to be used with unique delimiter
Remark: Values in csv is categorized on delimiter so the input value fetched should not have the delimiter value.

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | We require a valid PDF converter to convert the data from csv format to PDF reports
Counting the breaches       | Yes           | This is part of the software being developed 
Detecting trends            | Yes           | We need this to detect the trend when the reading was continuously increasing for 30 minutes
Notification utility        | Yes           | We need to check whether the notifications are being sent properly or not

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write(increasing of values for 30mins contiously) to the PDF from a csv containing positive and negative readings.
4. Write "No increase in values/Null " to the PDF when the csv doesnt contain any no deviation.
5. Write the number of breaches to the PDF from a csv containing positive and negative readings.
6. Write "No breaches found" to the PDF when the csv doesnt contain any breaches.
7. Check if PDF is stored on the server location after analysis.
8. Check if the appropriate user is notified in mail message if the server to store 
9. Check old files are delted and new files are created. This is to make sure that the folder should not occupy with all file
10. Check if the notification is sent after every new PDF generation.
11. Verify if new PDF is stored every week.

(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | pdf file     |new report available         | Mock report generate
Report inaccessible server | Server addess| Unable to acess the reportt |Fake file dependency
Find minimum and maximum   | csv File     | Maximum & minimum readings  | None - pure function
Detect trend               | CSV file     | Detect trends with timestamp| None -  pure function
Write to PDF               | CSV File     | PDF report generated        | Fake
