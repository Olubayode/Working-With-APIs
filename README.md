# Working-With-APIs

AUTHOR: Olubayode Ebenezer.


Created 27-06-2022 11:29:00
 
I Created a new GitHub repository with a README.md, and Python .gitignore file.

I Cloned it to my machine/computer, that will create a new folder on my computer with my repository’s content.

I created a new virtual environment in that folder named venv. 

I activated it and installed the Django python package (Hint: `pip install django`).

Also installed the django rest framework (pip install djangorestframework)

I created a new django project (Hint: `django-admin startproject <project_name>`). 

I Used an  ID as the name of the project.

I’ll be creating the beginnings of a URL shortener service.

Created a new application using the django startapp command. The app was called links.

I Added the links and rest_framework app to INSTALLED_APPS.

 I Created a new file, utils.py in my links app folder. I replaced the content of links/utils.py with this src file that you can as well see sample here 👇
 https://github.com/Olubayode/Working-With-APIs/blob/main/src/links/utils.py . 

In links/models.py , I created a new model Link. It should have the following attributes:

#  Link
# --------------

target_url : A url path of maxlength 200, use Django’s models.URLField

description : A string of maxlength 200, use Django’s models.CharField

identifier: A string of maxlength 20, use Django’s models.SlugField. Set blank=True and unique=True for the field.

author : A Foreign Key to the current user model. Make use of Django’s get_user_model function.

created_date : A date-time column, use Django’s models.DateTimeField.

active :  A boolean (True or False), determining if the shortened URL is publicly accessible. Make use of Django’s BooleanField. The default should be True.


 We now have a Link model in links/models.py with a custom save method.

I Created migrations for my new model using the makemigrations django command. 

I Run all migrations using, migrate django command.

To make my Link model accessible from the admin site, I  registered the Link model in links/admin.py . 

I went ahead to create a superuser, and created some Links from the admin dashboard.

# Now for the serializers. 

I Created a new file serizliers.py in the links app. It will hold all the logic for our serializers.
Create a new serializer, LinkSerializer, which inherits DRF’s 

serializers.ModelSerializer. It should have the following attributes:
class Meta:

model = Link

fields = “__all__”

 
On to the views. I will only allow users to interact with active/public urls through my API.

In blog/views.py,  create a new view/class PostListApi, which inherits DRF’s generic ListAPIView,  it’s config/attributes should be:

queryset = Link.objects.filter(active=True)

serializer_class = LinkSerializer

 I Created another view, PostCreateApi, which inherits DRF’s generic CreateAPIView, with attributes:

queryset = Link.objects.filter(active=True)

serializer_class = LinkSerializer

 I Creates another view, PostDetailApi which inherits DRF’s generic RetrieveAPIView, with attributes:

queryset = Link.objects.filter(active=True)

serializer_class = LinkSerializer

 I Created another view PostUpdateApi, which inherits DRF’s generic UpdateAPIView, with attributes:

queryset = Link.object.filter(active=True)

serializer_class = LinkSerializer


 I Create another view PostDeleteApi, which inherits django’s generic DestroyAPIView, with attributes:

queryset= Link.objects.filter(active=True)

serializer_class = LinkSerializer


I Create a file, links/urls.py, if it doesn’t already exist.

I replace  the content of links/urls.py with the content you can see samples here 👇
 https://github.com/Olubayode/Working-With-APIs/blob/main/src/links/urls.py 

 I went to the project_app/urls.py and added a new url pattern with the following content:

path("api/links/", include("links.urls"))


 Staged and Commit your Django project and push my changes to my GitHub repository. 


# Resources:

Introduction To Django Rest Framework by Femi (https://www.youtube.com/watch?v=EDyt4dvLu1g&t=1448s)

Django REST Framework Views - Generic Views | TestDriven.io ( https://testdriven.io/blog/drf-views-part-2/)

What is a URL shortener? ( https://blog.rebrandly.com/what-is-a-url-shortener/)
