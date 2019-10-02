# Live Project

## Intro:

At the end of my time at the Tech Academy, I spent six weeks working with a team of fellow students to develop a full scale MVC/MVVM Web Application in C#. It was structured in two week sprints, during which I focused on both Front-End and Back-End development stories. 

### Front End Stories:

[4973 - Create ShiftTime Modal](https://github.com/allisonhill00/CSharpLiveProject/tree/master/FrontEndStories#create-shifttime-modal)

[4997 - Chat Box Upgrade](https://github.com/allisonhill00/CSharpLiveProject/tree/master/FrontEndStories#chat-box-upgrade)

[5114 & 4990 - NavBar Vital Change and Vertical Navigation Bar Final Touch](https://github.com/allisonhill00/CSharpLiveProject/tree/master/FrontEndStories#navbar-vital-change-and-vertical-navigation-bar-final-touch)

[5177 & 5178 - NavBar Icon Updates](https://github.com/allisonhill00/CSharpLiveProject/tree/master/FrontEndStories#navbar-icon-updates)

[5148 - Implement Contact Us Page](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FrontEndStories/README.md#implement-contact-us-page)

[5162 - ChatModal Header Bug](https://github.com/allisonhill00/CSharpLiveProject/blob/master/FrontEndStories/README.md#chatmodal-header-bug)

[5151 - Mobile Friendly Design](https://github.com/allisonhill00/CSharpLiveProject/tree/master/FrontEndStories#mobile-friendly-design)

### Back End Stories:

[5061 - Implement ShiftTime Modal](https://github.com/allisonhill00/CSharpLiveProject/tree/master/BackEndStories#implement-shifttime-modal)

[5027 - Job to Schedules Function](https://github.com/allisonhill00/CSharpLiveProject/tree/master/BackEndStories#job-to-schedules-function)

[5103 - Calendar Pull Existing Schedule](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#calendar-pull-existing-schedule)

[5099 - Implement Schedule Dictionary](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#implement-schedule-dictionary)

[5085 & 5087 - User Role Assignment Must Be Required and Save Changes Minor Bug](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#user-role-assignment-must-be-required-and-save-changes-minor-bug)

[5074 - User Manager Clean Up](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#user-manager-clean-up)

[5106 - Refactor Users Controller](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#refactor-users-controller)

[5148 - Implement Contact Us Page](https://github.com/allisonhill00/CSharpLiveProject/blob/master/BackEndStories/README.md#implement-contact-us-page)

### Bonus Project: Bug Fix

The PM of the Management Portal project was also the PM of another project, that was already delivered to the customer and live online. That app encountered a bug which crashed the site, so she asked me to address it in between stories on the Management Portal project. 

There is currently an issue that a person can create a schedule without selecting either a job or a person from the drop down list and the system saves the item with a null value for the unselected item. This results in null value exceptions on the dashboard page where the schedule tries to display. 
Add client side validation using JavaScript (ie a script that check for these things prior to sending the data to the controller) to ensure that the value being sent to the controller is not null for person or job. This may mean checking that the display for the select list is not --Select Person-- or --Select Job Site--, or it may mean checking that the value for the select list is not null. Use the custom modal pop-up with a message letting them know the item(s) are required with only a single button to dismiss the alert.
Implement this same validation in the Edit view as well.

I had to change the form method from a button submission to a regular form to have the submit button trigger the JS function before it went to the controller:
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
