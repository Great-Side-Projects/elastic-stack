<a name="readme-top"></a>


[![MIT License][license-shield]][license-url]
[![LinkedIn][linkedin-shield]][linkedin-url]


<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://www.elastic.co/es/elastic-stack">
    <img src="https://static-www.elastic.co/v3/assets/bltefdd0b53724fa2ce/blt0090c6239e64faf8/62aa0980c949fd5059e8aebc/logo-stack-32-color.svg" alt="Logo" width="250" height="">
  </a>

  <h3 align="center">Elastic stack</h3>

  <p align="center">
    Elastic stack is a set of tools for ingesting, storing, searching, and visualizing data. It is a powerful tool for analyzing data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more. It is a powerful tool for analyzing data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more.
    <br />
    <a href="https://www.elastic.co/docs"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="http://20.64.115.37:5601/login?next=%2F">View Demo</a>
    ·
    <a href="https://github.com/Great-Side-Projects/elastic-stack/issues">Report Bug</a>
    ·
    <a href="https://github.com/Great-Side-Projects/elastic-stack/issues/new">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
        <li><a href="#Architecture-design">Architecture design</a></li>
        <li><a href="#Architecture-diagram">Architecture diagram</a></li>
     </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project
Kibana login

[![Product Name Screen Shot][product-screenshot-UI]](http://20.64.115.37:5601)
[![Product Name Screen Shot2][product-screenshot-UI2]](http://20.64.115.37:5601)
[![Product Name Screen Shot3][product-screenshot-UI3]](http://20.64.115.37:5601)

I am using elastic stack to analyze the logs of data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more. with elastic stack, you can ingest, store, search, and visualize data.
- logstash is a tool for collecting, parsing, and storing logs for 
 future use. It is a powerful tool for analyzing data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more.
- Elasticsearch is a powerful tool for analyzing data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more.
- Kibana is a powerful tool for analyzing data in real-time. It is used for log and data analytics, full-text search, application monitoring, and more.


<p align="right">(<a href="#readme-top">back to top</a>)</p>


### Built With

This project is built with the following technologies:


* [![Docker][DockerImage]](https://www.docker.com/)
* [![VM][AzureVM]](https://azure.microsoft.com/es-es/services/virtual-machines/)
* [![Telebit Cloud](https://img.shields.io/badge/Telebit%20Cloud-005571?style=for-the-badge&logo=telebit&logoColor=white)](https://telebit.cloud/)

### Architecture design

The architecture design is based in how to deploy Elastic stack in a VM Azure with CI/CD in GitHub Actions.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Architecture diagram
[![Architecture diagram][architecture-diagram]](http://20.64.115.37:5601)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- GETTING STARTED -->
## Getting Started

Here you can find the steps to run the project in your local environment to explore the elastic stack proyect.

### Prerequisites

This is an example of how to list things you need to use the software and how to install them.

* Docker
* Docker-compose
* if you are in a VM, you need to open the port 5601 a public access to kibana.
* Telebit Cloud for the public access to the kibana. 

### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/Great-Side-Projects/elastic-stack.git
   ```
2. Go to the root folder of the project
   ```sh
   cd elastic-stack
   ``` 
3. find a .env file and set the environment variables for the elastic stack. 

- `[!IMPORTANT]` mandatory variables for the elastic stack are the following:
  - `ELASTIC_USERNAME`=userelastic
  - `ELASTIC_PASSWORD`=pass
  - `ELASTICSEARCH_SERVICEACCOUNTTOKEN`=token (next step) 
  - Other variables are optional, they are used for the logstash to connect to the mysql and kafka.   
   
   ```properties
    MYSQL_USERNAME=user #user for the mysql to connect logstash to mysql (pipeline/mysql-to-elasticsearch.conf)
    MYSQL_PASSWORD=pass #password for the mysql to connect logstash to mysql (pipeline/mysql-to-elasticsearch.conf)
    ELASTIC_USERNAME=elastic #user for the elastic search, default user is "elastic"
    ELASTIC_PASSWORD=pass #password for the elastic search.
    KAFKA_USERNAME=userkafka #user for the kafka to logstash connection SASL authentication (pipeline/kafka-to-elasticsearch.conf)
    KAFKA_PASSWORD=pass #password for the kafka to logstash connection SASL authentication (pipeline/kafka-to-elasticsearch.conf)
    ELASTICSEARCH_SERVICEACCOUNTTOKEN=token #token for the elastic search service account to connect to the kibana
    MYSQL_HOST=hostmysql
   ```
  How to get the `ELASTICSEARCH_SERVICEACCOUNTTOKEN`?
  - first of all, **elasticsearch services** has to be up.

   ```sh
    #user and password for the elastic user in the .env file.
    curl -X POST -u elastic:pass "localhost:9200/_security/service/elastic/kibana/credential/token/token1?pretty"
    #response
    {
    "created" : true,
    "token" : {
    "name" : "token1",
    "value" : "AAEAAWVsYXN0aWMva2liYW5hL3Rva2VuMTpGb2VCWFdHc1FobVF4ZjBUT2J4a1ZR"
      }
    }
    #set the "value" in the .env file 
    #Ej:
    ELASTICSEARCH_SERVICEACCOUNTTOKEN=AAEAAWVsYXN0aWMva2liYW5hL3Rva2VuMTpGb2VCWFdHc1FobVF4ZjBUT2J4a1ZR
    ```

4. Create the docker-compose with the following command
 
   ```sh
    #if don't need logstash, you can comment the services in the elk-compose.yaml file. 

    docker compose -f elk-compose.yaml up
    ctrl + c to stop the docker-compose
   ```
5. Open your browser and go to `http://localhost:5601/` to see the kibana UI.
6. Login with the user and password that you have configured in the .env file. explore de UI and elasticsearch from console. 
    ```properties
     ELASTIC_USERNAME: elastic #user for the elastic search, default user is "elastic"
     ELASTIC_PASSWORD: pass #password for the elastic search.
    ```
7. if you need to expose in https with a public domain, you can use Telebit Cloud. 
   - https://telebit.cloud/
    ```sh
    #install telebit
    export TELEBIT_USERSPACE=no #install as a system service (launchd, systemd only)
    curl https://get.telebit.io | bash
    # register in telebit
    # email is needed to register in telebit
    
    ...
    #activate the telebit service --just in case you have installed as a system service
    ~/telebit activate --system-launcher
    #run telebit to expose the port 5601
    ~/telebit http 5601
    
    #or run telebit in subdomain
    telebit http 5601 {subdomain}
    ej: telebit http 5601 kibana

    # telebit status
    ~/telebit status

    #get the public domain ej: 
    https://kibana.wise-moth-21.telebit.io/
    ```
8. **optional:** if you have problem with reboot the VM and the telebit service is not running, you can to create and enable the Telebit service with systemd
    
    Create a service file in `/etc/systemd/system/telebit.service` with the following content:
    ```sh
    # create the service file
    sudo nano /etc/systemd/system/telebit.service
    ```
    copy and paste the following content in the file:
    ```ini
    [Unit]
    Description=Telebit Daemon
    After=network.target

    [Service]
    ExecStart=/yourpath/Applications/telebit/bin/telebit daemon --config /home/azureuser/.config/telebit/telebit.yml
    Restart=always
    User=youruser
    WorkingDirectory=/yourworkingpath/

    [Install]
    WantedBy=multi-user.target
    ```
    Reload systemd services:
    ```sh
    sudo systemctl daemon-reload
    ```
    Enable the service to start at boot:
    ```sh
    sudo systemctl enable telebit
    ```
    Start the Telebit service:
    ```sh
    sudo systemctl start telebit
    ```
    Check the status of the service:
    ```sh
    sudo systemctl status telebit

    ...
    Loaded: loaded (/etc/systemd/system/telebit.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2024-09-23 20:52:09 UTC; 8s ago
   Main PID: 108934 (telebit)
      Tasks: 12 (limit: 9458)
     Memory: 17.5M
        CPU: 250ms
     CGroup: /system.slice/telebit.service
             ├─108934 /bin/bash /home/azureuser/Applications/telebit/bin/telebit daemon --config /home/azureuser/.config/telebit/telebit.yml
             └─108935 /home/azureuser/Applications/telebit/bin/node /home/azureuser/Applications/telebit/bin/telebit.js daemon --config /home>

   Sep 23 20:52:09 vmubuntu systemd[1]: Started Telebit Daemon.
   Sep 23 20:52:10 vmubuntu telebit[108935]: telebit daemon v0.20.8
   Sep 23 20:52:10 vmubuntu telebit[108935]: [info] waiting for init/authentication (missing relay and/or token)
    ```
     
10.  Enjoy!

      
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- USAGE EXAMPLES -->
## Usage

### Easy way:
- Go to `http://localhost:5601/` to see the kibana UI.

### Pro way:
- Api rest to ingest data in the elastic search.
https://www.elastic.co/guide/en/elasticsearch/reference/current/rest-apis.html

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ROADMAP -->
## Roadmap

- [x] Implement Docker compose for deployment
- [x] Implement CI/CD with GitHub Actions
- [x] Implement VM Azure for deployment
- [x] Implement logstash to ingest data from mysql
- [x] Implement logstash to ingest data from kafka

See the [open issues](https://github.com/Great-Side-Projects/kafka/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the "develop" Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTACT -->
## Contact

Angel Morales - [LinkedIn](https://www.linkedin.com/in/angelmoralesb/) - angelmoralesb@gmail.com

Project Link: [https://github.com/Great-Side-Projects/elastic-stack](https://github.com/Great-Side-Projects/elastic-stack)

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* [Elastic Stack](https://www.elastic.co/es/elastic-stack)
* [Choose an Open Source License](https://choosealicense.com)
* [Docker](https://www.docker.com/)
* [GitHub Actions](https://docs.github.com/es/actions)
 
<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/othneildrew/Best-README-Template.svg?style=for-the-badge
[contributors-url]: https://github.com/Great-Side-Projects/kafka/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/othneildrew/Best-README-Template.svg?style=for-the-badge
[forks-url]: https://github.com/Great-Side-Projects/kafka/forks
[stars-shield]: https://img.shields.io/github/stars/othneildrew/Best-README-Template.svg?style=for-the-badge
[stars-url]: https://github.com/Great-Side-Projects/kafka/stargazers
[issues-shield]: https://img.shields.io/github/issues/othneildrew/
[issues-url]: https://github.com/Great-Side-Projects/kafka/issues
[license-shield]: https://img.shields.io/github/license/othneildrew/Best-README-Template.svg?style=for-the-badge
[license-url]: https://github.com/Great-Side-Projects/quickshortapi/blob/main/LICENSE
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/angelmoralesb/
[product-screenshot-UI]: images/screenshotUI.png
[DockerImage]: https://img.shields.io/badge/Docker-0db7ed?style=for-the-badge&logo=docker&logoColor=white
[AzureWebApp]: https://img.shields.io/badge/Azure%20Web%20App-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white
[PostgreSQL]: https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white
[architecture-diagram]: images/Elastic-Stack-Architecture-Design.drawio.png
[AzureVM]: https://img.shields.io/badge/Azure%20VM-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white
[product-screenshot-UI2]: images/screenshotUI2.png
[product-screenshot-UI3]: images/screenshotUI3.png
[product-screenshot-UI4]: images/screenshotUI4.png
[product-screenshot-UI5]: images/screenshotUI5.png
[product-screenshot-UI6]: images/screenshotUI6.png
