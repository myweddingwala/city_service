# API Reference Book:

## Must Have Headers
Each of the requests coming in to myweddingwala servers should have some required headers/ parameters present.
To access the api which returns the list of services offered and list of cities in which myweddingwala operates, please include the following headers.
* Myweddingwala-Space 
* Auth-Presentation

For now, they can have defined values mentioned below:
* Myweddingwala-Space  == "XYZ"
* Auth-Presentation == "Anonymous"

# Curl example to get the list of cities in which myweddingwala operates:
```bash
curl -H "Accept: application/json" -H "Myweddingwala-Space: XYZ" -H "Auth-Presentation: Anonymous" http://myweddingwala.com/get/cites"
```

If the return status is 200, then the key response will contain a key by the name result which will be a list of cities. example return:
```javascript
{
  "error": false,
  "result": ["Jaipur", "Delhi", "Chandigarh", "Amritsar", "Bhopal", "Surat", "Noida"]
}
```


# Curl example to get the list of services offered by myweddingwala
```bash
curl  -H "Accept: application/json" -H "Myweddingwala-Space: XYZ" -H "Auth-Presentation: Anonymous" http://myweddingwala.com/get/services"
```

If the return status is 200, then the key response will contain a key by the name result which will list all of offered services. Example return:

```javascript
{
  "error": false,
  "result": ["Venues", "Entertainment", "Rentals", "Caterers", "Wedding Planners", "Beauty Services", "Photography/Videography"]
}
```

# Example to post the contact us form.
There are few required data parameters to perform this request. The list is mentioned below:
1. name: This is the name of the person trying to contact MyWeddingWala.com with an inquiry. This is a required field.
2. phone_number: This is the phone number of the person. 
3. email: This is the email address of the person.
4. message: This is the user message, which is the actual query text for MyWeddingWala.com representative.
```bash
curl -X POST -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/inquiry/new' --data '{
"name": "Sumit Sharma",
"phone_number": "+91 90000 90000",
"email": "sumit@gmail.com",
"message": "This is a foo bar example."
}'
```

If the return status is 200, then the form post was successful. Example successful response:
```javascript
{
  "error": false, 
  "result": "message added to store."
}
```


# Add a new user(customer)/vendor to store
Use this API to register a new customer or verndor to the store.
## Use Cases:
1. Use this API to register a new user with a username and password.
2. If the username is taken, it returns a response which says "user name taken", and can be used to prompt the end user to try a different username.

## Example URL's:
* http://myweddingwala.com/auth/user/<string:user_type>/new/<string:username>
1. **user_type**: This could be **customer** (if trying to register a new customer), or **vendor** (uf trying to register a new vendor).
2. **username**: This is the name by which user wants to register. This has to unique. No duplication is allowed.

## Example curl post command which is successful
```bash
curl -X POST -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/auth/user/vendor/new/VendorUserName' --data '{
"password": "ASDASDASD"
}'
```
Response back from the server.
```javascript
The above url registers a new Vendor with the name "VendorUserName".
{
  "error": false, 
  "next_query_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1NDc0Mzg3OTcsImlhdCI6MTU0NzQzODE5NywidXNlciI6InN1amttbSIsImlzcyI6Ik15V2VkZGluZ1dhbGEuY29tIn0.jKWY_3Jrbrkxl8sp4YPIbtpoQmWmxGThq4dfTbnc3NM", 
  "result": "user registered"
}
```

===Point to Note with the above return===
The response includes a key **next_query_token** which will be used by user/vendor to query/ upload to the website store.

## Example curl post command which is successful, but mentions that name is taken.
I am using the same above command to make sure that the username "VendorUserName" is already taken.
```bash
curl -X POST -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/auth/user/vendor/new/VendorUserName' --data '{
"password": "ASDASDASD"
}'
```
Response back from the server.
```javascript
The response shows that username "VendorUserName" is already taken.
{
  "error": false, 
  "result": "user name taken"
}
```

# Validating if a user/ vendor is a registered user.
This API could be used to validate if the login is attempted from a register user/vendor.

## Example URL's:
* http://myweddingwala.com/auth/user/validate/<string:username>

## Example curl command (username/password mismatch).
```bash
curl -X PUT -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/auth/user/validate/sujkmm' --data '{
"password":"ADDSS"
}'
```
Response back from the server.
```javascript
{
  "error": false, 
  "result": "username/password mismatch"
}
```
The above result states that there is a mismatch with either the username or the password.

## Example curl command (Successful login).
```bash
curl -X PUT -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/auth/user/validate/SumitS' --data '{
"password":"ADDSS"
}'
```

Response back from the server.
```javascript
"error": false, 
"next_query_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE1NDc0NDAzNDMsImlzcyI6Ik15V2VkZGluZ1dhbGEuY29tIiwidXNlciI6IlN1bWl0UyIsImV4cCI6MTU0NzQ0MDk0M30.uw-YSendjf-v6c6AXycGlRA_vjZoG33X8CpQyyn2v-8", 
  "result": "registered user"
}
```
This response verifies that the user is genuine, add gives the next_query_token key for the next query to either get/upload resources on MyWeddingWala store.


# Curl example for adding vendor info to store:
```bash
curl -X POST -H 'Content-Type: application/json' -H 'Myweddingwala-Space: XYZ' -H 'Auth-Presentation: Anonymous' -i 'http://52.90.203.3/vendor/SumitS/city/chandigarh/new_registration' --data '{
"vendor_name": "SumitS",
"city": "chandigarh",
"contact_person_name":"Sumit Sharma",
"email":"Sumit@gmail.com",
"fax": "+123123",
"website_url": "https://somelinkhere",
"business_name":"Sumit Wedding Farms",
"vendor_type": "Farm House Wedding",
"address":{
    "first line": "1234 roada road",
    "city": "chandigarh",
    "state": "chandigarh",
    "Country": "India",
    "zip code": "160047"
},
"phone":{
   "telephone_number": "0172 6644425",
   "mobile_number": "+91 96541 85515"
},
"about_me": "Its a family owned business, which is great, blah blah blah blah \n adad \t adsad",
"information": {
    "price_per_plate": "1000"
},
"cities": ["chandigarh", "mohali", "zirakpur"]
}'
```


Response back from server.
```javascript
{
  "error": false, 
  "message": "Vendor registered successfully"
}
```

