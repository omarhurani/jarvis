
# Test resource handling
First, a route needs to be define from which we can accept the received requests for this resource. Following the RESTful conviction, the name of the endpoint would be something like: **xxxxxxx/api/Test**.
This endpoint should accept four kinds of requests:

- **POST (xxxxxxx/api/Test)**: creates a new test. The test data is passed in the body of the request.
- **DELETE (xxxxxxx/api/Test/{ID})**: deletes the test with the specified ID from the database.
- **GET (xxxxxxx/api/Test)**: lists all the tests.
- **PUT/PATCH (xxxxxxx/api/Test/{ID})**: updates the test with the specified ID with the data that is passed in the body of the request.
Then, this endpoint needs to be associated with the controller that handles the requests performed on the Test resource. To achieve this, a new resource is defined in the **routes/api.php** file.
```php
Route::resource('test', 'API\TestController',['except' => ['create']]);
```
Then, the specified controller is created, and the five functions (store, update, destroy, index, show) are defined and mapped with the previously mentioned endpoints.
Before defining the functions, and for security measures, the accessibility to the controller should be defined using the authentication API as shown:
```php
public function __construct(){
$this->middleware(['auth:api','scope:tester,client'])->only(['index']);
    $this->middleware(['auth:api','scope:client'])->only(['store']);
    $this->middleware(['auth:api','scope:client,tester'])->only(['show']);
    $this->middleware(['auth:api','scope:client'])->only(['update']);
    $this->middleware(['auth:api','scope:client'])->only(['destroy']);
}
```

The previous code defines what type of users can access each function in the controller, using an authentication API which will be explained later.
After that, the code for each function is implemented, which does through the following process:

- Validate the inputs if any are present.
- Fetch the needed resources from the database.
- Apply the needed processing on the data.
- Store the results back in the database.

The code for the five functions in the Test resource controller was as shown:
```php
/**
* list all Tests for authenticated users
* GET /api/Test
*/
public function index(Request $request)
{  
   $user = auth()->guard('client')->user();
   $tests = $user->tests()->get();
   return $this->sendResponse($tests->toArray(), 'Tests retrieved successfully.');
}
/**
* Store a newly created Test in storage.
* Post /api/Test
*
*/
public function store(Request $request)
{
   $input = $request->all();
   $validator = Validator::make($input, [
       'name' => 'required|String',
       'websiteURL' => 'required|URL',
       'credit' => 'required|numeric',
       'post_url' => 'URL',
       'testers' => 'required|numeric|min:1',
       'tags' => 'String'   
   ]);

   if($validator->fails()){
       return $this->sendError('Validation Error.', $validator->errors());      
   }
   $user = auth()->guard('client')->user();
   $test = $user->tests()->create($input);
   return $this->sendResponse($test->toArray(), 'Test created successfully.');
}
 /**
* show a Test
* GET /api/Test/{id}
*/
public function show($id)
{
   if(auth()->user()->tokenCan('tester'))
       $user = auth()->guard('tester')->user();
   else
       $user = auth()->guard('client')->user();

   $test =$user->tests()->find($id)->first();
  
   if (is_null($test)) {
       return $this->sendError('Test not found or no access to this test');
   }
   return $this->sendResponse($test->toArray(), 'Test retrieved successfully.');
}
/**
* update a Test in storage.
* PUT/PATCH /api/Test/{id}
*/
public function update(Request $request, Test $test)
{
   $input = $request->all();
   $validator = Validator::make($input, [
       'name' => 'String',
       'websiteURL' => 'URL',
       'credit' => 'numeric|min:0',
       'post_url' => 'URL',
       'testers' => 'numeric|min:1',
       'tags' => 'String'   
   ]);
   if($validator->fails()){
       return $this->sendError('Validation Error.', $validator->errors());      
   }
   $user = auth()->guard('client')->user();
   $test = $user->tests()->find($test->id);
   if (is_null($test)) {
       return $this->sendError('Test not found or no access to this test');
   }
   if(isset($input['name'])){
       $test->name = $input['name'];
   }
   if(isset($input['websiteURL'])){
       $test->websiteURL = $input['websiteURL'];
   }
   if(isset($input['credit'])){
       $test->credit = $input['credit'];
   }
   if(isset($input['tags'])){
       $test->tags = $input['tags'];
   }
   if(isset($input['pst_url'])){
       $test->tags = $input['post_url'];
   }
   if(isset($input['testers'])){
       $test->testers = $input['testers'];
   }
   $test->save();
   return $this->sendResponse($test->toArray(), 'Test updated successfully.');
}
/**
* Delete a Test from storage.
* DELETE /api/Test/{id}
*/
public function destroy(Request $req,Test $test)
{
   $user = auth()->guard('client')->user();
   try{
       if($user->tests()->find($test->id)){
           $test->delete();
           return $this->sendResponse("", 'Test deleted successfully.');
       }
       else{
         return $this->sendError('no access to this record or it was deleted');
       }
   }catch(Exception $x){
     return $this->sendError( 'no access to this record or it was deleted');
   }  
}

```
Now, the endpoint is ready to receive the data. 

