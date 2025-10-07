# Ex.05 Design a Website for Server Side Processing
## Date:7.10.2025

## AIM:
 To design a website to calculate the area of the rectangle


## FORMULA:
A=L*B
<br> A--> Area (in m )
<br> L --> Length (in m )
<br> B --> Breadth (in m² )

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create python programs for views and urls to perform server side processing.

### Step 5:
Create a HTML file to implement form based input and output.

### Step 6:
Publish the website in the given URL.

## PROGRAM :
~~~

math.html

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Area of a Rectangle</title>
<style>
  body {
    margin: 0;
    background-color: #ab208b;
    font-family: Arial, sans-serif;
  }
  .container {
    width: 350px;
    background-color: #082c5e;
    color: #f2bace;
    border: 2px dashed #0a294e;
    padding: 20px;
    margin: 150px auto;
    box-sizing: border-box;
  }
  h1 {
    margin-top: 0;
    text-align: center;
    color: #f2bace;
    font-weight: bold;
  }
  label {
    display: block;
    color: #f2bace;
    margin-top: 15px;
    font-weight: bold;
  }
  input[type="number"], input[readonly] {
    width: 90%;
    padding: 6px 5px;
    margin-top: 5px;
    border-radius: 3px;
    border: 1px solid #ccc;
  }
  button {
    display: block;
    width: 100%;
    margin-top: 20px;
    padding: 6px 5px;
    font-size: 14px;
    background-color: #0d325f;
    color: #f2bace;
    border: none;
    border-radius: 3px;
    cursor: pointer;
  }
  button:hover {
    background-color: #0e50a6;
  }
  .unit {
    font-weight: normal;
    font-size: 0.9em;
    color: #f2bace;
    margin-left: 5px;
  }
</style>
</head>
<body>
  <div class="container">
    <h1>Area of a Rectangle</h1>
    <form id="areaForm" method="POST">
      {% csrf_token %}
      <label>Length <span class="unit">(in m)</span></label>
      <input type="number" id="length" name="length" value="{{ length }}" min="0" step="any" />
      
      <label>Breadth <span class="unit">(in m)</span></label>
      <input type="number" id="breadth" name="breadth" value="{{ breadth }}" min="0" step="any" />
      
      <button type="submit">Calculate</button>
      
      <label>Area <span class="unit">m²</span></label>
      <input type="number" id="area" name="area" value="{{ area|default:'0.00' }}" readonly />
    </form>
  </div>
</body>
</html>

views.py

from django.shortcuts import render

def rectangle_area(request):
    context={}
    context['area'] = None
    context['length'] = 0
    context['breadth'] = 0
    
    if request.method == 'POST':
        print("POST method is used")
        l= float(request.POST.get('length', 0))
        b= float(request.POST.get('breadth', 0))
        print('request=',request)
        print('Lengtht=',l)
        print('Breadth=',b)
        area=int(l) * (b)
        context['area'] = area
        context['length'] = l
        context['breadth'] = b
        print('area=',area)

    return render(request, 'mathapp/math.html', context)

    urls.py

    from django.contrib import admin
    from django.urls import path
    from mathapp import views
    urlpatterns = [
        path('admin/',admin.site.urls),
        path('rectangle_area/',views.rectangle_area,name="rectangle_area"),
        path('',views.rectangle_area,name="rectangle_area"),
]

~~~

## SERVER SIDE PROCESSING:


![alt text](<server side image.png>)



## HOMEPAGE:

![alt text](<homepage image.png>)


## RESULT:
The program for performing server side processing is completed successfully.
