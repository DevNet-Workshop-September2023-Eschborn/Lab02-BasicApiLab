# Slot--Basic-API-Lab

# Basic API Lab

### Ressourcen

| Student Number  | Workstation |  Zugang |
| ------------- | ------------- | ------------- |
| deckofcards | https://www.deckofcardsapi.com/  |  
| Postman | https://www.postman.com/downloads/ | 
| APIC        | https://10.2.0.43/               | wsuser{studentnumber}/DevnetWorkshop! |

In this lab you will install Postamn and learn how to do basic requests to the Deck of Cards API. We will work with environment in Postman and extract and reuse values from the requests you made. When you are done with the tasks on the Deck of Cards API, we will cover the basic interaction with the ACI APIC.

### Work with Postman

Install Postman on your laptop https://www.postman.com/downloads/, if this is not possible use your assigned workstation

Open Postman

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/397c5a1f-197b-4239-b357-7c5a8e0c2b82)

Click on skip or sign in, if you do have an account or want to create one.

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/2bb928a3-036f-4fbc-aa48-91870008f02d)

Create a new collection “deckofcards”. The Collection is used to store, group and sort the requests you made to reuse them later.

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/3e65c8e4-82d0-404b-ac75-671b818bd0f8)

Right Click on deckofcards and create a new request

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/99645157-e5ed-4439-97e5-0dc45ab09f3f)

Create your first request for Level 1. All API Endpoints you need are documented on the Deck of Cards homepage.

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/1c66cf3a-a9d5-409b-a3eb-776be7d9e507)

Level 1: 
1. Get a deck of cards
2. Shuffle the deck (use the same deck you got in step 1)
3. Draw a card from the shuffled Deck

### APIC API

1. Login to the APIC via WebUI (credentials provided by instructor)

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/24b1f0e5-1162-4d3e-b1c2-e013d22b33b2)

2. Open Postman and create a new collection

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/96e7f054-1d8f-4a73-9c56-519c1a1698c3)

3. Create your APIC environment

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/8453034b-6853-4552-a8e5-0c41fc8e5560)

4. Add the Variables to the Environment
  - apic
  - username
  - password

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/5d9230b0-c2c8-4318-90e3-dc62e231fb44)
 
5. Create APIC Login request
  - Create a POST Request with following URL
    https://{{apic}}/api/aaaLogin.json

  - Enter the Following Body under the RAW section of the request
```
{
    "aaaUser": {
        "attributes": {
            "name": "{{username}}",
            "pwd": "{{password}}"
        }
    }
}
```
6. Send the Request and observe the response

Proceed if Response Status is 200 OK


## Lab 2 - Tenant Creation

1. Login via the Webbrowser to the APIC
2. Open the API Inspector

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/c40f37ba-500e-456d-94e6-8ab29e16fa4f)

3. Create a new Tenant with the name of your user
4. Filter for POST in the API Inspector window and find the URL ending with tn-[yourtenantname]
5. Observe the API Inspector and copy the payload aswell as the URL in a new Postman request

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/86f5f74e-6fc5-43fa-9ede-b54a3afd17b6)

6. Use your Postman Login request to Login to the APIC
7. Delete your tenant with the “Delete” Method

![image](https://github.com/DevNet-Workshop-May-2023/Lab02-BasicApiLab/assets/57700911/930512e6-cb73-47ff-8279-c0339b71c4b6)

8. Recreate the Tenant by changing the Method to “POST”

## Lab 3 - Query the APIC

### Query the Endpoint table of the APIC

1. Using the API Inspector to search Endpoints. 
   Go To Operations -> EP Tracker -> search for 10.2.128.13 and observe the API Inspector
2. Create a new “GET” request with the URL from the API Inspector to query for the Endpoint

### Query the Healthscore of all leafs
1. Use the Main Dashboard page
2. Capture the page loading with the API Inspector and look for “health”
3. to query remove “subscription” behind API Call

## Bonus

### Deck of cards - Level 2

1. Get a deck
2. Save the Deck ID in the environment
3. Shuffle the deck using a variable
4. Draw a card using the variable


Hint: 
Create an environment Variable -> and work with this code under “Tests”

var jsonData = JSON.parse(responseBody);
postman.setEnvironmentVariable(“variable_name", jsonData.whateverineed);

## APIC API Bonus

### Query for all Faults in the fabric

### Create Following Structure
1. Tenant
2. VRF
3. bridge domain
4. Application Profile containing 3 EPGs Web, DB, APP
