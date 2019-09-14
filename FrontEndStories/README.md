# Front End Stories

This is where the intro goes. This is where I write about my overall experience. Wheeeee

### Table of Contents:

[4973 - Create ShiftTime Modal](#create-shifttime-modal)

[4997 - Chat Box Upgrade](#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](#navbar-vital-change-and-vertical-navigation-bar-final-touch)

### Create ShiftTime Modal

[Back to Top](#front-end-stories)

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

[Back to Top](#front-end-stories)

### Chat Box Upgrade

[Back to Top](#front-end-stories)

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

[Back to Top](#front-end-stories)

### NavBar Vital Change and Vertical Navigation Bar Final Touch

[Back to Top](#front-end-stories)

CONTENT GOES HERE

[Back to Top](#front-end-stories)
