INTG to Prod Move 01 07 2026

Merged PR 40887: bug-couldnt-save-activity-if-invoicing-module-s-di%bled

bug-could nt-save-activity-if-invoicing -module-is-disabled

Dev to INTG move 01 07 2026
Nikhil DR ilto P ineg
Nikhil DR request P dev
Task 89323: Case Management Test Feedback
Nikhil DR request !40852 ito P d"
Bug 89446, Bug 89455
Nikhil DR !40864 hto P dev


Given that a device:
	Takes a reading every 5 minutes
	May have a unique combination of sensors that are included in the readings
	Attempts to send a combined reading file (mainData) every 15 minutes
	Will continue appending readings onto the mainData file until it is received
 
Given that ingestion:
	Sends an ack back to controller after receiving the file
	Gets necessary information about the controller (an IoT device) from the mainData filename
	Does not open the mainData file
 
We need to display to users how many mainData files are received on time in a given month 