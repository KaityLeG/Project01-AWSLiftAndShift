# Project01-AWSLiftAndShift
<p align="center">
  <img src="https://github.com/KaityLeG/Project01-AWSLiftAndShift/blob/main/images/AWSLiftAndShiftProject.drawio%20(2).png?raw=true"  title="hover text">
  </p>
  <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS1.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Create security group for the Load Balancer.
  Inbound rules being : HTTP(80) HTTPS(443) IPv6(0)   
  </p>
   <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS4.png" width="700"  title="hover text">
  </p>
 <p align="center">
  Created security group for application. Edited inbound rules to: SSH(22) Custom TCP(8080) to Allow traffic from vkaity prod elb.
  </p>
  <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS5.png" width="700"  title="hover text">
  </p>
  <p align="center">
   Created backend security group for backend services such as RabbitMQ, MySQL, and Memcache will be attached. Edit inbound rules to be Custom TCP(5672) Custom TCP(11211) MySQL/Aurora(3306) All traffic(All) . All traffic will allow traffic to flow within itself.
</p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS6.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Created Key Pair.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS7.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Created Private Hosted Zone in Route 53
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS8.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Created records for instances of DB01, MC01 , and RMQ01. Create a record by going to "Create record". Attributing the record name according to the instances. Choose Record type to be A which will route traffic IPv4 addresses. The Value will be the private IP addresses of the threw instances.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS9.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Go into properties of the application and make sure the JDBC is configured according to the instances host names and IP addresses. You can see the changes with the records and host names I created earlier.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS10.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Went inside the project resources and created an articifact using 
 
  ```
  mvn install
  ```
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS11.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Here you can see the .war fle created from the mvn install command. We now have our artifact of our applcaition created.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS12.png" width="700"  title="hover text">
  </p>
  <p align="center">
  inserting my (dummy AWS User, now deleted of course :) ) AWS profile using "aws configure" command. I now created an s3 bucket to store the artifacts created my going into the target/ folder of the project and copying it to the s3 bucket. Using AWS CLI commands.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS13.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Created an IAM Role to attach to the application instance to allow writing to s3 to store the artifacts.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS14.png" width="700"  title="hover text">
  </p>
  <p align="center">
  SSh'd into application(tomcat) instance
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS15.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Checked to see if tomcat instance are up and running. Installed AWS CLI within the webapps/ folder to copy artifacts and move into tmp folder. 
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS16.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Made my way into into the classes folder to get to the  application properties to check the JBDC configurations once more. Installed and used telnet to check if conenctions were made properly.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS17.png" width="700"  title="hover text">
    </p>
    <p align="center">
    Here I made a target group for the load balancer to direct traffic to.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS18.png" width="700"  title="hover text">
  </p>
  <p align="center">
  We set the protocol to HTTP: 8080. I selected the default VPC. I let the threshold with a timeout of 5 seconds. And have 30 secs between health checks.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS19.png" width="700"  title="hover text">
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS20.png" width="700"  title="hover text">
 <p align="center">
  Then I registered the ec2 instances created to this particular target group created.
  </p>  
</p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS22.png" width="700"  title="hover text">
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS23.png" width="700"  title="hover text">
  <p align="center">
  I created the load balancer. Made sure its itnernet facing to the public. Selected the subnets that I want the traffic to be within.
  </p>
</p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS24.png" width="700"  title="hover text">
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS25.png" width="700"  title="hover text">
    <p align="center">
  Select the security group created for the ELB I made earlier.
</p>
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS26.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Make sure to forward to the correct targert group with the registered ec2 instances. Make sure it is listening on port 80 and 443. HTTP and HTTPS.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS27.png" width="700"  title="hover text">
  </p>
  <p align="center">
  In the secure lisrtener settings I selected an ACM certificate I created for security of the web application.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS28.png" width="700"  title="hover text">
  </p>
  <p align="center">
  On GoDaddy I used the DNS of the domain I created there and added the elb url to it so it can forward to this particular DNS name.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS29.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Here is the web applciation up and running.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS30.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Here Im creating an Image to start with creating an auto scaling group for the application for high availilibity.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS31.png" width="700"  title="hover text">
  </p>
  <p align="center">
  I selected the security gfroup for the applicaiton I created.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS32.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Selected the subnets I want to scale the ec2 instances in.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS33.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Here, I attached the target group to we created earlier to this for auto scaling group.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS34.png" width="700"  title="hover text">
  </p>
  Now here I specified the capapcity for the autoscaling group. I set it so that it stays at a minimum of two and have a maximum of 2 as well.
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS35.png" width="700"  title="hover text">
  </p>
  <p align="center">
  I added tags for this here
  </p>
    <p align="center">
  <img src="https://raw.githubusercontent.com/KaityLeG/Project01-AWSLiftAndShift/main/images/AWSLS36.png" width="700"  title="hover text">
  </p>
  <p align="center">
  Here you can see the healthiness of the instances inside the target group. 
</p>

















</p>
