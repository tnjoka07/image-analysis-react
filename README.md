# IAS-project
Image Analysis web application
Backend - FastApi
Frontend - React


# OS setting - Be sure to use Ubuntu as the base OS for your environment settings.
Be sure to use Ubuntu as the base OS for your environment settings.
If you use Windows OS or Mac as the base, pixel restrictions will affect Docker, preventing you from building and displaying data as intended.
## Environment Setup
### Requiremets
The IAS web application requires the following minimum/recommended hardware specifications to run;
1. Storage - You'll need about 200GB minimum sto setup the web application. The recommended storage space however is about 500GB. Ensure you've already allocated the specified space before proceeding.
2. GPU (nvidia) - Your local setup should have at minimum a GT 1030 to ensure your code input works well with the GPU. The recommended GPU that you'll have to upgrade to while you continue to work at life analytics is GTX 1050/ GTX 1050 TI.
3. Processor - Your setup should have at least i5 (3.8 GHz or more) or i7 (3.5 Ghz or more). Recommened processor is a later generation i5 or i7 with 4 GHz or more or comes with turbo boost. If you have AMD processor Ryzen 5 or 7 later generation recommended with speeds of 3.5 GHz or more.
4. RAM - Your memory should be at least 16GB. Anything less than this would mean you can't demonstrate properly your work during meetings as you'll be runnning the web application as well as other application such as zooom, qupath, imagej, napari which may consume alot of memory (Hence, your local setup might probably freeze - which is not acceptable!).

### Setup IAS platform on your local setup.
- Run the following command in the IAS-project folder to start all backend services
```bash
# Installation and setup command

$ docker compose -f docker-compose.development.yml up -d
```
#### Take Note: Very Important !!!
1. Use the command above as it is, DON'T CHANGE IT. 
2. If this is the first time running this command it will take some time while the docker images are downloaded.
3. If you don't have nvidia gpu, use `docker-compose.development.cpu.yml` instead of `docker-compose.development.yml`

For the front-end docker service setup completion (development), please input the following commands and restart it.
```bash
$ cd react
$ cp -a .dummy.env .env

# this will install all modules and could take some time (case: npm -v < 9.0.0)
$ npm install 

# (case: npm -v >= 9.0.0)
$ npm install --legacy-peer-deps
```

Once the react installation is done, you can go ahead and build the front-app image using the following command.

```
docker compose -f docker-compose.development.yml build front-app
```

Docker service for blender will require [microsopynodes.zip](https://extensions.blender.org/add-ons/microscopynodes/) added in the blender's app folder.

#### Downloading samples
Samples for testing/development can be downloaded from [https://idr.openmicroscopy.org/](https://idr.openmicroscopy.org/). Use the website to track down the ids and use an ftp client to download the respective samples... Once downloaded, you'll need imagej/fiji to merge the sample into their respective dimensions or how you see fit. 

FTP link
`ftp://ftp.ebi.ac.uk/pub/databases/IDR/`

#### GPU configuration with docker containers
If you have a GPU (nvidia) on your local setup, you can install the nvidia toolkit to configure docker and detect the GPU in the running docker containers

[Nvidia Toolkit Configuration Link](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#configuring-docker)

---
### Explanation about backend
The backend is configured as docker container.
1. mainApi is fastAPI framework backend to provider api to the frontend ( ias-project-react-mainapi)
2. Database docker container ( mongo )
3. Database Viewer for the backend database ( mongo-express )
    ```
    Basic Auth
    URL: http://localhost:8081/
    username: user
    password: #C2Y8YqvV
    ```
    Please change env_files/mongo-express.env if you don't want to enter user and password.
4. Others are image processing modules working as backend api that comes with different set of environment conditions/requirements that prevent them from being added to the mainApi backend container.

Because the backend is configured with docker system. The development should be docker dev container.

### Explanation about frontend
- The frontend is configured with react.js under the react/ folder
The gole is Viv viewer to display every images on frontend by using backend that customize image processing using ashlar python module.

- Detail Explanation about Frontend project structure and Data system.
 Main Page file is MainFrame.js 
 Descibe full page of the frontend and most skeleton was configured on this file , Should touch carefully and understand as fully.
 There are three parts called - left panel area, central panel area, right panel area
  1. Left Panel part + Right Panel Part
      Both parts exist in src/components/tabsLeft and src/components/tabsRight.
  2. Central Panel exists in src/components/avivator (uses [hms-dbmi/viv](https://hms-dbmi.github.io/viv/))
      * This is an important part in this project. 

*** This project structure is configured as perfectly and as well for image processing and [viv viewer](https://hms-dbmi.github.io/viv/).

### Links
- [http://localhost/](http://localhost/) - Frontend (react)
- [http://localhost:8000/docs](http://localhost:8000/docs) - Backend documentation (fastapi)
- [http://localhost:8081/](http://localhost:8081/) - Database (mongo-express)
- [http://localhost:4000/phpldapadmin/](http://localhost:4000/phpldapadmin/) - LDAP access (phpldapadmin)


### About GCP - Currently not used
Current(24.10.2022) use GCP for server and link subscription google.
https://console.cloud.google.com/home/dashboard?project=capable-alcove-265511

To be able to operate on the following sites.
  - Project Name : LifeAnalytics
  - Vm instance : Compute Engine / Vm Instances / lifeanalytics-vm
  - Debian version : 9.2
  - External IP : 34.72.210.99
  - account name(ssh key account) : iasgcp (ias-project-react repository)
  - Reference File : gitaction workflow command - ssh_ci.yml
  
  
### About Web Page - Active
The web page is deployed at [https://life-analytics.net/](https://life-analytics.net/) under a custom setup involving docker compose and there are future plans to migrate to kubernetes.

## License
Apache License 2.0

### Credentials
```
life-service
AnyDesk ID: 1402239427
AnyDesk PSW: IntegrateService@2024ias
Username: lifeana03
PSW: lifeana03

life-analytics
AnyDesk ID: 1637661836
AnyDesk PSW: IntegrateImaging"2022ias
Username: lifeana02
PSW: lifeana02

life-trainer
AnyDesk ID: 1734862151
AnyDesk PSW: IntegrateTraining@2024ias
Username: lifeana01
PSW: lifeana01

NAS SSH
Username: lifeana02
PWS: 3hA8fHG4

LDAP Credentials
Username: cn=admin,dc=life-analytics,dc=net
PSW: lifeanaldap02!
```
