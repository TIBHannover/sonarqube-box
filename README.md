# SonarQube

Install an SonarQube instance via ansible. Test it locally with Vagrant and VirtualBox.

Documentation see also
* https://www.sonarqube.org/

**Note**: only for testing / evaluation purposes, because an inmemory-db is used. Ansible-Vars have to be changed for production - see https://galaxy.ansible.com/lrk/sonarqube

## Installation on local system for testing

Prerequisites
* [Git](https://git-scm.com/downloads)
* [Vagrant](https://www.vagrantup.com/downloads.html)
* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

Perform the following steps in the terminal (Linux / macOS) or in the GitBash (Windows).
```
git clone git@github.com:TIBHannover/sonarqube-box.git
cd sonarqube-box
vagrant up
```

When the installation is complete (a few minutes, depending on the download speed), the index can be opened in the browser

<http://192.168.98.122:9000/>

First time credentials: `admin` / `admin`

## Analysis of local project

* see https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/
* login into sonarqube and configure a project: Manually -> locally -> generate token
* you may use the sonarqube-docker-image to process the analysis

```
docker run -it -v ${PATH_TO_YOUR_REPO_TO_ANALYZE}:/usr/src -e SONAR_HOST_URL="http://192.168.98.122:9000" -e SONAR_LOGIN="${YOUR_TOKEN}" --rm sonarsource/sonar-scanner-cli:latest
```

