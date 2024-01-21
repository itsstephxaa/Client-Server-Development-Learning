# Client-Server-Development-Learning
** keep in mind that i am utilizing Apporto Virtual lab for this example since that's what my school provides **
Module One
You have been given a preloaded database containing email documents…….Exit MongoDB and return to the Linux prompt. Using the database provided, execute the following administrative commands:
Load the database by executing the following at the Linux command line in the terminal:
	○ cd /usr/local/datasets
	○ mongoimport --username="${MONGO_USER}" --password="${MONGO_PASS}" --port=${MONGO_PORT} --host=${MONGO_HOST} --db enron --collection emails --authenticationDatabase admin --drop ./enron.json

NOTE: The 'cd' command prior to this command means 'change directory' to the /usr/local/datasets directory.  That is where the enron.json file is located.  The ./ before the enron.json means 'look in the current directory'.  So, be sure to run that first
NOTE: You must type in the previous commands because cutting and pasting will generate an incorrect character for quotation marks. The MongoDB instance set up in your Apporto virtual lab has an administrative user configured, and the four environment variables MONGO_USER, MONGO_PASS, MONGO_PORT, and MONGO_HOST are pre-configured in your environment. Each of these must be added to the mongoimport =command because the database is not running on the same machine that is running your virtual lab. The --drop option allows you to run the command several times without worrying about duplicate information being loaded into the database


Retrieve a document from the collection by executing the following commands in the mongo shell:
show dbs		#lists directory of databases
use enron		#this sets db to the enron database
show collections	#lists directory of collections
db.emails.findOne()	#retrieves a document from the emails collection




Execute the command to find the size of a single document of your choosing from the enron database
	○ enron> Object.bsonsize(db.emails.findOne())
NOTE: For this command to work, you may need to activate compatibility with legacy versions of the mongo shell. You accomplish this by entering the following at the shell prompt:
	snippet install mongocompat…….answer yes to the two questions the shell asks, and you should be all set
	
Execute the command to find the size of the collection of documents in the enron database
	○ enron> db.emails.totalSize()

	


Module Two
Access the dataset for this assignment, city_inspections.json, in the /usr/local/datasets directory in your Apporto environment. Using the mongoimport tool and documents found in the city_inspections.json file, load the database “city” into the “inspections” collection. Complete this task by typing the following commands in the Linux terminal to perform the import in the right directory:

	○ Change into the Apporto directory with the data sets:
	cd /usr/local/datasets/
	○ Use the mongo import utility to load the data set:
mongoimport –-username=”${MONGO_USER}” \
   –-password=”${MONGO_PASS}” –-port=${MONGO_PORT} \
   --host=${MONGO_HOST} –-db city –-collection inspections \ 
   --authenticationDatabase admin –-drop ./city_inspections.json

NOTE: In any Linux systems, commands must be exact and use proper syntax and case sensitivity.

Verify your load by “using” the “city” database, and issuing the following queries in the mongo shell:
	 
	A. db.inspections.find({"id" : "10021-2015-ENFO"})
	
	B. db.inspections.find({"result":"Out of Business"},{"business_name":1}).limit(10)



Using the appropriate commands in the mongo shell, insert a document to the database named “city” within the collection named “inspections.” Use the following key-value pairs as data for your document.

Key	Value
id	"20032-2020-ACME"
certificate_number	9998888
business_name	"ACME Explosives"
date	Today's date
result	"Business Padlocked"
sector	"Explosive Retail Dealer-999"
address	number -> 1721
	street -> Boom Road
	city -> BRONX
	zip -> 10463

Be sure to insert the address as a subdocument and use the JavaScript function Date() for “Today’s date.” Verify your database creation and insertion using the findOne() function in the mongo shell. 
	○ db.inspections.insert({"id" : "20032-2020-ACME" , "certificate_number" : 9998888, "business_name" : "ACME Explosives", "date" : Date(), "result" : "Business Padlocked", "sector" : "Explosive Retail Dealer-999", "address" : {"number" : 1721, "street" : "Boom Road", "city" : "BRONX", "zip" : 10463}})

	○ db.inspections.findOne({"id" : "20032-2020-ACME"})



a. What is the distinct list of inspection “sector” in the current inspections collection? How many are in the list? Do not count by hand.
	○ used db.inspections.distinct("sector").length
	○ 87 in the current inspections collection


b. What is the difference in the date data type for the business named “AUSTIN 2012” versus your business document insertion of “Acme Explosives”?
	○ used db.inspections.findOne({"business_name" : "AUSTIN 2012"})
	○ The difference in the date data type from the business name "AUSTIN 2012" verses my business document insertion of "ACME Explosives" is that for the ACME Explosives, the date type has a format of WEEK DAY-MONTH-DAY-YEAR, including a time stamp of hour-minutes-milliseconds (coordinated universal time). On the other hand, the AUSTIN 2012 only contains MONTH-DAY-YEAR and does not have a time stamp.


c. How many businesses have a “Violation Issued”? (See Value column above.)
	○ used db.inspections.count({"result" : "Violation Issued"})
	○ 13823 businesses have a violation issued 



4. Using the appropriate command in the mongo shell, update the document with the ID “20032-2020-ACME” in the collection “inspections” in the database “city” with the information below.

Key	Value
business_name	"New ACME Flowers"
Result	"Business Re-opened
comments	"Flowers after the explosion"

Verify your database update using the appropriate find() function in the mongo shell
○ used db.inspectionsfindOne()



Using the database “city” with documents found in the “inspections” collection, perform the tasks listed below. Verify by providing screenshots of the results as evidence.

a. Update all the documents that contain the key-value pair "city":"ROSEDALE" in the address subdocument by changing the zip code in the address subdocument to "76114".
	○ used db.inspections.updateMany()


b. Remove the first document with the key-value pair "result":"Violation Issued."
	○ used db.inspections.deleteOne()





