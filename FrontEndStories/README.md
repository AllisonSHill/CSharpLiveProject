# Front End Stories

Writing front end code is always fun because it involves an element of design. For the Management Portal project, I worked on several exciting front end elements. I had a great time creating the chat bubbles, and they turned out really cute. I also updated the site to include a mobile version, with a ViewSwitcher and a fully responsive design. 

### Table of Contents:

[4973 - Create ShiftTime Modal](#create-shifttime-modal)

[4997 - Chat Box Upgrade](#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](#navbar-vital-change-and-vertical-navigation-bar-final-touch)

[5177 & 5178 - NavBar Icon Updates](#navbar-icon-updates)

[5148 - Implement Contact Us Page](#implement-contact-us-page)

[5162 - ChatModal Header Bug](#chatmodal-header-bug)

[5151 - Mobile Friendly Design](#mobile-friendly-design)

### Create ShiftTime Modal

This story was for the addition of a button in the existing Job Create form, that would launch a Shift Time Modal. It was specified that the modal contain a series of text boxes, one for a default shift time, and one for each day of the week, to enter alternate shift times if needed. The story specifically stated that the modal was to be a separate partial view, within the Jobs folder. After I completed this story, I took a [back end story](#https://github.com/allisonhill00/CSharpLiveProject/tree/master/BackEndStories#implement-shifttime-modal) for the initial implementation of the modal's functionality. 

[Click Here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/ShiftTime_Modal_HTML.html) to view the full HTML for the modal partial view. Here is a code snippet, an example of the default text box:

```html
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
```

I also added the link to launch the new modal in the Create Job form:
```html
@{Html.RenderPartial("~/Views/Jobs/_shiftTimeModal.cshtml");}
        <div class="createBtn">
            <button type="button" class="btn btn-default" data-toggle="modal" data-target="#ShiftTimeModal">
                Add Shift Times
            </button>
        </div>
```
When I finished this story, I chose to implement the Shift Time modal's functionality as my next story: [Back End: Implement ShiftTime Modal](https://github.com/allisonhill00/CSharpLiveProject/tree/master/BackEndStories#implement-shifttime-modal)

[Back to Table of Contents](#front-end-stories)

### Chat Box Upgrade

The Management Portal site already had a pretty good chat feature, from the work of previous students. The chat feature was set up and functional to open on all logged in user's screens when a message was sent, as well as save the messages in a database and populate old messages every time the chat modal was launched. The story I took was an upgrade to the design. The client wanted chat bubbles designed in a specific style, and the story included a picture of the desired look: 

![Example Chat Bubbles](https://github.com/allisonhill00/pictures/blob/master/4997%20ChatBox%20Upgrade/example%20bubbles1.png)

Here are my chat bubbles: 

![My Chat Bubbles](https://github.com/allisonhill00/pictures/blob/master/4997%20ChatBox%20Upgrade/finished%20bubbles.png)

To accomplish this look, I targeted specific elements within the CSS. The currently logged in user needed chat bubbles styled differently than everyone else in the conversation, so I differentiated with "my" and "your" chat:

```css
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

//Creating the tails
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

//Creating the tails
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
I amended the Javascript functions to utilize the differentiation between the "my" and "your" styling, but first, there was a minor back end element to this story. I had to pass the identity of the currently logged in user into the Javascript functions, so they would correctly style the chat bubbles. I created the variable "me" in the Chat Controller:
```c#
string me = Context.User.Identity.Name;
```
Then I could update the Javascript functions.

```js
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
```js
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
To mimic the phone messenger look, I also added to the functions, animating the chat messages to scroll down on launch, and when a new message is recieved, and to add new messages to the bottom, pushing old messages up. 
```js
function openChat() {
    $("#chat-modal").fadeIn("slow");
    $("#chatIcon").fadeOut("slow");
    $('#discussion').animate({
        scrollTop: $('#discussion').get(0).scrollHeight
    }, 0);
}
```
All that created a functional and super cute chat! 
Before I turned in the story, though, for bonus functionality I added a script for the user to be able to send new chat messages by hitting the enter key inside the message box: 
```js
//use enter key to send new chat message
$("#message-box").keyup(function (e) {
    if (e.keyCode === 13) {
        $("#send-message").click();
    }
});
```

[Back to Table of Contents](#front-end-stories)

### NavBar Vital Change and Vertical Navigation Bar Final Touch

There was already a navbar, but it didn't have the functionality desired. Its most pressing issue was that even though it was launched from a small icon, it left a persistent invisible div when collapsed that covered the left side of the content of the page. With the exception of the overall look of the open navbar, and the links themselves, I refactored all of the functionality and visual elements to create a much simpler, cleaner, more functional navbar. 

The story for the navbar update specified many elements:
- The side-nav should have two states, opened state and collapsed state. See images. 
- On Collapsed state, we should only see the icons for the navigation items. While on Opened state, all their names are visible.
- On Collapsed state, if you click on one of the icons, additional icons for child items (ViewAll or Create) shows up under the parent icon. See image. 
- The three bars (hamburger menu) is responsible for opening and collapsing the side-nav.
- The side-nav should be static and shouldn't be affected by scrolling.
- The side-nav should not cover or in any way interfere with the contents of the page opened in either state.
- It should be responsive to small screens.
- Add the Social Media icons and the copyright text as shown in the image.

![Navbar Reference Image](https://github.com/allisonhill00/pictures/blob/master/Left%20side%20navbar/from%20story.png)

I created a single navbar with a toggleable "active" state, and added the hamburger menu icon as well as the close icon at the top. I also updated the icons, and refactored the class and id system of all of the HTML to assist with styling. To check out the full HTML, [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/NavBar_Full_HTML.html). 

Here is a snippet of the HTML, the Users heading and drop down:
```html
<li class="has-sub">
    <a href="#" title="Users"><i class="fa fa-users"></i><text class="nav-title">Users</text></a>
    <ul>
        <li><a href="@Url.Action("Create", "CreateUserRequest")" title="Add Users"><i class="fa fa-user-plus sub-icon"></i><text class="nav-sub-title">Add Users</text></a></li>
        <li><a href="@Url.Action("Index", "CreateUserRequest")" title="Unregistered Users"><i class="fa fa-user-times sub-icon"></i><text class="nav-sub-title">Unregistered Users</text></a></li>
        <li><a href="@Url.Action("Index", "Users")" title="All Users"><i class="fa fa-address-book sub-icon"></i><text class="nav-sub- title">All Users</text></a></li>
    </ul>
</li>
```

I added Javascript to toggle the "active" styling:
```js
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

Once the navbar was functional, I wrote the styling for the two states. If you want to check out all the CSS I wrote for the navbar, 
[click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/NavBar_Full_CSS.css).

Here's a little snippet of the CSS, if you don't want to view the whole thing:
```css
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
```

Finished Navbar:

![Navbar Inactive](https://github.com/allisonhill00/pictures/blob/master/Left%20side%20navbar/Desktop%20Inactive.png)

Finished Navbar active state:

![Navbar Active](https://github.com/allisonhill00/pictures/blob/master/Left%20side%20navbar/Desktop%20Active%20w%20users.png)

After the navbar was functional and looked great on my desktop, I added three additional sizes of media breakpoints, so the navbar would be responsive at all possible screen sizes. That CSS is also included in the stylesheet linked above, or [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/NavBar_Full_CSS.css).

For a bonus story, after I completed the NavBar, I took on two additional stories to update their icons to be less confusing to users. 

#### NavBar Icon Updates
First:
Jobs and Job Sites on the navigation bar share the same icon which is confusing to users. 
Please change the nav icon for the Job site with an icon related to map/location.

I took on two mini stories after the navbar update, both quick adjustments to the navbar icons. 

First:
Jobs and Job Sites on the navigation bar share the same icon which is confusing to users. 
Please change the nav icon for the Job site with an icon related to map/location.

For this one, I updated the Job Sites marker to fa-map-marker, in both _Layout.cshtml and _Layout.Mobile.cshtml.

Second:
Remove the "Send New Message" from the dropdown list of the Chat nav item, as we aren't using it anymore. 

I simply deleted the icon from both the Layout views. 

[Back to Table of Contents](#front-end-stories)

### Implement Contact Us Page

We want to add a working Contact page to our Management Portal, which will have the basic fields for the unregistered visitor of the site to fill out like Name, Email Address, Phone number, Subject, and Message to send to the Admin.

Replace the "Take a look" link on the Home/Index view page with "Contact Us". This button link should take the site visitor to the new Contact Page you will create. The page itself was a pretty basic contact form, to view the HTML for that, [click here].

Here is a snippet of that code as well, the email entry form:
```html
<div class="form-group">
    <label for="Email" class="control-label col-md-2">Email Address *</label>
    <div class="col-md-10">
        @Html.EditorFor(model => model.Email, new { htmlAttributes = new { @class = "form-control", autocomplete = "off" } })
        @Html.ValidationMessageFor(model => model.Email, "", new { @class = "text-danger" })
    </div>
</div>
```

I also added a link to the home page for visitors to the site to access the contact form. 

```
<h5 class="card-title">Want to send us a message?</h5>
<input type="button" class="home_btn" onclick="location.href='@Url.Action("Index", "ContactUs")'" value="Contact Us">
```

This was a full stack story, to look at the back end functionality I added, check out its other half. 
[Back end Components](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#implement-contact-us-page)

[Back to Table of Contents](#front-end-stories)

### ChatModal Header Bug

The ChatModal Header Bug was another mini story that I took a while after I had finished the ChatModal bubbles. 

The story stated that the chat modal header is supposed to display the name of the currently logged in username. But the display name was hidden because the background color of the ChatModal had accidentally been changed to white. 

This story was a quick fix in the CSS - Just had to update one line, background-color.

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

This story was a big undertaking. There had been many elements designed and built for the portal that did not work for mobile. The story said:
Most of the users will be accessing this site on their mobile devices, so we need to make it mobile-friendly. The site is not totally responsive to various screen sizes, yet. Your job is to fix this bug to make the site mobile friendly. 

The first thing I did was install a ViewSwitcher - a preexisting package I just had to install from the package manager console. 

```
PM> install-package jQuery.Mobile.MVC
```

The next thing I did was create bundles for the mobile styling and scripts: 

```c#
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

Then I wrote a CSS page to be triggered by the ViewSwitcher. To view my whole mobile stylesheet, [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/MobileSite_Full_CSS.css).

These steps took care of a lot of the styling, and I had already created a mobile navbar in a previous story. I created partial views for all the tables within the site, and called them from the desktop view when mobile was detected. There are tables in the desktop view for Jobsites, Jobs, Schedules, and Users (active, suspended, and unregistered). 

Desktop view for JobSites table:
![JobSite Desktop](https://github.com/allisonhill00/pictures/blob/master/Mobile%20site/jobSites%20Desktop%20table.png)

JobSites table mobile view:
![JobSite Mobile](https://github.com/allisonhill00/pictures/blob/master/Mobile%20site/JobSites%20Mobile%20Table.png)

For example, here is the code for the JobSites Mobile partial view, which was called when in "Mobile View" from the Index. To view the JobSites index, and code for the desktop table, [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/JobSites_Desktop_HTML.html). 

JobSites Mobile Partial View:
```html
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

I had to add a controller function for each partial view. I simply duplicated the Index functions within each controller, and called the partial views instead.
JobSite controller added function: 
```c#
public ViewResult _JobSiteIndexMobile(string sortOrder, string currentFilter, string searchString, int? page)
        {
            //Duplicate of code from _Index function
        }
```

There were two styles of tables on the site, the Users List was the other style from the JobSites table. 

Desktop view for Users List:
![Users Desktop](https://github.com/allisonhill00/pictures/blob/master/Mobile%20site/UserList%20Desktop%20table.png)

Users List mobile view:
![Users Mobile](https://github.com/allisonhill00/pictures/blob/master/Mobile%20site/UserList%20Mobile%20table.png)

To view the code for the Users List mobile table, [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/UsersListTable_Mobile_HTML.html).

The last element I had to address was the chat. For the mobile site, it was requested that the chat open in a different window, and fill that window, while maintaining the same functionality. To view the HTML and CSS I added to accomplish this, [click here](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FullCode/MobileChat_Full_HTML.html).

Mobile Chat end result:
![Mobile Chat](https://github.com/allisonhill00/pictures/blob/master/Mobile%20site/Chat%20mobile.png)

[Back to Table of Contents](#front-end-stories)
