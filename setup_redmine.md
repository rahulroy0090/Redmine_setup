 

# 1. Install and configure redmine on Podman 


#Create a folder for PostgreSQL data
echo "Creating folder for PostgreSQL data..."
mkdir -p /home/rahul/data/redmine/postgres

## Change ownership of the folder
echo "Changing ownership of the folder..."
podman unshare chown 999:999 /home/rahul/data/redmine/postgres

## Create the Redmine Pod
echo "Creating the Redmine Pod..."
podman pod create --name redmine --publish 3100:3000 --publish 5432:5432

## Run the PostgreSQL container
echo "Running the PostgreSQL container..."
podman run -dt \
    --pod redmine \
    --name redmine-postgres \
    -e POSTGRES_DB=support \
    -e POSTGRES_USER=postgres \
    -e POSTGRES_PASSWORD=password \
    -e POSTGRES_HOST_AUTH_METHOD=trust \
    -e PGDATA=/var/lib/postgresql/data/pgdata \
    -v /home/rahul/data/redmine/postgres:/var/lib/postgresql/data \
  docker.io/postgres:latest

## Run the Redmine application container
echo "Running the Redmine application container..."
podman run -dt \
    --pod redmine \
    --name redmine-app \
    -e REDMINE_DB_POSTGRES=127.0.0.1 \
    -e REDMINE_DB_PORT=5432 \
    -e REDMINE_DB_DATABASE=support \
    -e REDMINE_DB_USERNAME=postgres \
    -e REDMINE_DB_PASSWORD=password \
    docker.io/redmine:latest

## Open Redmine in the default web browser
echo "Opening Redmine in the web browser..."

xdg-open http://localhost:3100


------------------------------------------------------------------------





# 2. Create multiple Project.

Login redmine account.

User:  admin
Password: admin

![Local Image](1.login_page.png)

### Then, Click on Administration tab.

![Local Image](2.Click_On_admin.png )

### Then, Click on Project icon.

![Local Image](3.Click_On_Project.png )

### Then, Click on New-Project icon.

![Local Image](4.Click_On_New-Project.png )

### Then, Open New-Project page.

##### Name:  Enter the project name here....  

##### Description:  Enter the Description here......

##### Click on "Create buttion"/ "Create and add another".


![Local Image](5.New_project_.png )

<!-- ![Local Image](6.second_project.png ) -->


### Then, Click on Project tab.
##### Here all the list of projects.

![Local Image](7.All_project_list.png )

# 3. Create user and assign to emp-group.

### Click on Administration tab.
### Click on "User" icon.

![Local Image](8.Click_On_Users.png )


### Then, Click on "New-user" icon.

![Local Image](9.Click_On_new_users.png )

### Here open new-user page.

#####  Login :  Enter user-login(E-mail)
##### First name : Enter the name here..
##### Last name : Enter the last name here..
##### Email :  Enter the Email id here..
##### Language: Select Language here..

##### Password : Enter password here....
##### Confirmation : Enter the Re-Password here..

##### Must change password at next logon: Mark this opcation...


##### Click on Create buttion.




![Local Image](10.Created_new_user.png )

# Now, assign to emp-group.

### Click on "Groups" icon.

![Local Image](11.Click_On_Group.png )


### Then, Click on "New-Group" icon.

![Local Image](12.Click_on_new_group.png )


### Then, open  New group page.

##### Name : Enter the gorup name here...

##### Click on "Create" buttion.

![Local Image](13.Emp-group_created.png )


### Then, Click on Group icon.
##### then, Click on "Group name" from list.


![Local Image](14.Click_on_emp-group.png )

### Then, Click on "User" tab.

![Local Image](15.Click_On_User.png )

### Then, Click on "New user".

![Local Image](16.Click_On_New-user.png )

### Now, Select the user here.
### Then, Click on add buttion.


![Local Image](17.Add_user_to_group.png )



<!-- ![Local Image](18.Click_on_project.png ) -->

<!-- ![Local Image](19.Click_on_add-project.png ) -->


<!-- ![Local Image](20.Add_project.png ) -->


# 4. Create role emp-role and to emp-tracker 

### Click on "Roles and perrmission".

![Local Image](21.Click_On_Roles-and-permission.png )


### Then, Click on "New role".

![Local Image](22.Click_On_New-role.png )

### Now, open New role page here .
### Then, save the page.

![Local Image](23.new_role_page.png )

# Crete Trackers(emp-tracker).

### Click on "Trackers". 

![Local Image](24.Click_On_Trackers.png )

### Then click on "New tracker".

![Local Image](25.Click-On-New-Tracker.png )

##### Name: Enter the "tracker name".....  
##### Default status: Select the status here....
##### Description : Enter the description here.....

##### Project: Select the project from list here. 

##### Click on "Create" buttion.


###### But here Default status: Empty

###### Now, we need to create status

### Click on " Issue statues ".
### Then Click on "New-Issue" buttion.
### Then Open New issue page here.
![Local Image](29.Issue%20status.png)



![Local Image](30.New-status_page.png)  



![Local Image]( 31.New_issue_created.png )


# 5. Create workflow.

### Click on "workflow ".

![Local Image](27.Click_On_Workflow.png )

### Now, Select the "Role" and "Tracker" here.
### Then, Click on "Edit" buttion.

![Local Image](28.Workflow_page.png )

### Then, Open Workflow page.

##### New-> In Progress -> Resolved -> Closed
#####      In Progress -> Reject 
#####      In progress -> Hold 

##### Then, click on "Save" buttion.
![Local Image](32.Workflow_status.png )

 

 




