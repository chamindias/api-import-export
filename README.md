API Import Export
=================

This tool is used to import and export APIs from WSO2 API Manager.

Main functionality of API Export is to retrieve all the required meta information and registry
resources for the requested API and generate a zipped archive.

Zipped archive consists of the following structure

    <APIName>-<version>
    |_ Meta Information
       |_ api.json
       |_ swagger.json
    |_ Documents
       |_ docs.json
       |_ documents with type 'file'
    |_ Image
       |_ icon.<extension>
    |_ WSDL
       |_ <ApiName>-<version>.wsdl
    |_ Sequences
       |_ In Sequence
          |_<Sequence Name>.xml
       |_ Out Sequence
          |_<Sequence Name>.xml
       |_ Fault Sequence
          |_<Sequence Name>.xml

API Import accepts the exported zipped archive and creates an API in the imported environment.

This feature has been implemented as a RESTful API.

RESTful API is protected with basic authentication.

Usage
----------------------------------

A WAR(Web Archive) can be generated by building this source.

## API Import Export among cross tenants

Place the api-import-export.war under repository -> deployment -> server -> webapps in WSO2 APi Manager 1.9.0 .

## API Import Export for a single tenant
Log in to API Management console for the required tenant domain and deploy the WAR file.

* Once the web archive is deployed, API Import and Export can be done via invoking RESTful apis.

## Sample cURL command for API export with super tenant

    curl -H "Authorization:Basic YWRtaW46YWRtaW4=" -X GET "https://10.100.7.39:9443/api-import-export/export-api?name=test&version=1.0.0&provider=admin"  -k > exportedApi.zip

## Sample cURL command for API export with a tenant

    curl -H "Authorization:Basic YWRtaW46YWRtaW4taWSt34=" -X GET "https://10.100.7.39:9443/api-import-export/export-api?name=test&version=1.0.0&provider=admin@tenantdomain.com" -k > exportedApi.zip

## Sample cURL command for API import

    curl -H "Authorization:Basic YWRtaW46YWRtaW4=" -F file=@"full/path/to/the/zip/file" -k -X POST "https://10.100.7.40:9443/api-import-export/import-api"
