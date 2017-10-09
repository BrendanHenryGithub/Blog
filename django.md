# MDN django tutorial
>[MDN Django tutorial](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/skeleton_website)

## Step 1  
1. Build the project skeleton:   

        django-admin.py startprojecT PROJECTNAME
2. Create the applicateion: 

        ./manage.py startapp APPNAME
3. Registering the catalog application:  

    you should add the application's config class to the ./settings.py "INSTALED_APPS"   for example : 'catalog.apps.CatalogConfig' (APP's name is 'catalog' in this case)
4. Specifying the database: (default database is SQLite)
5. Hooking up the URL mapper: ./urls.py

        # Use include() to add URLS from the catalog application 
        from django.conf.urls import include
        urlpatterns += [
            url(r'^catalog/',include('catalog.urls')),
        ]
        
        #Add URL maps to redirect the base URL to our application
        from django.views.generic import RedirectView
        urlpatterns += [
            url(r'^$', RedirectView.as_view(url='/catalog/',permanent=True)),
        ]

        # Use static() to add url mapping to serve static files during development (only)
        from django.conf import settings
        from django.conf.urls.static import static

        urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT)
6. Also create a ./catalog/urls.py to create urlmapper

        from django.conf.urls import url 
        from . import views

        urlpatterns = [

        ]
7. Running database migrations
        
        # You'll need to run the below commands every time your models change in a way that will affect the structure of the data that need to be stored.
        ./manage.py makemigrations
        ./manage.py migrate
8. Running the website 

        ./manage.py runserver

## Step 2 deal with models

1. Modeldefinition:
>Models are defined in an application's models.py file. They are implemented as subclasses of django.db.models.Model, and include fields, methods and metadata.

2. Fields:        
- Common field types:[full list of field types](https://docs.djangoproject.com/en/1.10/ref/models/fields/#field-types)

        CharField
        TextField
        IntergerField
        DateField
        EmailField
        FileField
        AutoField
        ForeignKey
        ManyToManyField

- Common field arguments:[full list of field options](https://docs.djangoproject.com/en/1.10/ref/models/fields/#field-options)
        
        help_text
        max_length
        verbose_name
        default
        null
        blank
        choices
        primary_key

3. Metadata
> You can declare model-level metadata for your Model by declaring class metadata

        #common use of this is sorted the class
        ordering = ["xxx","xxx"]

4. Methods
- __str__()
        
        def __str__(self):
                return self.field_name

- get_absolute_url(self):

        def get_absolute_url(self):
                #Return the url to access a particular instance of the model.
                return reverse('model-deatial-view',args=[str(self.id)])

5. Searching for records

        all_books = Book.objects.all()
        # or
        number_wild_books = Book.object.filter(title__contains='wild').count()

## Step3 Admin Site

1. Registering models: display models in the admin site

        #./catalog/admin.py
        from django.contrib import admin

        admin.site.register(Book)

2. Create superuser

        ./manage.py createsuperuser

3. Admin site configuration  
> To change how a model is displayed in the admin interface you define a ModelAdmin class and register it with the model

        # admin.site.register(Author)
        @admin.register(Author)
        class AuthorAdmin(admin.ModelAdmin):
            pass

- Configure list views:
        
        class AuthorAdmin(admin.ModelAdmin):
            list_display = ('xxxx','xxx')

- Add list filter:

        class BookInstanceAdmin(admin.ModelAdmin):
            list_filter = ('status','due_back')

- Controlling which fields are displayed and laid out 

        #laid out
        fields = ['first_name', 'last_name', ('date_of_birth', 'date_of_death')]

        #Sectioing detail view
        fieldsets = (
            (None, {
                'fields': ('book','imprint', 'id')
            }),
            ('Availability', {
                'fields': ('status', 'due_back')
            }),
        )

- Inline editint of associated records:
        
        class BooksInstanceInline(admin.TabularInline):
            model = BookInstance
            extra = 0

        @admin.register(Book)
        class BookAdmin(admin.ModelAdmin):
            list_display = ('title', 'author', 'display_genre')
            inlines = [BooksInstanceInline]   

## Step4 Create home page
1. Change the ./catalog/urls.py

        urlpatterns = [
            url(r'^$', views.index, name='index'),
        ]

2. Change the ./catalog/views.py

        def index(request):
            ...
            return render(request,'xxx.html',context={'xxx':xxx,})

3. Create the ./catalog/templates directory and create some html templates in here
>[Templates(Django Doc)](https://docs.djangoproject.com/en/1.10/topics/templates/)
>[Manage static files](https://docs.djangoproject.com/en/1.10/howto/static-files/)

        template tags : {%  %}
        template variables : {{  }}

## Step5 Generic class-base view
1. Add URL mapping 

        url(r'^books/$', views.BookListView.as_view(), name='books')

2. ListView & DetailView (class base):

        from django.views import generic

        class BookListView(generic.ListView):
            model = Book
            paginate_by = 10
            context_object_name = 'my_book_list'   # your own name for the list as a template variable
            queryset = Book.objects.filter(title__icontains='war')[:5] # Get 5 books containing the title war
            template_name = 'books/my_arbitrary_template_name_list.html'  # Specify your own template name/location

        
- When you use generic view class, it will auto look for template in ./catalog/templates/catalog/book_list.html     (./application_name/templates/application_name/the_model_name_list.html )

- You can add attributes to change the default behaviour

- Overriding methods in class-based views

        #You can overriding get_queryset to change the list of records returned
        class BookListView(generic.ListView):
            model = Book

        def get_queryset(self):
            return Book.objects.filter(title__icontains='war')[:5] # Get 5 books containing the title war

        # You can also overriding get_context_data to pass additional context variables to template
        class BookListView(generic.ListView):
            model = Book

            def get_context_data(self, **kwargs):
                # Call the base implementation first to get a context
                context = super(BookListView, self).get_context_data(**kwargs)
                # Get the blog from id and add it to the context
                context['some_data'] = 'This is just some data'
                return context
        
        #First get the existing context from our superclass.
        #Then add your new context information.
        #Then return the new (updated) context.

3. [Regular Expression](https://docs.python.org/3/library/re.html)

4. Passing additional options in your URL maps    
This approach can be useful if you want to use the same view for multiple resources, and pass data to configure its behaviour in each case

        url(r'^/url/$', views.my_reused_view, {'my_template_name': 'some_path'}, name='aurl'),
        url(r'^/anotherurl/$', views.my_reused_view, {'my_template_name': 'another_path'}, name='anotherurl'),

## Step6 Sessions Framework

1. Enabling Session     
The configuration is set up in the INSTALLED_APPS and MIDDLEWARE sections of the project file (locallibrary/locallibrary/settings.py), as shown below:

        INSTALLED_APPS = [
            ...
            'django.contrib.sessions',
            ....

        MIDDLEWARE = [
            ...
            'django.contrib.sessions.middleware.SessionMiddleware',
            ....

2. Using session     
- You can access the session attribute in the view from the request parameter.     
- The session attribute is a dictionary-like object that you can read and write in your view.

        # Get a session value by its key (e.g. 'my_car'), raising a KeyError if the key is not present
        my_car = request.session['my_car']

        # Get a session value, setting a default if it is not present ('mini')
        my_car = request.session.get('my_car', 'mini')

        # Set a session value
        request.session['my_car'] = 'mini'

        # Delete a session value 
        del request.session['my_car']

3. Saving session data
- By default,if you're updating some data using its session key as shown in the previous section, then you don't need to worry about this! For example:

        # This is detected as an update to the session, so session data is saved.
        request.session['my_car'] = 'mini'

- If you updating some data with a more complex way, you should explicitly mark the session as having been modifield

        # Session object not directly modified, only data within the session. Session changes not saved!
        request.session['my_car']['wheels'] = 'alloy'

        # Set session as modified to force data updates/cookie to be saved.
        request.session.modified = True

        # You can change the behavior so the site will update the database/send cookie on every request by adding SESSION_SAVE_EVERY_REQUEST = True into your project settings (locallibrary/locallibrary/settings.py).