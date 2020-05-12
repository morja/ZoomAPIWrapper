ZoomAPIWrapper
==============

This is A simple PHP wrapper for calling the Zoom V2 API's. It aims to be
- Simple to use
- LIghtweight (no external dependencies)

What it Does Do
---------------

The class handles API authentication for you, as well as setting up the relevant curl options for the type of request you want to do.

What it Doesn't Do
------------------

*Compose body data*: When the endpoint your are calling requires the request body you are sending to include JSON data it is up to you to compose the required data (either as a PHP data structure or as a JSON data string)

*Handle pagination for you*: Most list endpoints support pagination of results. This wrapper doesn't automatically make multiple requests to get all the pages for you. If the results of your API call fills a page, then it is up to you to make another call for the next page of results (if you want the next page that is!).

Installing 
==========

Download ZoomAPIWrapper.php and require this in your code.

How to Get Your API Key
=======================

You need to go to the Zoom "App Marketplace", log in using your zoom account and then select "Build App" from the "Develop" dropdown menu. This link should take you there: https://marketplace.zoom.us/develop/create

Then you need to choose the JWT option for "server-to-server integration". Once you will out some basic information you will be taken to the "App Credentials" page which will give you your API key and API secret.

Usage
=====

  $zoom = new ZoomAPIWrapper( <API_key>, <API_secret> );
  
  $response = $zoom->doRequest(<METHOD>, <endpoint_path> [,<query_parameter_array> [,<path_parameter_array> [,<request_body_array_or_string>] ] ]);
  
  // $response is false if there is a problem with the request e.g. path includes a request parameter which hasn't been specified in the request_parameter_array
  // N.B. Remember to test with '$response === false' as in some cases a successful call will result in an empty string for $response
  // If you want details of the nature of the problem with your request you can get an array of errors like this...
  if ( $response===false ) {
    $errors = $zoom->requestErrors();
  }

  // If there were no errors (i.e. $response!==false) you can still call requestErrors() - it will return an empty array

  // If the request goes ahead then $response will contain the decoded response from Zoom
  
  // If you want to know the HTTP response code you can get it like this...
  $httpResponse = $zoom->responseCode();
  
  
Examples
========

See examples.php

TODO
====

There may be other things I haven't encountered yet, but the main one I'm aware of is lack of support for file uploads as required by /users/{userId}/picture
