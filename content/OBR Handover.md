1. Admin Page
2. Get access to passwords and Databases - Sanky
3. Papertrail access - Sanky
4. [OBRA portal](https://obrp.test.dcs.comitas.com/account/login)
5. [OBRA Portal](https://obrp.test.dcs.comitas.com/school-event-booking/booking)
6. Experience shop - TBD
7. BB vs ZB order names whats the
8. whats is parked rides
9. aspsms.ch for messenger
10. check if we got OBRA database
11. setup payment - Sanky

# Day 2
1. setup OBR to display booking and stripe payment

# Day 3
1. create stripe account
2. Download and extract stripe CLI
	1. go to extracted folder
	2. run `stripe login`
	3. open the link you get in browser to login with stripe account
	4. onnce login is complete - run `stripe listen --forward-to "https://localhost:5000/api/payment/webhook")`
	5. Goto dashboard of stripe and get the keys
		1. stripe Private key -  should be added to api secrets
		2. stripe public key - should be added to `Src\ClientApp\src\assets\config\config.json`

# Day 4
1. Email templates
	1. sendgrid
	2. get sendgrid credentials from Jonas
		1. login requires OTP
2. Experience shop
	1. Inbound API
3. Result service
	1. UploadSeasonResultXmlFile
	2. FetchObraResultDocumentsAsync
	3. [OBRA portal](https://obrp.test.dcs.comitas.com/event-results)
4. Translations
	1. Resx resource manager
		1. https://old.dotnetfoundation.org/projects/resx-resource-manager

# Day 5
1. Taskrunners
	1. send event deploma
	2. obra result fetcher
	3. 
2. obra service
	1. two way transfer - QueryNotificationManager



# Fall pending changes
1. create new tasks and assign to sanketh
	1. cant complete registrration when you select sector as others
	2. start date is missing in TT reports
	3. profile pic shown has difference in leave report and employee overview absences  - absence tabs
	4. Also, explain the usage of backgroundTaskQueue.EnqueueTask
	5. sending emails in bulk
	6. instead of fetching absencetype separately, use include - // Batch fetch all absence types needed (in case not all were included)
	7. code review changes
		1. InvoiceService
			1. use projections instead of INCLUDES inside GetPagedAsync
			2. CreateInvoicesAsync at the end we are throwing error - but instead come up with proper error message to show to user
		2. `minWidth: '50em'` this should not be font dependant - come up with a new strategy for entire app where we have similar - refer CancelInvoiceDetailComponent
		3. `import-public-holiday-dialog.ts` do not block the user if import takes too long