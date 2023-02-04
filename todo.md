
>**TABLE OF CONTENT:**
1. [Task List](#base-mode-task-list-crud) 
2. [Stretch Goals - selective](#stretch-goals-my-selective-of-choices)
3. [setups & installation](#setups) 
    * [html](#folder-serverpublichtmlindex)
    * [stylesheet](#folder-serverpubliccssstylecss)
    * [jQuery](#folder-serverpublicvendorsjqueryjs)
    * [client.js](#folder-serverpublicscriptclientjs)
    * [database.sql](#root-folder-databasesql)
    * [server.js](#folder-serverserverjs)
    * [routers](#folder-serverrouters)
    * [modules](#folder-servermodulespooljs)
4. [GitHub merge/branch](#github-pullmerge)
5. [go to README](./README.md)
6. [go to official instruction](https://github.com/PrimeAcademy/weekend-sql-to-do-list/blob/main/INSTRUCTIONS.md)
---

## BASE MODE: task list (crud)

### <ins>HTML + with Bootstrap</ins>
- *UI that allow user to create a task on front end*
    * [] input text field
    * [x] button: add new task
  


### <ins>CSS + with Bootstrap</ins>
*When a task is done, it should look different on the UI. This is done using CSS and connected to the code that determines if the task is done*
    * [x] background color, must have 
    * [x] font family, must have
    * [] font size, must have  
    * [] input/task crossed out when task is completed 
    * [] additionally, input/task should also changed background color to a different color when complete
    * [x] responsive website application


### <ins>CLIENT + SERVER + DATABASE</ins>
*When a task is created the front end it should be able to store data inside the database* 
    * [] `POST`req/res from client to server 
    * [] server will access router for `POST`req/res (should be connected to module (pool.js) aka communication with the database SQL and add to database there)


*When a task is created the front end should refresh to show all tasks that needs to be complete.*
    * [] `GET`req/res from client to server to retrieve the data stored from previous POST request. 
    * [] server will access router for `GET`req/res (should be connected to module (pool.js) aka communication with the database SQL and store data there)
    * [] render() to append 
         -- [] new task
         -- [] button: delete task - dynamic added with each task  <button class="btn"><i class="fa fa-trash"></i></button> 



*Each task should have an option to 'complete'*
    * [] `PUT`req/res from client to server wth unique ID 
    * [] server will access router for `PUT` req/res (should be connected to module (pool.js) aka communication with the database SQL and also update data there)
    * [] when the checkbox is clicked - `this` task will `update` the task by creating a visual change in the input with strike through text appearance and maybe turned the background color 2 shade grey??? 
   

*Each task should have an option to 'delete'*
    * [] `DELETE` from client to server wth unique ID 
    * [] server will access router for `DELETE` req/res (should be connected to module (pool.js) aka communication with the database SQL)
    * [] Deleting a Task should remove it BOTH from the front end as well as the Database.



[] *Any tasks that is COMPLETE or INCOMPLETE should remain on the database (unless deleted)*


<br>

----

## STRETCH GOALS (*my selective of choices*)
1. Practice git branching with each of the task listed above 

2. Style with bootstrap 

3. IF TIME ALLOW: `feature-confirm-delete`
     - []  In whatever fashion you would like, create an 'are you sure: yes / no' option when deleting a task.
        - Some styled options are [Bootstrap Modal](https://getbootstrap.com/docs/4.0/components/modal/) or [Sweet Alerts](https://sweetalert.js.org/guides/): Use the CDN option.


<br>

---

## setups:
1. installation
    - [x] npm init --yes (if package JSON IS NOT present on repo)
    - [x] npm install --yes
    - [x] npm install express
    - [x] npm install pg
    - [x] npm install nodemon (optional)

2. folders
   [x] - `server`
       [x] - `modules`
           [x] - pool.js
       [x] - server.js
       [x] - `routers`
           [] - name.router.js
    
   [x] - `public` 
       [x] - `css`
           [x] - styles.css 
       [x] - html (index)
       [x] - `script` 
           [x] - client.js
       [x] - `vendors`
            [x]- jQuery 

3. `database.sql` [x]

4. `.gitignore` [x]
    node_modules/
    *.log
    .DS_Store
    .vscode/

----

## folder: server/public/html.index
* [x] Your boilerplate and HTML codes goes here!

## folder: server/public/css/style.css
* [x] Your styling codes goes in this file

## folder: server/public/vendors/jquery.js
* [x] Source CDN or add your jQuery files here

## folder: server/public/script/client.js
1. if using jQuery - document on ready!
    ```js
    $(document).ready(function () {
    console.log('jQuery sourced.');
    });
    ```

2. Any event handlers, Render, DOM manipulation goes here!

3. CRUD goes here (req/res = POST, GET, UPDATE, DELETE) goes here - communication with the server side

----

## root folder: database.sql
1. create a new database through Postico

2. database name = `weekend-to-do-app`

3. inside the root folder: `database.sql`
* this is where your database instruction go! See examples below:
    ```js
    CREATE TABLE "books" (
        "id" SERIAL PRIMARY KEY,
        "title" VARCHAR (250) NOT NULL,
        "author" VARCHAR (100) NOT NULL,
        "published" DATE,
    "isRead" BOOLEAN DEFAULT FALSE
    );
    ```

    ```js
    INSERT INTO "books" 
	("title", "author", "published") 
     ```
    ```js
    VALUES 
	('Another Brooklyn', 'Jacqueline Woodson', '8-9-2016', true),
	('Another Brooklyn', 'Jacqueline Woodson', '8-9-2016'),
	('The Girl on the Train', 'Paula Hawkins', '1-13-2015'),
	('Scandalous Behavior', 'Stuart Woods', '1-5-2016')
    ```
    ```js
    SELECT * FROM "books";
    ```
   
----

## folder: server/server.js
1. imports such as examples below: 
    ```js
        const express = require('express');
        const bodyParser = require('body-parser');
        const nameOfRouter = require('./routes/book.router.js');
        const app = express();
    ```

2. Setup body parser - to translating request body into JSON
    ```js
    app.use(bodyParser.urlencoded({extended: true}));
    app.use(bodyParser.json());
    ```

3. Serve back static files by default
    ```js
    app.use(express.static('server/public'))
    ```

4. Start listening for requests on a specific port
    ```js
    const PORT = process.env.PORT || 5000;
    app.listen(PORT, () => {
    console.log('listening on port', PORT);
    });
    ```
5. connect app with the router
    ```js
    app.use(mainRoute);
    ```

6. UNLESS you have 'Routers', otherwise CRUD goes here (req/res = POST, GET, UPDATE, DELETE) goes here!

----

## folder: server/routes/
1.  import express, router, and pool modules
    ```js
    const express = require('express');
    const router = express.Router();
    const pool = require('../modules/pool');
    ```
2. CRUD goes here (req/res = POST, GET, UPDATE, DELETE) goes here!

3. export router (get import to server side)
    ```js
    module.exports = router;
    ```
---

## folder: server/modules/pool.js
1. import pg module
    ```js
    const pg = require('pg');
    ```
2. setup environment
    ```js
    const pool = new pg.Pool({
        database: 'weekend-to-do-app',
        host: 'localhost',
        port: 5432, 
    })
    ```

3. export module 
    ```js
    module.exports = pool;
    ```

---

## GitHub Pull/Merge 

* **If working with a group use the following shortcut for your git stuff!**

1. one person create a repo and invite team to join 
1. accept invite to repo 
1. `git clone` to your local 
1. `git pull origin main`
1. `git branch YOUR NEW BRANCH NAME HERE`
1. `git checkout` (this will switch to YOUR NEW BRANCH NAME HERE)
1. make your changes, once done continue next step below:
    * `git add .`
    * `git commit -m 'message'`
    * `git push YOUR NEW BRANCH NAME HERE`
1. READY TO MERGE? once merge --> merge == final! ALWAYS check work, comments BEFORE you merge!!!
    * `git checkout main`
    * Merge from YOUR NEW BRANCH NAME HERE into main:
        * `git merge --no-ff YOUR NEW BRANCH NAME HERE`
    

[See step-by-steps source here](https://github.com/PrimeAcademy/amethyst-syllabus/blob/main/lecture-notes/week-08-fullstack-sql/08-01_git-branching.md)

---

## Common Tasks/Commands

- `git branch BRANCH-NAME` - Create a branch with the name of **BRANCH-NAME**
- `git branch` - Display the branch you're currently on
- `git branch -a` - Show all available branches that have been created
- `git checkout BRANCH-NAME` - Switch to the branch with name **BRANCH-NAME**
- `git checkout -b BRANCH-NAME` - Create a new branch and check it out
- `git merge --no-ff BRANCH-NAME` - Merge **BRANCH-NAME** into the current branch (use `git branch` to determine the current branch)
- `git pull origin BRANCH-NAME` - Pull down changes from the remote
- `git checkout -b BRANCH-NAME` - Combines branch creation with checkout in one handy command

[source here](https://github.com/PrimeAcademy/amethyst-syllabus/blob/main/lecture-notes/week-08-fullstack-sql/git-branching-cheatsheet.md)
