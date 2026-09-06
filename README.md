# Project : CRUD Application Development using Bootstrap & Django
# Date : 06-09-26
# AIM

To develop a Django-based CRUD web application using Bootstrap to perform Create, Read, Update, and Delete operations on student records.

# ALGORITHM

1. Create a Django project and application.
2. Define the `Student` model with required fields such as Name and Email.
3. Configure the SQLite database and run migrations.
4. Configure URL routing for Home, Add, Update, and Delete operations.
5. Create the Home view to retrieve and display student records.
6. Create the Add view to insert new student records into the database.
7. Create the Update view to modify existing student records.
8. Create the Delete view to remove student records from the database.
9. Design the web pages using Bootstrap with forms, tables, and responsive buttons.
10. Run the Django server and test all CRUD operations through the web browser.

# PROGRAM

## form.html
```


<!DOCTYPE html>
<html>
<head>
    <title>Student Management Portal</title>

    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css"
          rel="stylesheet">
</head>

<body class="bg-light">

<div class="container my-5">
    <div class="text-center mb-5">
        <h1 class="fw-bold text-primary">Student Management Portal</h1>
        <p class="text-secondary">Manage Student Records Easily</p>
    </div>


    <div class="row mb-4">
        <div class="col-lg-4 mb-4">

            <div class="card shadow h-100">

                <div class="card-header bg-primary text-white">
                    <h5 class="mb-0">Register New Student</h5>
                </div>

                <div class="card-body">

                    <form action="/create/" method="POST">

                        {% csrf_token %}

                        <div class="mb-3">
                            <label class="form-label fw-bold">
                                Student Full Name
                            </label>

                            <input type="text"
                                   name="name"
                                   class="form-control"
                                   placeholder="Enter student name"
                                   required>
                        </div>


                        <div class="mb-3">
                            <label class="form-label fw-bold">
                                Email Address
                            </label>

                            <input type="email"
                                   name="email"
                                   class="form-control"
                                   placeholder="Enter email"
                                   required>
                        </div>


                        <div class="d-grid">
                            <button type="submit"
                                    class="btn btn-primary">
                                Add Student
                            </button>
                        </div>

                    </form>

                </div>
            </div>
        </div>
        <div class="col-lg-8 mb-4">

            <div class="card shadow h-100">

                <div class="card-header bg-dark text-white
                            d-flex justify-content-between align-items-center">

                    <h5 class="mb-0">Registered Students</h5>

                    <a href="{% url 'home' %}"
                       class="btn btn-sm btn-outline-light">
                        Refresh
                    </a>

                </div>


                <div class="card-body">

                    <div class="table-responsive">

                        <table class="table table-hover align-middle">

                            <thead class="table-dark">

                                <tr>
                                    <th>ID</th>
                                    <th>Name</th>
                                    <th>Email</th>
                                </tr>

                            </thead>


                            <tbody>

                                {% for i in result %}

                                <tr>

                                    <td>
                                        <span class="badge bg-primary">
                                            {{ i.Idno }}
                                        </span>
                                    </td>

                                    <td>{{ i.Name }}</td>

                                    <td>{{ i.Email }}</td>

                                </tr>

                                {% empty %}

                                <tr>
                                    <td colspan="3"
                                        class="text-center text-muted">
                                        No student records found.
                                    </td>
                                </tr>

                                {% endfor %}

                            </tbody>

                        </table>

                    </div>

                </div>
            </div>
        </div>

    </div>
    <div class="row">

        <div class="col-lg-6 mb-4">

            <div class="card shadow h-100">

                <div class="card-header bg-info text-white">
                    <h5 class="mb-0">Update Student</h5>
                </div>


                <div class="card-body">

                    <form action="{% url 'up' %}" method="POST">

                        {% csrf_token %}


                        <div class="mb-3">

                            <label class="form-label fw-bold">
                                Student ID
                            </label>

                            <input type="number"
                                   name="id"
                                   class="form-control"
                                   placeholder="Enter student ID"
                                   required>

                        </div>


                        <div class="mb-3">

                            <label class="form-label fw-bold">
                                New Name
                            </label>

                            <input type="text"
                                   name="name"
                                   class="form-control"
                                   placeholder="Enter new name"
                                   required>

                        </div>


                        <div class="mb-3">

                            <label class="form-label fw-bold">
                                New Email
                            </label>

                            <input type="email"
                                   name="email"
                                   class="form-control"
                                   placeholder="Enter new email"
                                   required>

                        </div>


                        <div class="d-grid">

                            <button type="submit"
                                    class="btn btn-info text-white">
                                Update Student
                            </button>

                        </div>

                    </form>

                </div>
            </div>
        </div>
        <div class="col-lg-6 mb-4">

            <div class="card shadow h-100">

                <div class="card-header bg-danger text-white">
                    <h5 class="mb-0">Delete Student</h5>
                </div>


                <div class="card-body">

                    <form action="{% url 'del' %}" method="POST">

                        {% csrf_token %}


                        <div class="mb-3">

                            <label class="form-label fw-bold">
                                Student ID
                            </label>

                            <input type="number"
                                   name="id"
                                   class="form-control"
                                   placeholder="Enter student ID"
                                   required>

                        </div>


                        <div class="d-grid mt-4">

                            <button type="submit"
                                    class="btn btn-danger"
                                    onclick="return confirm(
                                    'Are you sure you want to delete this student?'
                                    );">

                                Delete Student

                            </button>

                        </div>

                    </form>

                </div>
            </div>
        </div>

    </div>

    <div class="text-center mt-4 mb-3">

        <p class="text-secondary">
            Student Management Portal
        </p>

    </div>

</div>


<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js">
</script>

</body>
</html>


```
## models.py
```
from django.db import models
from django.contrib import admin

class Student(models.Model):
    Idno = models.AutoField(primary_key=True)
    Name = models.CharField(max_length=100)
    Email = models.EmailField(unique=True)

class StudentAdmin(admin.ModelAdmin):
    list_display = ['Idno','Name','Email']
```
## views.py
```
from django.shortcuts import render, redirect
from .models import Student


def home(request):
    result = Student.objects.all()
    return render(request, 'form.html', {'result': result})


def create(request):
    if request.method == "POST":
        name = request.POST.get("name")
        email = request.POST.get("email")

        Student.objects.create(
            Name=name,
            Email=email
        )

    return redirect("home")


def update(request):
    if request.method == "POST":
        idd = request.POST.get("id")

        student = Student.objects.get(Idno=idd)

        student.Name = request.POST.get("name")
        student.Email = request.POST.get("email")

        student.save()

    return redirect("home")


def delete(request):
    if request.method == "POST":
        idd = request.POST.get("id")

        Student.objects.get(Idno=idd).delete()

    return redirect("home")
```
## urls.py
```
from django.contrib import admin
from django.urls import path
from app import views

urlpatterns = [
    path('admin/', admin.site.urls),

    path('', views.home, name='home'),
    path('create/', views.create, name='crea'),
    path('update/', views.update, name='up'),
    path('delete/', views.delete, name='del'),
]

```
# OUTPUT
![alt text](<Screenshot 2026-09-06 144916.png>)

## ADD
![alt text](<Screenshot 2026-09-06 144937.png>)

## UPDATE
![alt text](<Screenshot 2026-09-06 145029.png>)
![alt text](<Screenshot 2026-09-06 145038.png>)

## DELETE
![alt text](<Screenshot 2026-09-06 145053.png>)
![alt text](<Screenshot 2026-09-06 145108.png>)

# RESULT

A Django-based CRUD web application was successfully developed using Bootstrap to perform Create, Read, Update, and Delete operations on student records with SQLite as the backend database.
