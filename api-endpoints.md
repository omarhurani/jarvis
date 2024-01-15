# Table of API endpoints

| Method           | URI                             | Action                                              | Middleware                           |
|------------------|---------------------------------|-----------------------------------------------------|---------------------------------------|
| POST             | api/client                       | Controllers\API\ClientController@store              | api,guest                             |
| GET\| HEAD    | api/client                       | Controllers\API\ClientController@index              | api,auth:client                       |
| DELETE           | api/client/{client}              | Controllers\API\ClientController@destroy            | api,auth:client                       |
| PUT\| PATCH   | api/client/{client}              | Controllers\API\ClientController@update             | api,auth:client                       |
| GET\| HEAD    | api/client/{client}              | Controllers\API\ClientController@show               | api,auth:client                       |
| GET\| HEAD    | api/test                         | Controllers\API\TestController@index                | api,auth:api,scope:tester,client      |
| POST             | api/test                         | Controllers\API\TestController@store                | api,auth:api,scope:client             |
| DELETE           | api/test/{test}                  | Controllers\API\TestController@destroy              | api,auth:api,scope:client             |
| PUT\| PATCH   | api/test/{test}                  | Controllers\API\TestController@update               | api,auth:api,scope:client             |
| GET\| HEAD    | api/test/{test}                  | Controllers\API\TestController@show                 | api,auth:api,scope:client,tester      |
| GET\| HEAD    | api/test/{test}/testCase         | Controllers\API\TestCaseController@index           | api,auth:api,scope:tester,client      |
| POST             | api/test/{test}/testCase         | Controllers\API\TestCaseController@store           | api,auth:api,scope:client             |
| PUT\| PATCH   | api/test/{test}/testCase/{testCase}| Controllers\API\TestCaseController@update         | api,auth:api,scope:client             |
| GET\| HEAD    | api/test/{test}/testCase/{testCase}| Controllers\API\TestCaseController@show           | api,auth:api,scope:client,tester      |
| DELETE           | api/test/{test}/testCase/{testCase}| Controllers\API\TestCaseController@destroy        | api,auth:api,scope:client             |
| POST             | api/test/{test}/testResult        | Controllers\API\TestResultsController@store        | api,auth:tester,auth:client,scope:tester,client|
| GET\| HEAD    | api/test/{test}/testResult        | Controllers\API\TestResultsController@index        | api,auth:tester,auth:client,scope:tester,client|
| DELETE           | api/test/{test}/testResult/{testResult}| Controllers\API\TestResultsController@destroy   | api,auth:tester,auth:client,scope:tester,client|
| PUT\| PATCH   | api/test/{test}/testResult/{testResult}| Controllers\API\TestResultsController@update    | api,auth:tester,auth:client,scope:tester,client|
| GET\| HEAD    | api/test/{test}/testResult/{testResult}| Controllers\API\TestResultsController@show      | api,auth:tester,auth:client,scope:tester,client|
| POST             | api/testResult/{testResult}/testCaseAnswer| Controllers\API\TestCaseAnswerController@store | api,auth:api,scope:tester              |
| GET\| HEAD    | api/testResult/{testResult}/testCaseAnswer| Controllers\API\TestCaseAnswerController@index | api,auth:api,scope:tester,client       |
| DELETE           | api/testResult/{testResult}/testCaseAnswer/{testCaseAnswer}| Controllers\API\TestCaseAnswerController@destroy| api,auth:api,scope:tester              |
| PUT\| PATCH   | api/testResult/{testResult}/testCaseAnswer/{testCaseAnswer}| Controllers\API\TestCaseAnswerController@update | api,auth:api,scope:tester              |
| GET\| HEAD    | api/testResult/{testResult}/testCaseAnswer/{testCaseAnswer}| Controllers\API\TestCaseAnswerController@show | api,auth:api,scope:client,tester      |
| POST             | api/test/{test}/testReview        | Controllers\API\TestReviewController@store        | api,auth:api,scope:client              |
| GET\| HEAD    | api/test/{test}/testReview        | Controllers\API\TestReviewController@index        | api,auth:api,scope:client              |
| GET\| HEAD    | api/test/{test}/testReviewcreate  | Controllers\API\TestReviewController@create       | api                                   |
| PUT\| PATCH   | api/test/{test}/testReview/{testReview}| Controllers\API\TestReviewController@update   | api,auth:api,scope:client              |
| DELETE           | api/test/{test}/testReview/{testReview}| Controllers\API\TestReviewController@destroy  | api,auth:api,scope:client              |
| GET\| HEAD    | api/test/{test}/testReview/{testReview}| Controllers\API\TestReviewController@show    | api,auth:api,scope:client              |
| GET\| HEAD    | api/tester                       | Controllers\API\TesterController@index             | api,auth:tester                        |
| POST             | api/tester                       | Controllers\API\TesterController@store             | api,guest                              |
| PUT\| PATCH   | api/tester/{tester}               | Controllers\API\TesterController@update            | api,auth:tester                        |
| GET\| HEAD    | api/tester/{tester}               | Controllers\API\TesterController@show              | api,auth:tester                        |
| DELETE           | api/tester/{tester}               | Controllers\API\TesterController@destroy           | api,auth:tester                        |
| GET\| HEAD    | api/user                         | Closure                                             | api                                   |
