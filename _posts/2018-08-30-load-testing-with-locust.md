---
layout: post
title: "Load testing with Locust"
date: 2018-04-13
excerpt: "Getting started with Locust and the basic APIs"
tags: [hackathon]
feature: https://toilatester.files.wordpress.com/2018/08/charts.png
comments: true
---

# Load testing with Locust.io

## Preface

In this article, I’d like to introduce Locust – a load testing tool that is written in Python which has many interesting features that I think might be helpful for the Performance Testers whose are considering a new method / solution for the Load testing framework.

In this post, I try to cover the basics of Locust and will update more detail tutorials in other related future articles.

*Note:* The source code of the demos in this blog can be found in [this repository](https://github.com/locmai/locust-demo).

## Introduction

The original idea for Locust was from [Carl Byström](https://github.com/cgbystrom) who made the first proof of concept in June 2010. [Jonatan Heyman](https://github.com/heyman) picked up Locust in January 2011, implemented the current concept of Locust classes and made it work distributed across multiple machines. Then, ESN Social Software has adopted Locust as an in-house Open Source project.

The main idea is about making a load testing tool which helps to write test scenarios in plain code and can run distributed load tests easily. Here we have Locust.

## Getting started with Locust

### Installation

Before installing Locust, ensure that you have [Python 3.6+](https://www.python.org/) running on your computer.

#### Installing with pip (Recommended for Stable version)

The simplest way to install Locust is using pip:

{% highlight bash %}
pip install locustio
{% endhighlight %}

After the installation, you can check the version of Locust by using the command:

{% highlight bash %}
locust --version
[2018-08-26 17:03:14,986] ./INFO/stdout: Locust 0.8.1
{% endhighlight %}

#### Installing the latest version from GitHub (Latest dev version)

The stable version at the time this post was written was 0.8.1. Apparently the version missed a few newest features. If you want the latest version from the developers, you could download from the GitHub Repository and install from there:


{% highlight bash %}
git clone https://github.com/locustio/locust.git
cd locust
python setup.py install
{% endhighlight %}

#### Installing with Docker

For now, there is no official Docker image for Locust, but you can pull it from the [following source](https://quay.io/repository/honestbee/locust?tag=latest&tab=tags) or build the image yourself:

{% highlight bash %}
docker pull quay.io/honestbee/locust
{% endhighlight %}

### Writing your first Locustfile

OK. We have finished installing Locust library on our machines. Let’s jump right into it and start writing our test script.

But wait, we need to prepare some simple API endpoints first. I will use Flask for the quick setup:

{% highlight bash %}
pip install flask
{% endhighlight %}

Create a main.py file (or whatever.py file):

{% highlight python %}
# main.py
from flask import Flask, request, jsonify, app

import time
import random

app = Flask(__name__)

@app.route('/api', methods=['GET', 'POST'])
def index():
    if request.method =='GET':
        return jsonify(method=request.method)
    return jsonify(method=request.method,payload=request.json)

if __name__ == '__main__':
    app.run(host='0.0.0.0')
{% endhighlight %}

The above code contains an “/api” route which will return the requests’ methods under JSON format and it accepts GET or POST requests only. Also if it was a POST request with the JSON body, we will also return the payload, too.

Start running the API server, it will be exposed on port 5000:

{% highlight bash %}
python main.py
* Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
{% endhighlight %}

Okay, now we have our “system under test”. We can start some testing activities.

Locust requires at least one locustfile – just a normal Python file (.py) – which contains one or more Locust classes to run the test.

A simple locustfile would look like this:

{% highlight python %}
# locustfile.py
from locust import Locust, TaskSet, task

class UserTaskSet(TaskSet):              #3
    @task                                #4
    def my_task(self):
        print("executing my_task")

class User(Locust):                      #1
    task_set = UserTaskSet               #2 
    min_wait = 5000
    max_wait = 15000
{% endhighlight %}

At #1, we have the User class inherited from the Locust class. A locust class represents a virtual user that will perform the tasks written in the task sets managed by the Locust.

In the above example, we have defined User and we set the task_set attribute to the UserTaskSet class which inherited from TaskSet class. (#2, #3). And to define a task to be performed in the TaskSet, we add the @task decorator before the method (#4)

You can start running the script by using the locust command, Locust will find the file with the name “locustfile”. If you named it something else, you can add the -f flag with the name you set:

{% highlight bash %}
locust -f whatever.py
{% endhighlight %}

You can access to the Web UI at [http://localhost:8089/](http://localhost:8089/) .

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/webui.png">
	<figcaption>Locust's Web UI.</figcaption>
</figure>

You can set a number of users and the hatch rate (how many users will be spawned each second). Then start swarming.

For now, our script only makes the users printing out “executing my_task” string. Let’s define some real tasks for our virtual users.

To simulate some HTTP requests, we need our Locust to have some specific options and methods . The HttpLocust is written for this purpose. It is an implementation of the Locust class that will create an HTTP client attribute on instantiation which supports for managing HTTP requests / responses.

Let’s modify our script a little:

{% highlight python %}
# locustfile.py
from locust import HttpLocust, TaskSet, task 

class UserTaskSet(TaskSet):
    @task
    def get_index_task(self): 
        self.client.get("/api")    #3 

class User(HttpLocust):            #1 
    task_set = UserTaskSet 
    min_wait = 5000 
    max_wait = 15000
    host = "http://localhost:5000" #2 
{% endhighlight %}

#1 The User class before now inherited from HttpLocust class.

#2 Define the target host (which is our API server from before) with the host attribute in HttpLocust class.

#3  The “self” in the task methods is the instance of the HttpLocust class, which we can call the client attribute from it and use the method ‘get’ to the “/api” endpoint.

Now, add a new task which send a POST request to the server:

{% highlight python %}
# locustfile.py
from locust import HttpLocust, TaskSet, task 

class UserTaskSet(TaskSet):
    @task
    def get_index_task(self): 
        self.client.get("/api", name="GET /api")

    @task
    def post_index_task(self):        # New task here
        payload = {'username': 'locmai'}
        self.client.post("/api", data=payload, name="POST /api")

class User(HttpLocust):
    task_set = UserTaskSet 
    min_wait = 5000 
    max_wait = 15000
    host = "http://localhost:5000"
{% endhighlight %}

As adding the new task, we can set a name for the each request as the parameters.

Start running our script:

{% highlight bash %}
locust -f locustfile.py
{% endhighlight %}

Open the browser and navigate to the [http://localhost:8089/](http://localhost:8089/) , enter the number of virtual users and the hatch rate, then click Start Swarming:

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/starttesting.png">
	<figcaption>Start testing with Locust</figcaption>
</figure>

That’s it! Now we can go deeper into the APIs that Locust provide and we can write more flexible script.

### Web UI

Locust provides a Web UI that shows relevant test details and control the test runs. You can also customize it and add a few extra features yourself if you wanted to (I might have another post on how to do it and provide some use cases later on).

On the top navigation bar, you can see the details about the Target Host, users’ status, number of users hatched and update a new desired number, RPS, Failures rate. Stop and reset statistic details button.

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/starttesting.png">
	<figcaption>Simple Web UI</figcaption>
</figure>

In the main section, we have Statistics tab which shows some basic information related to our test run like type of the request, name, number of request executed successfully and unsuccessfully, the average, min, max response times, etc.

In the Charts tab, we have just a few but enough .live charts:

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/charts.png">
	<figcaption>Live charts</figcaption>
</figure>

The failures and the Exceptions tabs show what requests failed and the errors thrown during the test runs.

And we can also download all the test details with CSV format in the Download Data tab

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/download.png">
	<figcaption>Download Data</figcaption>
</figure>

Locust also exposes some endpoints for getting the metrics. I will mention in another blog post for more details and more specific.

### Other Locust’s stuffs

#### Multi-Locust script

We can define different Locust classes in the same locust file. For example (multilocust.py):

{% highlight python %}
from locust import HttpLocust, TaskSet, task
from locusttasks.commontasks import NormalUserTasks, AdminUserTasks


class NormalUser(HttpLocust):
    min_wait = 1 * 1000
    max_wait = 2 * 1000
    task_set = NormalUserTasks
    weight = 1


class AdminUser(HttpLocust):
    min_wait = 1 * 1000
    max_wait = 2 * 1000
    task_set = AdminUserTasks
    weight = 2
{% endhighlight %}

As in the above example, we have two different Locust classes: Normal User represents the normal user that has a different TaskSet from the Admin User class. The file could run by the following commands:

{% highlight bash %}
locust -f multilocust.py # Run test with all Locust classes
locust -f multilocust.py AdminUser # Run test with only AdminUser
{% endhighlight %}

The users distribution will be based on the weight of the HttpLocust classes, if not set, the default weight will be 1. As in the example, the AdminUser has the weight of 2, NormalUser only has 1, if we set the number of users to 90, there will be 60 Admin users and 30 Normal users.

#### Min wait / Max wait

The wait time before executing tasks will be randomized in the range of min_wait and max_wait attributes. These attributes can be set in the HttpLocust class or the TaskSet class.

#### Defining @task methods

There are two ways to define a task in a TaskSet class.

The first way is to use the @task decorator as shown in the previous examples.

The second way is to declare a list called tasks in the TaskSet class and adding the methods into the list:

{% highlight python %}
def get_index(self):
    self.client.get('/api', name="GET /api")

def post_index(self):
    payload = {"username": "admin", "password": "secret"}
    self.client.post('/api', data=payload, name="POST /api")


class UserTasks(TaskSet):
    tasks = [get_index, post_index]

    @task
    def page404(self):
        self.client.get('/page_not_found')
{% endhighlight %}

We can also set the task’s weight (just like the weight of Locust class – but for tasks) by adding the parameters:

{% highlight python %}
class WebsiteUserTasks(TaskSet):
    @task(3)
    def get_index(self):
        self.client.get("/api", name="GET /api")

    @task(1)
    def post_index(self):
            payload = {'username': 'locmai', 'password': 'locmai@kms'}
            self.client.post("/api",data=payload, name="POST /api")
{% endhighlight %}

In the above example, we have task get_index with the weight is 3 and the post_index’s weight is 1. So that the task get_index will likely be executed more than 3 times the number of times the task post_index be executed.

The tasks will be performed in a random order. To make a sequence order for the requests, you can add the requests into one tasks with the order you want. Or you can use the TaskSequence class which will be introduced in version 0.9.0 ( You can try it out by installing the latest version)

#### Using TaskSequence with @seq_task

The TaskSequence is similar to the TaskSet class but it requires for the order of the tasks by adding the @seq_task(order_param) decorator before the methods:

{% highlight python %}
class NormalUser(TaskSequence):
    @seq_task(1)
    def login_first(self):
        pass

    @seq_task(2)
    @task(25) # You can also set the weight in order to execute the task for `weight` times one after another.
    def then_read_thread(self):
        pass

    @seq_task(3)
    def then_logout(self):
        pass
{% endhighlight %}

In the example, the tasks will be executed by the order: login_first -> then_read_thread -> then _logout

#### Setup, teardown, on_start, on_stop

We can manage the test cycle with the default methods:

from locust import HttpLocust, TaskSet, task

{% highlight python %}
class WebSiteUserTasks(TaskSet):
    def setup(self):
        print("Setup of TaskSet")

    def on_start(self):
        print("Locust hatched")

    @task(3)
    def get_index(self):
        self.client.get("/api", name="GET /api")
    
    def on_stop(self):
        print("Locust stopped")

    def teardown(self):
            print("Teardown of TaskSet")

class WebsiteUser(HttpLocust):
    host = "http://localhost:5000"
    min_wait = 2 * 1000
    max_wait = 5 * 1000
    task_set = WebSiteUserTasks

    def setup(self):
        print("Setup of Locust")

    def teardown(self):
        print("Teardown of Locust")
{% endhighlight %}

* Setup method in Locust class: Will be executed once before the test started.
* Teardown method in Locust class: Will be excuted once after test stopped.
* Setup method in TaskSet class: Will be executed once (and differ from the one in Locust class) before the test started.
* Teardown method in TaskSet class: Will be excuted once (and differ from the one in Locust class) after the test stopped.
* on_start in TaskSet: Will be executed for each locust instance hatched.
* on_stop in TaskSet: Will be executed for each locust instance after they died / stopped.

#### Handling HTTP requests

As mentioned, HttpLocust class will create a client attribute which actually is an instance of the HttpSession from the default request library of Python. You can read more about the API in the Official doc [here](http://docs.python-requests.org/en/master/).

#### Other APIs

For more detail information on how to implement new event hooks, responses handling, please refer to the [official Locust docs](https://docs.locust.io/en/stable/api.html).  I will have a detail blog post on how to customize the APIs soon.

### Running Locust distributed

We have go through a simple list of the APIs and how to implement basic Locust scripts. Now we are going to setup the distribution for our load tests.

You can enable distribution mode by using the –master and –slave flags.

First, start the Master locust which will be responsible for controlling the slave instances. You  will need a dummy locustfile for starting the master, this file could be use for customizing the Web UI if needed.

{% highlight bash %}
locust -f dummy.py --master
{% endhighlight %}

Now start the Locust slave and connect it to the master instance, you will have to define the locustfile for running the test here:

{% highlight bash %}
locust -f locustfile_slave.py --slave --master-host=<IP-of-the-host>
{% endhighlight %}

Manually adding the Locust slaves. You can access the Web UI and see how many slaves have been added to the cluster. And simply start running test on the Web UI as usual.

As you can see, the setup for running Locust in distributed mode is pretty simple. We can even leverage some Cluster systems like Kubernetes or Docker Swarm for quickly scale up the slaves, I will have a details blog post on how to setup a distributed system on Kubernetes cluster with all the configurations.

For example, you can scale up the Locust cluster with Helm and Kubernetes and easily mange them all:

<figure>
	<img src="https://toilatester.files.wordpress.com/2018/08/locust.gif">
	<figcaption>Scaling with Kubernetes Cluster</figcaption>
</figure>

## In Summary

Overall, Locust was created to solve some specific issues of current existing performance tools, and it did a great job. Using this framework and some Python experience you can write performance scripts pretty fast, store them within your Python project, spend minimum time on maintenance without additional GUI applications and simulate thousands of test users even on a very slow machine. The framework is also small and very extendable which is the great feature for us to explore more about this tool.

And that’s it for now. See you soon in the future Locust articles.