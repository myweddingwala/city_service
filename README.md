# city_service first API usage

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

