# Vonage SMS Verification Using Vonage API

## Set up 
- Register your own Vonage account. 
- Copy down the API secret and token. 
- Create a local .env file similiar to .env.example and paste your own API token and secret.
- Install dependancies: `npm i`.
- Run the server: `node server.js`. 
- Go to `http://localhost:3000` to begin. 

## Routes
We have the following routes in our application: 
- `/` - the home page, where you will determine if a user is authenticated and prompt them to authenticate if not
- `/authenticate` - to display a page where the user can enter their phone number
- `/verify` - when the user has entered their phone number, redirect here to start the verification process and display a page where they can enter the code that they receive
- `/check-code` - when the user has entered the verification code, this endpoint will use the Verify API to check if the code that they entered is the one that they were sent
- `/cancel` - to remove any session details and send the user back to the home page

## API request 
1. Send the verification request

We start the verification process by using the Verify API request endpoint to generate a verification code and send it to the user. 
By default, the first verification attempt is sent by SMS. If the user fails to respond within a specified time period then the API makes a second and, if necessary, third attempt to deliver the PIN code using a voice call. 

2. Check the verification code

To verify the code submitted by the user we make a call to the Verify check endpoint. We pass in the request_id (which was returned by the call to the Verify request endpoint in the previous step).
The response tells us if the user entered the correct code. If the status is zero then the code they entered is the same one that they were sent. In that case, create a user session object.
After checking the code, return user to the home page.
