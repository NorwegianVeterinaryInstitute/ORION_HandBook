IRIDA
========

IRIDA - Integrated Rapid Infectious Disease Analysis Project 

Background:
------------
IRIDA is a web-based, secure and end-to-end analysis platform for surveillance and molecular data analysis. IRIDA is primarily developed by IRIDA consortium supported multiple funding agencies in Canada and other countries. Here we report the details from our evaluation.

**1. User friendliness:** 
IRIDA is a browser based platform with simple login portal. User names are created by instance administrators. IRIDA data management and analysis is project based. Creating projects, uploading data and analysis steps are mostly easy and self explanatory. But the users have to get used to the “shopping-cart” method for data analysis. One should add the samples to cart to run the pipelines. Previous basic web portal and using online Bioinformatics tools experience is good enough to create projects, adding data and manage access control. English is the working language in IRIDA. But it's possible to use other languages. 

**2. User data management:**
User has to create a project with few details before adding sample data (WGS, metadata and results). The one who creates the project is the manager of the project and can add other users to that project and define their role(Owner, manager or collaborator). Collaborator has read-only access. Only the owner has all the access to data. Any kind of access to data is restricted within the members of the project. Users outside a  project can’t see and access the data/results in that project. Data can be exchanged between projects if the project member(s) has enough permission in responsible projects to exchange data between the projects. Other instances of IRIDA also can be added as associated projects to an existing project as a data resource. 

**3. Adding metadata:**
IRIDA comes with basic metadata template for each sample to add important/basic details. Also, user can add as many as metadata columns he needs for his data. But free texts are allowed. That’s a problem.    

**4. Functionalities** 
4.1 Individual tools: IRIDA is based on Galaxy framework. Galaxy is browser based Bioinformatics platform with a possibility of using almost all the Bioinformatics tools and pipelines. Administrators can easily install/implement/remove most of the Bioinformatics tools. And, executing a tool is very easy in Galaxy with a simple training.

4.2 Pipelines: IRIDA comes with 7 premade pipelines which can do all the general data analysis (assembly, annotation, typing and Phylogenetics). New pipelines can be easily added based on Galaxy workflows by IRIDA instance administrators. 

Good microbial Bioinformatics knowledge is needed to choose the pipelines based on your data and the goals. 

4.3 Visualization tools: IRIDA comes with visualization tools like GenGIS, Islandviewer and Island compare, Phyloviz. More visualization tools can be added in Galaxy framework.

Good microbial Bioinformatics knowledge is needed to use the visualization tools due to input file formats and pre-analysis. 

4.4 Automation of data transfer from sequencers: IRIDA has developed an option to load/transfer the data from sequencers after the sequencing run is over directly to IRIDA platform securely and run pipelines on the data. Choosing a pipeline to analyse the transferred data is done at the manager of the project level inside IRIDA platform.

Technical details: Secure API keys and other security configurations are needed to facilitate this option. Linux System administration and (windows) networking knowledge and experience is needed.

4.5 Activity Log:
Users’ every activity on any project is logged and the details are available. 

4.6 Data communication between instances and other tools:
External tools can interact with IRIDA REST API. Communication is authenticated by OAuth2. Standard output formats are XML, JSON, FastQ and Fasta

**5. Installation and administration:**
IRIDA is developed primarily using Java using Galaxy framework as the base. One should install Galaxy framework (or use an existing one) first before installing IRIDA web interface. Galaxy and IRIDA are configured to communicate with each other. Galaxy uses PostGres (it depends) and IRIDA uses MySQL.

IRIDA installation documentation has most of the installation steps covered but still one should need a Unix/Linux system administrator and web developer level knowledge to understand, fill the technical gaps and dependencies, install the instance and maintain it. 

5.1 Technical knowledge needed for administration: 
* Knowledge in Java 8 and Spring Framework
* Knowledge in package managers (f. ex. conda) 
* Knowledge in REST APIs
* Knowledge in RDBMS (f. ex. MySQL/PostGres) are needed. 
* Knowledge in Apache TomCat 
* Galaxy installation and configuration experience is a huge advantage
* Administrator does not need to configure anything for secure login during installation
* Galaxy and IRIDA uses different port numbers if they are installed in the same server (recommended to install them in different servers)
* SLURM job scheduler knowledge to configure Galaxy to use high performance computing facility
Read about Liquibase 

5.2 Administration details: 
* Users are created by administrator with temporary password
* IRIDA uses Spring Security for authentication and role based access control
* Important to learn Spring Security configuration for administration(and future single sign-on services if needed)
* Installing pipelines are partially automated
* Some of the tools should be installed manually using galaxy administration portal
* Technical-manual configuration is needed for converting Galaxy workflow to IRIDA pipelines
* IRIDA releases few updates a year and updating IRIDA is mostly smooth
* IRIDA uses MySQL to keep the data, analyses, access log details
* IRIDA maintains an excellent technical support for the administrator questions
* Recommended to have a test IRIDA installation beside production environment for testing purposes

5.3 Additional details to Administrators:
List the samples, data and results based on species, timelines and other parameters for a new analysis or to generate reports. 
Big data can be transferred to IRIDA instead of uploading them through browsers


**6. Secure login:**
IRIDA uses Spring Security for authentication, authorization and project role definition(data access control). Spring Security is one of the most powerful security frameworks available. 

6.1 Technical details: Spring security has key authentication features like Lightweight Directory Access Protocol (LDAP), Single sign-on and more. Administrator does not need to configure anything during installation. But, important to know Spring Security and the configuration. 

**7. High performance computing (HPC):**
IRIDA uses galaxy to submit jobs and galaxy can be configured to use SLURM job scheduler in HPC or cluster environment. 

**8. Expandability:**
IRIDA has plug-in style system for adding tools and pipelines. IRIDA has contribution document which explains that clearly step by step.

**8. User support:**
IRIDA development team has Gitter (https://gitter.im/irida-lobby/) channel to give live support to other instance administrators and users during working hours (Winnipeg time, GMT-6). They are very responsive to email inquiries and preplanned skype calls. 

**9. Code maintenance and development:**
IRIDA is an open source project (https://github.com/phac-nml/irida) with long term funding from Canadian Federal government and other funding agencies. IRIDA team has hired set of developers to maintain and further develop IRIDA platform. IRIDA consortium is open for contributions from other teams and developers as well.

**10. Existing user base and feedback:** 
IRIDA has more than 12 active instances in Canada and other parts of the world. 
We have got a good feedback from the existing users of IRIDA.

**11. Further developments:** 
IRIDA releases two or more updates every year with new features and bug fixes. One of the important features in the future development pipeline is the integration of Ontologies into IRIDA. 
