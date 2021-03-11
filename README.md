# MIT Athena Locker-hosted Website
Want to see these guides each on their own page?  Please check out our [wiki](https://github.com/Tau-Beta-Pi-MIT/website/wiki)!

## Overview
This repository contains HTML, CSS, and JavaScript code along with images for our website, hosted [here](tbp.mit.edu/www).  This code can be edited and pushed to our Athena server by individuals with appropriate credentials.  

## Installation/Requirements
The only capabilities you'll need on your machine are `ssh` and `git`.  Once you have these set up, you'll be ready to make modifications to the site as you see fit!

## Navigating to our code on the Athena server
Our codebase is hosted in an MIT's athena locker, which is accessible through remote login via `ssh`.  You can navigate to our codebase on the Athena server by following these instructions:

1. Make sure you’re on the moira mailing list tbp-officers@mit.edu.

2. `ssh` into the Athena server: 

`ssh <kerb>@athena.dialup.mit.edu`

**PW**: your kerb password + Duo Authentication (1 for Duo Push)

3. Navigate to our directory where our codebase is hosted:

`cd /mit/tbp/www`

## Website Structure
At a high level, this website uses SSI, HTML, and CSS.  We'll discuss the specifics of how SSI and CSS are used to augment the repository's HTML.  

### Server Side Includes (SSI)
This website uses the [server side includes (SSI)](https://en.wikipedia.org/wiki/Server_Side_Includes) scripting language for formatting and repeating different blocks of html.  Code used for each web page (e.g. header, footer, navigation, home navigation) is contained in the `includes/` directory.  The contents of these files can be added to a separate `.shtml` web page through the following command:

`<!--#include virtual="includes/home-nav.htm"-->`

(In this case, the above command would include the code page for `home-nav.htm` in the new web page.)  If you plan on creating a new web page with a header, navigation bar, and footer, you should use the following piece of code as a template:

```
<!--#include virtual="includes/header.htm"-->
<!--#include virtual="includes/home-nav.htm"-->

<!--BODY OF CODE GOES HERE-->

<!--#include virtual="includes/footer.htm"-->
<!--#include virtual="includes/bottom.htm"-->
```

These commands are parsed using the Python SSI server files in this repository.  It is strongly advised **NOT** to edit these SSI server files.

### CSS
CSS is also used throughout this codebase to format objects, text, and images.  The main sources of CSS can be found in `stylesheets/app.css` and `stylesheets/foundation.css`.

### Web Page Directories
The contents of the website's home page are given by `index.shmtl`.  All other main navigation files (e.g. web pages) can be found in the same directory as `index.shmtl`.  Files used as components of a web page (e.g. `careerfair.shtml`) can be found in the `includes/pages/` directory.

## Updating Our Elibigibles Portal
To update our eligibles portal for the new initiation class, please first make sure the following conditions are met:

1. Eligibility requirements are kept in a publishable google sheet that has the **exact** same format as [this example google sheet](https://docs.google.com/spreadsheets/d/1QTJir8L7kylD65rg0VoDer1m0lLwqVBFXcu7hB9SWzE/edit?usp=sharing).  You can also change the format, but you may need to change the `eligibles_landing_page.shtml` if you do.

2. Make sure you use checkboxes to denote if a requirement is completed.

3. Finally, please make sure that data validation for checkboxes is correct on the Google sheet page that captures all of these requirements.  To do this, select all checkboxes, right click, and select "Data Validation".  Please make sure the "Checked" and "Unchecked" fields correspond to "Complete" and "Incomplete", respectively, as these will be what's displayed for the eligibles in the eligibles portal.

Once these steps are complete, please complete the following instructions:

1. Make sure you are tracking requirements through google sheets.  In the eligibles portal, Go to **File** --> **Publish to the Web**.  Publish in any format.
2. Make sure that the 4th header/column of the requirements spreadsheet is written exactly as "Kerberos" (without quotations).
2. Now, go to **Share**, and find the ID for the google sheet, where the ID can be identified by pattern-matching with this link: `https://docs.google.com/spreadsheets/d/<ID>/edit?usp=sharing`.
3. Next, navigate to `./eligibles_landing_page.shtml`, line 71, and change the ID of the `src` link such that it looks like:
`https://spreadsheets.google.com/feeds/cells/<ID>/1/public/values?alt=json-in-script&callback=doData`.
4. Test this out locally by starting a local server and querying one of the kerberos entries of the new database.  If the kerberos is in the database, you should see two rows appear.
5. Push to GitHub and pull from Athena using the process below.  That's it!
6. **NOTE**: The password for the eligibles portal is `tbp_davinci`.  You can change this on line 25 of `./eligibles_portal.shtml`.

## Suggested workflow for making changes ([feature/branch workflow](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)):
1. Create a branch on the GitHub repository for the feature you’d like to add (e.g. a button for logging tutoring hours):

`git checkout -b name_of_your_branch`

2. Make changes to this codebase on the new branch on your local machine.  Once you're ready to commit and push your changes:

`git add .`

`git commit -m "your_commit_statement"`

`git push -u origin name_of_your_branch`

3. Now navigate to the repository on the Athena server, by following the instructions in the section above ("Navigating to our code on the Athena server").  Once there, fetch the new branch using a git fetch of this syntax: `git fetch <remote-repo> <remote-branch>:<local-branch>` (give it the same name for simplicity):

`git fetch origin name_of_your_branch:name_of_your_branch`

4. Now checkout the new branch on the Athena server:

`git checkout name_of_your_branch`

5. Next, inspect the website at tbp.mit.edu/www to make sure your changes appear as you'd expect and are free of bugs.  **NOTE**: Changes don't always appear immediately, so you noticed that nothing has changed on tbp.mit.edu/www, give it a little more time to wait for the changes to be visible.  If you're using an IDE such as PyCharm, you can also do this locally by examining any of the `.shmtl` files on your `localhost` server port.

6. Once you're satisfied with how everything looks, perform a merge pull request on the GitHub repo (this is accomplished most effectively by just doing this through [GitHub online](https://github.com/)).  Integrate your new changes with the master branch (or have other members of the development team review your changes, and then pull) and then (on both your local machine and the Athena server), switch back to the master branch and pull:

`git checkout master`

`git pull`

7. Finally, after you pull again on both your local computer and the remote Athena server, verify that the website looks as you'd expect it to and is free of bugs!

Feel free to email [rmsander@mit.edu](mailto:rmsander@mit.edu)) with any questions about this workflow or the website.
