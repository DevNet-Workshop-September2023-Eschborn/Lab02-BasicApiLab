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

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/4190441d-853e-4215-b914-7e16c402dd51)


Click on skip or sign in, if you do have an account or want to create one.

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/c7b2fb91-c3a5-4cc7-baa5-0e0b4b9ef8d3)


Create a new collection “deckofcards”. The Collection is used to store, group and sort the requests you made to reuse them later.

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/eae715e1-7fda-4bea-8452-6cdfd8b49d72)


Right Click on deckofcards and create a new request

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/2aa41ae7-17f0-418b-a806-23e450947337)


Create your first request for Level 1. All API Endpoints you need are documented on the Deck of Cards homepage.

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/d676079d-3f0c-4149-9b0d-c62f2b22eade)


Level 1: 
1. Get a deck of cards
2. Shuffle the deck (use the same deck you got in step 1)
3. Draw a card from the shuffled Deck

-----

### Working with envorinments

Postman offers the posibillity to create "Environments" this is a set of variables which you can use in your calls. This offers you the possibility to create and use the same API calls in different environments. In addition, these variables can automatically be filled with values from previous calls. To use the environment variables in your calls, you can reference them like that {{variableName}}

Level 2:
1. Create an environment
2. Add the deck of cards url as a variable
3. Use this variable in your next tasks

1. Get a deck
2. Save the Deck ID in the environment
3. Shuffle the deck using a deck as variable
4. Draw a card using the variable

### Using return values

For the next tasks we will be using the return values from previous calls. We are assuming that we are working with json responses, which we can parse and reuse in Postman. For everyone not familiar with Java Script, we will provide the code below. The only thing you have to change the desired target variable name and which value should be stored there. Just use and modify the API calls you used before.

```
Create an environment Variable -> and work with this code under “Tests”

var jsonData = JSON.parse(responseBody); //this line takes the response and makes it available as a json object
postman.setEnvironmentVariable(“variable_name", jsonData.whateverineed);
```

Level 3:
1. Get a deck
2. Save the Deck ID in the environment
3. Shuffle the deck using a deck as variable
4. Draw a card using the variable



### APIC API

1. Login to the APIC via WebUI (credentials provided by instructor)

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/fe10fdc4-6e89-4bbf-b39e-e5432d028c2d)


2. Open Postman and create a new collection

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/f79fa80e-96b7-480f-9ead-3b3e8102ee96)


3. Create your APIC environment

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/b8f37d6b-0bfc-4318-a114-a4dd89a186ba)


4. Add the Variables to the Environment
  - apic
  - username
  - password

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/30f1ccfa-514f-4ed7-9a38-af3956950d3e)

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

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/7c989b2a-78b5-40a4-91df-9be6adb17bd1)


3. Create a new Tenant with the name of your user
4. Filter for POST in the API Inspector window and find the URL ending with tn-[yourtenantname]
5. Observe the API Inspector and copy the payload aswell as the URL in a new Postman request

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/1366ce19-119f-4031-adca-a9f3116922ec)


6. Use your Postman Login request to Login to the APIC
7. Delete your tenant with the “Delete” Method

![image](https://github.com/DevNet-Workshop-September2023-Eschborn/Lab02-BasicApiLab/assets/66415321/2aa4ddaf-429e-4c1b-8eb8-989cafaf5861)

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

## API Bonus

### 1 Query for all Faults in the fabric

### 2 Create Following Structure and use the deck of cards api for naming
Try to work with the environment as much as possible

1. Get a new Deck
2. Shuffle the deck
3. Log into APIC
4. Create a Tenant
5. Create VRF
6. Create a Bridge domain
8. Create an Application Profile
9. Draw 3 times a card and name the EPGs after the cards name
