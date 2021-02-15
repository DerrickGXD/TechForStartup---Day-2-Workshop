# TechForStartup---Day-2-Workshop-1 (Client Server System Design)

# Codes
Coding Question : [Click Here](https://codesandbox.io/s/tech-workshop-question-client-server-system-design-s1ui3?file=/src/index.js)
<br/>
Full Working Code : [Click Here](https://codesandbox.io/s/tech-workshop-client-server-system-design-ohf50?file=/src/index.js)

Please try to attempt the coding question before looking at the full working code.

# Scenario
iCUBE would like to create a website to allow participants to register for Tech For Startups. To keep track of the name of participants who sign up, we will be using a server. For simplicity in our workshop, we will only keep track of the name of last participant who sign up. When a user signs up, the server should update its variable **name** with the name used to sign up. To ensure the website still keeps track of the name in another page, iCUBE creates another page. When the user clicks **Next Page** and goes to another page, the website can still retrieve the name from server.

The back end server script is `index.js`. The front end website scripts are `main_page.html` and `next_page.html`. We will be using **REST API** to communicate between front end and back end. In simple terms, the front end can request a query to back end with an endpoint starting with "/" and the back end will send front end with what it requests. We will be using **XMLHTTPRequest** in front end to submit a query and **Express.js** in back end to receive a query.

# Tasks
1. Identify how `index.js` receives a query via endpoints. When a server starts, it will first receive a query with "/". Currently after receiving "/", the server sends a message *Welcome to Tech For Startups!!*. Instead of sending this message, you should display `main_page.html` to show the registration page.
2. The registration page has a form to fill in first name, last name and team name. Clicking the submit button will request a query to the back end with endpoint "/register". `main_page.html` already has the code to request a query to the endpoint, alongside with first name, last name and team name. What you need to do is process the query in `index.js`. You should save the variable **name** with full name (first name + last name), and sends a reply to the front end with a message *{Name} From {Team Name} Has Registered!*. If `main_page.html` successfully recieves , the `main_page.html` should replace *Anonymous Has Registered!* with the message.
3. In `next_page.html`, write the **XMLHTTPRequest** to request **name** from `main_page.html`. Use the endpoint "/name" to submit a query. Refer to `main_page.html` on how to write **XMLHTTPRequest**. You should also replace the text *Anonymous* with the name that you requested.
4. In `index.js`, implement the GET query for the endpoint "/name" and send the variable **name** back to front end.
5. Check whether the code is working. At `main_page.html`, register a participants. Click **Next Page** and you should see **Well Done Anonymous** is replaced with **Well Done {name}**.

# TechForStartup---Day-2-Workshop-2 (Model View Controller)

# Codes
Coding Question : [Click Here](https://codesandbox.io/s/tech-workshop-question-model-view-controller-lu2fd?file=/index.html)
<br/>
Full Working Code : [Click Here](https://codesandbox.io/s/tech-workshop-model-view-controller-11lhe?file=/index.html)

Please try to attempt the coding question before looking at the full working code.

# Scenario
iCUBE would like to create an internal app for both Marketing and Event teams. The app helps both teams to track the number of participants in the team. Whenever students sign up, they will reach out the head of Event team and tell their availability for the event (will attend or might attend). The head of Event will fill in the **Add Participants Form** in the main page with the student's name and availability. The Marketing team is interested in the number of sign-ups for the event, while the Event team is interested in the minimum number of turnouts for the event. Hence, the app should do the following:

1. Below **Participants List (Marketing Team)**, display the list of participants who *WILL ATTEND* or *MIGHT ATTEND* the event.
2. Below **Participants List (Event Team)**, display the list of participants who *WILL ATTEND* the event.

# Tasks
We will be using a simple **Model View Controller** system design for this app. We have created `model.js`, `view.js` and `controller.js` for each class. The system designs that iCUBE would like to build is as follows:

1. Model and View will be connecting with the Controller, but Model and View do not connect with each other. This is already written in `init.`
2. Whenever submit button is clicked, the function `submitEvent` in View will be called. View should get the input of name and status ("will" or "might"), sends them to Controller (by calling `updateParticipantsList` in Controller) and inform it to update participant list.
3. When the Controller is notified, it sends the name to the Model (by calling `addMarketing` or `addEvent` in Model depending on the status) and inform it to update its lists.
4. When the Model is notified, it will update **marketing_list** (list of names who will or might attend) and **event_list** (list of names who will attend) depends on the functions invoked.
5. The Model will send the latest **marketing_list** and **event_list** to Controller (by calling `updateDisplayList` in Controller) and inform it to update the lists to display.
6. When the Controller is notified, it converts both lists to strings, sends them to View (by calling `changeDisplay` in View) and inform it to update the lists to display.
7. When the View is notified, it updates the display with new list.
