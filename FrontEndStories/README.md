# Front End Stories

This is where the intro goes. This is where I write about my overall experience. Wheeeee

### Table of Contents:

[4973 - Create ShiftTime Modal](#create-shifttime-modal)

[4997 - Chat Box Upgrade](#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](#navbar-vital-change-and-vertical-navigation-bar-final-touch)

[5148 - Implement Contact Us Page](#implement-contact-us-page)

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

[Back to Table of Contents](#front-end-stories)

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

[Back to Table of Contents](#front-end-stories)

### NavBar Vital Change and Vertical Navigation Bar Final Touch

CONTENT GOES HERE

[Back to Table of Contents](#front-end-stories)

### Implement Contact Us Page

```
@model ManagementPortal.Models.ContactUs
@{
    ViewBag.Title = "Contact";
}
<h2>Contact Us</h2>
@using (Html.BeginForm())
{
    @Html.AntiForgeryToken()
<div class="form-horizontal" id="contactContainer">
    @Html.ValidationSummary(true, "", new { @class = "text-danger" })
    <div class="form-group">
        <label for="Name" class="control-label col-md-2">Name *</label>
        <div class="col-md-10">
            @Html.EditorFor(model => model.Name, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
            @Html.ValidationMessageFor(model => model.Name, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        <label for="Email" class="control-label col-md-2">Email Address *</label>
        <div class="col-md-10">
            @Html.EditorFor(model => model.Email, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
            @Html.ValidationMessageFor(model => model.Email, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        <label for="Phone" class="control-label col-md-2">Phone Number</label>
        <div class="col-md-10">
            @Html.EditorFor(model => model.Phone, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
            @Html.ValidationMessageFor(model => model.Phone, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        <label for="Subject" class="control-label col-md-2">Subject</label>
        <div class="col-md-10">
            @Html.EditorFor(model => model.Subject, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
            @Html.ValidationMessageFor(model => model.Subject, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        <label for="Message" class="control-label col-md-2">Message *</label>
        <div class="col-md-10">
            @Html.EditorFor(model => model.Message, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
            @Html.ValidationMessageFor(model => model.Message, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        <p class="col-md-2">*<small> required fields</small></p>
    </div>
    <div class="form-group">
        <div class="col-md-offset-2 col-md-10">
            <input type="submit" id="contactUs" value="Send" class="btn-base btn-w-100px" />
        </div>
    </div>
    <div>
        <div>
            @if (ViewBag.Message != null)
            {
                <div>@ViewBag.Message</div>
            }
        </div>
    </div>
</div>
}
```

I also had to add a link to the home page for visitors to the site to access the contact form. 

```
<h5 class="card-title">Want to send us a message?</h5>
					<input type="button" class="home_btn" onclick="location.href='@Url.Action("Index", "ContactUs")'" value="Contact Us">
				</div>
			</div>
			<div class="col-4 ">
```

This was a full stack story, to look at the back end functionality I added, check out its other half. 
[Back end Components](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#implement-contact-us-page)

[Back to Table of Contents](#front-end-stories)
