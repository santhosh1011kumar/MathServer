# Ex.04 Design a Website for Server Side Processing
## Date:

## AIM:
To create a web page to calculate total bill amount with GST from price and GST percentage using server-side scripts.

## FORMULA:
Bill = P + (P * GST / 100)
<br> P --> Price (in Rupees)
<br> GST --> GST (in Percentage)
<br> Bill --> Total Bill Amount (in Rupees)

## DESIGN STEPS:

### Step 1:
Clone the repository from GitHub.

### Step 2:
Create Django Admin project.

### Step 3:
Create a New App under the Django Admin project.

### Step 4:
Create a HTML file to implement form based input and output.

### Step 5:
Create python programs for views and urls to perform server side processing.

### Step 6:
Receive input values from the form using request.POST.get().

### Step 7:
Calculate the total bill amount (including GST).

### Step 8:
Display the calculated result in the server console.

### Step 9:
Render the result to the HTML template.

### Step 10:
Publish the website in Localhost.

## PROGRAM:
## views.py:
from django.shortcuts import render

def gst_amt_calculator(request):
    gst_amt = None
    if request.method == 'POST':
        try:
            price = float(request.POST.get('price'))
            gst = float(request.POST.get('gst'))
           

            if price >= 0 and gst >= 0:
                gst_amt = price + ((price * gst) / 100)
            else:
                # Handle potential negative inputs error
                gst_amt = "Error: Inputs cannot be negative."
        except ValueError:
            # Handle potential non-numeric inputs error
            gst_amt = "Error: Invalid input. Please enter numeric values."

    # Pass the result to the template
    context = {
        'gst_amt': gst_amt
    }
    return render(request,'math.html', context)


## urls.py:
from django.contrib import admin
from django.urls import path, include
from mathapp import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', views.gst_amt_calculator, name='gst_amt'),
]


## math.html:

<!DOCTYPE html>
<html>
<head>
    <title>GST Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #4e73df, #1cc88a);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

         .container {
            background: white;
            padding: 40px;
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
            width: 350px;
            text-align: center;
        }

        h1 {
            margin-bottom: 25px;
            color: #333;
        }

        label {
            font-weight: bold;
            display: block;
            text-align: left;
            margin-bottom: 5px;
        }

        input {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 6px;
            border: 1px solid #ccc;
            font-size: 14px;
        }

        input:focus {
            outline: none;
            border-color: #4e73df;
            box-shadow: 0 0 5px rgba(78, 115, 223, 0.5);
        }

        button {
            width: 100%;
            padding: 10px;
            background: #4e73df;
            color: white;
            border: none;
            border-radius: 6px;
            font-size: 16px;
            cursor: pointer;
            transition: 0.3s;
        }

        button:hover {
            background: #2e59d9;
        }

        .result {
            margin-top: 20px;
            padding: 15px;
            border-radius: 8px;
            background: #f8f9fc;
            font-size: 18px;
            font-weight: bold;
        }

        .error {
            color: red;
        }

        .success {
            color: #1cc88a;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>GST Calculator</h1>

    <form method="post">
        {% csrf_token %}
        <label for="price">Price :</label>
        <input type="text" id="price" name="price" required>

        <label for="gst">GST (R in %):</label>
        <input type="text" id="gst" name="gst" required>

        <button type="submit">Calculate</button>
    </form>

    {% if gst_amt is not None %}
        <div class="result">
            {% if "Error" in gst_amt|stringformat:"s" %}
                <p class="error">{{ gst_amt }}</p>
            {% else %}
                <p class="success">Total Price After GST: ₹ {{ gst_amt|stringformat:".2f" }}</p>
            {% endif %}
        </div>
    {% endif %}
</div>

</body>
</html>


## OUTPUT - SERVER SIDE:
![alt text](<Screenshot 2026-03-09 091429.png>)

## OUTPUT - WEBPAGE:
![alt text](<Screenshot 2026-03-09 090929.png>)

## RESULT:
The a web page to calculate total bill amount with GST from price and GST percentage using server-side scripts is created successfully.
