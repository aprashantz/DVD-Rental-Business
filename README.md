# **User Manual (Instruction of running program)**

To run the program with dummy data, a text file for seeding is provided.
Using that file, database can be seeded and program can be run from
Visual Studio or with command ‘dotnet run’.


# Implementation of functions

| **Function** | **Description**                                                                                                                                                                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1            | From the Cast Member’s bridge entity, those DVD number is used with user’s chosen actor number. After that, DVD Title information is retrieved with those DVD numbers.                                                                                                          |
| 2            | Five tables which are DVDTitle, CastMember, DVDCopy, Actor, DVDOnShelves are used to make this function work. To count available copies, if data returned has null value or not in any copies. If null value is present, count of available copies is increased to count total. |
| 3            | To return a member’s loan within past 31 days, only the loan history from present date to last 31 days is filtered and obtained information was passed to interface.                                                                                                            |
| 4            | To show all cast members, actors of each DVD are combined and passed in list. Later to show in view, other DVD information like producer, studio is passed along with list of actors.                                                                                           |
| 5            | To show the last loan of selected member, first loan information is picked from the descending order list of the loans taken by the member.                                                                                                                                     |
| 6            | To add a new loan record, drop down list is provided to user for selecting member and DVD copy. The loan information is then serialized and store in loan table of the database.                                                                                                |
| 7            | Before setting DVD returned date to a loan, loan period time is calculated and information is shown on view as per loan period.                                                                                                                                                 |
| 8            | Member’s information is shown along with their total loan count. To count their loans, Loan table is used and repetition of a member in the rows is counted.                                                                                                                    |
| 9            | User can create a new record of DVD with available producers, studio information along with the release date. Apart from drop down records, user can add new records for producers, studio if required.                                                                         |
| 10           | Using this function, assistant and manager can remove the old DVD copies.                                                                                                                                                                                                       |
| 11           | This function is used to produce those DVDs on loan shown with dates.                                                                                                                                                                                                           |
| 12           | This function is used to show inactive users who have not borrowed any loans in last 31 days.                                                                                                                                                                                   |
| 13           | Using this function, assistant and managers can view those DVD which are not borrowed in last 31 days.                                                                                                                                                                          |
| 14           | Users of the system are allowed to change their account password with this functionality.                                                                                                                                                                                       |

<span id="_Toc102992326" class="anchor"></span>Table 1 Concise
description of functionalities

# Software Architecture

![mvc architecture - ASP.Net Core MVC](media/image15.jpeg)

<span id="_Toc102992325" class="anchor"></span>Figure 15 MVC
Architecture

Working mechanism of MVC architecture in short:

The model view controller architecture pattern serves the front-end user
requests of the system. Controller classes of each functions handles the
user’s request and using the Model class, database is connected and
essential data is flown between controller and database using Model
class. Then Controller class passes information to View which is then
obtained in user friendly manner in the interface. This way, a MVC
architecture works in short (Deacon, 2016).

# Description of methods of Class

To fulfil the requirements of the coursework, several classes were
constructed while some of the classes were auto-generated as built-in
ASP .NET functionalities.

Auto-generated classes:

  - ActorsController

  - DVDCategoriesController

  - DVDCopiesController

  - DVDTitlesController

  - HomeController

  - LoansController

  - LoanTypesController

  - MembersController

  - MembershipCategoriesController

  - ProducersController

  - StudiosController

Self-created classes to implement functionalities from requirements:

  - ActorDVDController

  - DVDDetailsController

  - DVDLoanController

  - DVDonShelvesController

  - DVDReturnController

  - MemberDetailsController

  - MemberLoansController

  - OldCopiesController

  - RolManagerController

  - UserRolesController

Common methods in controllers:

<table>
<thead>
<tr class="header">
<th><strong>Method</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>public async Task&lt;IActionResult&gt; Index()</td>
<td>It returns records of desired data to the view or user interface. The table list of producers, actors, studio, DVD details are rendered using this method.</td>
</tr>
<tr class="even">
<td>public async Task&lt;IActionResult&gt; Details(int? id)</td>
<td>It returns a detailed view of a record of a particular row when ‘Details’ button is clicked for a particular row of data.</td>
</tr>
<tr class="odd">
<td>public async Task&lt;IActionResult&gt; Create([Bind("Properties of class as parameter")] DataModel modelInstance)</td>
<td><p>This same format is used to create methods to insert data in the table. For example: if we want to add new actor record, the function will be public async Task&lt;IActionResult&gt; Create([Bind("ActorNumber,ActorSurname,ActorFirstName")] Actor actor)</p>
<p>In this same format, other classes has their own create method but the format is same for create operation.</p></td>
</tr>
<tr class="even">
<td>public async Task&lt;IActionResult&gt; Edit(int? id)</td>
<td>This method is used in the controller classes where there is need to edit the information of a row/tuple. For example: editing actor, producer, studio and similar records, this function is used in our system.</td>
</tr>
<tr class="odd">
<td>public async Task&lt;IActionResult&gt; Delete(int? id)</td>
<td>This method is used to return the view to delete user’s chosen row from the table.</td>
</tr>
<tr class="even">
<td>public async Task&lt;IActionResult&gt; DeleteConfirmed(int id)</td>
<td>This method confirms the deletion of a row from the table and returns new updated view in the interface.</td>
</tr>
<tr class="odd">
<td>private async Task&lt;List&lt;string&gt;&gt; GetUserRoles(ApplicationUser user)</td>
<td>This method is used to retrieve user roles from the database.</td>
</tr>
<tr class="even">
<td>public UserRolesController(UserManager&lt;ApplicationUser&gt; userManager, RoleManager&lt;IdentityRole&gt; roleManager)</td>
<td>This method is used to make changes in the roles of users where manager can assign or remove roles to the users of the system.</td>
</tr>
</tbody>
</table>

<span id="_Toc102992327" class="anchor"></span>Table 2 Method and its
description

# Work Experience in ASP .NET CORE MVC

This is my first time working in MVC architecture and found that auto
generation of some parts of CRUD operations were really time saving from
my perspective. I was only familiar with micro-framework like Flask and
after using ASP .NET Core MVC, I found this framework very effective to
carry out CRUD functionality web applications. Language-Integrated Query
(LINQ) which we used was similar to the SQLAlchemy that I previously
used in Flask.

The NuGet packages like SQL Server, User Identity were useful and I
found the shared layout feature very handy for my part of task because,
with this, there was no need to make changes in every static html
content of other pages. While working with CSS, I felt task redundancy.
To minimize it, I used a solarized bootstrap theme for overall project.

# Bibliography

Deacon, J., 2016. *Rare Parts.* \[Online\]  
Available at:
<span class="underline">https://www.rareparts.com/pdf/MVC.pdf</span>  
\[Accessed 27 April 2022\].

#
