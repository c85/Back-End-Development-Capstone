# Create Band Website with Django

![]https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/IDSN-logo.png

**Estimated time needed**: 90 minutes

Welcome to the **Create Band Website wth Django** hands-on lab. In this lab, you will create the main website for the band. The lab provides a GitHub template repository to get you started.

At the end of the lab, you will:
1. Create the main home page for the band
1. Create the songs page that lists all the titles of the songs
1. Craete the photos page that displays pictures from past events
1. Allow users to log in and:
	1. See concerts they are attending
	1. Change attendance at concerts
1. Allow admin user to create, delete, and edit concerts


## Objectives
In this lab, you will:

- Start a Django Server
- Create and run database migrations
- Create a Django admin user
- Create backend views for the Django application
- Send JSON data to templates
- Create Django models
- Check for authenticated users in Django backend

### Note: Important Security Information

Welcome to the Cloud IDE. This is where all your development will take place. It has all the tools you will need to use, including **Python** and **Flask**.

It is important to understand that the lab environment is ephemeral. It only lives for a short while before it is destroyed. It is imperative that you push all changes made to your own GitHub repository so that it can be recreated in a new lab environment any time it is required.

Also, note that this environment is shared and, therefore, not secure. You should not store any personal information, usernames, passwords, or access tokens in this environment for any purpose.

## Your Task
If you haven\&#x27;t generated a GitHub Personal Access Token you should do so now. You will need it to push code back to your repository. It should have &#x60;repo&#x60; and &#x60;write&#x60; permissions, and be set to expire in &#x60;60&#x60; days. When Git prompts you for a password in the Cloud IDE environment, use your Personal Access Token instead. Follow the steps in the [Generating Git Token Lab](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/labs/deployment/git_token.md.html &quot;Generating Git Token Lab&quot;) for detailed instructions.

The environment may be recreated at any time, so you may find that you have to perform the Initialize Development Environment each time the environment is created.

## Note on Screenshots
Throughout this lab, you will be prompted to take screenshots and save them on your device. You will need these screenshots to either answer graded quiz questions or upload the screenshots as your submission for peer review at the end of this course. Your screenshot must have either the .jpg or .png extension.

To take screenshots, you can use various free screen-capture tools or your operating system&#x27;s shortcut keys. For example:

- Mac: you can use &#x60;Shift + Command + 3 (⇧ + ⌘ + 3)&#x60; on your keyboard to capture your entire screen, or &#x60;Shift + Command + 4 (⇧ + ⌘ + 4)&#x60; to capture a window or area. It will be saved as a .jpg or .png file on your Desktop.

- Windows: you can capture your active window by pressing &#x60;Alt + Print Screen&#x60; on your keyboard. This command copies an image of your active window to the clipboard. Next, open an image editor, paste the image from your clipboard to the image editor, and save the image as .jpg or .png.

## Create New Repository from Template

1. Click this URL to open the starter code project: https://github.com/ibm-developer-skills-network/sfvih-Back-end-Development-Capstone
2. Use the green **Use this template** button to clone this repository to your own private GitHub account.

	**Do not use Fork; use the Template button.**

	![Create new repository from template](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-fork-template.png &quot;Create new repository from template&quot;)

3. Give your repository the name &#x60;Back-end-Development-Capstone&#x60;. This is the name that graders will be looking for to grade your work.
4. Ensure you select the &#x60;Public&#x60; option for your repository and then create it.

## Evidence
1. Note down the URL of your GitHub repository (not the template) to submit for peer review. Recall the graders are looking for a repository named &#x60;Back-end-Development-Capstone&#x60; in your account.

## Initialize Development Environment

Because the Cloud IDE environment is ephemeral, it may be deleted at any time. The next time you come into the lab, a new environment may be created. Unfortunately, this means that you will need to initialize your development environment every time it is recreated. This shouldn\&#x27;t happen too often as the environment can last for several days at a time, but when it is removed, this is the procedure to recreate it.

## Overview
Each time you need to set up your lab development environment, you will need to run three commands.

Each command will be explained in further detail, one at a time.

The commands include:

&#x60;&#x60;&#x60;
git clone https://github.com/$GITHUB_ACCOUNT/Back-end-Development-Capstone.git
cd /home/project/Back-end-Development-Capstone
bash ./bin/setup.sh
exit
&#x60;&#x60;&#x60;

Now, let\&#x27;s discuss each of these commands and explain what needs to be done.

## Task 1 - Clone the repository
Initialize your environment using the following steps:

1. Open a terminal with &#x60;Terminal&#x60; &gt; &#x60;New Terminal&#x60; if one is not open already.

2. Next, use the export GITHUB_ACCOUNT command to export an environment variable that contains the name of your GitHub account.

   &gt; **Note:** Substitute your real GitHub account for the {your_github_account} placeholder below:

&#x60;&#x60;&#x60;bash
export GITHUB_ACCOUNT&#x3D;{your_github_account}
&#x60;&#x60;&#x60;

3. Then use the following commands to clone your repository.

&#x60;&#x60;&#x60;bash
git clone https://github.com/$GITHUB_ACCOUNT/Back-end-Development-Capstone.git
&#x60;&#x60;&#x60;

## Task 2 - Initialize the development environment

4. Change to the Back-end-Development-Capstone directory, and execute the &#x60;./bin/setup.sh&#x60; command.
&#x60;&#x60;&#x60;bash
cd /home/project/Back-end-Development-Capstone
bash ./bin/setup.sh
&#x60;&#x60;&#x60;

5. You should see the follow at the end of the setup execution:

	![setup script done](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/get_pics_setup_done.png &quot;setup script done&quot;)

6. Finally, use the &#x60;exit&#x60; command to close the current terminal. The environment will not be fully active until you open a new terminal in the next step.

&#x60;&#x60;&#x60;bash
exit
&#x60;&#x60;&#x60;

## Validate
To validate that your environment is working correctly, you must open a new terminal because the Python virtual environment will only activate when a new terminal is created. You should have ended the previous task by using the &#x60;exit&#x60; command to exit the terminal.

1. Open a terminal with &#x60;Terminal&#x60; &gt; &#x60;New Terminal&#x60; and check that everything worked correctly by using the &#x60;which python&#x60; command:

	Check which Python you are using:

	&#x60;&#x60;&#x60;bash
	which python
	&#x60;&#x60;&#x60;&#x60;

	You should get back:

	&#x60;&#x60;&#x60;
	(backend-django-venv) theia:project$ which python
	/home/theia/backend-django-venv/bin/python
	&#x60;&#x60;&#x60;

	Check the Python version:

	&#x60;&#x60;&#x60;bash
	python --version
	&#x60;&#x60;&#x60;

	You should get back some patch level of Python 3.8:

	&#x60;&#x60;&#x60;
	Python 3.8.0
	&#x60;&#x60;&#x60;

This completes the setup of the development environment. Anytime your environment is recreated, you will need to follow this procedure.

## Project Overview

You created the &#x60;songs&#x60; and the &#x60;photos&#x60; microservices in the last two modules. You are now asked to create the main &#x60;Django&#x60; website for the band. An incomplete template has been provided by the previous developer. You have already created a repository in your GitHub account from this template. You will now complete the following exercises to run this Django application locally in the lab environment.

## Exercise 1: Complete Django Data Models

Migrations are Django’s way of propagating changes you make to your models (adding a field, deleting a model, and others) into your database schema. They are designed to be mostly automatic, but you will need to know when to make migrations, when to run them, and the common problems you might encounter.

There are several commands which you will use to interact with migrations and Django’s handling of database schema:

- **migrate**, responsible for applying and dissociating migrations.
- **makemigrations**, responsible for creating new migrations based on the changes you have made to your models.
- **sqlmigrate**, displays the SQL statements for a migration.
- **showmigrations**, lists a project\&#x27;s migrations and their status.

Before you make and run migrations, you need to finish the data models in the code. The classes are provided and you will fill out the data types in this exercise.

## Your Tasks

### Task 1: Create a branch to work on

1. Change into the project directory.
	&#x60;&#x60;&#x60;bash
	cd /home/project/Back-end-Development-Capstone
	&#x60;&#x60;&#x60;

1. Since you are working in GitHub, you must pull the latest changes from the main branch to stay up to date. You can then create a new branch.

	The steps are:
	&#x60;&#x60;&#x60;
	git checkout main
	git pull
	git checkout -b backend-rest
	&#x60;&#x60;&#x60;

	&gt; This will switch to the main branch, pull the latest changes, and create a new branch. You will be asked to push all your changes to your GitHub repo and merge all code back into your main branch with a pull request.

You can use the &#x60;git branch&#x60; command to see your current branch:
&#x60;&#x60;&#x60;bash
git branch
&#x60;&#x60;&#x60;

Your output should look something like this:
&#x60;&#x60;&#x60;
$ git branch
* backend-rest
  main
&#x60;&#x60;&#x60;

### Task 2: Complete the data model classes
Open the &#x60;Back-end-Development-Capstone/concert/models.py&#x60; file in the editor.

1. You will notice that the previous developer left the &#x60;Concert&#x60; model properties commented out.
	&#x60;&#x60;&#x60;
	class Concert(models.Model):
		# concert_name
		# duration
		# city
		# date
	&#x60;&#x60;&#x60;
1. Let\&#x27;s add these properites with the following attributes:
	- &#x60;concert_name&#x60;: CharField with a max_length of 255
	- &#x60;duration&#x60;: an IntegerField
	- &#x60;city&#x60;: CharField with a max_length of 255
	- &#x60;date&#x60;: DateField with the default time of now

1. Similarly, you will notice the &#x60;Photo&#x60; model commented out:
	&#x60;&#x60;&#x60;
	class Photo(models.Model):
		# id
		# pic_url
		# event_country
		# event_state
		# event_city
		# event_date
	&#x60;&#x60;&#x60;

1. You will fill it out with the following attributes:
	- &#x60;id&#x60;: IntegerField as a primary key
	- &#x60;pic_url&#x60;: CharField with max_length of 1000
	- &#x60;event_country&#x60;: CharField with max_length of 255
	- &#x60;event_state&#x60;: CharField with max_length of 255
	- &#x60;event_city&#x60;: CharField with max_length of 255
	- &#x60;event_date&#x60;: DateField with the default time of now

1. Finally, the &#x60;Song&#x60;model also needs all the attributes as follows:
	- &#x60;id&#x60;: IntegerField as a primary key
	- &#x60;title&#x60;: CharField with max_length of 255
	- &#x60;lyrics&#x60;: TextField

## Solutions
1. &#x60;Concert&#x60; model should look as follows:
	&lt;details&gt;
		&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	class Concert(models.Model):
		concert_name &#x3D; models.CharField(max_length&#x3D;255)
		duration &#x3D; models.IntegerField()
		city &#x3D; models.CharField(max_length&#x3D;255)
		date &#x3D; models.DateField(default&#x3D;datetime.now)
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. &#x60;Photo&#x60; model should look as follows:
	&lt;details&gt;
		&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	class Photo(models.Model):
		id &#x3D; models.IntegerField(primary_key&#x3D;True)
		pic_url &#x3D; models.CharField(max_length&#x3D;1000)
		event_country &#x3D; models.CharField(max_length&#x3D;255)
		event_state &#x3D; models.CharField(max_length&#x3D;255)
		event_city &#x3D; models.CharField(max_length&#x3D;255)
		event_date &#x3D; models.DateField(default&#x3D;datetime.now)

	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. &#x60;Song&#x60; model should look as follows:
	&lt;details&gt;
		&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	class Song(models.Model):
		id &#x3D; models.IntegerField(primary_key&#x3D;True)
		title &#x3D; models.CharField(max_length&#x3D;255)
		lyrics &#x3D; models.TextField()

	&#x60;&#x60;&#x60;
	&lt;/details&gt;

### Task 3: Make and run migrations
1. Create the initial migrations using the &#x60;makemigrations&#x60; command.
	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	python manage.py makemigrations
	&#x60;&#x60;&#x60;
	&lt;/details&gt;
1. Run the migrate command for the migrations you just created.
	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	python manage.py migrate
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

## Evidence
1. Take a screenshot of the terminal after executing the &#x60;migrate&#x60; command.
2. Save the screenshot as &#x60;django-migrate.jpg&#x60; (or &#x60;.png&#x60;).


## Exercise 2: Run the Django App in the Lab Environment

Before you proceed with the rest of the backend exercises, you can run the application locally in the lab enivonrment and see the home page.

## Your Tasks
1. Run the &#x60;runserver&#x60; command to run the application locally.
	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	python manage.py runserver
	&#x60;&#x60;&#x60;
	&lt;/details&gt;
	This should start the Django server at port 8000.
1. Curl &#x60;localhost:8000&#x60; to see if you get a 200 HTTP code from the running server. Note that you are already running the server in the terminal. Open a new terminal or split the existing terminal to execute the curl command:
	&#x60;&#x60;&#x60;bash
	curl -s -o /dev/null -w &quot;%{http_code}&quot; http://localhost:8000
	&#x60;&#x60;&#x60;
	You should see an output of &#x60;200&#x60;:
	&#x60;&#x60;&#x60;
	(venv) theia:project$ curl -s -o /dev/null -w &quot;%{http_code}&quot; http://localhost:8000

	200(venv)
	&#x60;&#x60;&#x60;
1. If you got 200 OK, you can proceed to launch the application by clicking &#x60;Launch Applciation&#x60; icon on the left bar. Once the tab opens, you can enter port as &#x60;8000&#x60; and click the &#x60;Your Application&#x60; button.

	![Launch Django App Locally](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-app-local-launch.png &quot;Launch Django App Locally&quot;)

	You should see the application open in a new tab. Note that none of the links on the top of the page are working. The remaining exercises in the lab will guide you on how to get these links and the admin site working.
	![Django Application Running Locally](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/djang-app-tab.png &quot;Django Application Running Locally&quot;)

## Evidence
1. Take a screenshot of the browser running your application.
2. Save the screenshot as &#x60;django-app-browser.jpg&#x60; (or &#x60;.png&#x60;).

## Exercise 3: Fix Songs page

The &#x60;Songs&#x60; page displays all songs and lyrics for each when the user clicks on a song title. Currently, there is no URL mapped to the songs method in the view file. All the URLs are stored in &#x60;concert/urls.py&#x60; file. You need to add the URL for the songs.

## Your Tasks

### Task 1 : Fix songs URL

Open the &#x60;Back-end-Development-Capstone/concert/urls.py&#x60; file in the editor.

1. You should see all the URLs defined in this file:
	&#x60;&#x60;&#x60;
	urlpatterns &#x3D; [
		re_path(r&quot;^$&quot;, views.index, name&#x3D;&quot;index&quot;),
		path(&quot;&quot;, views.songs, name&#x3D;&quot;songs&quot;),
		...
	]
	&#x60;&#x60;&#x60;
1. Replace the first empty string for the songs urlpattern with &#x60;song/&#x60;
	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	path(&quot;songs/&quot;, views.songs, name&#x3D;&quot;songs&quot;),
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. If you click on the songs link now, you will get an error. However, you have made progress. Instead of the link not working at all, you are one step closer to getting it to work.


### Task 2 : Fix songs view

The songs link is working, but the view is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;songs&#x60;.
	&#x60;&#x60;&#x60;
	def songs(request):
		# songs &#x3D; {&quot;songs&quot;:[]}
		# return render(request, &quot;songs.html&quot;, {&quot;songs&quot;: [insert list here]})
		pass
	&#x60;&#x60;&#x60;
1. You will eventually hook this method with the song microservice you created in the previous lab. For now, let\&#x27;s return the following dummy data back to the &#x60;songs.html&#x60; template.
	&#x60;&#x60;&#x60;
	[{&quot;id&quot;:1,&quot;title&quot;:&quot;duis faucibus accumsan odio curabitur convallis&quot;,&quot;lyrics&quot;:&quot;Morbi non lectus. Aliquam sit amet diam in magna bibendum imperdiet. Nullam orci pede, venenatis non, sodales sed, tincidunt eu, felis.&quot;}]
	&#x60;&#x60;&#x60;

	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def songs(request):
		songs &#x3D; {&quot;songs&quot;:[{&quot;id&quot;:1,&quot;title&quot;:&quot;duis faucibus accumsan odio curabitur convallis&quot;,&quot;lyrics&quot;:&quot;Morbi non lectus. Aliquam sit amet diam in magna bibendum imperdiet. Nullam orci pede, venenatis non, sodales sed, tincidunt eu, felis.&quot;}]}
		return render(request, &quot;songs.html&quot;, {&quot;songs&quot;:songs[&quot;songs&quot;]})
	&#x60;&#x60;&#x60;
	&gt; Note that you also need to remove the &#x60;pass&#x60; statement from the last line of the method.
	&lt;/details&gt;

1. You should now see a song dislayed when you click the &#x60;Songs&#x60; page.

	![Songs page working in django](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-songs-page-working.png &quot;Songs page working in django&quot;)

1. You should also see the lyrics pop up when you click the song.
	![Songs lyrics modal working](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/djang-songs-modal-working.png &quot;Songs lyrics modal working&quot;)

## Evidence
1. Take a screenshot of your application showing the modal dialog along with the single song in the backgroud.
2. Save the screenshot as &#x60;django-song-modal.jpg&#x60; (or &#x60;.png&#x60;).

## Exercise 4: Fix Photos page

The &#x60;Photos&#x60; page displays pictures from past events by the band in different cities across the world. Currently, there is no URL mapped to the photos method in the view file. All the URLs are stored in &#x60;concert/urls.py&#x60; file. You need to add the URL for the photos.

## Your Tasks

### Task 1 : Fix photos URL

Open the &#x60;Back-end-Development-Capstone/concert/urls.py&#x60; file in the editor.

1. You should see all the URLs defined in this file:
	&#x60;&#x60;&#x60;
	urlpatterns &#x3D; [
		re_path(r&quot;^$&quot;, views.index, name&#x3D;&quot;index&quot;),
		path(&quot;songs&quot;, views.songs, name&#x3D;&quot;songs&quot;),
		path(&quot;&quot;, views.photos, name&#x3D;&quot;photos&quot;),
		...
	]
	&#x60;&#x60;&#x60;
1. Replace the first empty string for the photos urlpattern with &#x60;photos&#x60;.
	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	path(&quot;photos/&quot;, views.photos, name&#x3D;&quot;photos&quot;),
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. If you click on the photos link now, you will get an error. However, again, you have made progress.


### Task 1 : Fix photos view
The photos link is working, but the view is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;photos&#x60;.
	&#x60;&#x60;&#x60;
	def photos(request):
		# photos &#x3D; None
		# return render(request, &quot;photos.html&quot;, {&quot;photos&quot;: photos})
		pass
	&#x60;&#x60;&#x60;
1. You will eventually hook this method with the pictures microservice you created in the previous lab. For now, let&#x27;s return the following dummy data back to the &#x60;photo.html&#x60; template.
	&#x60;&#x60;&#x60;
	[{
        &quot;id&quot;: 1,
        &quot;pic_url&quot;: &quot;http://dummyimage.com/136x100.png/5fa2dd/ffffff&quot;,
        &quot;event_country&quot;: &quot;United States&quot;,
        &quot;event_state&quot;: &quot;District of Columbia&quot;,
        &quot;event_city&quot;: &quot;Washington&quot;,
        &quot;event_date&quot;: &quot;11/16/2022&quot;
    }]
	&#x60;&#x60;&#x60;

	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def photos(request):
		photos &#x3D; [{
		&quot;id&quot;: 1,
		&quot;pic_url&quot;: &quot;http://dummyimage.com/136x100.png/5fa2dd/ffffff&quot;,
		&quot;event_country&quot;: &quot;United States&quot;,
		&quot;event_state&quot;: &quot;District of Columbia&quot;,
		&quot;event_city&quot;: &quot;Washington&quot;,
		&quot;event_date&quot;: &quot;11/16/2022&quot;
		}]
		return render(request, &quot;photos.html&quot;, {&quot;photos&quot;: photos})
	&#x60;&#x60;&#x60;
	&gt; Note that you also need to remove the &#x60;pass&#x60; statement from the last line of the method.
	&lt;/details&gt;

1. You should now see a photo dislayed when you click the &#x60;photos&#x60; page

	![Working photos page](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-photos-page-working.png &quot;Working photos page&quot;)


## Evidence
1. Take a screenshot of your application showing the single photo in the photos page.
2. Save the screenshot as &#x60;django-photos.jpg&#x60; (or &#x60;.png&#x60;).


## Exercise 5: Fix the Sign Up flow

The &#x60;Signup&#x60; flow allows the user to create an account with the site so they can book concerts.

## Your Tasks

### Task 1 : Fix &#x60;signup&#x60; URL

Open the &#x60;Back-end-Development-Capstone/concert/urls.py&#x60; file in the editor.

1. You should see all the URLs defined in this file:
	&#x60;&#x60;&#x60;
	urlpatterns &#x3D; [
		re_path(r&quot;^$&quot;, views.index, name&#x3D;&quot;index&quot;),
		path(&quot;songs&quot;, views.songs, name&#x3D;&quot;songs&quot;),
		path(&quot;photos&quot;, views.photos, name&#x3D;&quot;photos&quot;),
		path(&quot;&quot;, views.login_view, name&#x3D;&quot;login&quot;),
		path(&quot;&quot;, views.logout_view, name&#x3D;&quot;logout&quot;),
		path(&quot;&quot;, views.signup, name&#x3D;&quot;signup&quot;),
		...
	]
	&#x60;&#x60;&#x60;
1. Replace the first empty string for the signup urlpattern with &#x60;signup/&#x60;.
	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	path(&quot;signup/&quot;, views.signup, name&#x3D;&quot;signup&quot;),
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. If you were to click the &#x60;Signup&#x60; link now, you will get an error. However, again, you have made progress and we will fix this error in the next Task.


### Task 2 : Fix Signup View
The Signup link is working, but the view is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;signup&#x60;.
	&#x60;&#x60;&#x60;
	def signup(request):
    	pass
	&#x60;&#x60;&#x60;
1. This view will handle both use cases when the user is asking for the signup form and also when the user is submitting the signup form after adding their details. Let\&#x27;s consider the first. You simply return &#x60;signup.html&#x60; template with the &#x60;SignUpForm&#x60; form.
	&#x60;&#x60;&#x60;
	return render(request, &quot;signup.html&quot;, {&quot;form&quot;: SignUpForm})
	&#x60;&#x60;&#x60;
1. The second case is a little more involved. You will have to check if the request is a &#x60;POST&#x60; request. A &#x60;POST&#x60; request will indicate the user submitted a form. There are a number of steps after this:
	- get the &#x60;username&#x60; from the request.
	- get the &#x60;password&#x60; from the request.
	- look for the user with this username.
	- if the user already exists, return to &#x60;Signup&#x60;page with the message &#x60;user already exists&#x60;.
	- if the user does not exist, log in the user wih their new credentials, and return to the index page.

	We have provided the following skeleton code to get you started:
	&#x60;&#x60;&#x60;
	if request.method &#x3D;&#x3D; &quot;POST&quot;:
        username &#x3D; {insert code to get username from the request}
        password &#x3D; {insert code to get password from the request}
        try:
            user &#x3D; {insert code to find user using User.objects.filter method}
            if user:
				return {insert code to render the signup.html page with the SignUpForm form and a message of &quot;user already exist&quot;}
            else:
                user &#x3D; {insert code to create a new user using the User.objects.create method. Remmeber to use the make_password method to create the password securely}
                {insert code to log in the user with the django.contrib.aut. module}
                {insert code to return the user back to the index page}
        except User.DoesNotExist:
            return {insert code to render the &#x27;signup.html&#x27; page with the &#x27;SignUpForm&#x27; form}
    return {insert code to render the &#x27;signup.html&#x27; page with the &#x27;SignUpForm&#x27; form}
	&#x60;&#x60;&#x60;

1. If your code works without errors, you should now see a sign up form when you click the &#x60;signup&#x60; link.

	![Django Sign Up form working](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-signup-working.png &quot;Django Sign Up form working&quot;)
1. You should be able to create a new user and sign in. However, once you have signed in, the &#x60;logout&#x60; link is still broken. We will fix that in the next exercise.


## Final Solution
1. Ensure your solution for the login_view method matches the following:
	&lt;details&gt;
	&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def signup(request):
		if request.method &#x3D;&#x3D; &quot;POST&quot;:
			username &#x3D; request.POST.get(&quot;username&quot;)
			password &#x3D; request.POST.get(&quot;password&quot;)
			try:
				user &#x3D; User.objects.filter(username&#x3D;username).first()
				if user:
					return render(request, &quot;signup.html&quot;, {&quot;form&quot;: SignUpForm, &quot;message&quot;: &quot;user already exist&quot;})
				else:
					user &#x3D; User.objects.create(
						username&#x3D;username, password&#x3D;make_password(password))
					login(request, user)
					return HttpResponseRedirect(reverse(&quot;index&quot;))
			except User.DoesNotExist:
				return render(request, &quot;signup.html&quot;, {&quot;form&quot;: SignUpForm})
		return render(request, &quot;signup.html&quot;, {&quot;form&quot;: SignUpForm})
	&#x60;&#x60;&#x60;
	&lt;/details&gt;


## Exercise 6: Fix Login and Logout

The &#x60;Login&#x60; flow allows the user to log in with their account. They are then able to see the concert page with a list of all concerts. The &#x60;Logout&#x60; flow will log the user out of the application. If you open the application in its current state, you will see the &#x60;Login&#x60; button, but nothing happens when you click it. Your task in this exercise is to fix both these views.

## Your Tasks

### Task 1 : Fix Login and Logout URL

Open the &#x60;Back-end-Development-Capstone/concert/urls.py&#x60; file in the editor.

1. You should see all URLs defined in this file:
	&#x60;&#x60;&#x60;
	urlpatterns &#x3D; [
		re_path(r&quot;^$&quot;, views.index, name&#x3D;&quot;index&quot;),
		path(&quot;songs&quot;, views.songs, name&#x3D;&quot;songs&quot;),
		path(&quot;photos&quot;, views.photos, name&#x3D;&quot;photos&quot;),
		path(&quot;&quot;, views.login_view, name&#x3D;&quot;login&quot;),
		path(&quot;&quot;, views.logout_view, name&#x3D;&quot;logout&quot;),
		...
	]
	&#x60;&#x60;&#x60;
1. Replace the first empty string for the login urlpattern with &#x60;login/&#x60; and the logout urlpattern with &#x60;logout/&#x60;.
	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	path(&quot;login/&quot;, views.login_view, name&#x3D;&quot;login&quot;),
	path(&quot;logout/&quot;, views.logout_view, name&#x3D;&quot;logout&quot;),
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. If you click the &#x60;Login&#x60; link now, you will get an error. However, again, you have made progress and we will fix this error in the next Task.


### Task 2 : Fix Login View
The Login link is working, but the view is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;login_view&#x60;.
	&#x60;&#x60;&#x60;
	def login_view(request):
    	pass
	&#x60;&#x60;&#x60;
1. This view will handle both use cases when the user is asking for the login form and also when the user is submitting a login form. Let&#x27;s consider the first. You simply return &#x60;login.html&#x60; template with the &#x60;LoginForm&#x60; form.
	&#x60;&#x60;&#x60;
	return render(request, &quot;login.html&quot;, {&quot;form&quot;: LoginForm})
	&#x60;&#x60;&#x60;
1. The second case is a little more involved. You will have to check if the request is a &#x60;POST&#x60; request. A &#x60;POST&#x60; request would indicate the user submitted a form. There are a number of steps after this:
	- get the &#x60;username&#x60; from the request
	- get the &#x60;password&#x60; from the request
	- if the username and password are correct, send them to the index page
	- if the username or password are incorrect, send them back to the login page

	We have provided the following skeleton code to get you started:
	&#x60;&#x60;&#x60;
	if request.method &#x3D;&#x3D; &quot;POST&quot;:
        if request.method &#x3D;&#x3D; &quot;POST&quot;:
        username &#x3D; {insert code to get username from the request}
        password &#x3D; {insert code to get password from the request}
        try:
            user &#x3D; {insert code to find the user with the username}

            if {insert code to check the username and password}:
                {insert code to log in the using the django.contrib.auth module}
                return HttpResponseRedirect(reverse(&quot;index&quot;))
        except User.DoesNotExist:
            return {insert code to render the &#x60;login.html&#x60; method using the &#x60;LoginForm&#x60; form}
	&#x60;&#x60;&#x60;

1. If your code works without errors, you should now see a login form when you click the &#x60;Login&#x60; button.

	![Django login link working](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-login-working.png &quot;Django login link working&quot;)

	You can try logging in with the user you created in the previous task. Alternatively, you can sign up as a new user and log in to ensure your code works.

### Task 3 : Fix Logout View
As noted in the previous exercise, the logout link is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;logout_view&#x60;.
	&#x60;&#x60;&#x60;
	def logout_view(request):
    	pass
	&#x60;&#x60;&#x60;
1. The logout view will simply log out the user using the &#x60;django.contrib.auth&#x60; module. Additionally, it will redirect the user to the login screen.
	&lt;details&gt;
	&lt;summary&gt;Click here for hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def logout_view(request):
		{insert code to logout the user using the django.contrib.auth module}
		{insert code to return the user to the login page using the HttpResponseRedirect module}
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

	You can test the logout flow by logging in and then clicking on the &#x60;Logout&#x60; button.

## Final Solution
1. Ensure your solution for the login_view method matches the following:
	&lt;details&gt;
	&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def login_view(request):
		if request.method &#x3D;&#x3D; &quot;POST&quot;:
			username &#x3D; request.POST.get(&quot;username&quot;)
			password &#x3D; request.POST.get(&quot;password&quot;)
			try:
				user &#x3D; User.objects.get(username&#x3D;username)

				if user.check_password(password):
					login(request, user)
					return HttpResponseRedirect(reverse(&quot;index&quot;))
			except User.DoesNotExist:
				return render(request, &quot;login.html&quot;, {&quot;form&quot;: LoginForm})
		return render(request, &quot;login.html&quot;, {&quot;form&quot;: LoginForm})

	def logout_view(request):
		logout(request)
		return HttpResponseRedirect(reverse(&quot;login&quot;))
	&#x60;&#x60;&#x60;
	&lt;/details&gt;


## Exercise 7: Fix the Concert Page

The &#x60;Concert&#x60; page shows a logged in authenticated user and their concerts. The user can either attend a concert or choose not to attend. As before, you will first fix the URL and then fix the concert view. You need to sign in as a valid user to test the tasks below. You can log in with a user you created in the previous exercises or create a brand new user.

## Your Tasks

### Task 1 : Fix concert URL

Open the &#x60;Back-end-Development-Capstone/concert/urls.py&#x60; file in the editor.

1. You should see all the URLs defined in this file:
	&#x60;&#x60;&#x60;
	urlpatterns &#x3D; [
		re_path(r&quot;^$&quot;, views.index, name&#x3D;&quot;index&quot;),
		path(&quot;songs&quot;, views.songs, name&#x3D;&quot;songs&quot;),
		path(&quot;photos&quot;, views.photos, name&#x3D;&quot;photos&quot;),
		path(&quot;login/&quot;, views.login_view, name&#x3D;&quot;login&quot;),
		path(&quot;logout/&quot;, views.logout_view, name&#x3D;&quot;logout&quot;),
		path(&quot;signup/&quot;, views.signup, name&#x3D;&quot;signup&quot;),
		path(&quot;&quot;, views.concerts, name&#x3D;&quot;concerts&quot;),
		...
	]
	&#x60;&#x60;&#x60;
1. Replace the first empty string for the concert urlpattern with &#x60;concert/&#x60;.
	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	path(&quot;concert/&quot;, views.concerts, name&#x3D;&quot;concerts&quot;),
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. If you click the &#x60;Concert&#x60; link now after logging in as a valid user, you will get an error. However, again, you have made progress and we will fix this error in the next Task.


### Task 2 : Fix Concert View
The Concert link is working, but the view is still broken. Open the &#x60;Back-end-Development-Capstone/concert/views.py&#x60; file in the editor.

1. Go to the method named &#x60;concerts&#x60;.
	&#x60;&#x60;&#x60;
	def concerts(request):
    	pass
	&#x60;&#x60;&#x60;
1. This view will first check if the user is authenticated and if so, show the list of concerts to the user by rendering the &#x60;concerts.html&#x60; template with the appropriate data. We have provided the following skeleton code to get you started:
	&#x60;&#x60;&#x60;
	if {insert code to check if the user is authenticated}:
        lst_of_concert &#x3D; {insert code to create an empty list}
        concert_objects &#x3D; {insert code to get all Concerts using the Concert.objects object}
        {insert code to loop through all items in the concert_objects}:
            try:
                status &#x3D; item.attendee.filter(
                    user&#x3D;request.user).first().attending
            except:
                status &#x3D; &quot;-&quot;
            lst_of_concert.append({
                &quot;concert&quot;: item,
                &quot;status&quot;: status
            })
        return {insert code to render the &#x60;concerts.html&#x60; page with the data of {&quot;concerts&quot;: lst_of_concert}}
    else:
        return {insert code to redirect the user to the login page as the user is not authenticated}
	&#x60;&#x60;&#x60;

1. If your code works without errors, you should now see the list of concerts when you click the &#x60;concert&#x60; link after logging in as a valid user.

	![Django Concert Page](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-concerts-2.png &quot;Django Concert Page&quot;)

Notice that the concert details are not showing up. You will fix this in the next exercise.

## Final Solution
1. Ensure your solution for the login_view method matches the following:
	&lt;details&gt;
	&lt;summary&gt;Click here for the solution.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	def concerts(request):
		if request.user.is_authenticated:
			lst_of_concert &#x3D; []
			concert_objects &#x3D; Concert.objects.all()
			for item in concert_objects:
				try:
					status &#x3D; item.attendee.filter(
						user&#x3D;request.user).first().attending
				except:
					status &#x3D; &quot;-&quot;
				lst_of_concert.append({
					&quot;concert&quot;: item,
					&quot;status&quot;: status
				})
			return render(request, &quot;concerts.html&quot;, {&quot;concerts&quot;: lst_of_concert})
		else:
			return HttpResponseRedirect(reverse(&quot;login&quot;))
	&#x60;&#x60;&#x60;
	&lt;/details&gt;


---

## Exercise 8 - Admin and Models

You need to create a super user before you can create concerts.

### Task 1: Create a superuser
1. Open the terminal and change into the project directory
	&#x60;&#x60;&#x60;bash
	cd /home/project/Back-end-Development-Capstone
	&#x60;&#x60;&#x60;
1. Create a superuser. Remember the username and password. The lab uses a username of &#x60;admin&#x60;, an email of &#x60;admin@admin.com&#x60;, and a password of &#x60;admin&#x60;.
	&#x60;&#x60;&#x60;bash
	python manage.py createsuperuser
	&#x60;&#x60;&#x60;
	The output should look as follows:

	![django create superuser](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-create-superuser.png &quot;django create superuser&quot;)

### Task 2 : Register Concert model with the admin interface

If you log into the admin site &#x60;/admin&#x60; with the superuser username and password, you will see that the concert object does not appear there. In this exercise, register the &#x60;concert&#x60; model with the admin interface.

![Admin broken site](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-CD0320EN-SkillsNetwork/images/django-admin-broken.png &quot;Admin broken site&quot;)

Open the &#x60;Back-end-Development-Capstone/concert/admin.py&#x60; file in the editor.

1. Register the &#x60;Concert model&#x60; with the admin interface.

	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;
	admin.site.register(Concert)
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

## Exercise 9: Push code back to GitHub

Now that you have finished the code for the microservice, you can push the &#x60;backend-rest&#x60; branch back to your GitHub fork. Since you are the only one working on this project, go ahead and merge the PR and delete the branch. Make sure all your code changes are pushed back to the main branch before proceeding to the next lab.

1. Use the &#x60;git commit -am&#x60; command to commit your changes with the message &quot;implemented django application&quot;, and the &#x60;git push&#x60; command to push those changes to your repository.
&gt; Note: You will be prompted to set up your git user and email the first time you push:
	&#x60;&#x60;&#x60;
	git config --local user.name &quot;{your GitHub name here}&quot;
	git config --local user.email {your GitHub email here}
	&#x60;&#x60;&#x60;

	&lt;details&gt;
		&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	git commit -am &quot;{message here}&quot;
	git push --set-upstream origin {branch name here}
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

	&lt;details&gt;
	&lt;summary&gt;Click here for a hint.&lt;/summary&gt;

	&#x60;&#x60;&#x60;bash
	git commit -am &quot;implemented django application&quot;
	git push --set-upstream origin backend-rest
	&#x60;&#x60;&#x60;
	&lt;/details&gt;

1. Create a pull request on GitHub to merge your changes into the main branch, and, since there is no one else on your team, accept the pull request, merge it, and delete the branch.

The main branch, at this point, should have your completed code.

## Conclusion

Congratulations! You have finished the Django project. You fixed the URLs and the various views. You also implemented the models that are used in the views and the admin interface. Note that we are hardcoding the songs and photos service. We will connect the real microservices in the final lab of Capstone.

## Next Steps
You have created all the microservices required for this course. You are well on your way to deploying all the services on the cloud.

## Author(s)
CF

## Changelog
| Date | Version | Changed by | Change Description |
|------|--------|--------|---------|
| 2023-02-04 | 0.1 | CF | Initial version created |
| 2023-02-09 | 0.2 | SH | QA pass with edits |
| 2023-02-21 | 0.3 | SH | QA pass after updates |
| 2023-02-21 | 0.3 | CF | Code fixes |