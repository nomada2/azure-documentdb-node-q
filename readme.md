#Microsoft Azure DocumentDB Node.js Q promises wrapper

[![Join the chat at https://gitter.im/Azure/azure-documentdb-node](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Azure/azure-documentdb-node?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

![](https://img.shields.io/npm/v/documentdb-q-promises.svg)
![](https://img.shields.io/npm/dm/documentdb-q-promises.svg)
![](https://img.shields.io/github/issues/azure/azure-documentdb-node-q.svg)

This project provides a node module that makes it easy to interact with Azure DocumentDB. 

For documentation please see the Microsoft Azure [Node.js Developer Center](http://azure.microsoft.com/en-us/develop/nodejs/) and the [Microsoft Azure DocumentDB Node.js SDK Documentation](http://azure.github.io/azure-documentdb-node-q/).

##Installation

This is a wrapper of the [Azure DocumentDB Node.js SDK](https://github.com/Azure/azure-documentdb-node) using the [Q promises](https://github.com/kriskowal/q) library.

	npm install documentdb-q-promises

##Usage

To use this SDK to call Azure DocumentDB, you need to first [create an account](http://azure.microsoft.com/en-us/documentation/articles/documentdb-create-account/).

##Hello world example code using Q promises
```js
	var DocumentClient = require('documentdb-q-promises').DocumentClientWrapper;
	
	var host = [hostendpoint];                    // Add your endpoint
	var masterKey = [database account masterkey]; // Add the masterkey of the endpoint
	
	var client = new DocumentClient(host, {masterKey: masterKey});
	var databaseDefinition = { id: "sample database" }
	var collectionDefinition = { id: "sample collection" };
	var documentDefinition = { id: "hello world doc", content: "Hello World!" };
	
	var database, collection, document;
	client.createDatabaseAsync(databaseDefinition)
    	.then(function(databaseResponse) {
        	database = databaseResponse.resource;
        	return client.createCollectionAsync(database._self, collectionDefinition);
    	})
    	.then(function(collectionResponse) {
        	collection = collectionResponse.resource;
        
        	return client.createDocumentAsync(collection._self, documentDefinition);
    	})
		.then(function(documentResponse) {
			var document = documentResponse.resource;
			console.log('Created Document with content: ', document.content);
		})
    	.fail(function(error) {
        	console.log("An error occured", error);
    	});
 ```

###Youtube Videos

Getting started with Azure DocumentDB on Node.js:

[![Azure Demo: Getting started with Azure DocumentDB on Node.js](http://img.youtube.com/vi/UAE7h9PCZjA/0.jpg)](http://www.youtube.com/watch?v=UAE7h9PCZjA)

##Need Help?

Be sure to check out the Microsoft Azure [Developer Forums on MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB) or the [Developer Forums on Stack Overflow](http://stackoverflow.com/questions/tagged/azure-documentdb) if you have trouble with the provided code.

##Contribute Code or Provide Feedback

If you would like to become an active contributor to this project please follow the instructions provided in [Azure Projects Contribution Guidelines](http://azure.github.io/guidelines.html).

If you encounter any bugs with the library please file an issue in the [Issues](https://github.com/Azure/azure-documentdb-node-q/issues) section of the project.

##Learn More

* [Azure Developer Center](http://azure.microsoft.com/en-us/develop/nodejs)
* [Azure DocumentDB Node.js SDK Documentation](http://azure.github.io/azure-documentdb-node-q/)
* [Azure DocumentDB Service](http://azure.microsoft.com/en-us/documentation/services/documentdb/)
