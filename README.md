# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked in the **Tasks** section below.

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

1. Access to the Server containing the telemetrics in a csv file
2. Access to the csv file (admin rights)
3. waiting time to access the file (time bound).
4. Notification triggered by notifier once the report is available or not.

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | we can not change the functionality only test if working or not
Counting the breaches       | Yes           | we can check by mocking/stubb
Detecting trends            | Yes           | we can check if trend recorded or not
Notification utility        | Yes           | we can check on if notification sent or not

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. 	action : Write minimum and maximum to the PDF  
	from : csv file
	when : containing positive and negative readings
1. 	action : Write "Invalid input" to the PDF 
	from : csv file
	when :there is no expected data
1.	action: Write count of breach to the pdf
	from : csv file
	when : file containing the readings
1. 	action: Write the recorded trends to the pdf 
	from : csv file
	when : file containing the readings
1.  action : Write None to the pdf
	from : csv file
	when : file does not containg data

	
(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability |update variable|  -                         | mock notify function is working
Report inaccessible server | csv file path |  bool                      | fake localServer function
Find minimum and maximum   | csv data      | bool                       | stubb the Find function
Detect trend               | recorded min_max values | bool             | stubb Detect trend function
Write to PDF               | csv analysed data | bool                   | stubb updatePDF function
