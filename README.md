[![Python application test with Github Actions](https://github.com/feteezuk/AWS_hello/actions/workflows/main.yml/badge.svg)](https://github.com/feteezuk/AWS_hello/actions/workflows/main.yml)

# Steps
1. In **Github**, Create repo called **"AWS_hello"**
2. Create **new SSH key** for **virtual environment** using command(in terminal):**ssh-keygen -t rsa**
3. Copy public key from terminal, then type ```cat public_key_url``` to get full path
4. In Github, Go to **Profile,then Settings, SSH Keys, Add New, Add Key and Title then submit, Created new ssh key!**
5. Go back to **AWS_hello repo** and hit enter and grab ssh code

## Go to AWS TERMINAL
1. In terminal, 
	1. **cd /home/ec2-user/environment** and press ENTER
  	2. **git clone git@github.com:feteezuk/AWS_hello.git** and press ENTER
  	3. **cd AWS_hello/**

## Build Out Scaffolding - 
#### Create following files: 
1. touch Makefile
2. touch hello.py
3. touch test_hello.py
4. touch requirements.txt

IN AWS ENVIRONMENT, 

# OPEN Makefile
**Add code :
```
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

test:
	python -m pytest -vv test_hello.py


lint:
	pylint --disable=R,C hello.py

all: install lint test

```

***SAVE FILE

# OPEN hello.py
**Add code :
   
```
   def toyou(x):
    return "hi %s" % x

def add(x):
    return x + 1


def subtract(x):
    return x - 1
```
    
***SAVE FILE
   
# OPEN requirements.txt
***Add code :  
   
```
   pytest
   pylint
```
***SAVE FILE

# OPEN test_hello.py
   **Add code :  
   
```
  from hello import toyou, add, subtract

def setup_function(function):
    print(" Running Setup: %s " % function.__name__)
    function.x = 10

def teardown_function(function):
    print(" Running Teardown:%s" % function.__name__)
    del function.x
    
#Run to see failed test
#def test_hello_add():
    #assert add(test_hello_add.x) == 12

def test_hello_subtract():
    assert subtract(test_hello_subtract.x) == 9
```   

### Create Virtual Environment
In terminal, type one line at a time 
```
1. python3 -m venv ~/.AWS_hello
2. source ~/.AWS_hello/bin/activate 
```
   
### Install All Dependencies, Run Lint, Then Run Test
1. ```make install``` This installs all the dependencies
2. ```make lint``` This double checks your code for errors / bugs
3. ```make test``` This tests your test file code against your original file (hello.py vs test_hello.py)

### PUSH TO GITHUB
1. ```git add * ``` Adds all files to staging area
2. ```git commit -m "initial commit"``` Commits all files
3. ```git push``` If you get an error message, this may be your first time commiting this file
  4. try ```git pull``` 
### ERROR MESSAGE AFTER git push
``` Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., git pull ...) before pushing again
```

## SET UP GITHUB ACTION
1. Go to Github repo **AWS_hello**, and click on Actions **TAB**
2. Click **Set up a workflow yourself**
3. Remove all the code within the **main.yaml** file
4. Add the following code below to main.yaml
5. Hit start commit, give title "initial config" and then hit "Commit New File"

```
name: Python application test with Github Actions

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.5
      uses: actions/setup-python@v1
      with:
        python-version: 3.5
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pylint
      run: |
        make lint
    - name: Test with pytest
      run: |
        make test
```

This code above says that everytime a push happens
1. run latest version of **ubunto**
2. run latest version of **python**
3. run **make install**
4. run **make lint**
5. run **make test**


### 

1. In Github, Go to **Actions**
2. Github will run your code in the .yml file 
3. Make sure the **python version** is correct. I received an error because python version 3.5 was written.
4. There should be a green light if everything is working correctly. 
5. If there is a red light, you can click to see exactl where the error is coming from.

### TO GET STATUS BADGE
1. In the **Actions** tab, click the 3 dots on the upper right 
2. select **create status badge**
3. Post this badge on top of the **Read Me** page


