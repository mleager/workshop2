# workshop2

Using the same basic Dockerized Django project from Workshop1 -
with the objective to deploy the app to an AWS EC2 instance.

Overview:
  - Use Workshop1 Django project
  - Containerize app and associatied Postges DB using docker-compose.yml
  - Build and Deploy Image to AWS EC2 Instance

Step-by-Step:
   1. - Add new inbound rule for EC2 instance's security group 
        
        -- Allow inbound requests for port 5433 for Postgres server     
        
   2. - Create ECR repo
        
        -- Go to 'Push Commands' and save the CLI command for authenticating Docker client to the the ECR registry
        -- Will be used at the end
        
   3. - Setup RDS service
    
   4. - Update ALLOWED_HOSTS with th EC2 DNS address in workshop2/app/nc_tutorials/settings.py 
    
   5. - Create docker-compose.yml file with the ECR repo's URI
        in the 'image' keys for the Django app and nginx app
        
        -- Also set web service's environment with the DB endpoint and EC2 DNS
        
   6. - Create .env file for DB settings 
        
        -- from decouple import config and apply to DATABASE settings in workshop2/app/nc_tutorias/settings.py 
        
   7. - Create GitHub repo, add remote origin, and push project to it
    
   8. - Clone GitHub repo to EC2 instance via SSH session
    
   9. - In SSH session, cd into project folder, compose dockerized project
        
        -- docker-compose up -d
        
  10. - Run migrations for Django app's DB
        
        -- docker-compose exec web python manage.py makemigrations --noinput
        -- docker-compose exec web python manage.py migrate --noinput
    
    * When I originally setup EC2 via the SSH session, I installed Docker Compose V1 (which requires hypen in docker-compose cli command)
      I am not yet proficient in linux commands/provisioning so I kept this version rather than installing V2
          
  11. - Confirm container is running on the Elastic IP
   
  12. - Use Insomnia to send a few POST requests and confirm containerized Django web app is accepting
   
  13. - Push workshop2 image to the ECR 
  
        -- Use the CLI Push Command that was saved after the ECR repo was created
        -- docker-compose push 
        -- Confirm the Django and NGINX images are now inside the ECR repo via AWS console 
