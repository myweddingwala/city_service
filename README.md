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
curl -H "Accept: application/json" -H "Myweddingwala-Space: XYZ" -H "Auth-Presentation: Anonymous" http://myweddingwala.com/get/cites"

If the return status is 200, then the key response will contain a key by the name result which will be a list of cities. example return:
```javascript
{
  "error": false,
  "result": ["Jaipur", "Delhi", "Chandigarh", "Amritsar", "Bhopal", "Surat", "Noida"]
}
```


# Curl examples to get the list of services offered by myweddingwala
curl  -H "Accept: application/json" -H "Myweddingwala-Space: XYZ" -H "Auth-Presentation: Anonymous" http://myweddingwala.com/get/services"

If the return status is 200, then the key response will contain a key by the name result which will list all of offered services. Example return:

```javascript
{
  "error": false,
  "result": ["Venues", "Entertainment", "Rentals", "Caterers", "Wedding Planners", "Beauty Services", "Photography/Videography"]
}
```

