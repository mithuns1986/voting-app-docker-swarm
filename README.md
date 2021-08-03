# voting-app-docker-swarm

Setting up a sample voting app using Docker
Docker Sample Voting app is a distributed application which uses a Postgres database and Redis message queue, with application components running in Python, .NET and Node.js containers. All the components of the app are published in public images on Docker Hub.

Voting app

In this lab you’ll learn how to set up a sample voting app using Docker Swarm. You’ll gain experience of working with Docker Compose and Docker Swarm

Init your swarm
Let’s create a Docker Swarm first. Open up the first instance and initiate Swarm mode cluster.

docker swarm init --advertise-addr $(hostname -i)
This node becomes a manager node. The output displays a command to add a worker node to this swarm as shown below:

Swarm initialized: current node (xf323rkhg80qy2pywkjkxqusp) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-41uv2d4keynz33b5z9nozygzfai4gpu7ufk33347i2vgfgtu1h-1vizoglo6pwz9w4hugim46ayl 192.168.0.18:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
The above token ID is unique for every swarm mode cluster and hence might differ for your setup. From the output above, copy the join command (watch out for newlines).

Next, Open up the new instance and paste the below command. This should join the new node to the swarm mode cluster and this new node becomes a worker node. In my case, the command would look something like this:

 docker swarm join \
    --token SWMTKN-1-089phhmfamjor1o1qj8s0l4wdhyvegphg6vtt9p3s8c35upltk-eecvhhtz1f2vpjhvc70v6v
vzb \
    10.0.50.3:2377
Output:

$ docker swarm join --token SWMTKN-1-089phhmfamjor1o1qj8s0l4wdhyvegphg6vtt9p3s8c35upltk-eecvhh
tz1f2vpjhvc70v6vvzb 10.0.50.3:2377
This node joined a swarm as a worker.
Show members of swarm
Type the below command in the first terminal:

docker node ls
The output shows you both the manager and worker node indicating 2-node cluster:

ID                           HOSTNAME  STATUS  AVAILABILITY  MANAGER STATUS
xf323rkhg80qy2pywkjkxqusp *  node1     Ready   Active        Leader
za75md1p0hpc2qswefj8uyktk    node2     Ready   Active
2. Cloning the repository
The source code repo for the sample voting app includes a Docker Compose file to bring up required microservices. Start by cloning the repo:

git clone https://github.com/dockersamples/example-voting-app && cd example-voting-app
3. Running Voting App Compose file
docker stack deploy --compose-file docker-stack.yml vote
4. Verifying the services
docker service ls
Wait for few seconds. Open up Swarm Visualizer tool

5. Accessing the voting app
The vote interface is then available on port 5000.
