# MongoDB Using Node.js

This repository tracks my progress in the MongoDB University course.

## November 21, 2016 - Completed Week 6 - Aggregation Frameworks
1. Created aggregation frameworks for database collections using the aggregate() method. 
2. Aggregation frameworks implement a pipeline system that consists of stages that each perform a unique operation on a collection of documents.
3. Basic pipeline operations include $match, $project, $sort, $skip, and $limit.
4. Designed sophisticated, multi-stage sort queries using $unwind and $group for a Crunchbase database and a school grades database.
5. Added group accumulators like $sum, $avg, $push, and $addToSet.

### Example:
#### Using the Crunchbase database, write an aggregation query that determines the number of unique companies associated with each person.

```` javascript
db.companies.aggregate([

	// match on relationships that exist
	{ $match: { "relationships.person" : { $ne: null}}},

	// show name and relationships; hide _id
	{ $project: {name:1, relationships:1, _id:0}},

	// $unwind deconstructs the relationships array and 
    // creates a new document for each element of that array
	{ $unwind: "$relationships" },

	// group by person and count the number of unique
	// companies associated with that person
	{ $group: {
		_id: "$relationships.person",
		companies: {$addToSet: "$name"},
		count: { $sum: 1 }
	}},

	// sort descending from the person with the most 
	// companies to the least
	{ $sort: { count:-1 }}
	
]).pretty();
````

## November 7, 2016 - Completed Week 4 - Schema Design
1. Analyzed advantages of normalized data in relational databases
2. Studied database design in Mongo without using design schema

## October 31, 2016 - Completed Week 3 - NodeJS Driver
1. Focused on creating queries using the Node.js driver
2. Implemented command line options to modify MongoDB queries
3. Created queryDocument object utilizing the user's specified options


