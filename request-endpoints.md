# Table of request endpoints

| Method           | URI                             | Action                                                    | Middleware                                 |
|------------------|---------------------------------|-----------------------------------------------------------|--------------------------------------------|
| GET\|HEAD        | client/all                      | Controllers\API\ClientController@all                       | web,auth:client,auth:api,scope:client       |
| POST             | client/createtask               | Controllers\Client\TestTaskController@create               | web,auth:api,scope:client                   |
| POST             | client/login                    | Controllers\Client\AuthController@login                   | web,guest:client                           |
| GET\|HEAD        | client/logout                   | Controllers\Client\AuthController@logout                  | web,auth:client                            |
| POST             | client/register                 | Controllers\Client\AuthController@register                | web,guest:client                           |
| POST             | client/reviewanswer             | Controllers\Client\TestTaskController@review              | web,auth:api,scope:client                   |
| POST             | client/settaskactive            | Controllers\Client\TestTaskController@setActive           | web,auth:api,scope:client                   |
| GET\|HEAD        | google-callback                 | Controllers\GoogleAuthController@handleProviderCallback | web                                        |
| GET\|HEAD        | google-login                    | Controllers\GoogleAuthController@redirectToProvider      | web                                        |
| GET\|HEAD        | logout                          | Controllers\Tester\AuthController@logout                 | web,auth:api                               |
| GET\|HEAD        | paypal-confirm                  | Controllers\PayPalController@confirm                     | web                                        |
| POST             | reset/email                     | Controllers\Client\ForgotPasswordController@sendEmail    | web,guest:api                              |
| POST             | reset/password                  | Controllers\Client\ResetPasswordController@resetEmail     | web,guest:client                           |
| POST             | tester/addtest                   | Controllers\Tester\WebController@addTest                 | web                                        |
| GET\|HEAD        | tester/all                      | Controllers\API\TesterController@all                      | web,auth:tester,auth:api,scope:tester      |
| POST             | tester/login                     | Controllers\Tester\AuthController@login                 | web,guest:tester                           |
| GET\|HEAD        | tester/logout                    | Controllers\Tester\AuthController@logout                | web,auth:api                               |
| POST             | tester/register                  | Controllers\Tester\AuthController@register               | web,guest:tester                           |
| POST             | tester/sendanswer                | Controllers\Tester\WebController@sendAnswer              | web,auth:api,scope:tester                   |


