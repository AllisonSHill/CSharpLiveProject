# Live Project

## Intro:

At the end of my time at the Tech Academy, I spent six weeks working with a team of fellow students to develop a full scale MVC/MVVM Web Application in C#. It was structured in two week sprints, during which I focused on both Front-End and Back-End development stories. 

## Front End Stories:

### Create ShiftTime Modal

The first story was the front-end development of a modal on the Job Creation page to add shift times to new jobs as they were created. The request was for the addition of a button in the existing Job Create form, in place of an existing text box to add shift times, that would launch a ShiftTime Modal. The modal wanted to contain a series of text boxes for a default shift time, as well as the ability to enter alternate shift times for every day of the week. The story specifically stated that the modal be a separate partial view, within the Jobs folder. After I completed this story, I took a back end story /Link this here/ for the initial implementation of the modal's functionality. 

//screenshot of partial view code

### Chat Box Upgrade

The third story I worked on was upgrading the site's chat feature. The chat feature was already set up to open on all logged in user's screens when a message was sent, as well as save the messages in a database and populate old messages every time the Chat Modal was launched. I created chat bubbles based on a sample image I was given. 

//screenshot of sample image
//screenshot of css

I then added a script to allow the messages to be sent using the enter key. 

//script for enter key function

The most challenging part of this story was figuring out how to change the styling of the chat bubbles based on the currently logged in user, so the user would see their chat messages on the right of the module, and a different color than everyone else's chat. I ended up using a combination of code within the ChatHub controller as well as the JS. 

//screenshot of chat function
//screenshot of final chat view

## Back End Stories:

### Implement ShiftTime Modal

The goal of this story was to write a function for the ShiftTime Modal to save a ShiftTime object and match it with a job that is being created. There was a note in the story that there would be a follow up story to link the ShiftTime to the correct Job in the database. I accomplished this task by adding to the Create function within the JobsController, using a bind statement to submit the data from the ShiftTime Modal through clicking the Submit button of the parent Add Job form. 

//screenshot of JobsController create function

### Job to Schedules Function

From story: We will want to be able to display the schedule items sorted by job. To allow for future functionality to filter these by person or by date, etc, We need a function that takes a specific list of schedule items and builds a dictionary item where the key is the job and the value is the list of schedules for that job. 

### User-Role Assignment Must Be Required and Save Changes Minor Bug

From stories: 
When the Admin creates a new user (on CreateUserRequest/Create)
there is a drop down option to assign the new user a "Role". This must be a required field and the Admin shouldn't be allowed to create a new user  (submit the page) without a role. 

In Manage/EditAccountInfo view page, the save changes button is serving its purpose by saving the changes. But more than that, it should also take the user back Mange/Index page or (Home/Dashboard) when clicked. 

Each of these stories needed only one line of code to complete them, so I finished them up quickly. 

### User Manager Clean Up

I chose to work on a story that addressed four separate bugs in the User Manager. This was a board where the site Admin could update user roles and delete users. 

From story:
1) There is sometimes an error message stating that a user is already in a role they are being assigned to. This means that we are not unassigning the old role when changing the role. Add logic to the back end to unassign the user from the previous role before assigning them to the new role.

2) The error message for not deleting someone from the database who is on the schedule displays the users GUID instead of their name when alerting the admin they cannot delete this user. Change this to be the user's display name.

3) The message asking if the admin is sure they want to delete a user displays the username. Change this to the display name.

4) There should be a cancel option for assigning the role or deleting the user. Make sure there are two buttons on the pop-up message, one for OK and one for Cancel. The cancel one should use a cancel function that does not complete the action.

While working on this story, I ran into some issues that revelealed to the PM that the UserController needed to be refactored. A separate story was created for this, and I took that too because I was familiar with the errors that were currently happening. 

### Refactor User Controller

From story: 
1) Refactor the _UserList method so it grabs the list of users from the database, and sends that list as the model instead of going through what was the process of creating a UserVM. 
2) Exclude the UserVM from the project, test to make sure nothing is dependent on it. Remove any dependencies you find, and delete the User VM.
3) Determine what if anything the Index Users view is doing, and modify it to simply display a list of all users.
4) Determine what if anything the isAdminUser is doing. Replace it with the built in Identity method of checking roles.
5) Add comments to the Users Controller documenting the functions and their purpose, and where they are used.
