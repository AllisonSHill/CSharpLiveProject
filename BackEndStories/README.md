# Back End Stories:

I worked on several back end stories, both creating functions and fixing bugs within existing functions. This was my first experience entering into an existing project and trying to work backwards to fix issues, but it didn't prove as difficult as I was expecting. I was able to accomplish quite a few back end stories in the short time I was working on the Management Portal project. I implemented a few new pages and forms, as well as handled quite a few bug fixes, and handled the refactoring of some previously messy functions. 

### Table of Contents:

[5027 - Job to Schedules Function](#job-to-schedules-function)

[5099 - Implement Schedule Dictionary](#implement-schedule-dictionary)

[5103 - Calendar Pull Existing Schedule](#calendar-pull-existing-schedule)

[5074 - User Manager Clean Up](#user-manager-clean-up)

[5106 - Refactor Users Controller](#refactor-users-controller)

[5085 & 5087 - User Role Assignment Must Be Required and Save Changes Minor Bug](#user-role-assignment-must-be-required-and-save-changes-minor-bug)

[5061 - Implement ShiftTime Modal](#implement-shifttime-modal)

[5148 - Implement Contact Us Page](#implement-contact-us-page)

[Bonus Project: Bug Fix](#bonus-project-bug-fix)


### Job to Schedules Function

This story stated:
We will want to be able to display the schedule items sorted by job. To allow for future functionality to filter these by person or by date, etc, We need a function that takes a specific list of schedule items and builds a dictionary item where the key is the job and the value is the list of schedules for that job. 

For this story, I just wrote a function in the Jobs Controller, building the dictionary:

```c#
//Job to schedules dictionary function
private Dictionary<Job, List<Schedule>> AddToDictionary(List<Schedule> schedules)
{
    var scheduleDict = new Dictionary<Job, List<Schedule>>();
    foreach (var schedule in schedules)
    {
        var schedJob = schedule.Job;
        if (scheduleDict.ContainsKey(schedJob))
            {
            scheduleDict[schedule.Job].Add(schedule);
            }
        else
            {
            var assignedSchedules = new List<Schedule>();
            assignedSchedules.Add(schedule);
            scheduleDict.Add(schedJob, assignedSchedules);
            }
        }
    return scheduleDict;
}
```

[Back to Table of Contents](#back-end-stories)


### Implement Schedule Dictionary

This story was created after I created the Schedule dictionary, so I took it too to implement the next step in that functionality:

The schedule controller has an AddToDictionary function that takes a list of schedules and returns a dictionary object that has Jobs as the key for associated Schedule items. Have the index of Schedules implement this dictionary function, and change the Index view so it relies on the dictionary model instead of the Schedules model. Then use a foreach Job in Model loop to display Job title and Job type, with a list of associated schedule items following that. The schedule items should display name and dates.
Optional Add on:
Allow for filtering from the index that will send a modified list of schedules that match the filter to display in the index.

The story was pretty clear about how it wanted to be accomplished. I updated the Schedules Controller Index method.

Initial code - Schedules Controller:

```c#
public ActionResult Index(string sortOrder, string currentFilter, string searchString, int? page, ErrorModalVM error = null)
        {
            if (error != null)
            {
                ViewBag.ErrorModalVm = error;
            }

            ViewBag.CurrentSort = sortOrder;
            ViewBag.PersonSortParm = sortOrder == "person_desc" ? "person_asc" : "person_desc";
            ViewBag.JobSortParm = sortOrder == "job_desc" ? "job_asc" : "job_desc";
            ViewBag.EndSortParm = sortOrder == "enddate_desc" ? "enddate_asc" : "enddate_desc";
            ViewBag.StartDateSortParm = String.IsNullOrEmpty(sortOrder) ? "startdate_asc" : "";

            if (searchString != null)
            {
                page = 1;
            }
            else
            {
                searchString = currentFilter;
            }

            ViewBag.CurrentFilter = searchString;

            var schedules = from s in db.Schedules
                       select s;
                       //*****activate the code below after Schedules database is fixed for Search funtionality 7/26/19 - J.R. 
            //if (!String.IsNullOrEmpty(searchString))
            //{
            //    schedules = schedules.Where(s => s.Person.Contains(searchString)
            //                           || s.Job.Contains(searchString));
     }
```

My Updated Function - Schedules Controller:

```c#
    public ActionResult Index(string sortOrder, string currentFilter, string searchString, int? page, ErrorModalVM error = null)
        {
            //var schedules = db.Schedules.ToList();
            if (error != null)
            {
                ViewBag.ErrorModalVm = error;
            }
            if (searchString != null)
            {
                page = 1; //pagination not active right now, shows all schedules 9/12/19
            }
            else
            {
                searchString = currentFilter; //get input from search form
            }
            ViewBag.CurrentFilter = searchString;
            var allSchedules = from s in db.Schedules
                            select s;
            if (!String.IsNullOrEmpty(searchString)) //filter schedules for search keyword
            {
                allSchedules = allSchedules.Where(s => s.Person.FirstName.Contains(searchString)
                                       || s.Person.LastName.Contains(searchString)
                                       || s.Job.JobTitle.Contains(searchString)
                                       || s.Job.JobType.Contains(searchString));
            }
            List<Schedule> schedules = new List<Schedule>(allSchedules); //display filtered schedules
            var dictionary = AddToDictionary(schedules);
            return View(dictionary);
        }
```

Even though this was a back end story, I still had to update the view to utilize the dictionary information, and add in the search box functionality: 

```html
@using ManagementPortal.Common
@using ManagementPortal.Models
@model Dictionary<Job, List<Schedule>>
@{
    ViewBag.Title = "Schedules";
}

<div class="IndexBody">
    <h2>Schedules</h2>

    <p>
        @Html.Partial(AnchorButtonGroupHelper.PartialView, AnchorButtonGroupHelper.GetCreate())
    </p>
    @using (Html.BeginForm("Index", "Schedules", FormMethod.Get))
    {
        <p>
            @Html.TextBox("SearchString", ViewBag.CurrentFilter as string)
            <input type="submit" value="Search" />

            @*show default page button*@
            <a type="button" class="btn btn-sm" href="@Url.Action("Index")">
                Show Schedules
            </a>
        </p>
    }
        <table class="table">
            <tr>
                <th scope="col">
                    @Html.ActionLink("Job Title", "Index", new { sortOrder = ViewBag.JobSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                <th scope="col">
                    @Html.ActionLink("Job Type", "Index", new { sortOrder = ViewBag.JobTypeSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                <th scope="col">
                    @Html.ActionLink("Person", "Index", new { sortOrder = ViewBag.PersonSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                <th scope="col">
                    @Html.ActionLink("Start Date", "Index", new { sortOrder = ViewBag.StartDateSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                <th scope="col">
                    @Html.ActionLink("End Date", "Index", new { sortOrder = ViewBag.EndSortParm, currentFilter = ViewBag.CurrentFilter })
                </th>
                <th scope="col"></th>
            </tr>
                @foreach (var Job in Model)
                {
                    var number = Job.Value.Count() +1;
                    <tr>
                        <td rowspan="@number">
                            @Html.DisplayFor(Model => Job.Key.JobTitle)
                        </td>
                        <td rowspan="@number">
                            @Html.DisplayFor(Model => Job.Key.JobType)
                        </td>
                        </tr>
                    foreach (var schedule in Job.Value)
                    {
                        <tr>
                        <td>
                            @Html.DisplayFor(Model => schedule.Person.FullName)
                        </td>
                        <td>
                            @Html.DisplayFor(Model => schedule.StartDate)
                        </td>
                        <td>
                            @Html.DisplayFor(Model => schedule.EndDate)
                        </td>
                            </tr>
                    }
                }
            </table>

    @****************         Modal Error         *****************@

    @if (ViewBag.ErrorModalVM != null)
    {
        @Html.Partial("_ErrorModal", (ManagementPortal.ViewModels.ErrorModalVM)ViewBag.ErrorModalVM)
    }
</div>
```

[Back to Table of Contents](#back-end-stories)


### Calendar Pull Existing Schedule

This story stated that the calendar allows for people to set their schedule for time off, but we wanted it to also populate the events currently scheduled. I was asked to create a method within the Calendar Controller that will check for existing schedule items and add them to the calendar. 

I wrote a ShowScheduleItems function in the Calendar Controller, and called it from the Index function to run on page load:

```c#
[HttpGet]
public void ShowScheduleItems()
{
    var schedules = db.Schedules.ToList();
    foreach (var schedule in schedules)
    {
        var schEvent = new CalendarEvent();
        //convert schedule event properties into calendar event properties
        schEvent.Subject = Convert.ToString(schedule.Job.JobTitle);
        schEvent.Start = schedule.StartDate;
        schEvent.End = schedule.EndDate;
        schEvent.Description = "Employee: " + Convert.ToString(schedule.Person.DisplayName) + "  " + "\nJob Type: " + Convert.ToString(schedule.Job.JobType);
        schEvent.IsFullDay = true;
        schEvent.ScheduleId = Convert.ToString(schedule.ScheduleId);
        if (schEvent.End > DateTime.Now.Date && schEvent.Start < DateTime.Now.Date)
        {
            schEvent.Start = DateTime.Now.AddMinutes(1);
        }
        try
        {
            if (ModelState.IsValid)
            {
                //check if an event with a matching ScheduleId is currently on the calendar
                var match = db.CalendarEvents.Where(a => a.ScheduleId == schEvent.ScheduleId).SingleOrDefault();
                if (match != null)
                {
                    var oldSchEvent = match;
                    //check for differences in any properties between events with matching ScheduleId and update db
                    if (oldSchEvent.Subject != schEvent.Subject)
                    {
                        oldSchEvent.Subject = schEvent.Subject;
                    }
                    else if (oldSchEvent.Start != schEvent.Start)
                    {
                        oldSchEvent.Start = schEvent.Start;
                    }
                    else if (oldSchEvent.End != schEvent.End)
                    {
                        oldSchEvent.End = schEvent.End;
                    }
                    else if (oldSchEvent.Description != schEvent.Description)
                    {
                        oldSchEvent.Description = schEvent.Description;
                    }
                    else if (oldSchEvent.IsFullDay != schEvent.IsFullDay)
                    {
                        oldSchEvent.IsFullDay = schEvent.IsFullDay;
                    }
                    else
                    {
                        continue;
                    }
                    //update database entry
                    db.Entry(oldSchEvent).State = EntityState.Modified;
                    db.SaveChanges();
                }
                else //add new event
                {
                    db.CalendarEvents.Add(schEvent);
                    db.SaveChanges();
                }
            }
        }
        catch
        {
            throw new ArgumentException("Event cannot end before today's date.");
        }
    }
}
```

Then I added code so when an schedule event was deleted from either the schedule and the calendar, it was deleted in the other location as well: 

```c#
[HttpPost]
        public JsonResult DeleteEvent(int eventID)
        {
            var status = false;
            var calEvent = db.CalendarEvents.Where(a => a.EventID == eventID).FirstOrDefault();
            if (calEvent != null)
            {
                if (calEvent.ScheduleId != null)
                {
                    //Send schedules to list
                    var schedules = db.Schedules.ToList();
                    foreach (var schedule in schedules)
                    {
                        if (Convert.ToString(schedule.ScheduleId) == calEvent.ScheduleId) //Check for matching ScheduleId
                        {
                            db.Schedules.Remove(schedule);
                        }
                    }
                    db.CalendarEvents.Remove(calEvent);
                    db.SaveChanges();
                }
            }
            status = true;
            return new JsonResult { Data = new { status = status } };
        }
 ```
 
[Back to Table of Contents](#back-end-stories)


### User Manager Clean Up

I chose a story that addressed four separate bugs in the User Manager. This was a board where the site Admin could update user roles and delete users. 

The first bug I addressed was: 
- There should be a cancel option for assigning the role or deleting the user. Make sure there are two buttons on the pop-up message, one for OK and one for Cancel. The cancel one should use a cancel function that does not complete the action.

I did this one by enclosing the JS functions in an if/else statement - which added the "ok" and "cancel" buttons to the pop up automatically. This code is also duplicated below in the functions. 
```js
if (confirm("Warning: Are you sure you want to change this user's role? "))
```

The second bug was:
- There is sometimes an error message stating that a user is already in a role they are being assigned to. This means that we are not unassigning the old role when changing the role. Add logic to the back end to unassign the user from the previous role before assigning them to the new role.

I updated the function in User Controller, here is the old function for comparison:
```c#
if (user.UserRole != userRole)
        {
            if (user != null)
            {
                return Json(new { result = "warning", warning = $"Are you sure you want to change this user's role? " });
            }
            var oldRole = user.UserRole;
            user.UserRole = userRole;
            userManager.AddToRole(user.Id, userRole);
            if (userManager.IsInRole(user.Id, oldRole))
            {
                userManager.RemoveFromRole(user.Id, oldRole);
            }
            _context.SaveChanges();
            return Json(new { result = "success", userName = user.UserName, oldRole = oldRole, newRole = userRole });
        }
```

Here is my update:
```c#
[HttpPost]
[ValidateAntiForgeryToken]
[Authorize(Roles = "Admin")]
public ActionResult UpdateUserRole(string userId, string userRole)
{
    if (!string.IsNullOrEmpty(userId) && !string.IsNullOrEmpty(userRole))
    {
        var userManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(_context));
        var user = userManager.FindById(userId);
        if (user != null)
        {
            if (user.UserRole != userRole)
            {
                var oldRole = user.UserRole;

                if (userManager.IsInRole(user.Id, oldRole))
                {
                    userManager.RemoveFromRole(user.Id, oldRole);
                }
                user.UserRole = userRole;
                userManager.AddToRole(user.Id, userRole);

                _context.SaveChanges();

                return Json(new { result = "success", displayName = user.DisplayName, oldRole = oldRole, newRole = userRole });
            }
            else
            {
                return Json(new { result = "error", message = $"user was already in role: {userRole}" });
            }
        }
        else
        {
            return Json(new { result = "error", message = $"user id {userId} could not be found in the database" });
        }
    }
    else
    {
        return Json(new { result = "error", message = "missing required arguments" });
    }
}
```

This is the Javascript function for updating users, reflecting changes from both bug fixes:

```js
function updateUserRole(formId) {
var form = $('#roleForm_' + formId);
if (confirm("Warning: Are you sure you want to change this user's role? ")) {
    $.ajax({
        url: form.attr("action"),
        type: form.attr("method"),
        data: form.serialize(),
        datatype: "application/json",
        success: function (returnJson) {
            if (returnJson.result == "success") {
                alert("Success! " + returnJson.displayName + " is now a " + returnJson.newRole);
            }
            else if (returnJson.result == "error") {
                alert("Error: " + returnJson.message); 
            }
            else if (returnJson.result == "warning") {
                alert("Warning: " + returnJson.warning);
            }
            else if (returnJson.result == "message") {
                alert("Error: " + returnJson.message);
                location.reload();
            }
        },
        error: function () {
            alert("Error: invalid ajax request");
        }
    });
}
else {
    return false;
}
}
```

The next bug was:
- The error message for not deleting someone from the database who is on the schedule displays the users GUID instead of their name when alerting the admin they cannot delete this user. Change this to be the user's display name.

For this bug I just had to edit the message in the RemoveUser Controller function because the userID and DisplayName were already accessible from that function: 
```c#
return Json(new { result = "error", message = $"User {user.DisplayName} is on schedule and could not be deleted." });
```

The final bug stated: 
The message asking if the admin is sure they want to delete a user displays the username. Change this to the display name.

For this one, from the view, I passed in the DisplayName to the JS function instead - accomplished by changing the model from a UserVM (which we ultimately deleted) to the regular ApplicationUser Model that all the other views and functions were referencing to get user info:

```c#
@using (Html.BeginForm("RemoveUser", "Users", FormMethod.Post, new { id = $"removeForm_{i}" }))
        {
            <input type="hidden" name="userId" value="@Model[i].Id" />
            @Html.AntiForgeryToken()
            <input type="button" onclick="removeUser(@i, '@Model[i].DisplayName')" value="Remove User" />
        }
```

Then I just updated the JS function for the pop up messages:

```js
//REMOVE USER
function removeUser(formId, displayName) {
    var form = $('#removeForm_' + formId);

    if (confirm("Are you sure you want to remove user: " + displayName + "?\nThis action cannot be undone.")) {
        $.ajax({
            url: form.attr("action"),
            type: form.attr("method"),
            data: form.serialize(),
            datatype: "application/json",
            success: function (returnJson) {
                if (returnJson.result == "success") {
                    alert("Success! " + displayName + " has been removed...");
                    $('#userRow_' + formId).remove();
                }
                else if (returnJson.result == "error") {
                    alert("Error: " + returnJson.message);
                }
            },
            error: function () {

            }
        });
    }
    else {
        return false;
    }
}
```

While working on this story, I ran into some issues that revealed to the PM that the UserController needed to be refactored. A separate story was created for this, and I took that too because I was familiar with the current issues. 

[Back to Table of Contents](#back-end-stories)


### Refactor Users Controller

For this story, I had to:
- Refactor the _UserList method so it grabs the list of users from the database, and sends that list as the model instead of going through what was the process of creating a UserVM. 
- Exclude the UserVM from the project, and test to make sure nothing is dependent on it. Remove any dependencies you find, and delete the User VM.
- Determine what, if anything, the isAdminUser function is doing. Replace it with the built in Identity method of checking roles.
- Add comments to the Users Controller documenting the functions and their purpose, and where they are used.

Here is my refactored UsersController, with comments:

```c#
using ManagementPortal.Models;
using Microsoft.AspNet.Identity;
using Microsoft.AspNet.Identity.EntityFramework;
using System.Linq;
using System.Web.Mvc;

namespace ManagementPortal.Controllers
{
    public class UsersController : ApplicationBaseController
    {
        private readonly ApplicationDbContext db = new ApplicationDbContext();

        //Display Users/Index view if logged in user is Admin
        [HttpGet]
        [Authorize(Roles = "Admin")]
        public ActionResult Index()
        {
            var model = db.Users.ToList();
            return View("Index", model);
        }

        //Display _UserList on dashboard if logged in user is Admin
        [ChildActionOnly]
        [Authorize(Roles = "Admin")] 
        public ActionResult _UserList()
        {
            var model = db.Users.ToList(); 
            return PartialView("_UserList", model); 
        }

        //Update user role in database from _UserList
        [HttpPost]
        [ValidateAntiForgeryToken]
        [Authorize(Roles = "Admin")]
        public ActionResult UpdateUserRole(string userId, string userRole) //called with "Update" button from _UserList view
        {
           
            if (!string.IsNullOrEmpty(userId) && !string.IsNullOrEmpty(userRole)) //check for required parameters
            {
                if (User.Identity.GetUserId() == userId) //check if current user ID matches ID of user role being changed, return error if true
                {
                    return Json(new { result = "message", message = "You cannot change your own role" });
                }
                else
                {
                    var userManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(db));
                    var user = userManager.FindById(userId); //get user from database
                    if (user != null) //check if requested user exists
                    {
                        if (user.UserRole != userRole) //check if user is already assigned to role they are being switched to
                        {
                            var oldRole = user.UserRole;
                            if (userManager.IsInRole(user.Id, oldRole)) //remove old role from user in db
                            {
                                userManager.RemoveFromRole(user.Id, oldRole);
                            }
                            user.UserRole = userRole; //update variable userRole to new role
                            userManager.AddToRole(user.Id, userRole); //add new role to user in db
                            db.SaveChanges();
                            return Json(new { result = "success", displayName = user.DisplayName, oldRole = oldRole, newRole = userRole }); //send variables to js function for success message
                        }

                        else //return error if user is already assigned to role they are being switched to
                        {
                            return Json(new { result = "error", message = $"user was already in role: {userRole}" });
                        }
                    }
                    else //return error if requested user isn't in database
                    {
                        return Json(new { result = "error", message = $"user id {userId} could not be found in the database" });
                    }
                }
                
            }
            else //return error if userId or userRole is empty for selected user
            {
                return Json(new { result = "error", message = "missing required arguments" });
            }
        }

        //Remove user from database from _UserList
        [HttpPost]
        [ValidateAntiForgeryToken]
        [Authorize(Roles = "Admin")]
        public ActionResult RemoveUser(string userId) //called with "Remove User" button in _UserList
        {
            if (User.Identity.GetUserId() == userId) //check if current user ID matches ID of user being removed, return error if true
            {
                return Json(new { result = "error", message = "you cannot delete yourself" });
            }
            else
            {
                if (!string.IsNullOrEmpty(userId)) //check for ID of user being removed
                {
                    var userManager = new UserManager<ApplicationUser>(new UserStore<ApplicationUser>(db));
                    var user = userManager.FindById(userId); //get user from database
                    if (user != null) //check if user being removed exists in database
                    {
                        var logins = user.Logins; //get login info for user being removed
                        var rolesForUser = userManager.GetRoles(userId); //get role for user being removed
                        using (var transaction = db.Database.BeginTransaction()) //open db connection
                        {
                            var schedules = (from s in db.Schedules //fetch list of users schedules
                                             where s.Person.Id == user.Id
                                             select s).ToList();
                            if (user.Schedules.Count > 0) //check if user is on schedule, return error if true
                            {
                                return Json(new { result = "error", message = $"User {user.DisplayName} is on schedule and could not be deleted." });
                            }
                            foreach (var login in logins.ToList()) //remove login info for user being removed
                                {
                                    userManager.RemoveLogin(login.UserId, new UserLoginInfo(login.LoginProvider, login.ProviderKey));
                                }
                            foreach (var role in rolesForUser.ToList()) //unassign user being removed from role
                                {
                                    userManager.RemoveFromRole(userId, role);
                                }
                                userManager.Delete(user); //delete user from db
                                transaction.Commit();
                                return Json(new { result = "success" });
                        }
                    }
                    else //return error is user being removed is not in db
                    {
                        return Json(new { result = "error", message = $"User {user.DisplayName} could not be found in the database" });
                    }
                }
                else //return error if user ID of user being removed not found
                {
                    return Json(new { result = "error", message = "missing required arguments" });
                }
            }   
        }

        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
}
```

For this one I also had to update the Index to a super basic table - bc this is a back end story so I don't need to worry about making it pretty: 
There was one more element to the story:
- Determine what, if anything, the Index Users view is doing, and modify it to simply display a list of all users.

I had to add a table to the Index users view to display the list:

```html
@using ManagementPortal.Models
@model List<ApplicationUser>
@{
    ViewBag.Title = "Index";
}

<h2>Welcome Admin</h2>

<table class="table table-striped table-light rounded-lg">
    <tr>
        <th>
            User Name
        </th>
        <th>
            First Name
        </th>
        <th>
            Last Name
        </th>
        <th>
            Phone Number
        </th>
        <th>
            Email Address
        </th>
        <th>
            Role
        </th>
        <th></th>
    </tr>

    @foreach (var user in Model)
    {
        <tr>
            <td>
                @user.UserName
            </td>
            <td>
                @user.FirstName
            </td>
            <td>
                @user.LastName
            </td>
            <td>
                @user.PhoneNumber
            </td>
            <td>
                @user.Email
            </td>
            <td>
                @user.UserRole
            </td>
        </tr>
    }
</table>
```

[Back to Table of Contents](#back-end-stories)


### User-Role Assignment Must Be Required and Save Changes Minor Bug

I took on two mini stories at the end of my Back End sprint, to fill some time. 

The first one I took requested:
When the Admin creates a new user (on CreateUserRequest/Create) there is a drop down option to assign the new user a "Role". This must be a required field and the Admin shouldn't be allowed to create a new user (submit the page) without a role. 

I simply added the Required tag to the Users Model:
```c#
[Required]
[Display(Name = "User Role")]
public string UserRole { get; set; }
```

Then it was as simple as adding one line to the "Create New User" view:
```c#
@Html.ValidationMessageFor(model => model.UserRole, "", new { @class = "text-danger" })
```

The second mini story stated:
In Manage/EditAccountInfo view page, the save changes button is serving its purpose by saving the changes. But more than that, it should also take the user back Mange/Index page or (Home/Dashboard) when clicked. 

All I had to do was one minor edit on the Manage Controller/EditAccountInfo function, which was triggered by the save changes button. 

```c#
return RedirectToAction("Index", "Manage");
```

[Back to Table of Contents](#back-end-stories)


### Implement ShiftTime Modal

I did this story right after I created the ShiftTime Modal: [Front End: Create ShiftTime Modal](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FrontEndStories/README.md#create-shifttime-modal)

The story stated that the ShiftTime Modal needed to save a ShiftTime object and match it with the job that is being created. I was requested to create a function that would collect the information from the form submission and send it to the ShiftTime controller. There was a note in the story that there would be a follow up story to link the ShiftTime to the correct Job in the database. 

I ended up being unable to use the ShiftTime Controller for this function, because the form-within-a-form prevented anything from being submitted without creating the whole job. I ultimately completed this story by adding to the Create function within the JobsController, using a bind statement to submit the data from the ShiftTime Modal through clicking the Submit button of the parent Add Job form. 

```c#
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
 
 I also added to the _ShiftTimeModal.cshtml partial view to call the controller function.
 ```html
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
                    
                    FORM INFORMATION - SEE FRONT END IF INTERESTED
                    
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
 ```
      
[Back to Table of Contents](#back-end-stories)


### Implement Contact Us Page

This was a full stack story so I also created the view, check out more details, and that code, in the Front End section: 
[Front end Components](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FrontEndStories/README.md#implement-contact-us-page)

The controller: 
```c#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using ManagementPortal.Models;
using System.Net.Mail;
using System.Web.Mvc;
using System.Text;
using System.Threading;
using System.Net;
namespace ManagementPortal.Controllers
{
    public class ContactUsController : Controller
    {
        [HttpGet]
        public ActionResult Index()
        {
            return View();
        }
        [HttpPost]
        public ActionResult Index(ContactUs userInput)
        {
            if (ModelState.IsValid)
            {
                var toAddress = "liveprojectdummyacct@gmail.com";
                var fromAddress = userInput.Email.ToString();
                var subject = userInput.Subject;
                var message = "<b>Name: </b>" + userInput.Name + "<br>" + "<b>Email: </b>" + userInput.Email + "<br>" + "<b>Telephone: </b>" + userInput.Phone + "<br><br>" + "<b>Message: </b>" + userInput.Message;
                SendEmail(toAddress, fromAddress, subject, message);
            }
            return View();
        }
        public void SendEmail(string toAddress, string fromAddress, string subject, string message)
        {
            using (MailMessage newMessage = new MailMessage())
            {
                newMessage.From = new MailAddress(fromAddress);
                newMessage.To.Add(new MailAddress(toAddress));
                newMessage.Subject = subject;
                newMessage.Body = message.ToString();
                newMessage.IsBodyHtml = true;
                        try
                        {
                            SmtpClient smtp = new SmtpClient();
                            smtp.Host = "smtp.gmail.com";
                            smtp.Port = 587;
                            smtp.Credentials = new NetworkCredential
                            ("liveprojectdummyacct@gmail.com", "123qweASD!");
                            smtp.EnableSsl = true;
                            smtp.Send(newMessage);
                            ModelState.Clear();
                            ViewBag.Message = "Thank you for contacting us! Someone will get back to you shortly. ";
                        }
                        catch (SmtpFailedRecipientsException ex)
                        {
                            foreach (SmtpFailedRecipientException t in ex.InnerExceptions)
                            {
                                var status = t.StatusCode;
                                if (status == SmtpStatusCode.MailboxBusy ||
                                    status == SmtpStatusCode.MailboxUnavailable)
                                {
                                    Response.Write("Delivery failed - retrying in 5 seconds.");
                                    Thread.Sleep(5000);
                                    //resend
                                    SmtpClient smtp = new SmtpClient();
                                    smtp.Host = "smtp.gmail.com";
                                    smtp.Port = 587;
                                    smtp.Credentials = new NetworkCredential
                                    ("liveprojectdummyacct@gmail.com", "123qweASD!");
                                    smtp.EnableSsl = true;
                                    smtp.Send(newMessage);
                                }
                                else
                                {
                                    ViewBag.Message = $"Failed to deliver message to " + t.FailedRecipient;
                                }
                            }
                        }
                        catch (Exception ex)
                        {
                            ViewBag.Message = ex.ToString();
                        }
                        finally
                        {
                            newMessage.Dispose();
                        }
                    }
                }
        }
    }
```

The Model:
```c#
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Threading.Tasks;
namespace ManagementPortal.Models
{
    public class ContactUs
    {
        [Required]
        public string Name { get; set; }
        [Required]
        [EmailAddress]
        public string Email { get; set; }
        [Phone]
        public string Phone { get; set; }
        public string Subject { get; set; }
        [Required]
        public string Message { get; set; }
    }
}
```

[Back to Table of Contents](#back-end-stories)


### Bonus Project: Bug Fix

The PM of the Management Portal project was also the PM of another project, that was already delivered to the customer and live online. That app encountered a bug which crashed the site, so she asked me to address it in between stories on the Management Portal project. The story for the bug fix read: 

There is currently an issue that a person can create a schedule without selecting either a job or a person from the drop down list and the system saves the item with a null value for the unselected item. This results in null value exceptions on the dashboard page where the schedule tries to display. 
Add client side validation using JavaScript (ie a script that check for these things prior to sending the data to the controller) to ensure that the value being sent to the controller is not null for person or job. This may mean checking that the display for the select list is not --Select Person-- or --Select Job Site--, or it may mean checking that the value for the select list is not null. Use the custom modal pop-up with a message letting them know the item(s) are required with only a single button to dismiss the alert.
Implement this same validation in the Edit view as well.

I had to change the form method from a button submission to a standard form to have the submit button trigger the JS function before it went to the controller:
```
@using (Html.BeginForm("Edit", "Schedules", FormMethod.Post, new { id = "editSchedule" }))
```
Then I just wrote a couple scripts to make sure the user had selected values from the dropdown: 
```
@*Modal for error message*@
@Html.Partial("~/Views/Shared/InfoMessageModalPartial.cshtml")
    @section Scripts {
        @Scripts.Render("~/bundles/jqueryval")
        <script type="text/javascript">
            //Confirm that a person is selected from the drop down
            //Throw error message if no person is selected
            $("#createSchedule").submit(function (event) {
                if ($("#Person").val() == 0) {
                    modalInfo("Employee is Required");
                    event.preventDefault();
                }
                else {
                    return;
                }
            });
            //Confirm that a jobsite is selected from the drop down
            //Throw error message if no jobsite is selected
            $("#createSchedule").submit(function (event) {
                if ($("#Jobsite").val() == 0) {
                    modalInfo("Job Title is Required");
                    event.preventDefault();
                }
                else {
                    return;
                }
            });
        </script>
```

This bonus project was interesting because I was so used to the structure of the Management Portal site I had been working on, that jumping into another site for a quick fix was a fun challenge. Being able to deliver this fix quickly was an accomplishment that I'm proud of, especially since the end client saw the results right away. 
