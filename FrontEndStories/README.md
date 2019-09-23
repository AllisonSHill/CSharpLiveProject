# Front End Stories

This is where the intro goes. This is where I write about my overall experience. Wheeeee

### Table of Contents:

[4973 - Create ShiftTime Modal](#create-shifttime-modal)

[4997 - Chat Box Upgrade](#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](#navbar-vital-change-and-vertical-navigation-bar-final-touch) - This needs all content

[5148 - Implement Contact Us Page](#implement-contact-us-page)

[5162 - ChatModal Header Bug](#chat-modal-header-bug)

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

There was already a navbar, but it didn't have the functionality desired. (SCREEN SHOTS FROM STORY HERE)
I basically started over with the CSS, using none of the existing styling. 

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

### ChatModal Header Bug

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

