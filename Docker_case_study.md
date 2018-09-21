# **Docker Case Study**

### **Objective**:-
- Dynamic Allocation of Linux systems for users
- Each user should have independent Linux System
- Specific training environment should be created in Container
- User should not allow to access other containers/images
- User should not allow to access docker command
- Monitor participants containers
- Debug/live demo for the participants if they have any doubts/bug in running applications. 
- Automate container creation and deletion.

## Creating the container image
- First build a new `ubuntu` container

    `sudo docker run --name train -it ubuntu /bin/bash`
- Start the container

    `sudo docker start docker_contain`
- Attach to the container

  `sudo docker attach docker_contain`
- Install packages required

  `apt update
apt install vim
apt install gcc`
- Create questions.txt, instructions.txt and save them.

  `touch questions.txt 
touch instructions.txt`
- Commit the container
 
 `docker commit ­a "sonal2806" 37f609ba3b38 docker_contain_imageN `
## Allocate Linux systems for users
1. Create a shell script `create_userContainers.sh` to automatically create docker containers using a specific environment docker image for every user.

    - `users.txt`
        ```
        user1
        user2
        user3
        ```
    - `create_userContainers.sh`
        ```sh
        echo -n "Enter user list file: "
        read file

        while read user
            do 
                docker create -it --name $user <Training Image> /bin/bash
            done < $file
        ```
2.  Run the shell script `create_userContainers.sh` and enter the `users.txt`. This creates a docker container corresponding to each username from that file.
3.  The user can then use the container allocated to him/her using `useContainer.sh` script.
    - `useContainer.sh`
        ```sh
        echo -n "Enter your username: "
        read name
        docker start $name
        docker attach $name
        ```
4.  This allows user to enter to his/her allocated Linux system and has only access to the bash of that system.

## Monitoring the container
- using `monitorContainer.sh` script.

    - `monitorContainer.sh`
        ```sh
        echo -n "Enter container name to be monitored: "
        read name
        docker logs -f $name
        ```
## deletion of the containers
- Automate the deletion using the `deleteContainers.sh` script.

    - `deleteContainers.sh`
        ```sh
        echo -n "Enter 'all' to delete all user containers or enter 'user' to delete a specific user container: "
        read typ
        if [ "$typ" == "all" ]
        then
            echo -n "Enter the user list file: "
            read file
            while read user
                do
                    docker rm $user
                done < $file
        else
            echo -n "Enter the username: "
            read name
            docker rm $name
        fi
        ```
- You can either delete all users or user by name using sh delete_Containers.sh
