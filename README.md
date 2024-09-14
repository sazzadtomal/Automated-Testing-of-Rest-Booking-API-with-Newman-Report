### **Rest Booking API Testing with Postman Newman**
This project demonstrates API testing using Postman, providing a collection of tests to validate various endpoints of the API. 

### **Features**

- Tests for GET, POST, PUT, DELETE requests
- Collection of tests covering different API endpoints
- Environment setup for easy switching between environments
- Pre-request scripts for data setup
- Test scripts for assertions and validations

## API Documentation:
- https://documenter.getpostman.com/view/27840720/2sAXqp7iCM
  
### **Technology used:**
- Postman
- Newman

### **Prerequisite:**
- Node Js
- Newman
- Newman Html Report Library

### **Installation**

1. Postman: If you haven't already, [download and install Postman.](https://www.postman.com/downloads/)
2. Clone the repository:
 ```console 
  git clone https://github.com/sazzadtomal/Automated-Testing-of-Rest-Booking-API-with-Newman-Report.git
```
3. Import the Postman collection:
    - Open Postman.
    - Click on the Import button.
    - Select the file from the repository.
4. Import the Postman environment:
    - In Postman, click on the gear icon in the top right corner.
    - Select **Import** and choose the file.
5. Newman and Report Installation Process:
    - Newman Install Command:
     ```console 
      npm install -g newman
    ```
    - Newman Html Report Install Command:
     ```console 
      npm install -g newman-reporter-htmlextra
    ```
### **Usage**
1. Select Environment:
    -   In Postman, select the appropriate environment (e.g., Development, Production) from the top-right dropdown.
3. Run Collection:
    -   Select the imported collection from the Collections sidebar.
    -   Click on the Runner button to open the collection runner.
    -   Select the desired environment.
    -   Click Start Test to run the collection.
8. View Results:
    -   Once the tests are complete, view the results in the Runner tab.
    -   Detailed test results can be viewed for each request.

## **Testing**

## Test Case Scenarios:

## _**1. Create New Booking**_

### Request URL: https://restful-booker.herokuapp.com/booking/
### Request Method: POST
### Pre-request Script:
```console 
    let firstName = pm.variables.replaceIn("{{$randomFirstName}}")
    pm.environment.set("firstName", firstName)
   
    
    let lastName = pm.variables.replaceIn("{{$randomLastName}}")
    pm.environment.set("lastName", lastName)
    
    
    let totalPrice = pm.variables.replaceIn("{{$randomInt}}")
    pm.environment.set("totalPrice", totalPrice)
    
    
    let depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
    pm.environment.set("depositPaid", depositPaid)
   
    
    const moment = require('moment')
    const today = moment()
    pm.environment.set("checkin", today.add(1,'d').format("YYYY-MM-DD"))
    pm.environment.set("checkout",today.add(5,'d').format("YYYY-MM-DD"))
    
    let additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")
    pm.environment.set("additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
	  "bookingdates" : {
    	  "checkin" : "{{checkin}}",
    	  "checkout" : "{{checkout}}"
	  },
	  "additionalneeds" : "{{additionalNeeds}}"
  }
```
  **Response Body:**
 ```console 
  {
    "bookingid": 5477,
    "booking": {
        "firstname": "Clement",
        "lastname": "Fritsch",
        "totalprice": 463,
        "depositpaid": true,
        "bookingdates": {
            "checkin": "2024-09-16",
            "checkout": "2024-09-21"
        },
        "additionalneeds": "protocol"
    }
}
```
 ## _**2. Get Booking Details By ID**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: GET
### Response Body:
 ```console 
{
    "firstname": "Clement",
    "lastname": "Fritsch",
    "totalprice": 463,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-09-16",
        "checkout": "2024-09-21"
    },
    "additionalneeds": "protocol"
}
```
## _**3. Create A Token For Authentication.**_
### Request URL: https://restful-booker.herokuapp.com/auth
### Request Method: POST
### Pre-request Script: None
### Request Body:
 ```console 
{
	"username": "admin",
	"password": "password123"
}
```
  **Response Body:**
 ```console 
{
    "token": "7ae13f0de88f581"
}
```

 ## _**4. Update the Booking Details**_
### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: PUT
### Pre-request Script:
```console 
    let firstName = pm.variables.replaceIn("{{$randomFirstName}}")
    pm.environment.set("firstName", firstName)
    
    
    let lastName = pm.variables.replaceIn("{{$randomLastName}}")
    pm.environment.set("lastName", lastName)
    
    
    let totalPrice = pm.variables.replaceIn("{{$randomInt}}")
    pm.environment.set("totalPrice", totalPrice)
    
    
    let depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
    pm.environment.set("depositPaid", depositPaid)
    
    
    const moment = require('moment')
    const today = moment()
    pm.environment.set("checkin", today.add(1,'d').format("YYYY-MM-DD"))
    pm.environment.set("checkout",today.add(5,'d').format("YYYY-MM-DD"))
    
    let additionalNeeds = pm.variables.replaceIn("{{$randomNoun}}")
    pm.environment.set("additionalNeeds", additionalNeeds)
```
  **Request Body:** 
 ```console 
  {
	  "firstname" : "{{firstName}}",
	  "lastname" : "{{lastName}}",
	  "totalprice" : {{totalPrice}},
	  "depositpaid" : {{depositPaid}},
	  "bookingdates" : {
    	  "checkin" : "{{checkin}}",
    	  "checkout" : "{{checkout}}"
	  },
	  "additionalneeds" : "{{additionalNeeds}}"
  }
```
  **Response Body:**
 ```console 
  {
    "firstname": "Lilyan",
    "lastname": "Williamson",
    "totalprice": 55,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2024-09-16",
        "checkout": "2024-09-21"
    },
    "additionalneeds": "alarm"
}
```

 ## _**5. Delete Booking Record**_

### Request URL: https://restful-booker.herokuapp.com/booking/bookingid
### Request Method: DELETE
### Response Body: None 

## Run Command:  
- Run Command for Console: 
```console 
newman run "Sazzad_Alam_Tomal_01521333429_RestfulBooker_APITesting.postman_collection.json" -e RestfulBookerEnvironment.postman_environment.json
```
- Run Command for Report: 
```console 
newman run "Sazzad_Alam_Tomal_01521333429_RestfulBooker_APITesting.postman_collection.json" -e RestfulBookerEnvironment.postman_environment.json -r cli,htmlextra
```

## Newman Report Summary:
![Dashboard](https://github.com/user-attachments/assets/dd5e5747-2e71-4039-905a-d89cc1b1906e)
![Iterations](https://github.com/user-attachments/assets/f022718b-4b77-4b66-a62e-f4ee776b11b2)
![Failed](https://github.com/user-attachments/assets/fc7f86d4-36af-41ea-87c0-8ed644d56a39)
![Skipped](https://github.com/user-attachments/assets/7097cf47-69f9-42be-8107-89fb5cbb3bb0)

