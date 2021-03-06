# SPIN-rule-engine
A RESTFUL web API built on top of the existing TopQuadrant SPIN API ( http://topbraid.org/spin/api/) that executes SPIN rule inference on provided models. The engine supports a specialised API for the DEM models that can extract and execute the rules included in DEM policies, and reports the changes back to models using the PERSIST API.

The SPIN engine uses the SPIN API to run inference on the model.
<h1> Installation and execution </h1> 
<h2> Commandline </h2>
Download the latest release here: https://github.com/pericles-project/SPIN-rule-engine/releases/download/1.1/spinengine.zip <br>
extract, move to folder and run from shell: <br> 
 `java -jar spinengine.jar`
<h2> Web service </h2>
The project is based on Maven, in order to direclty run the web service (port 8080 by default):<br>
1. - install Maven <br>
2. - clone or download the repository <br>
3. - go to the folder and run `mvn jetty:run` <br>
4. - open the browser at the local address: <br>
http://127.0.0.1:8080/spinengine/runInferencesGet?baseURI=http://topbraid.org/examples/kennedysSPIN
<br>
<h3> WAR file install</h3>
Follow steps 1-2 and then package the war file using the standard MVN command:
3 -  go to the folder and run `mvn war:war` <br>
<br>

<h1>The API: :honeybee:</h1><br>
DEM Specific API is described in the project documentation <br>
The complete API documentation - automatically generated - with different language clients is included here: https://pericles-project.github.io/SPIN-rule-engine/apidocs/ 
Currently the API is implemented as a restful service that can be invoked usign both GET and POST methods. The following methods are implemented and can be executed via simple web call:<br>
* `runInferencesGet` <br>
* `runInferencesPost` <br>
* `runConstraintsGet` <br>
* `runConstraintsPost` <br><br>
All the methods use the following 4 parameters (1st parameter is necessary, the other 3 optionals):<br>
* `baseURI`: the URI for the base document <br>
* `document`: (optional) the document contents <br>
* `SPINURI`:  (optional) The URI for the SPIN document (to be merged with the base document) <br>
* `SPINdocument`: the SPIN document contents <br>
* `outFormat`: the format for output serialisation. Can be one any of the apache Jena ones: https://jena.apache.org/documentation/io/rdf-output.html<br> 
The Constraints checking method support one further parameter, that asks the engine to execute the inference before checking the constraints: 
* `doInference` (optional): true or false (default false)

<h1> Output</h1>
The output includes the follwing elements, as simple JSON strings:
* `constraints`: the constraints inference out model 
* `model`: the updated model
* `newTriplets`: the new triples
* `consoleLog`: console output or errors
   
When the output format is specified to be json, the models are written instead to the following:
* `jsonModel`: the updated model
* `jsonNewTriplets`: the new triples
* `jsonConstraints`: the constraints inference out model 
<h2>An example </h2> 

This example is executed running the engine for constraint checking with inference:<br>
`http://127.0.0.1:8080/spinengine/runConstraintsGet?baseURI=http://topbraid.org/examples/kennedysSPIN&doInference=true`
