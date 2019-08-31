# LiveProjectSprint1

At the end of my time at the Tech Academy, I worked on a group project intended to simulate a real-world team development environment. My fellow students and I worked together in two-week sprints to develop a full scale MVC application for a real client. During my first two week sprint, I worked on three stories. 

The first story was the front-end development of a modal on the Job Creation page to add shift times to new jobs as they were created. The request was for the addition of a button in the existing Job Create form, in place of an existing text box to add shift times, that would launch a ShiftTime Modal. The modal wanted to contain a series of text boxes for a default shift time, as well as the ability to enter alternate shift times for every day of the week. The story specifically stated that the modal be a separate partial view, within the Jobs folder. 

//screenshot of partial view code

After I finished the front end story and created a modal in which to enter shift times, I took on a second story for the initial implementation of the modal's functionality. The goal of this story was to write a function for the ShiftTime Modal to save a ShiftTime object and match it with a job that is being created. There was a note in the story that there would be a follow up story to link the ShiftTime to the correct Job in the database. I accomplished this task by adding to the Create function within the JobsController, using a bind statement to submit the data from the ShiftTime Modal through clicking the Submit button of the parent Add Job form. 

//screenshot of JobsController create function

The third story I worked on was upgrading the site's chat feature. The chat feature was already set up to open on all logged in user's screens when a message was sent, as well as save the messages in a database and populate old messages every time the Chat Modal was launched. I created chat bubbles based on a sample image I was given. 

//screenshot of sample image
//screenshot of css

I then added a script to allow the messages to be sent using the enter key. 

//script for enter key function

The most challenging part of this story was figuring out how to change the styling of the chat bubbles based on the currently logged in user, so the user would see their chat messages on the right of the module, and a different color than everyone else's chat. I ended up using a combination of code within the ChatHub controller as well as the JS. 

//screenshot of chat function
//screenshot of final chat view

