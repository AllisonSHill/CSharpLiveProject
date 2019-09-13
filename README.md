# Live Project

## Intro:

At the end of my time at the Tech Academy, I spent six weeks working with a team of fellow students to develop a full scale MVC/MVVM Web Application in C#. It was structured in two week sprints, during which I focused on both Front-End and Back-End development stories. 

## Front End Stories:

### Create ShiftTime Modal

The first story was the front-end development of a modal on the Job Creation page to add shift times to new jobs as they were created. The request was for the addition of a button in the existing Job Create form, in place of an existing text box to add shift times, that would launch a ShiftTime Modal. The modal wanted to contain a series of text boxes for a default shift time, as well as the ability to enter alternate shift times for every day of the week. The story specifically stated that the modal be a separate partial view, within the Jobs folder. After I completed this story, I took a back end story /Link this here/ for the initial implementation of the modal's functionality. 

```
@model ManagementPortal.Models.ShiftTime

@{
    ViewBag.Title = "Create";
}

<div id="ShiftTimeModal" class="modal fade hidden-print" tabindex="-1" role="dialog">
    <div class="modal-dialog modalShiftTimes" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                </button>
                <h4 class="modal-title">Modify Shift Times</h4>
            </div>
            <div class="modal-body">
                <div id="formContent">
                    @using (Html.BeginForm("Create", "ShiftTimes", FormMethod.Post, new { id = "form-shiftTimeAdd" }))
                    {
                        <div class="form-horizontal">
                            <div class="form-group">
                                @Html.LabelFor(model => model.Default, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Default, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Default, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Monday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Monday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Monday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Tuesday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Tuesday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Tuesday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Wednesday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Wednesday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Wednesday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Thursday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Thursday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Thursday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Friday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Friday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Friday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Saturday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Saturday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Saturday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                            @Html.ValidationSummary(true, "", new { @class = "text-danger" })
                            <div class="form-group">
                                @Html.LabelFor(model => model.Sunday, htmlAttributes: new { @class = "control-label col-md-2" })
                                <div class="col-md-6">
                                    @Html.EditorFor(model => model.Sunday, new { htmlAttributes = new { @class = "form-control" } })
                                    @Html.ValidationMessageFor(model => model.Sunday, "", new { @class = "text-danger" })
                                </div>
                            </div>
                        </div>

                        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
                    }
                </div>
            </div>
        </div>
    </div>
</div>
```

### Chat Box Upgrade

The third story I worked on was upgrading the site's chat feature. The chat feature was already set up to open on all logged in user's screens when a message was sent, as well as save the messages in a database and populate old messages every time the Chat Modal was launched. I created chat bubbles based on a sample image I was given. 

//screenshot of sample image

```
.chatBubbles {
    border-radius: 20px;
    padding: 8px 15px;
    display: inline-block;
    background-attachment: fixed;
    position: relative;
}

#myChat {
    text-align: right;
    color: white;
    margin-top: 0px;
    margin-bottom: 4px;
    background: grey;
    margin-right: 8%;
    margin-left: 25%;
    float: right;
}

#myChat::before {
    content: "";
    position: absolute;
    z-index: 0;
    bottom: 0;
    right: -8px;
    height: 20px;
    width: 20px;
    background: grey;
    background-attachment: fixed;
    border-bottom-left-radius: 15px;
}

#myChat::after {
    content: "";
    position: absolute;
    z-index: 1;
    bottom: 0;
    right: -10px;
    width: 10px;
    height: 20px;
    background: white;
    border-bottom-left-radius: 10px;
}

#yourChat {
    text-align: left;
    color: black;
    margin-top: 10px;
    margin-bottom: -5px;
    background: #DADADA;
    margin-left: 8%;
    margin-right: 25%;
}

#yourChat::before{
    content: "";
    position: absolute;
    z-index: 0;
    bottom: 0;
    left: -7px;
    height: 20px;
    width: 20px;
    background: #DADADA;
    border-bottom-right-radius: 15px;
}

#yourChat::after {
    content: "";
    position: absolute;
    z-index: 1;
    bottom: 0;
    left: -10px;
    width: 10px;
    height: 20px;
    background: white;
    border-bottom-right-radius: 10px;
}

#myName {
    text-align: right;
    float: right;
    margin-top: -10px;
    margin-bottom: -4px;
}

#yourName {
    text-align: left;
    margin-top: -20px;
}
```

For bonus functionality, I added script to allow new chat messages to be sent by hitting the enter key, and I changed the direction the message populated and scrolled to be more intuitive. 

```
//use enter key to send new chat message
$("#message-box").keyup(function (e) {
    if (e.keyCode === 13) {
        $("#send-message").click();
    }
});
```
```
//populates messages from database into messenger on startup
chat.client.populateMessages = function (messageList, me) {
    for (var message in messageList) {
        var userName = messageList[message]['UserName'];
        if (userName == me) {
            $('#discussion').prepend('<li><div id="myChat" class="chatBubbles">' + messageList[message]['Message'] + '</div></li><br><br><div id="myName"><sub>' + messageList[message]['UserName'] + '</sub ></div><br>');
        }
        else {
            $('#discussion').prepend('<li><div id="yourChat" class="chatBubbles">' + messageList[message]['Message'] + '</div></li><sub>' + messageList[message]['UserName'] + '</sub >');
            continue;
        }
    }
};  
```
```
//prints newly sent instant message to everyones messenger
chat.client.receiveMessage = function (userName, me, message) {
    if (userName == me) {
        $('#discussion').append('<li><div id="myChat" class="chatBubbles">' + message + '</div></li><br><br><div id="myName"><sub>' + userName + '</sub></div><br>');
    }
    else {
        $('#discussion').append('<li><div id="yourChat" class="chatBubbles">' + message + '</div></li><sub>' + userName + '</sub>');
    }
    $('#discussion').animate({
        scrollTop: $('#discussion').get(0).scrollHeight
    }, 800);
};
```

The most challenging part of this story was figuring out how to change the styling of the chat bubbles based on the currently logged in user, so the user would see their chat messages on the right of the module, and a different color than everyone else's chat. The solution ended up being very simple:  

```
string me = Context.User.Identity.Name;
```

//screenshot of final chat view

## Back End Stories:

### Implement ShiftTime Modal

The goal of this story was to write a function for the ShiftTime Modal to save a ShiftTime object and match it with a job that is being created. There was a note in the story that there would be a follow up story to link the ShiftTime to the correct Job in the database. I accomplished this task by adding to the Create function within the JobsController, using a bind statement to submit the data from the ShiftTime Modal through clicking the Submit button of the parent Add Job form. 

```
// POST: Jobs/Create
[HttpPost]
[ValidateAntiForgeryToken]
public ActionResult Create([Bind(Include = "JobIb,JobTitle,JobType,Active,Location,Manager")] Job job,
    [Bind(Include = "ShiftTimeId,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday,Sunday,Default")] ShiftTime shiftTime)
{
    shiftTime.Job = job;
    PopulateJobDropDowns(job);
    var LocationId = Request.Form["LocationSelector"].ToString();
    var ManagerId = Request.Form["ManagerSelector"].ToString();
    if (ModelState.IsValid)
    {
        job.Location = db.JobSites.Find(Int32.Parse(LocationId));
        job.Manager = db.Users.Find(ManagerId);
        db.Jobs.Add(job);
        db.ShiftTime.Add(shiftTime);
        db.SaveChanges();
        return RedirectToAction("Index");
    }
 ```
```
maybe add more? tbd.
```

### Job to Schedules Function

From story: We will want to be able to display the schedule items sorted by job. To allow for future functionality to filter these by person or by date, etc, We need a function that takes a specific list of schedule items and builds a dictionary item where the key is the job and the value is the list of schedules for that job. 

### Back End: Calendar Pull Existing Schedule

From story: The calendar allows for people to set their schedule for time off, but we want it to also populate the events currently scheduled. Create a method within the Calendar Controller that will check for existing schedule items and add them to the calendar. 

//screenshot of ShowScheduleItems method

Optional add-on:
Change the calendar class so it also references a schedule item, and have the one to one relationship cascade on delete.

//maybe screenshot of DeleteEvent method? Probably not though because its not impressive. Probably delete the whole optional add on as a thing and roll with the required part. 

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
