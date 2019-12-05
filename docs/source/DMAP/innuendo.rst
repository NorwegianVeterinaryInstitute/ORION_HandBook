INNUENDO
=========

INNUENDO: A novel cross-sectorial platform for the integration of genomics in surveillance of foodborne pathogens

Background:
-----------
INNUENDO is a light-weight browser based end-to-end analysis surveillance platform. INNUENDO is species dependent. INNUENDO can be installed in a laptop, PC and high-performance computing clusters. 

**1. User friendliness:** 
INNUENDO has a very simple front-end page to login, add data and run analysis pipelines.

**2. User data management:** 
INNUENDO does not have any defined user data management. Everyone those who are using the instance can see all the data and the results. 

**3. Adding metadata:**
INNUENDO has a simple metadata template for adding meta data. Free text allowed.

**4. Functionalities** 
4.1 Individual tools: 

4.2 Pipelines: INNUENDO comes with 6 species (Escherichia coli, Yersinia enterocolitica, Salmonella enterica and Campylobacter jejuni) specific analysis workflows/pipelines. New species and pipelines can be added.
4.3 Visualization tools: PHYLOViZ
4.4 Automation of data transfer from sequencers: NA
4.5 Activity Log: NA
4.6 Data communication between instances and other tools: No detail information is available


**5. Installation and administration:**
INNUENDO is developed using Java. It has two main parts, frontend and backend server.

5.1 Technical knowledge needed for administration: 
Knowledge in Java and NodeJS
Knowledge in NextFlow and FlowCraft
Knowledge in package managers (f. ex. conda) 
Knowledge in REST APIs
Knowledge in RDBMS (PostGres) are needed. 
Knowledge in Nginx web server
SLURM job scheduler knowledge to configure to use high performance computing facility
Knowledge on LDAP and phpldapadmin
Read about Allegrograph 

5.2 Administration details: 
Users are created by administrator with temporary password
Installing pipelines are automated
INNUENDO has released only one version so far
Recommended to have a test INNUENDO installation beside production environment for testing purposes

5.3 Additional details to Administrators:
List the samples, data and results based on species, timelines and other parameters for a new analysis or to generate reports. 
Big data can be transferred to INNUENDO instead of uploading them through browsers

**6. Secure login:**

INNUENDO uses LDAP and phpldapadmin for authentication.
6.1 Technical details: 

**7. High performance computing (HPC):**
INNUENDO can be configured to use SLURM job scheduler for HPC or a cluster environment.

**8. Expandability:**
More tools and  pipelines can be added. 

**8. User support:** 
Not established yet. Only through personal emails and video conferencing.


**9. Code maintenance and development:**
INNUENDO is an open source project (https://github.com/B-UMMI/INNUENDO). It was funded by EFSA and many other academic funding agencies. Currently, their development is stalled due to lack of developers. INNUENDO team is open for any outside collaborations and contributions.
 
**10. Existing user base and feedback:** 
INNUENDO has only one instance in Finland so far. We have got a mixed feedback from the existing users of INNUENDO.

**11. Further developments:**
Currently (as of December 2019), INNUENDO development is stalled due to lack of developers.
