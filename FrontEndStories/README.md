# Front End Stories

This is where the intro goes. This is where I write about my overall experience. Wheeeee

### Table of Contents:

[4973 - Create ShiftTime Modal](#create-shifttime-modal)

[4997 - Chat Box Upgrade](#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](#navbar-vital-change-and-vertical-navigation-bar-final-touch)

[5177 & 5178 - NavBar Icon Updates](#navbar-icon-updates)

[5148 - Implement Contact Us Page](#implement-contact-us-page)

[5162 - ChatModal Header Bug](#chatmodal-header-bug)

[5151 - Mobile Friendly Design](#mobile-friendly-design)

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

Added link to launch the Modal in the Create Job page.
```
@{Html.RenderPartial("~/Views/Jobs/_shiftTimeModal.cshtml");}
        <div class="createBtn">
            <button type="button" class="btn btn-default" data-toggle="modal" data-target="#ShiftTimeModal">
                Add Shift Times
            </button>
        </div>
```
When I finished this story, I chose to implement the Modal's functionality as my next story: [Back End: Implement ShiftTime Modal](https://github.com/allisonhill00/CSharpLiveProject/tree/master/BackEndStories#implement-shifttime-modal)

[Back to Table of Contents](#front-end-stories)

### Chat Box Upgrade

The third story I worked on was upgrading the site's chat feature. The chat feature was already set up to open on all logged in user's screens when a message was sent, as well as save the messages in a database and populate old messages every time the Chat Modal was launched. I created chat bubbles based on a sample image I was given. 

//screenshot of sample image

```
#discussion {
    overflow: auto;
    font-size: .9em;
    padding: 0px;
    list-style-type: none;
    overflow-y: scroll;
    max-height: 200px;
}

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

#message-box {
    resize: none;
    width: 80%;
    height: 35px;
    padding: 5px;
    border-radius: 5px;
    vertical-align: bottom;
    font-size: .9em;
}

#send-message {
    color: white;
    background-color: gray;
    height: 40px;
    width: 65px;
}
```
```
function openChat() {
    $("#chat-modal").fadeIn("slow");
    $("#chatIcon").fadeOut("slow");
    $('#discussion').animate({
        scrollTop: $('#discussion').get(0).scrollHeight
    }, 0);
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
In the ChatHub Controller, then I simply passed the variable me into the js functions. 
//screenshot of final chat view

[Back to Table of Contents](#front-end-stories)

### NavBar Vital Change and Vertical Navigation Bar Final Touch

There was already a navbar, but it didn't have the functionality desired. (SCREEN SHOTS FROM STORY HERE)
I basically started over with the CSS, using none of the existing styling. 

From story:
- The side-nav will have two states. (Opened stated & Collapsed state see images ABOVE.)
- On Collapsed state, we should only see the icons for the navigation items. While on Opened state, all their names are visible.
- On Collapsed state, if you click on one of the icons, additional icons for child items (ViewAll or Create) shows up under the parent icon. See image below or refer to Azure Dev Ops sidebar functionality. 
- The three bars (hamburger menu) is responsible for opening and collapsing the side-nav.
- The side-nav should be static and shouldn't be affected by scrolling.
- The side-nav should not cover or in any way interfere with the contents of the page opened in either state.
- It should be responsive to mobiles and small screens.
- Don't forget to add the Social Media icons and the copyright text as shown in the image.

//ADD IMAGES FROM STORY

Scootched the content over, needed breakpoints for that too: 
```
body {
    font-family: "Trebuchet MS", Helvetica, sans-serif;
    /*my adds **/
    background-image: url('images/bgPattern.png');
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
    margin: auto;
    padding-left: 80px; /*make space for collapsed navbar*/
}

/*override body padding to make header be full width*/
#header-nav {
    margin-left: -80px;
}

@media screen and (max-width: 480px) {
    body {
        padding-left: 45px
    }
    #header-nav {
        margin-left: -45px;
    }
}

@media screen and (min-width: 481) and (max-width: 768px) {
    body {
        padding-left: 60px
    }
    #header-nav {
        margin-left: -60px;
    }
}

@media screen and (min-width: 769) and (max-width: 991px) {
    body {
        padding-left: 70px
    }
    #header-nav {
        margin-left: -70px;
    }
}
```

```
/************BEGIN LEFT SIDE NAVBAR STYLING**********/

#menu.active {
    min-width: 230px;
    max-width: 230px;
    text-align: left;
}

#menu {
    min-width: 80px;
    max-width: 80px;
    text-align: center;
    height: auto;
    left: 0;
    background-color: white;
    position: absolute;
    z-index: 9998;
    font-family: serif;
    color: gray;
    white-space: nowrap;
}

.fa {
    padding-right: 15px;
    padding-left: 10px;
    color: gray;
    font-size: 1.5em;
}

#menu .social {
    font-size: 1.1em;
}

#menu.active .copyright {
    top: 45px;
    right: 82px;
}

#menu .copyright {
    transform: rotate(270deg);
    position: relative;
    top: 120px;
    bottom: 0px;
    right: 3px;
}

.copy-icon {
    font-size: .9em;
    padding: 5px;
}

#menu.active .sub-icon {
    padding-left: 15px;
}

#menu .sub-icon {
    padding-left: 5px;
    font-size: 1.2em;
    color: gray;
    cursor: pointer;
}

/*targets all list items*/
#menu ul,
#menu li,
#menu a {
    padding: 5px;
    padding-bottom: 8px;
    text-decoration: none;
    list-style-type:none;
}

/* Hide sub menus */
#menu ul ul {
    display: none;
}

#menu.active ul ul {
    visibility: visible;
}

/*hide menu item text in collapsed state*/
.nav-title {
    visibility: hidden;
}

.nav-sub-title {
    visibility: hidden;
}

/*main menu items expanded state styling*/
#menu.active .nav-title {
    font-size: 1.2em;
    color: rgb(117, 137, 138);
    visibility: visible;
}

.nav-title:hover {
    color: var(--dark-blue);
    cursor: pointer;
}

#menu.active .nav-sub-title {
    color: rgb(117, 137, 138);
    font-size: 1.1em;
    visibility: visible;
}

.nav-sub-title:hover {
    color: var(--dark-blue);
    cursor: pointer;
}

/*begin styles for open and close icons*/
#menu.active #dismiss {
    width: 50px;
    height: 50px;
    position: relative;
    top: 10px;
    left: 10px;
    display: block;
    visibility: visible;
}

#menu #dismiss {
    display: none;
}

#menu #open-menu {
    width: 50px;
    height: 50px;
    position: relative;
    top: 10px;
    left: 10px;
    display: block;
}

#menu.active #open-menu {
    display: none;
}
/*end styles for open and close icons*/

/*styles for max width 480px*/
@media screen and (max-width: 480px) {
    #menu.active {
        display: none;
    }

    #menu {
        min-width: 45px;
        max-width: 45px;
        height: auto;
        text-align: center;
        padding-top: 8px;
    }

    .fa {
        padding-left: 17px;
        font-size: .8em;
    }

    #menu .social {
        font-size: .6em;
        padding-right: 20px;
    }

    #menu .copyright {
        font-size: .5em;
        position: relative;
        top: 50px;
        padding-bottom: 63px;
        margin-left: 52px;
        right: 0px;
    }

    .copy-icon {
        font-size: .6em;
        padding: 2px;
    }

    #menu .sub-icon {
        padding-left: 17px;
        font-size: .7em;
    }

    /*targets all list items*/
    #menu ul,
    #menu li,
    #menu a {
        padding: 0px;
        padding-bottom: 2px;
    }

    #menu #dismiss {
        display: none;
    }

    #menu #open-menu {
        margin-left: -300px;
        position: absolute;
        visibility: hidden;
    }
}/*end styles for max-width 480px*/

/*styles for max width 768px*/
@media screen and (min-width: 481px) and (max-width: 768px) {
    #menu.active {
        min-width: 170px;
        max-width: 170px;
    }

    #menu {
        min-width: 60px;
        max-width: 60px;
        height: auto;
    }

    .fa {
        padding-right: 10px;
        padding-left: 10px;
        font-size: 1.1em;
    }

    #menu .social {
        font-size: .8em;
    }

    #menu.active .copyright {
        top: 25px;
        right: 60px;
    }

    #menu .copyright {
        font-size: .7em;
        top: 80px;
        padding-bottom: 55px;
        margin-left: 50px;
        right: 3px;
    }

    .copy-icon {
        font-size: .8em;
        padding: 0px;
    }

    #menu.active .sub-icon {
        padding-left: 15px;
    }

    #menu .sub-icon {
        padding-left: 5px;
        padding-right: 5px;
        font-size: .9em;
    }

    /*targets all list items*/
    #menu ul,
    #menu li,
    #menu a {
        padding: 4px;
        padding-bottom: 1px;
    }

    /*main menu items expanded state styling*/
    #menu.active .nav-title {
        font-size: .9em;
    }

    #menu.active .nav-sub-title {
        font-size: .8em;
    }

    #menu.active #dismiss {
        width: 35px;
        height: 35px;
        top: 8px;
        left: 10px;
    }

    #menu #open-menu {
        width: 35px;
        height: 35px;
        top: 8px;
        left: 10px;
    }
} /*end styles for max-width 768px*/

/*styles for max width 991px*/
@media screen and (min-width: 769px) and (max-width: 991px) {
    #menu.active {
        min-width: 200px;
        max-width: 200px;
    }

    #menu {
        min-width: 70px;
        max-width: 70px;
        height: auto;
    }

    .fa {
        padding-right: 10px;
        padding-left: 10px;
        font-size: 1.3em;
    }

    #menu .social {
        font-size: 1em;
    }

    #menu.active .copyright {
        top: 40px;
        right: 70px;
    }

    #menu .copyright {
        font-size: .9em;
        top: 105px;
        bottom: 0px;
        right: 0px;
    }

    .copy-icon {
        font-size: 1em;
        padding: 0px;
    }

    #menu.active .sub-icon {
        padding-left: 8px;
    }

    #menu .sub-icon {
        padding-left: 0px;
        padding-right: 15px;
        font-size: 1.2em;
    }

    /*targets all list items*/
    #menu ul,
    #menu li,
    #menu a {
        padding: 5px;
        padding-bottom: 6px;
    }

    /*main menu items expanded state styling*/
    #menu.active .nav-title {
        font-size: 1.1em;
    }

    #menu.active .nav-sub-title {
        font-size: 1em;
    }

    #menu.active #dismiss {
        width: 35px;
        height: 35px;
        top: 8px;
        left: 10px;
    }

    #menu #open-menu {
        width: 35px;
        height: 35px;
        top: 8px;
        left: 10px;
    }
}
/*end styles for max-width 991px*/

/*************END LEFT NAVBAR STYLING*****************/
```

I also wrote new javascript functions, instead of opening and closing the navbar I simply toggled the active state. 

What was there before: (MAYBE KEEP TBD)
```
// BEGIN NAVBAR HOVER/MOUSE EFFECTS

 //Slide navbar icon with mouse cursor
//$(document).ready(function () {
//    $(window).on("mousemove", function (e) {
//        var yPos = e.pageY - 140;
//        if (e.pageY > 140) { // Prevents icon from going into header
//            $(".icon-slider").css("transform", "translateY(" + yPos + "px");
//        }
//        else {
//            $(".icon-slider").css("transform", "translateY(" + 0 + "px");
//        }
//    });
//});

//$(document).ready(function () {
//    $("#open-menu").on("click", function () {
//        $(".navbar-collapse").addClass("show");
//        $(".animated-icon").addClass("open");
//    });
//    $("#dismiss").on("click", function () {
//        $(".navbar-collapse").removeClass("show");
//        $(".animated-icon").removeClass("open");
//    });
//});
```

What I wrote: (DEFINITELY KEEP)

```
$(document).ready(function () {
    $('#open-menu').on('click', function () {
        $('#menu').toggleClass('active');
    });
});

$(document).ready(function () {
    $('#dismiss').on('click', function () {
        $('#menu').toggleClass('active');
    });
});
```

I refactored the whole HTML. MAYBE KEEP WHOLE THING MAYBE JUST DO "FROM THIS TO THIS" WITH INFO FROM POST-IT ON DIFFERENT COMPONENTS

```
@*/*********************NAVbar*******************/*@

<div class="wrapper">
<nav id="menu">
    <div id="open-menu">
        <i class="fa fa-reorder"></i>
    </div>
    <div id="dismiss">
        <i class="fa fa-times"></i>
    </div>

    <ul class="navbar-nav mr-auto">
        <li class="active"><a href="@Url.Action("Dashboard","Home")"><i class="fa fa-home"></i><text class="nav-title">Home</text></a></li>

        @if (User.IsInRole("Admin"))
        {
            <!-- Create Users - ADMIN ONLY -->
            <li class="has-sub">
                <a href="#" title="Users"><i class="fa fa-users"></i><text class="nav-title">Users</text></a>
                <ul>
                    <li><a href="@Url.Action("Create", "CreateUserRequest")" title="Add Users"><i class="fa fa-user-plus sub-icon"></i><text class="nav-sub-title">Add Users</text></a></li>
                    <li><a href="@Url.Action("Index", "CreateUserRequest")" title="Unregistered Users"><i class="fa fa-user-times sub-icon"></i><text class="nav-sub-title">Unregistered Users</text></a></li>
                    <li><a href="@Url.Action("Index", "Users")" title="All Users"><i class="fa fa-address-book sub-icon"></i><text class="nav-sub-title">All Users</text></a></li>
                </ul>
            </li>

            <!-- Jobs - ADMIN ONLY -->
            <li class="has-sub">
                <a href="#" title="Jobs"><i class="fa fa-clipboard"></i><text class="nav-title">Jobs</text></a>
                <ul>
                    <li><a href="@Url.Action("Index", "Jobs")" title="View All"><i class="fa fa-list sub-icon"></i><text class="nav-sub-title">View All</text></a></li>
                    <li><a href="@Url.Action("ManagedList", "Jobs")" title="Managed List"><i class="fa fa-edit sub-icon"></i><text class="nav-sub-title">Managed List</text></a></li>
                    <li><a href="@Url.Action("Create", "Jobs")" title="Create New"><i class="fa fa-plus-square-o sub-icon"></i><text class="nav-sub-title">Create New</text></a></li>
                </ul>
            </li>

            <!-- JobSites - ADMIN ONLY -->
            <li class="has-sub">
                <a href="#" title="Job Sites"><i class="fa fa-clipboard"></i><text class="nav-title">Job Sites</text></a>
                <ul>
                    <li><a href="@Url.Action("Index", "JobSites")" title="View All"><i class="fa fa-list sub-icon"></i><text class="nav-sub-title">View All</text></a></li>
                    <li><a href="@Url.Action("Create", "JobSites")" title="Create New"><i class="fa fa-plus-square-o sub-icon"></i><text class="nav-sub-title">Create New</text></a></li>
                </ul>
            </li>
        }

        <!--Shift Times, Commented out for story 4808, Need to relocate to manager dashboard when created.
    Drop down menu items need to be updated to new format 9/17/19-->
        @*<li class="has-sub">
        <a href="#"><i class="fa fa-clock-o"></i><text class="nav-title">Shift Times</text></a>
        <ul>
            <li>@Html.ActionLink("View All", "Index", new { controller = "ShiftTimes" }, new { @class = "dropdown-item" })</li>
            <li>@Html.ActionLink("Create New", "Create", new { controller = "ShiftTimes" }, new { @class = "dropdown-item" })</li>

                </ul>
            </li>*@

        <!--Schedules-->
        <li class="has-sub">
            <a href="#" title="Schedules"><i class="fa fa-calendar"></i><text class="nav-title">Schedules</text></a>
            <ul>
                @if (User.IsInRole("Admin"))
                {
                    <li><a href="@Url.Action("Index", "Schedules")" title="View All"><i class="fa fa-list sub-icon"></i><text class="nav-sub-title">View All</text></a></li>
                    <li><a href="@Url.Action("Create", "Schedules")" title="Create New"><i class="fa fa-plus-square-o sub-icon"></i><text class="nav-sub-title">Create New</text></a></li>
                    <li><a href="@Url.Action("Index", "Calendar")" title="Time Off Calendar"><i class="fa fa-calendar sub-icon"></i><text class="nav-sub-title">Time Off Calendar</text></a></li>
                }
                @if (User.IsInRole("Employee"))
                {
                    <li><a href="@Url.Action("Index", "Schedules")" title="My Schedule"><i class="fa fa-calendar-check-o sub-icon"></i><text class="nav-sub-title">My Schedule</text></a></li>
                    //This is currently pointing to the schedule index view - a new view will need to be created that shows only the employee's schedule
                }
            </ul>
        </li>

        <!--News-->
        <li id="news" class="nav-item dropdown">
            <a href="#" title="News"><i class="fa fa-newspaper-o"></i><text class="nav-title">News</text></a>
            <ul>
                <li><a href="@Url.Action("Index", "CompanyNews")" title="View All"><i class="fa fa-list sub-icon"></i><text class="nav-sub-title">View All</text></a></li>
                @if (User.IsInRole("Admin"))
                {
                    <li><a href="@Url.Action("Create", "CompanyNews")" title="Create New"><i class="fa fa-plus-square-o sub-icon"></i><text class="nav-sub-title">Create New</text></a></li>
                }
            </ul>
        </li>

        <!--Chat-->
        <li class="has-sub">
            <a href="#" title="Chat"><i class="fa fa-comments"></i><text class="nav-title">Chat</text></a>
            <ul>
                <li><a href="@Url.Action("Index", "ChatMessages")" title="View All"><i class="fa fa-list sub-icon"></i><text class="nav-sub-title">View All</text></a></li>
                <li><a href="@Url.Action("Create", "ChatMessages")" title="Send New Message"><i class="fa fa-plus-square-o sub-icon"></i><text class="nav-sub-title">Send New Message</text></a></li>
                <li><i class="fa fa-comments sub-icon" onclick="openChat()" title="Open Messenger"></i><text class="nav-sub-title" onclick="openChat()" title="Open Messenger">Open Messenger</text></li>
            </ul>
        </li>
        <li></li><li></li><li></li>
        <li>
            <a href="http://facebook.com" target="_blank" title="Facebook"><i class="fa fa-facebook social"></i></a>
        </li>
        <li>
            <a href="http://twitter.com" target="_blank" title="Twitter"><i class="fa fa-twitter social"></i></a>
        </li>
        <li>
            <a href="http://dribbble.com" target="_blank" title="Dribbble"><i class="fa fa-dribbble social"></i></a>
        </li>
        <li>
            <a href="http://linkedin.com" target="_blank" title="Linkedin"><i class="fa fa-linkedin social"></i></a>
        </li>
        <li>
            <a href="http://instagram.com" target="_blank" title="Instagram"><i class="fa fa-instagram social"></i></a>
        </li>
        <li class="copyright"><i class="fa fa-copyright copy-icon"></i>&nbsp;by&nbsp;CompanyName.Inc</li>
        <li></li><li></li><li></li><li></li><li></li><li></li><li></li><li></li><li></li><li></li><li></li>
    </ul>
</nav>
</div>
    }
```

From this to this:

Refactor HTML so that the words can be hidden in collapsed state. 
from this:
```
<a class="nav-title" href="#"><i class="fa fa-clipboard icon-padding" onclick="openNav()"></i>Job Sites</a>
```
to this:
```
<a href="#"><i class="fa fa-clipboard icon-padding"></i><text class="nav-title">Job Sites</text></a>
```

Collapsed list items for icons and collapsable functionality 
from this:
```
<li>@Html.ActionLink("Unregistered Users", "Index", new { controller = "CreateUserRequest" }, new { @class = "dropdown-item" })</li>
```
to this: (update me)
```
<li><a href="@Url.Action("Index", "CreateUserRequest")"><i class="fa fa-paw"></i><text class="nav-sub-title">Unregistered Users</text></a></li>
```

except the one that's a button
from this:
```
@*<li><button id="open-messenger-btn" onclick="openChat()">Open Messenger</button></li>*@
```
to this: (update me)
```
<li><i class="fa fa-paw" onclick="openChat()"></i><text class="nav-sub-title" onclick="openChat()">Open Messenger</text></li>
```

[Back to Table of Contents](#front-end-stories)

### NavBar Icon Updates

These were two mini stories: 

First:
Jobs and Job Sites on the navigation bar share the same icon which is confusing to users. 
Please change the nav icon for the Job site with an icon related to map/location.

Second:
Remove the "Send New Message" from the dropdown list of the Chat nav item, as we aren't gonna use it anymore. 

For the first one I just replaced the icon in question with fa fa-map-marker, for the second I simply deleted the icon from both the shared views _Layout and _Layout.Mobile

[Back to Table of Contents](#front-end-stories)

### Implement Contact Us Page

We want to add a working Contact page to our Management Portal, which will have the basic fields for the unregistered visitor of the site to fill out like Name, Email Address, Phone number, Subject, and Message to send to the Admin.

Replace the "Take a look" link on the Home/Index view page with "Contact Us". This button link should take the site visitor to the new Contact Page you will create. 

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
```

This was a full stack story, to look at the back end functionality I added, check out its other half. 
[Back end Components](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#implement-contact-us-page)

[Back to Table of Contents](#front-end-stories)

### ChatModal Header Bug

The chat modal header is supposed to display the name of the currently logged in username. But due to minor style issues, we can not see the name displayed right now. 

This story was a quick fix in the CSS - Just had to update one line.

```
#chat-header {
    color: white;
    background-color: gray;
    border-radius: inherit;
    border: inherit;
}
```

[Back to Table of Contents](#front-end-stories)

### Mobile Friendly Design

Most of the users will be accessing this site on their mobile devices, so we need to make it mobile-friendly. If you inspect the Mangement Portal site using Chrome DevTools - mobile mode, you will see that there are many flaws. The site is not totally responsive to various screen sizes, yet. Your job is to fix this bug to make the site mobile friendly. 

Elements in no particular order. 

The first thing I did was install a ViewSwitcher - a preexisting package I just had to install from the package manager console. 

```
PM> install-package jQuery.Mobile.MVC
```

The next thing I did was create bundles for the mobile styling and scripts: 

```
using System.Web;
using System.Web.Optimization;

namespace ManagementPortal {
    public class BundleMobileConfig {
        public static void RegisterBundles(BundleCollection bundles) {
            bundles.Add(new ScriptBundle("~/bundles/jquerymobile")
                .Include("~/Scripts/Mobile/jquery.mobile-{version}.js"));

            bundles.Add(new StyleBundle("~/Content/Mobile/css")
                .Include("~/Content/Mobile/Site.Mobile.css",
                      "~/Content/font-awesome.css",
                      "~/Content/bootstrap.css"));
            
            bundles.Add(new StyleBundle("~/Content/jquerymobile/css")
                .Include("~/Content/Mobile/jquery.mobile-1.1.0.css",
                        "~/Content/Mobile/jquery.mobile.structure-1.1.0.css",
                        "~/Content/Mobile/jquery.mobile.theme-1.1.0.css"));
        }
    }
}
```

Then I wrote a CSS page to be triggered by the ViewSwitcher (you need to make many many cuts here):

```
.view-switcher {
    padding: 0.5em; 
    font-weight: normal;
    text-align: center;
    margin-right: -45px;
    margin-left: -45px;
}

/* styles for validation helpers */
.field-validation-error {
    color: #e80c4d;
    font-weight: bold;
}

.field-validation-valid {
    display: none;
}

input[type="text"].input-validation-error,
input[type="password"].input-validation-error {
    border: solid 1px #e80c4d;
}

.validation-summary-errors {
    color: #e80c4d;
    font-weight: bold;
    font-size: 1.1em;
}

.validation-summary-valid {
    display: none;
}


/*END AUTO GENERATED CODE FROM VIEWSWITCHER IMPLEMENTATION*/

:root {
    --light-pink: #EAA6CD;
    --navy-blue: #4E6A91;
    --blue-gray: #908AB6;
    --dark-blue: #56506C;
    --light-purple: #A091D4;
}

html, body {
    min-height: 100%;
    max-width: 850px;
}

body {
    font-family: "Trebuchet MS", Helvetica, sans-serif;
    background-image: url('../images/bgPattern.png');
    background-size: cover;
    background-position: center center;
    background-repeat: no-repeat;
    margin: auto;
    padding-left: 45px; /*make space for collapsed navbar*/
}

#header-nav{
    margin-left: -45px;
    margin-right: -45px;
}

.dashboard_text {
    margin-top: 30px;
    color: black;
    text-shadow: 2px 2px 8px white;
    font-size: 20px;
}

.dashboard_title {
    font-size: 40px;
    color: #eee;
    text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
    margin-top: 40px;
}

/* Set padding to keep content from hitting the edges */
.body-content {
    padding-left: 15px;
    padding-right: 15px;
}

/* Override the default bootstrap behavior where horizontal description lists 
   will truncate terms that are too long to fit in the left column 
*/
.dl-horizontal dt {
    white-space: normal;
}

.table-bg {
    background-color: white;
}

/*Profile image styling */
#ProfileImg {
    border: 2px solid white;
    border-radius: 50%;
    width: 35px;
    height: 35px
}

/*Universal h2 styles*/

h2 {
    text-align: center;
    color: white;
    font-size: 2em; /*this doesnt affect size of h2, find why*/
    font-weight: bolder;
    text-shadow: #200117 5px 0 10px;
}

/*Universal form background*/

.formContainer {
    background-color: rgba(201,173,167, 0.82);
    padding: 10px;
    border-radius: 10px;
    color: #000;
    min-width: 265px;
    margin-left: 15px;
    margin-right: -30px;
}

    .editor-field h5 {
        font-size: 14px;
        text-align: center;
    }

/***** Standardized Button styles****/
.btn-base {
    padding: 0.375rem 0.75rem;
    margin: 0 3px;
    border-radius: 0.25rem;
    border: 0px;
    color: #212529;
    background-color: #DADADA;
}

    .btn-base:hover {
        color: #212529;
        border-radius: 20px;
        box-shadow: 0px 0px 3px 5px #f8f8f8;
    }

.btn-w-100px {
    width: 100px;
}

.btn {
    margin-left: 10px;
}

/***** Login Page Styles *****/
/*#loginContainer {
    background-color: rgba(201,173,167, 0.82);
    padding: 20px;
    border-radius: 10px;
    color: #000;
    min-width: 265px;
}*/

#loginContainer {
    margin-left: -20px;
}

.loginItemContainer {
    background-color: #DADADA;
    border-radius: 5px;
    color: #4e4e4e;
    height: 38px;
    line-height: 38px;
    width: 60%;
    /*max-width: 190px;*/
    margin: 15px;
    padding: 0px 15px;
    /*font-size: 16px;*/
}

.loginItemBtn {
    cursor: pointer;
    padding: 0px;
    height: 100%;
    width: 100%;
    text-align: center;
}

.loginItemAnchor {
    color: #000;
    text-decoration: none !important;
    height: 100%;
    width: 100%;
    display: inline-block;
    cursor: pointer;
    text-align: center;
}

.loginItemContainer:hover, .createBtn:hover {
    border-radius: 20px;
    box-shadow: 0px 0px 3px 5px #f8f8f8;
    text-decoration: none !important;
}

.form-control {
    box-shadow: 0px 0px 1px 3px #f8f8f8 !important;
    border-radius: 1.25rem !important;
}


/**styling the scheduling page */
#scheduleContainer {
    background-color: rgba(201,173,167, 0.82);
    padding: 20px;
    border-radius: 10px;
    color: #000;
}

/** Create Button*/
.createBtn {
    background-color: #DADADA;
    max-width: 125px;
    border-radius: 5px;
    color: #f8f8f8;
    /*margin-bottom: 20px;*/
    margin-left: 15px;
}

/*Update Button*/
.updateBtn {
    background-color: #DADADA;
    width: 100px;
    border-radius: 5px;
    color: #f8f8f8;
    /*margin-right: auto;
    margin-left: auto;*/
}

#mobileTableBtn {
    padding-left: 0px;
    padding-right: 10px;
    width: 50px;
    text-align: center;
    display: inline-block;
    font-size: 14px;
}

#mobileEditColumn {
    max-width: 60px;
    justify-content: flex-end;
}

#mobileJobsEditColumn {
    max-width: 100px;
    justify-content: flex-end;
}

.mobileBold {
    font-size: 12px;
}

#mobileCheckbox {
    display: inline-block;
    margin-right: -20px;
}

#newJobSiteModalButton {
    margin-top: 10px;
}

.chat-row {
    border-bottom: 1px solid gray;
}

/*Centers the File Input Type*/

#selectProfileImageFile {
    width: 215px;
    margin-right: auto;
    margin-left: auto;
}

/*Centers the Update Button to align with the File Input Type*/
#updateProfileImage {
    width: 215px;
    margin-right: auto;
    margin-left: auto;
}

.defaultContainer {
    background-color: rgba(255, 255, 255,0.8);
    padding: 10px;
    width: auto;
}
/*styling the register form*/

/*#regForm { 
/*    background-color: rgba(201,173,167, 0.82);
    padding: 20px;
    border-radius: 10px;
    color: #000;
    min-width: 265px;
    margin-right: 50px;
}*/

/*#regBtns { 
/*    background-color: #DADADA;
    width: 35% !important;
    border-radius: 5px;
    padding: 1px 22px 1px 45px;
    margin-left: 15px;
}*/

/***** Chat Styling *****/

#messageContainer {
    width: auto;
    height: auto;
    margin-left: -45px;
}

#chat-header {
    color: white;
    background-color: gray;
    border-radius: inherit;
    border: inherit;
    height: 60px;
    position: fixed;
    width: 100%;
    z-index: 2;
}

.mobileChatTitle {
    text-align: center;
    margin-top: 20px;
    display: block;
}

#close-icon {
    padding-right: 15px;
    margin-top: -40px;
    display: inline-block;
}

#discussion {
    font-size: .9em;
    padding-right: 8px;
    padding-left: 8px;
    overflow-y: scroll;
    height: 91vh;
    width: 94vw;
    position: center;
    margin-left: 3%;
    background-color: white;
    list-style-type: none;
    /*min-height: 200px;
    max-height: 200px;*/
}

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

    #yourChat::before {
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

/* Textarea to enter a new message */

#messageBox {
    background: white;
    width: 100%;
    z-index: 4;
    position: fixed;
    margin-bottom: 0px;
    width: 94vw;
    position: center;
    margin-left: 3%;
    padding: 5px;
}
#message-box {
    width: 80%;
    height: 35px;
    padding: 5px;
    border-radius: 5px;
    font-size: .9em;
}

#send-message {
    display: inline-block;
    color: white;
    background-color: gray;
    height: 38px;
    width: 65px;
    position: fixed;
}
/***** End of chat styling *****/

/***** Navbar Styling *****/

/* for header dropdown menu */
.navdrop {
    list-style-type: none;
    padding-left: 10%;
    background-color: #dbe4e3;
    margin-bottom: -20px;
    margin-top: -10px;
    width: 170px;
}

#dropdown-menu {
    width: 170px;
    margin-top: 5px;
}

/*Closes the gap in the header drop-down menu so the menu isn't lost when the cursor is in the gap*/
.dropdown-menu {
    position: absolute;
    top: 45px;
    width: 245px;
}

/* remove underlines from links  */
.removelinkdefault {
    text-decoration: none !important;
}

/******for mobile allows open of dropdown on click********/
.dropdown:hover > .dropdown-menu {
    display: block;
    background-color: aliceblue;
}

/************BEGIN LEFT SIDE NAVBAR STYLING**********/

#menu {
    min-width: 45px;
    max-width: 45px;
    height: auto;
    text-align: center;
    padding-top: 8px;
    left: 0;
    background-color: white;
    position: absolute;
    /*z-index: 9998;*/
    font-family: serif;
    color: gray;
    white-space: nowrap;
}

.fa {
    padding-left: 14px;
    font-size: .8em;
    color: gray;
    visibility: visible;
}

#menu .social {
    font-size: .6em;
    padding-right: 20px;
}

#menu .copyright {
    transform: rotate(270deg);
    font-size: .5em;
    position: relative;
    top: 50px;
    padding-bottom: 63px;
    margin-left: 52px;
    right: 0px;
}

.copy-icon {
    font-size: .6em;
    padding: 2px;
}

#menu .sub-icon {
    padding-left: 17px;
    font-size: .7em;
    color: gray;
    cursor: pointer;
}

/*targets all list items*/
#menu ul,
#menu li,
#menu a {
    padding: 0px;
    padding-bottom: 2px;
    list-style-type: none;
}

    /* Hide sub menus */
    #menu ul ul {
        display: none;
    }

/*hide menu item text in collapsed state*/
.nav-title {
    visibility: hidden;
}

.nav-sub-title {
    visibility: hidden;
}

.nav-title:hover {
    color: var(--dark-blue);
    cursor: pointer;
}

.nav-sub-title:hover {
    color: var(--dark-blue);
    cursor: pointer;
}

#menu #dismiss {
    display: none;
}

#menu #open-menu {
    display: none;
}

/*************END LEFT NAVBAR STYLING*****************/



/** Header & Image **/

header {
    max-width: none;
    /*max-height: 125px;*/
    position: relative;
}

#site-header {
    background-image: url(../images/bgimage.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    background-position: right;
    width: auto;
    height: 70px;
}

#header-title {
    text-align: left;
    font-family: 'Vollkorn SC', cursive;
    font-size: 2.7vw;
    color: black;
}

    #header-title img {
        width: auto;
        height: 45px;
        margin-top: -5px;
    }

/*Moved the main container over to the right so that it was not being overlapped by the Navbar*/
/*#main {
    padding: 30px 50px 40px 50px;
}*/

footer {
    display: flex;
    width: 175px;
    height: 28px;
    font-size: 12px;
    margin: 10px auto;
    padding: 5px;
    padding-left: 10px;
    align-items: center;
    justify-content: center;
    background: rgb(255,255,255);
    background: radial-gradient(circle, rgba(255,255,255,0.4) 25%, rgba(195,195,195,0.2) 50%, rgba(140,140,160,0) 100%);
    border: 1px solid rgba(0, 0, 0, 0.325);
    border-radius: 0.25rem;
    overflow: hidden;
}

/****Company News Cards****/

#news-header {
    background-color: rgb(117, 137, 138);
    padding: 15px;
}

.float-right {
    font-size: 16px;
}

#news-container {
    margin-top: 15px;
}

#new-body {
    background-color: rgb(219, 228, 227);
}

#new-body .card {
    box-shadow: 4px 6px rgba(128,128,128,.7);
    width: 100%;
    min-width: 250px;
    display: block;
    position: relative;
}
#new-body .col {
    margin-bottom: 20px;
}

#new-body .card-header {
    height: 80px;
}

.col {
    /*-ms-flex-preferred-size: 0;
    flex-basis: 0;
    -ms-flex-positive: 1;*/
    flex-grow: 0;
    max-width: 100%;
}

/****Datepicker Styling****/
.ui-datepicker {
    background-color: white;
    border-radius: 10px;
    width: 200px;
    height: auto;
    margin: 5px auto 0;
}

    .ui-datepicker table {
        width: 100%;
    }

.ui-datepicker-header {
    background-color: var(--light-grey);
}

.ui-datepicker-title {
    text-align: center;
    font-weight: bold;
}

.ui-datepicker-prev {
    float: left;
    background-position: center -30px;
}

.ui-datepicker-next {
    float: right;
    background-position: center 0px;
}

/****Styling for Company News/Jobs Index***/

/*#editDeletButtons {
    width: 250px;
}

#dateContainer {
    width: 120px;
}*/

.indexContainer {
    background-color: rgba(255, 255, 255,0.8);
    padding: 10px;
    min-width: 350px;
    margin-left: 15px;
}

/*Added foreground and background colors to WorkType*/
#WorkType {
    background-color: skyblue;
    color: palevioletred;
}

.indexContainer row {
    margin: 10px;
}


/* Begin styling for Password Validation Box */
/*input#Password {
    width: 180px;
    padding: 3px;
    color: #000;
    float: left;
    margin-right: 10px;
}*/

#pwd_strength_wrap {
    border: 1px solid #D5CEC8;
    display: none;
    float: right;
    padding: 10px;
    position: absolute;
    width: 320px;
    background-color: white;
    z-index: 1;
    margin-left: 95%;
    top: 0px;
}

    #pwd_strength_wrap:before, #pwd_strength_wrap:after {
        content: ' ';
        height: 0;
        position: absolute;
        width: 0;
        border: 10px solid transparent; /* arrow size */
    }

    #pwd_strength_wrap:before {
        border-bottom: 7px solid rgba(0, 0, 0, 0);
        border-right: 7px solid rgba(0, 0, 0, 0.1);
        border-top: 7px solid rgba(0, 0, 0, 0);
        content: "";
        display: inline-block;
        left: -18px;
        position: absolute;
        top: 10px;
    }

    #pwd_strength_wrap:after {
        border-bottom: 6px solid rgba(0, 0, 0, 0);
        border-right: 6px solid #fff;
        border-top: 6px solid rgba(0, 0, 0, 0);
        content: "";
        display: inline-block;
        left: -16px;
        position: absolute;
        top: 11px;
    }

#pswd_info ul {
    list-style-type: none;
    margin: 5px 0 0;
    padding: 0;
}

    #pswd_info ul li {
        background: url(icon_pwd_strength.png) no-repeat left 2px;
        padding: 0 0 0 20px;
        color: red;
    }

        #pswd_info ul li.valid {
            background-position: left -42px;
            color: green;
        }

#passwordStrength {
    display: block;
    height: 5px;
    margin-bottom: 10px;
    transition: all 0.4s ease;
}

.strength0 {
    background: none; /* too short */
    width: 0px;
}

.strength1 {
    background: none repeat scroll 0 0 #FF4545; /* weak */
    width: 75px;
}

.strength2 {
    background: none repeat scroll 0 0 #FFC824; /* good */
    width: 150px;
}

.strength3 {
    background: none repeat scroll 0 0 #6699CC; /* strong */
    width: 225px;
}

.strength4 {
    background: none repeat scroll 0 0 #008000; /* best */
    width: 300px;
}
/* End styling for Password Validation Box */

/* Styling the Calendar*/
#calendar {
    background-color: rgba(34,34,34,.45);
    padding: 10px;
    border-radius: 20px;
    border-color: black;
    color: white;
    /*margin-top: 45px;*/
    position: center;
}

.employee_timeoffcalendar {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -30px;
    margin-left: 15px;
}

.employee_timeoffcalendar_h2 {
    margin-left: 45px;
}

    .fc-toolbar {
        font-size: 12px;
    }

.fc-button {
    width: 50px;
}

.fc-center {
    padding-top: 10px;
}

.fc-view-container {
    font-size: 12px;
}

.fc-day-header {
    background-color: #22223b;
}

.fc-axis.fc-widget-header {
    background-color: #4A4E69;
}

.fc-axis.fc-widget-content {
    background-color: #9a8c98;
}

.fc-widget-content {
    background-color: #bcbcbc;
}

.fc-day.fc-today.fc-state-highlight {
    background-color: #c9ada7;
}

.fc-day-number {
    color: black;
}
/* End of Styling the Calendar*/
/*==================================================================================
    Jobsite Details
*/

#jobSiteMap {
    height: 350px;
    width: 350px;
}

.invalidMap {
    background-color: rgb(185, 185, 185);
}

    .invalidMap div {
        line-height: 325px;
        text-align: center;
    }

/* End of Styling JobSite Map*/

/* Generic Card Styles */

#card-header-bg {
    background-color: rgb(117, 137, 138);
}

.card-shadow {
    box-shadow: 5px 7px rgb(148, 157, 164);
}

/* End Generic Card Styles */

.susp {
    display: inline;
    padding-left: 10px;
}

/* Home Styles */

.jumbotron {
    text-align: center !important;
}

#home_box {
    text-align: center;
    margin-top: 150px;
    /*margin-left: -80px;*/
}

.home_btn {
    background: #332635;
    color: white;
    border: 1.4px solid rgba(247,247, 249, 0.35);
    border-radius: 5px;
    width: 100%;
    margin: auto;
    padding: 3.5px;
}

    .home_btn:hover {
        color: lightgray;
        text-decoration: underline;
        box-shadow: grey 10px;
    }

#threeCards {
    font-size: 13px;
    width: 120px;
    background: rgba(99,43,73, 0.53);
    border-radius: 10px;
    margin-top: 220px;
    margin-left: -10px;
    display: inline-block;
    position: center;
}

#threeCards .card-title {
    font-size: 14px;
}

#home_jumbotron h1 {
    font-size: 42px;
    font-family: "Trebuchet MS", Helvetica, sans-serif;
    position: absolute;
    top: 10px;
    /*left: 225px;*/
}

#home_jumbotron p {
    position: absolute;
    font-family: "Trebuchet MS", Helvetica, sans-serif;
    top: 115px;
    left: 15px;
    font-size: 14px;
    font-style: italic;
}

    #home_jumbotron img {
        position: absolute;
        height: 100%;
        width: 100%;
        left: 0;
        top: 0;
        -webkit-transition: opacity 1s ease-in-out;
        -moz-transition: opacity 1s ease-in-out;
        -o-transition: opacity 1s ease-in-out;
        transition: opacity 1s ease-in-out;
    }

#home_jumbotron {
    position: absolute;
    overflow: hidden;
    height: 350px;
    min-width: 475px;
    max-width: 800px;
    margin-top: -140px;
    margin-left: -45px;
    /*margin-right: -45px;*/
}

@keyframes home_jumbotronFadeInOut {
    0% {
        opacity: 1;
    }

    17% {
        opacity: 1;
    }

    25% {
        opacity: 0;
    }

    92% {
        opacity: 0;
    }

    100% {
        opacity: 1;
    }
}

#home_jumbotron img:nth-of-type(1) {
    animation-delay: 8s;
}

#home_jumbotron img:nth-of-type(2) {
    animation-delay: 6s;
}

#home_jumbotron img:nth-of-type(3) {
    animation-delay: 4s;
}

#home_jumbotron img:nth-of-type(4) {
    animation-delay: 2s;
}

#home_jumbotron img:nth-of-type(5) {
    animation-delay: 0;
}

#home_jumbotron img {
    animation-name: home_jumbotronFadeInOut;
    animation-timing-function: ease-in-out;
    animation-iteration-count: infinite;
    animation-duration: 10s;
}

/*End Home styles*/

/*Chat Bubble Icon Hover Effects*/
.float-right img:hover {
    cursor: pointer;
    transform: scale(1.1);
    transition: transform .1s ease;
}
```

I created partial views for all the tables within the site, and called them from the desktop view when mobile was detected. There are tables in the desktop view for Jobsites, Jobs, Schedules, and Users (active, suspended, and unregistered). 

//SCREENSHOTS HERE

For example, here is the code for JobSites, the Mobile partial view and the added code to the Index to call it. As well as the controller function to allow that to happen. 

JobSites Mobile
```
@using ManagementPortal.Models
@using ManagementPortal.Common
@using ManagementPortal.Helpers
@using ManagementPortal.Enums
@model PagedList.IPagedList<ManagementPortal.Models.JobSite>
@using PagedList.Mvc;
@*@model IEnumerable<JobSite>*@

@{
    Layout = "";
}

<h5>Sort Job Sites By:</h5>
<center>
    @Html.ActionLink("SiteName", "Index", new { sortOrder = ViewBag.SiteSortParm, currentFilter = ViewBag.CurrentFilter }) |
    @Html.ActionLink("Address", "Index", new { sortOrder = ViewBag.AddressSortParm, currentFilter = ViewBag.CurrentFilter }) |
    @Html.ActionLink("Town", "Index", new { sortOrder = ViewBag.TownSortParm, currentFilter = ViewBag.CurrentFilter }) |
    @Html.ActionLink("State", "Index", new { sortOrder = ViewBag.StateSortParm, currentFilter = ViewBag.CurrentFilter }) |
    @Html.ActionLink("Zip", "Index", new { sortOrder = ViewBag.ZipSortParm, currentFilter = ViewBag.CurrentFilter }) |
</center>

<table class="table table-striped table-light rounded-lg">
    <tr>
        <th>
            Job Sites
        </th>
        <th></th>
    </tr>

    @foreach (var item in Model)
    {
        <tr>
            <td>
                <b class="mobileBold">Site Name: </b>@Html.DisplayFor(modelItem => item.SiteName)<br />
                <b class="mobileBold">Address: </b>@Html.DisplayFor(modelItem => item.Address)<br />
                <b class="mobileBold">Town: </b>@Html.DisplayFor(modelItem => item.Town)<br />
                <b class="mobileBold">State: </b>@item.State.GetDisplayName()<br />
                <b class="mobileBold">Zip Code: </b>@Html.DisplayFor(modelItem => item.Zip)
            </td>
            <td id="mobileJobsEditColumn">
                @Html.Partial(AnchorButtonGroupHelper.PartialView, AnchorButtonGroupHelper.GetEditDetailsDelete(item.JobSiteID.ToString()))
            </td>
        </tr>
    }

</table>
```

JobSites Desktop
```
@using ManagementPortal.Models
@using ManagementPortal.Common
@using ManagementPortal.Helpers
@using ManagementPortal.Enums
@model PagedList.IPagedList<ManagementPortal.Models.JobSite>
@using PagedList.Mvc;
@*@model IEnumerable<JobSite>*@

@{
    ViewBag.Title = "Index";
}

<h2>Job Sites</h2>
<div class="indexContainer">
    <p>
        @Html.Partial(AnchorButtonGroupHelper.PartialView, AnchorButtonGroupHelper.GetCreate())
    </p>

    @using (Html.BeginForm("Index", "Jobsites", FormMethod.Get))
    {
        <p>
            Find by name : @Html.TextBox("SearchString", ViewBag.CurrentFilter as string)
            <input type="submit" value="Search" />
        </p>


    }

    @if (ViewContext.HttpContext.GetOverriddenBrowser().IsMobileDevice)
    {
        { Html.RenderAction("_JobSiteIndexMobile", "JobSites"); }
    }
    else
    {
        <table class="table table-striped table-light rounded-lg">
            <tr>
                <th>
                    @Html.ActionLink("SiteName", "Index", new { sortOrder = ViewBag.SiteSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                @*<th>
                        @Html.DisplayNameFor(model => model.SiteName)
                    </th>*@

                <th>
                    @Html.ActionLink("Address", "Index", new { sortOrder = ViewBag.AddressSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                @*<th>
                        @Html.DisplayNameFor(model => model.Address)
                    </th>*@

                <th>
                    @Html.ActionLink("Town", "Index", new { sortOrder = ViewBag.TownSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                @*<th>
                        @Html.DisplayNameFor(model => model.Town)
                    </th>*@

                <th>
                    @Html.ActionLink("State", "Index", new { sortOrder = ViewBag.StateSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>

                @*<th>
                        @Html.DisplayNameFor(model => model.State)
                    </th>*@

                <th>
                    @Html.ActionLink("Zip", "Index", new { sortOrder = ViewBag.ZipSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>

                @*<th>
                        @Html.DisplayNameFor(model => model.Zip)
                    </th>*@
                <th></th>
            </tr>

            @foreach (var item in Model)
            {
                <tr>
                    <td>
                        @Html.DisplayFor(modelItem => item.SiteName)
                    </td>
                    <td>
                        @Html.DisplayFor(modelItem => item.Address)
                    </td>
                    <td>
                        @Html.DisplayFor(modelItem => item.Town)
                    </td>
                    <td>
                        @item.State.GetDisplayName()
                    </td>
                    <td>
                        @Html.DisplayFor(modelItem => item.Zip)
                    </td>
                    <td>
                        @Html.Partial(AnchorButtonGroupHelper.PartialView, AnchorButtonGroupHelper.GetEditDetailsDelete(item.JobSiteID.ToString()))
                    </td>
                </tr>
            }

        </table>
    }
        <br />
        Page @(Model.PageCount < Model.PageNumber ? 0 : Model.PageNumber) of @Model.PageCount

        @Html.PagedListPager(Model, page => Url.Action("Index",
            new { page, sortOrder = ViewBag.CurrentSort, currentFilter = ViewBag.CurrentFilter }))
    </div>
```

JobSite controller added function: 
```
public ViewResult _JobSiteIndexMobile(string sortOrder, string currentFilter, string searchString, int? page)
        {
            ViewBag.CurrentSort = sortOrder;
            ViewBag.SiteSortParm = string.IsNullOrEmpty(sortOrder) ? "name_desc" : "";
            ViewBag.AddressSortParm = sortOrder == "Date" ? "address_desc" : "Date";
            ViewBag.TownSortParm = string.IsNullOrEmpty(sortOrder) ? "town_desc" : "";
            ViewBag.StateSortParm = string.IsNullOrEmpty(sortOrder) ? "state_desc" : "";
            ViewBag.ZipSortParm = string.IsNullOrEmpty(sortOrder) ? "zip_desc" : "";

            if (searchString != null)
            {
                page = 1;
            }
            else
            {
                searchString = currentFilter;

            }

            ViewBag.CurrentFilter = searchString;

            var JobSites = from s in db.JobSites
                           select s;

            if (!String.IsNullOrEmpty(searchString))
            {
                JobSites = JobSites.Where(s => s.SiteName.Contains(searchString)
                                        || s.Address.Contains(searchString));
            }

            switch (sortOrder)
            {
                case "name_desc":
                    JobSites = JobSites.OrderByDescending(s => s.SiteName);
                    break;
                case "address_desc":
                    JobSites = JobSites.OrderByDescending(s => s.Address);
                    break;
                case "town_desc":
                    JobSites = JobSites.OrderByDescending(s => s.Town);
                    break;

                case "state_desc":
                    JobSites = JobSites.OrderByDescending(s => s.State);
                    break;

                case "zip_desc":
                    JobSites = JobSites.OrderByDescending(s => s.Zip);
                    break;

                default:
                    JobSites = JobSites.OrderBy(s => s.SiteName);
                    break;

            }
            int pageSize = 10;
            int pageNumber = (page ?? 1);
            return View(JobSites.ToPagedList(pageNumber, pageSize));
        }
```
Another example - User List: 

Call from Users Index:
```
 @if (ViewContext.HttpContext.GetOverriddenBrowser().IsMobileDevice)
                {
                    { Html.RenderAction("_UserListMobile", "Users"); }
                }
                else
                {
                    { Html.RenderAction("_UserList", "Users"); }
                }
                @*</div>
            <div class="card-body" id="new-body">*@
                @if (ViewContext.HttpContext.GetOverriddenBrowser().IsMobileDevice)
                {
                    { Html.RenderAction("_SuspendedUsersMobile", "Users"); }
                }
                else
                {
                    { Html.RenderAction("_SuspendedUsers", "Users"); }
                }
```

Mobile partial view _UserListMobile:
```
@using ManagementPortal.Common
@using ManagementPortal.Models
@using Microsoft.AspNet.Identity

@model List<ApplicationUser>

@{
    var selectListItems = UserRoleDropDown.GetStatesSelectListItems();
}

<div class="card card-shadow mb-3">
    <div class="card-header">
        <h4>Active Users</h4>
    </div>
    <div class="card-body">
        <table class="table table-striped table-light rounded-lg">
            <tr>
                <th>
                    User Information
                </th>
                <th>
                    Edit User
                </th>
            </tr>

            @for (var i = 0; i < Model.Count; i++)
            {
                if (!Model[i].Suspended)
                {
            <tr id="userRow_@i">
                <td>
                    <b class="mobileBold">User: </b>@Html.DisplayFor(modelItem => Model[i].UserName)<br />
                    <b class="mobileBold">First: </b>@Html.DisplayFor(modelItem => Model[i].FirstName)<br />
                    <b class="mobileBold">Last: </b>@Html.DisplayFor(modelItem => Model[i].LastName)<br />
                    <b class="mobileBold">Phone: </b><a href="tel:+@Model[i].PhoneNumber"> @Html.DisplayFor(modelItem => Model[i].PhoneNumber)</a><br />
                </td>
                <td id="mobileEditColumn">
                    @if (Model[i].Id != User.Identity.GetUserId())
                    {
                        <!-- REMOVE USER BUTTON -->
                        using (Html.BeginForm("RemoveUser", "Users", FormMethod.Post, new { id = $"removeForm_{i}" }))
                        {
                            <input type="hidden" name="userId" value="@Model[i].Id" />
                            @Html.AntiForgeryToken()
                            <button type="submit" id="mobileTableBtn" onclick="removeUser(@i, '@Model[i].DisplayName')"><i class="fa fa-trash"></i></button>
                        }
                        <!--SUSPEND USER-->
                        using (Html.BeginForm("SuspendUser", "Users", FormMethod.Post, new { id = $"suspendForm_{i}" }))
                        { 
                            @Html.AntiForgeryToken()
                            <button type="submit" id="mobileTableBtn" onclick="suspendUser(@i, '@Model[i].DisplayName')"><i class="fa fa-user-times"></i></button>
                            @Html.CheckBoxFor(Model => Model[i].Suspended, new { Name = "suspended" })
                            <input type="hidden" id="mobileCheckbox" name="userId" value="@Model[i].Id" />

                        }
                        <!-- USER ROLE DROPDOWN -->
                        using (Html.BeginForm("UpdateUserRole", "Users", FormMethod.Post, new { id = $"roleForm_{i}" }))
                        {
                            @Html.AntiForgeryToken()
                            <button type="submit" id="mobileTableBtn" onclick="updateUserRole(@i)" value="Update User Role"><i class="fa fa-pencil-square-o"></i></button>
                            <br />
                            @Html.DropDownList("userRole", new SelectList(selectListItems, "Value", "Text", Model[i].UserRole), new { @style = "font-size:14px;" })
                            <input type="hidden" id="mobileTableDropdown" name="userId" value="@Model[i].Id" />
                        }
                }
                </td>
            </tr>
                }

            }
        </table>

    </div>
</div>
```

I asked the PM and she requested that the chat open in a separate page, and be full screen in that window. 

Chat View: 
```
<!--SignalR is working just needs user signed in-->
<!-- Chat Modal -->
@using Microsoft.AspNet.Identity
@using ManagementPortal.Models

<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>@ViewBag.Title</title>
    <style>
        #header-nav {
            display: none;
        }
        #menu {
            display:none;
        }
        .view-switcher {
            display: none;
        }
        #overlay {
            background-color: rgba(255, 255, 255, .8);
        }
        footer {
            display: none;
        }
        #chat-modal {
            display: none;
        }
        .container {
            display: none;
        }
    </style>
    <script>
        $(document).ready(function () {
            $.mobile.ajaxEnabled = true;
        });
    </script>
</head>
<body>
    @RenderPage("../Shared/MobileChat.cshtml")
</body>
</html>
```
```
<!--SignalR is working just needs user signed in-->
<!-- Chat Modal -->
@using Microsoft.AspNet.Identity
@using ManagementPortal.Models
@*<div id="chat-modal" class="modal modal-right" tabindex="-1" role="dialog" aria-hidden="false">
    <div class="modal-dialog" role="document">
        <div class="modal-content">*@
@*<div id="mobileChat" class="" tabindex="" role="">
    <div class="" role="">
        <div class="">*@
<div id="messageContainer">
            <div id="chat-header" class="">
                <h4 class="mobileChatTitle">
                    @ViewData["DisplayName"] <!---So what this does is it gets the user's name-->
                </h4>
                <button id="close-icon" type="button" class="close" data-dismiss="modal" aria-label="Close" onclick="closeMobileChat()">
                    <span aria-hidden="true">&times;</span>
                </button>
            </div>
            <div id="discussion">
                <form class="chat-body">
                    <ul class="overflow-auto" id="discussionBubbles"></ul>
                </form>
            </div>

        @*</div>
    </div>
</div>*@
            <div id="messageBox">
<textarea id="message-box" placeholder="Type a message here..." required></textarea>
                <button id="send-message" type="button" class="btn" onclick="">Send</button>
            </div>
    </div>
```

New jQuery chat function
```
function openMobileChat() {
    window.open("/MobileChat/Index#");
    $('#discussion').animate({
        scrollTop: $('#discussion').get(0).scrollHeight
    }, 0);
}

function closeMobileChat() {
    window.close();
    $("#chatIcon").fadeIn("slow");
}
```

[Back to Table of Contents](#front-end-stories)
