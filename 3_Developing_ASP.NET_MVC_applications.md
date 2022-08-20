[Back to Syllabus](/README.md#course-syllabus)

## Learning Objectives
- Deploy ASP.NET MVC applications to Compute Engine
<br>

## Developing ASP.NET MVC Applications
ASP.NET gives web application developers access to
the dotnet framework. You can build applications on ASP.NET in the Google Cloud. In this module,
we'll show you how. In this module,
we'll look at how to create a web application using Microsoft's ASP.NET
MVC framework or Google Cloud Platform
Compute Engine. In Module 2 of this class, we looked at how to provision our Microsoft Windows Server and Microsoft SQL
Server Infrastructure. We've got an Active
Directory domain controller, a web server running Microsoft Internet
Information Services, and a pair of
Microsoft SQL Server instances running in an
always on availability group. Now it's time to
build an application. We'll be coding a simple ASP.NET MVC application
using C-Sharp. If you're a developer working with Microsoft
technologies, you'll know that
this is a great way to build a web application. We'll use Microsoft
Visual Studio as our integrated
development environment. We'll publish our application to Internet Information
Services using Google Cloud tools
for Visual Studio. If you're not a developer, just be aware that a web
application delivers application functionality using
the standard web browser. The browser accesses the
application as a URL, and the server responds with dynamic outputs
generated from data. In our case, from data stored
in Microsoft SQL Server. ASP.NET MVC makes use of a widely used
application architecture called Model View Controller. This architecture is frequently used when writing
web applications. It allows for a clean separation of concerns between modeling, manipulating, and
displaying data. Here's the first participant of our MVC application, the model. In an MVC application, the model's responsibility is to represent the application
data and business rules. In this example, we've created a model class using
C-Sharp called Contact. We'll use this to build an
address book application. We can see that
the contact class defines a set of properties, and in our application, we'll use this class to
create contact objects. Each contact will
have its own name, email address, and
cell phone number. Of course, in a more
full-featured application, the contacts would have
many more characteristics, but then it wouldn't
fit on a single slide. In addition, our contact
has a numeric ID. We'll make use of
Microsoft Entity Framework to simplify integration
with Microsoft SQL Server. The ID will be used
to enable us to map each contact object to a
record in a database table. The next plan in
MVC is the view. The views responsibility is to present model data
to the user and also to display forms that allow users to enter data to be
collected by the application. We've written our view using a templating language
called Razor. A Razor file is easy to
understand if you know HTML. As the templates
are written with HTML marker and embedded code. Our example shows a fragment of a Razor file
with C-Sharp code. We'll have a.CSHTML extension as it consists of C-Sharp
code and HTML marker. You'll notice in our
example that this template makes use of the dt
and dd HTML elements, which are used with the
description list elements to represent terms
and descriptions. A web designer would style
these elements using Cascading Style Sheets to present our address
book contacts to users. As well as an HTML Skeleton, a Razor file includes embedded C-Sharp code in
the form of a template. There are lots of different
ways of doing this. In our example, we've made use of a helper that's used to take the properties
from model objects and embed the model properties into the HTML output that sent back from the
server to the client. The final member in an MVC
triad is the controller. The controller receives
the request from the user's browser and is responsible for coordinating the response back
to the browser. In ASP.NET MVC, controllers are classes
written in C-Sharp code. The class contains
a set of methods. Each one of these is
called an action method. There's a default convention
that's used to map URLs against the class name
and the action method. In our example, imagine that our application
was running on a server located at
http://mycorp.com. The contacts controller and details action method
would be used to handle a request from a browser
using that base URL, followed by slash contacts, the name of the controller, then slash details, the
name of the action method. This would then be
followed by a number that corresponds to the ID of one of our contact objects or one of our contact records
in the database table. In the body of the details
method in our control, we've written code using Microsoft Entity
Framework to get the right code from SQL Server and return it to
the contact object. The controller
passes this object to the corresponding view, which formats it and returns
it to the user's browser. This slide shows just how
little code is required to connect a model to a database using Microsoft
density framework. As a developer, all you
have to do is inherit from the DB context base
class and add a property using the generic DbSet
collection of your model class. Entity Framework will
automatically create a database with a compatible
scheme of your model class, if it doesn't already exist. Then show that your model
objects can be created, retrieved, updated, and
deleted in that database. I already mentioned that
Visual Studio offers a great developer experience for coding ASP.NET MVC applications. Simply use the web
project template and select the MVC option. You'll be able to automatically
integrate your users existing Windows logins to get a seamless login experience against your new enterprise
web application. One nice thing about
writing ASP.NET MVC applications
with Visual Studio is that the development
environment will scaffold nearly all of
the MVC code for us. All we have to do is to
code the model and supply a class that knows how to map this model to the database
with Entity Framework. Once you finish
writing your code, then you'll also find it's straightforward to publish
your application to Internet Information
Services using Visual Studio,
integrated Web Deploy. Google have made it even easier to deploy
to Compute Engine virtual machines
for Visual Studio using Google Cloud tools.
<br>

## Hands-on Lab: Create an ASP.NET MVC Web Application
- Launch the Qwiklabs tool for open the Demo
    - Confirm the lab environment has been setup correctly
    - Install Microsoft Visual Studio 2015 Community Edition
    - Create an ASP.NET MVC application
    - Integrate Data Access with Entity Framework
    - Re-publish the ASP.NET application
<br>

[Go to Next Module](./4_Configuring_Resilient_Workloads.md)