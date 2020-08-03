# How to an elastick-stack with docker
> The simplest way to get an elastic-stack for your .Net Core project

*Straigth to the git repository?*
[github.com/elastic-stack](https://github.com/MichaelGuldborg/elastic-stack)

### Why you should setup an elastic-stack
Why? I think if you're here you already know why but just to make sure that we're both on the same hype level I'll give you a small sneak peak at why you should be excited to get an elastic-stack up and running at full speed!

<p float="center">
  <img src="/screenshots/kibana_dashboard.png" width="600" />
</p>


### Prerequisites
Firstly, if you haven't already please make sure that you've installed both [docker](https://docs.docker.com/engine/install/ubuntu/) and [docker-compose](https://docs.docker.com/compose/install/)
You can check this by running the commands
```bash
docker version
docker-compose version
```
I recommend that you setup an elastic-stack on a linux server with the following minimum specs (or double)
> Memory: 2 GB RAM
> Disk: 8 GB

### Clone, plug and play
Now for the part you're actually here for, the [git repository](https://github.com/MichaelGuldborg/elastic-stack)
```
git clone git@github.com:MichaelGuldborg/elastic-stack.git
```

The repository includes an elastic-stack.env.sample file with the following content. This file contains the required environment variables used in the docker-compose.yml when running the elastic-stack.
```
export ELASTIC_HOST=elasticsearch.example.com
export KIBANA_HOST=kibana.example.com
export ELASTIC_USERNAME=elastic
export ELASTIC_PASSWORD=changeme
export METRICBEAT_NAME=metricbeat-changeme
```

The only thing for you to to is either copy each line into the linux terminal or simply copy, rename and update the file with the values you want and run the source command to set all the environment variables.
```bash
source .elastic-stack.env
```
(If you're running windows and just want to test it out .. you replace the word "export" with "SET" and copy paste the lines into cmd to set the environment variables)

In order to now acctually run the elastic-stack all theres left to do is to run the following magic docker command
```
docker-compose up --detach
```

### Play around with it
By default  the elasticsearch and kibana application will be located at localhost:5602 and localhost:9200 respectively. You should be able to check these out through the browser or a simple curl command (kibana might be a little slow to start up so have patience).

If you haven't already I recommend you read this article about setting up a [reverse proxy with nginx](/#) for both applications as it will make them both more secure and easier to access remotely.

Once signed in to the kibana dashboard you can import some sample data-sets to get a feel for how the visualisation tools works. But what would be much more fun an interesting is some actual real-life data.

### Integrate server health with metricbeat
One set of data that might be interesting to log to the elastic stack is your server cpu, memory and disk status to make sure it never reaches critical load. In order to get this running the repository includes a folder called "monitoring". With the nescessary docker-files for metricbeat. Make sure all of the previous environment variables are set and then again simply run the magic docker command to start logging.
```
docker-compose up --detach
```
This data should show up in the *stack monitoring* section of kibana and have the name defined by the *METRICBEAT_NAME* environment variable.

