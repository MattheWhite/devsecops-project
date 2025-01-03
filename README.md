# DevSecOps Project 

The project aims to learn the modern DevSecOps approach, tools and methodologies. **Using several tech stacks, the main direction is to test the code of an open-source application (PyGoat). Detecting, testing and fixing (intentional) vulnerabilities, obsolescence and other vulnerabilities where applicable, all using GitHub Actions CI/CD tool.**

## Learning through OWASP pygoat project
The purpose is to give both developers and testers a platform for learning how to test applications and how to code securely. PyGoat is written in python and used Django web framework as a platform. It has both traditional web application vulnerabilities (i.e. XSS, SQLi) as well.


### *Table of Contents*

  * [Installation](#installation)
     * [From Sources](#from-sources)
     * [Docker Container](#docker-container)
     * [Installation Video](#installation-video)
  * [Uninstallation](#uninstallation)
  * [Solutions](#solutions-coming-soon)

## Installation

### From Sources

To setup the project on your local machine:
<br>

First, Clone the repository using GitHub website or git in Terminal
```
  git clone https://github.com/adeyosemanputra/pygoat.git
  ### To Download a specific branch
  git clone -b <branch_name> https://github.com/adeyosemanputra/pygoat.git
```

#### Method 1

1. Install all app and python requirements using installer file - `bash installer.sh`
2. Apply the migrations `python3 manage.py migrate`.<br>
3. Finally, run the development server `python3 manage.py runserver`.<br>
4. The project will be available at <http://127.0.0.1:8000> 

#### Method 2

1. Install python3 requirements `pip install -r requirements.txt`.<br> 
2. Apply the migrations `python3 manage.py migrate`.<br>
3. Finally, run the development server `python3 manage.py runserver`.<br>
4. The project will be available at <http://127.0.0.1:8000> 

#### Method 3

1. Install all app and python requirements using `setup.py` file - `pip3 install .`
2. Apply the migrations `python3 manage.py migrate`.<br>
3. Finally, run the development server `python3 manage.py runserver`.<br>
4. The project will be available at <http://127.0.0.1:8000> 


### Docker Container
1. Install [Docker](https://www.docker.com)
2. Run `docker pull pygoat/pygoat` or `docker pull pygoat/pygoat:latest`
3. Run `docker run --rm -p 8000:8000 pygoat/pygoat:latest`
4. Browse to <http://127.0.0.1:8000> 
5. Remove existing image using `docker image rm pygoat/pygoat` and pull again incase of any error


### From Docker-Compose 
1. Install [Docker](https://www.docker.com)
2. Run `docker-compose up` or `docker-compose up -d`

#### Build Docker Image and Run
1. Clone the repository  &ensp; `git clone https://github.com/adeyosemanputra/pygoat.git` 
2. Build the docker image from Dockerfile using &ensp; `docker build -f Dockerfile -t pygoat .`
3. Run the docker image &ensp;`docker run --rm -p 8000:8000 pygoat:latest`
4. Browse to <http://127.0.0.1:8000> or <http://0.0.0.0:8000> 


### Installation video 

1. From Source using `installer.sh`
 - [Installing PyGoat from Source](https://www.youtube.com/watch?v=7bYBJXG3FRQ)
2. Without using `installer.sh`
 - [![](http://img.youtube.com/vi/rfzQiMeiwso/0.jpg)](http://www.youtube.com/watch?v=rfzQiMeiwso "Installation Pygoat")


### Uninstallation

#### On Debian/Ubuntu Based Systems
- On Debian/Ubuntu based systems, you can use the `uninstaller.sh` script to uninstall `pygoat` along with all it's dependencies.
- To uninstall `pygoat`, simply run:
```bash
$ bash ./uninstaller.sh
```

#### On Other Systems
- On other systems, you can use the `uninstaller.py` script to uninstall `pygoat` along with all it's dependencies
- To uninstall `pygoat`, simply run:
```bash
$ python3 uninstaller.py
```


### Solutions (coming soon)

[More about pygoat](https://owasp.org/www-project-pygoat/)

[Forked project](https://github.com/nanuchi/devsecops-crash-course-pygoat)

#### Bugs & fixes
There were some bugs in the project mainly with the versions and compatibilities, due to the fact that the project was prepared earlier. Solutions were to fix and rewrite the package versions and make them compatible in both cases.
  
  1. **bug** &rarr; Fix Dockerfile RUN command for psycopg2  dependency installations, Debian *dnsutils* package version correction, prev. deb10u9 now not compatible, latest: deb10u11
  --- 
  2. **bug** &rarr; Fix second job's (`image_scan`) incompatibility issue, use specific runner version (not *latest*, somehow on the latest ubuntu 24.04 fails the pipeline due to version problems)
  `Specifying exact versions ensures compatibility, especially in environments where different systems need to run the same setup consistently.` **`It also prevents accidental upgrades to newer versions that might introduce breaking changes or incompatibilities. Like exactly this case, previous ubuntu-latest was specified, probably at the time it was the 22.04 version the latest.`**
      - *runs_on: ubuntu-22.04*
      - *with:
          docker_version: '26.1.4'*
  
  More useful links:
  - [Choosing runner for a job](https://docs.github.com/en/actions/writing-workflows/choosing-where-your-workflow-runs/choosing-the-runner-for-a-job)
  - [Check 22.04 specific runner compatibilities](https://github.com/actions/runner-images/blob/main/images/ubuntu/Ubuntu2204-Readme.md)
  - [Issue with dnsutils](https://github.com/nanuchi/devsecops-crash-course-pygoat/issues/2)
  - [Debian dnsutils package](https://packages.debian.org/buster/dnsutils) &rarr; after a quick search on Debian dnsutils you can find out which is the latest version of the package to use it in the job


## Used stacks
* GitHub Actions
* Python
* Bandit
  - SAST (Static Application Security Testing) scanning tool for `Python`, find common security issues in Python code
  - [*Configuration manual for Bandit*](https://bandit.readthedocs.io/en/latest/man/bandit.html)
  - `Defect Dojo` recommended vulnerability management tool for further scanning features, it can comsumption the output report file about the findings and work with it.
    Display all the content of the generated report file, merge findings, remember false positives and distill duplicates, and so on.
* Docker Scout
  - Container Image Scanning tool
  - We produce Docker Images as application artifacts which has to be scanned and tested before produciton. Great tool for image scanning is Docker Scout which is a **Docker native tool**.
