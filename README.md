## Restful Booking Reservation API with Postman Newman

This project demonstrates API testing with Postman by providing a set of tests for several API endpoints.
## Features
- Tests for GET, POST, PUT, DELETE requests
- A collection of tests covering different API endpoints.
- Environment Setup
- Pre-request scripts for data setup
- Post-response scripts for assertion and validations
    
## API Documentation

The complete API documentation is available on Postman:
- [Rest Booking Reservation API Documentation](https://documenter.getpostman.com/view/6221717/2sAXjNYBBb)

The documentation includes:

- **Base URL**: The root endpoint for the API.
- **Authentication**: Details on how to authenticate API requests.
- **Endpoints**: A comprehensive list of all available endpoints, their methods (GET, POST, PUT, DELETE), parameters, and example responses.
- **Error Handling**: Information about possible error codes and their meanings.

## Features

- **Create a Reservation**: Add new reservations with customer details, dates, and booking options.
- **View Reservations**: Retrieve existing reservations using filters like date range, customer name, or booking status.
- **Update a Reservation**: Modify reservation details such as date, customer information, or booking status.
- **Delete a Reservation**: Remove a reservation from the system.

## Technology Used
- Postman
- Newman

## Prerequisite
- Node JS
- Newman
- Newman HTML Report Library
  
## Installation and Setup

To set up and run the API locally, follow these steps:

1. **Postman:** [Download and install Postman](https://www.postman.com/downloads/) if you haven't already on your machine.
   
3. **Clone the repository**:
   ```
   git clone https://github.com/saifulcs40/Booking-Reservation-API-Testing.git
   ```
4. **Import the Postman Collection**
   - Open Postman
   - Click on the import Button
   - Select the file from the repository
5. **Newman and Report Installation**
   - Newman install command
     ```
      npm install -g newman
     ```
   - Newman HTML report installation command
     ```
       npm install -g newman-reporter-htmlextra
     ```
## Usage
1. Select Environment
  - In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
2. Run Collection
  - Select the imported collection from the Collections sidebar.
  - Click on the Runner button to open the collection runner.
  - Select the desired environment.
  - Click Start Test to run the collection.
3. View Results
  - Once the tests are complete, view the results in the Runner tab.
  - Detailed test results can be viewed for each request.

## Testing

## Test Case Scenarios

***1. Create New Booking***

Request URL: https://restful-booker.herokuapp.com/booking/

Request Method: POST

Pre-Request Script:
  ```bash
  var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
  pm.environment.set("firstName",firstName)

  var lastName = pm.variables.replaceIn("{{$randomLastName}}")
  pm.environment.set("lastName",lastName)

  var totalPrice = pm.variables.replaceIn("{{$randomInt}}")
  pm.environment.set("totalprice",totalPrice)
  
  var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
  pm.environment.set("depositpaid",depositPaid)
  
  const date = require("moment")
  const today = date()
  var checkin = today.add(5,"d").add(5,"Y").format("YYYY-MM-DD")
  pm.environment.set("checkin",checkin)

  var checkout = today.add(10,"d").add(5,"Y").format("YYYY-MM-DD")
  pm.environment.set("checkout",checkout)
  
  var additionalNeeds = pm.variables.replaceIn("{{$randomProduct}}")
  pm.environment.set("additionalneeds", additionalNeeds)
  ```

Request Body:
```
{
  "firstname" : "{{firstName}}",
  "lastname" : "{{lastName}}",
  "totalprice" : {{totalprice}},
  "depositpaid" : {{depositpaid}},
  "bookingdates" : {
    "checkin" : "{{checkin}}",
    "checkout" : "{{checkout}}"
    },
    "additionalneeds" : "{{additionalneeds}}"
}
```
Response Body:
```
{
    "bookingid": 726,
    "booking": {
        "firstname": "Misael",
        "lastname": "Robel",
        "totalprice": 381,
        "depositpaid": false,
        "bookingdates": {
            "checkin": "2029-09-09",
            "checkout": "2034-09-19"
        },
        "additionalneeds": "Ball"
    }
}
```
***2. Get Booking Details by ID***  

Request URL: https://restful-booker.herokuapp.com/booking/bookingid

Request Method: GET

Response Body: 
```
{
    "firstname": "Misael",
    "lastname": "Robel",
    "totalprice": 381,
    "depositpaid": false,
    "bookingdates": {
        "checkin": "2029-09-09",
        "checkout": "2034-09-19"
    },
    "additionalneeds": "Ball"
}
```
***3. Creating Token for Authentication***

Request URL: https://restful-booker.herokuapp.com/auth

Request Method: POST

Pre-request Scripts: None

Request Body: 
```
{
   "username": "admin",
   "password": "password123"
}
```

Response Body: 
```
{
    "token": "0850fba9b248dc4"
}
```

***4. Update the Booking Details***

Request URL: https://restful-booker.herokuapp.com/booking/bookingid

Request Method: PUT

Pre-request Script:
```
var updatedFirstName = pm.variables.replaceIn("{{$randomFirstName}}")
pm.environment.set("updatedfirstName",updatedFirstName)

var updatedtLastName = pm.variables.replaceIn("{{$randomLastName}}")
pm.environment.set("updatedlastName",updatedtLastName)

var updatedTotalPrice = pm.variables.replaceIn("{{$randomInt}}")
pm.environment.set("updatedtotalprice",updatedTotalPrice)

var updatedDepositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
pm.environment.set("updateddepositpaid",updatedDepositPaid)

const date = require("moment")
const today = date()
var updatedCheckin = today.add(10,"d").format("YYYY-MM-DD")
pm.environment.set("updatedcheckin",updatedCheckin)

var updatedCheckout = today.add(3,"d").format("YYYY-MM-DD")
pm.environment.set("updatedcheckout",updatedCheckout)

var updatedAdditionalNeeds = pm.variables.replaceIn("{{$randomProduct}}")
pm.environment.set("updatedadditionalneeds", updatedAdditionalNeeds)
```

Request Body:
```
{
	"firstname" : "{{updatedfirstName}}",
	"lastname" : "{{updatedlastName}}",
	"totalprice" : {{updatedtotalprice}},
	"depositpaid" : {{updateddepositpaid}},
	"bookingdates" : {
    	"checkin" : "{{updatedcheckin}}",
    	"checkout" : "{{updatedcheckout}}"
	},
	"additionalneeds" : "{{updatedadditionalneeds}}"
}
```

Response Body:
```
{
    "firstname": "Eda",
    "lastname": "Schultz",
    "totalprice": 45,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-09-14",
        "checkout": "2024-09-17"
    },
    "additionalneeds": "Keyboard"
}
```

***5. Deleting the Booking Record***

Request URL: https://restful-booker.herokuapp.com/booking/bookingid

Request Method: DELETE

Response Body: None 


## Run Newman Command to Generate Report

- Run this command to get the report in the console
  ```
  newman run Booking_Reservation.postman_collection.json -e Booking_Reservation.postman_environment.json
  ```
- Run this command to get the report in HTML format
  ```
  newman run Booking_Reservation.postman_collection.json -e Booking_Reservation.postman_environment.json -r cli,htmlextra
  ```

## Newman Report Summary

![Booking Reservation API Test Report](https://github.com/user-attachments/assets/04610a1c-07ee-4fe0-b40e-103822bde7bc)

![Booking Reservation API Test Report2](https://github.com/user-attachments/assets/c25c6909-1b72-4423-8dc0-b8a56af1656d)

![Booking Reservation API Test Report3](https://github.com/user-attachments/assets/987a79d0-c92b-49bd-9157-a305f2d1ab20)

![Booking Reservation API Test Report4](https://github.com/user-attachments/assets/0bbae091-6928-4be0-af8f-add20e81035f)

