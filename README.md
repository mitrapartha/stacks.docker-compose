
**Quick install.**  
*Note:*  You do not need any locally running apache or php or even mysql. In case you have, for initial test, it is preferable if you switch them off   

1. Install Docker Engine or Docker Desktop  

https://docs.docker.com/get-docker/  

 2. Clone this repo and change to Wordpress branch. Else you can download the zip directly and extract to a folder  
https://github.com/mitrapartha/stacks.docker-compose/archive/refs/heads/Wordpress.zip  

 - Run the docker application  

 - Go to the folder where you have extracted the zip     Copy the
    default_env to .env, open .env and start editing the variables
    (Wordpress variables are not mandatory)     
    
 -  Start the application with:  
*docker-compose up -d --build*   
(Linux users may need to install docker-compose separately, and also run the command with sudo)
You should see the Wordpress and PHPMYAdmin in the ports you have defined.  

- Stop the application with  
*docker-compose down*  
 
3. Development
Code should be in *project* folder  
Wordpress files should be in *uploads* folder  
Database raw files should be in *db_data* folder, but you should be able to export sql from phpmyadmin  

4. Best Practices
Do not put any info.php or database access script like adminer.php in *project* folder  
