Eflex
-----

A flextime calculation tool implemented with Erlang/OTP

Start the tool with the command

    eflex

or see its usage with

    eflex --usage

Here follows a users guide.

By default the Eflex files are stored in a directory called .eflex on
your home directory. Data for each calendar year will be stored in a
separate file containing calculation properties, holidays as well as
data for each individual week of the year.

If the .eflex directory is missing at startup, Eflex will parse old
Ericsson Flextool data files (located in your .Flextool directory on
your home directory) and generate corresponding Eflex year files. You
can bypass this behavior by creating the .eflex directory manually on
beforehand. A data file for the current year will automatically be
generated if it does not exist.

When processing the old Flextool data files, absence all day will be
coded as Flex and work will not be assigned to any particular
project. But this can be controlled by using some options:

  - start the Erlang shell with "eflex --debug"
  - `eflex:start([{absence_all_day, "Absence"}]).`
  - `eflex:start([{absence_all_day, "Vacation"}]).`
  - `eflex:start([{absence_all_day, "my code"}, {unspecified_work, "my project"}]).`

Once the tool is started, one week at the time will be displayed in
the main window. By default the current week is displayed. You can
navigate to other weeks in several ways:

  - press the page up key to go to previous week (<)
  - press shift (or control) and the page up key to go to previous month (<<)
  - press shift and control and the page up key to go to previous year (<<<)
  - press the page down key to go to next week (>)
  - press shift (or control) and the page down key to go to next month (>>)
  - press shift and control and the page down key to go to next year (>>>)
  - press the home key to go to the current week (Today)
  - press the left mouse button in the week column to select a week
    from the popup menu
  - press the left mouse button in the year column to select a year
    from the popup menu

The dates for holidays are displayed in red, while dates for working days and
free days are displayed in black. The dates for free days are enclosed in
parenthesis. A normal working day can be set to be a holiday and vice versa by
first pressing the left mouse key in a date cell and then select the desired
action in the popup menu. Holidays can also be altered in a similar manner in
the separate holiday editor window.

The numerical values in the cells can either be displayed as hours and minutes
or hours and decimals. The hours and minutes are separated with a colon
(e.g. 7.45) while hours and decimals are separated with a dot (e.g. 7,75). The
display format (decimal/minutes) and lots of other properties can be
customized. The values can however be ented in either unit regardless of the
choosen display unit. By default a work day is 7 hours and 45 minutes, a lunch
break is 40 minutes, a normal break is 30 minutes and you must have a break
after 4 hours work on work days and 5 hours of work on free days.

Whenever a value is edited in the tool, at least the current week is
recalculated. But all earlier weeks for the current year, may possibly also be
recalculated if needed. After the calculation, the data for the entire year
(including holidays and other calculation properties) is automatically stored
on disk.

Values in numerical and empty cells may be copied by pressing the left mouse
key and pasted by pressing the middle or right mouse key. If the value is
negative it vill will be converted to a positive value. The value can also be
pasted in other tools using the native paste mechanism.

For each week day the arrival time and the leave time can be edited. Based on
these values the mandatory breaks are calculated. It is possible to adjust
this computed value by entering an adjust value. The adjust value may either
be positive or negative. Based on all these values the actual working time and
flex time will be calculated.

The adjust value can be automatically updated when you need a break. When the
away a while button is pressed you have two minutes to prepare your absence by
for example locking the screen. That means that you may move the mouse the
first two minutes, but after that the first mouse move will be interpreted as
the break is over and the adjust value will be updated accordingly. If you for
some reason want to cancel the break, you can press the cancel button.

The values in the week column are the accumulated values for the current week
and the values in the year column are the accumulated values for the entire
year (up to the displayed week). The cells in the year and week columns cannot
be edited.

The leftmost column is called activity. The black activities are editable
while the red ones are not. Each activity (type) has an inital value which is
used as start value for calculations of that year. The initial value will
affect the accumulated year value.

Further activites may be added by selecting an activity type from a menu that
pops up when the left mouse button is pressed in the activity column. There
are two categories of activites. The first category is about activites that
regards attendance. They are displayed in the upper part of the popup menu as
well as the upper part of the main window. The values of these activities
affects the calculation of the flex time (it becomes blank when it reaches
zero).

The second category is about project related activities. They are displayed in
the lower part of the popup menu as well as the lower part of the main window.
The unspecified activity defaults to the actual working time. When a value is
entered for a project related activity, that value is automatically subtracted
from the unspecified activity. When you are done with specifying working time
for all projects, there should be no value left in the unspecified activity.

The auto code function automatically sets unspecified work to your favorite
project(s) and absence all day to your favorite attendance related
activity. The function can either be activated by pressing the auto code
button or the end key. The auto code function only updates days up to the
current date. Use the configuration editor window to specify four favorite
activities.

When a project activity is selected for unspecified work, it implies that 100%
of the unspecified work will be auto coded for that project. It is however
possible to code parts of the work to one project and parts to another. This
is achieved by entering clever share settings in the activity type editor. If
you want 100% of the work to be coded for a project, the share is 1 for that
project and 0 for all other. If you instead want 1/3 to be coded for one
project and 2/3 to another project, you enter the shares 1 and 2 respectively
for those projects and 0 for all others.

All activity types that are configured to be visible are shown in the activity
popup menu. New activity types may be added and existing ones may be
customized in the activity type editor.

The arrival and leave times for the current day are by default updated
automatically each minute, as long as the mouse pointer has been moved since
the last update. For each day, the first time that the mouse was moved is
noted as arrival time and the last move is noted as leave time.

The first mouse move in a new year will cause a new year file to be created.
The initial activity type values for the new year will be set to the
accumulated values of the year before. The activity types, calculation
properties and holidays will also be copied from the old year. If the old year
is updated further this will not be reflected in the new year file.

In the activity type editor window you can manage activity types. When a
property of an activity type is changed, it directly affects the activities
for that year. All changes are as always immediately stored on disk. 

New activity types are created by cloning existing ones and then customizing
them. When the name of an activity type is changed, all activities (instances)
of that types are also renamed. An activity type can only be deleted if there
are no activites (instances) of that type. The activities must be deleted
manually. It is however possible to obtain a summary for which weeks that have
activities of that partcular type. When viewing the summary it is possible to
click on a week in order to display that week in the main window.

The display unit for activities can either be decimal or minutes. The value of
entered values can either be used in calculations as they are (positive) or
their values can be negated (negative). For example when working overtime the
value added to the flex should be negative while the value for abcence should
be added as a positive value. Most activity values should be kept as they are
(positive). The visible/hidden property controls whether the activity type
should be visible in the activity type menu or not.

As a last resort you can to manually edit the year file with your favourite
editor. The data is stored in XML format. Most of the data should be rather
staightforward to edit. But please have these two things in mind when you edit
the file:

  - Do only edit the file if you are sure that the tool is not running
    as the tool will continously update the file on its own behalf.

  - The order of activities and activity types are significant. The
    predefined mandatory activities must be first, followed by the optional
    abcence/overtime related activites, followed by the unspecified activity,
    followed the project related activities. In other words, the order should
    be the same as displayed in the GUI with the exception of the unspecified
    activity that serves as a delimeter between abcence/overtime related
    activites and project related activites.

Enjoy!

H�kan Mattsson
