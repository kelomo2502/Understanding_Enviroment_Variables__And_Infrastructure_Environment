# Understanding_Enviroment_Variables__And_Infrastructure_Environment

## Background

In the world of technology and its building blocks, two essential concepts often come to the forefront: "Infrastructure Environments" and "Environment Variables." Despite both terms featuring "Environment," they play distinct roles in the realm of scripting and software development. This common terminology can lead to confusion, making it crucial to distinguish and understand each concept from the outset.

## Infrastructure Environments

Infrastructure environments refer to the various settings where software applications are developed, tested, and deployed, each serving a unique purpose in the software lifecycle.

## Environment Variables

On the other hand, environment variables are key-value pairs used in scripts or computer code to manage configuration values and control software behavior dynamically.

- sample environment variables

  ```bash
  DB_URL=localhost
  DB_USER=test_user
  DB_PASS=db_password
  ```

Here, the environment variables point to a local database on your laptop where you can safely experiment without affecting real or test data.

Lets begin by creating environment variable to determine if the script is running for local, testing, or production environment.

1. Create a script called aws_cloud_manager.sh
2. Put the code below

```bash
#!/bin/bash

# Checking and acting on the environment variable
if [ "$ENVIRONMENT" == "local" ]; then
echo "Running script for Local Environment..."
# Commands for local environment
elif [ "$ENVIRONMENT" == "testing" ]; then
echo "Running script for Testing Environment..."
# Commands for testing environment
elif [ "$ENVIRONMENT" == "production" ]; then
echo "Running script for Production Environment..."
# Commands for production environment
else
echo "No environment specified or recognized."
exit 2
fi

```

3. Give it the relevant permission to execute
`sudo chmod +x aws_cloud_manager.sh`

if you run this code on the terminal `export ENVIRONMENT=production` and execute aws_cloud_manager.sh,
you should get an output as this
`Running script for Production Environment...`
Now, you can see how environment variables can be used to dynamically apply logic in the script based on the requirement you are trying to satisfy.

Let's modify the script to take the ENVIRONMENT variable input as a postitonal argument by adding
`ENVIRONMENT=$1` at the top of the script just after the shebang
 $1 is the positional parameter which will be replaced by the argument passed to the script.
 Because it is possible to pass multiple parameters to a script, dollar sign  is used to prefix the position of the argument passed to the script. Imagine if another variable within the script is called
 NUMBER_OF_INSTANCES  that determines how many EC2 instances get provisioned, then calling the script might look like;

 if you run the aws_cloud_manager.sh again after the modification, you should get something like this

 ```bash
 Running script for Local Environment...
 Running 4 ec2 instances`
 ```

## Condition to check the number of arguments

 Creating shell scripts to meet specific requirements is one aspect of development, but ensuring their cleanliness and freedom from bugs is equally crucial. Integrating logical checks periodically to validate data is considered a best practice in script development.

 A prime example of this is verifying the number of arguments passed to the script, ensuring that the script receives the correct input required for its execution, and providing clear guidance to users in case of incorrect usage.

 Below code ensures that when the script is executed, exactly 1 argument is passed to it, otherwise it fails with an exit code of 1 and an shows a message telling the user how to use the script.
