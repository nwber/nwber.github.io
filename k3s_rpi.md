<h1>Kubernetes on a Raspberry Pi cluster</h1>

<img src="img/k8s.png" style="zoom: 67%;" />  <img src="img/docker.png" style="zoom: 67%;" /> <img src="img/prometheus-pic.png" style="zoom: 67%;" />  <img src="img/minecraft-pic.png" style="zoom: 67%;" />

I'm new to DevOps. I recently started as an Associate DevOps Engineer and there seem to be a million things to learn. In college, I took a Configuration Management course that ended up being DevOps 101, and I was exposed to things like Agile methodology and Infrastructure as Code. I already knew some Docker, so for a group project I figured I could learn Kubernetes. GKE is easy enough to use, but so much of the 'guts' is abstracted away in the GUI that it's almost dummy-proof. When I'm working in the cloud, I have a tendency to blow away an instance when it's acting funny. With a physical build, this will hopefully force me to learn the tools better, plus cloud bills get expensive fast. I'll be focusing on learning Kubernetes and it's respective tooling, but I'm interested in where this project may go as I learn more.

This will not be a comprehensive guide to do this yourself. However, I will link the sources I used where applicable. Inspired by Jeff Geerling's build.



<h3>Build List:</h3>

- Raspberry Pi 4B 2GB x4
- 8 port unmanaged switch
- 4 32GB microSD cards
- Ethernet and USB C cables x4
- Case for the Pis



This cluster clocks in with 16 ARM cores, 8GB RAM, 128GB of storage, and a network more than fast enough for node-to-node communication. Not exactly a high-end server but not bad for what it is.



<h3>Quick breakdown of the technology:</h3>

- [Docker](https://www.docker.com/why-docker) is a containerization tool. I won't explain all the advantages of containers but there's a lot. However, managing dozens or hundreds of containers can be difficult. So we use orchestrators. 
- [Kubernetes](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/) (shorthand k8s) is an open-source container orchestration tool made by Google, based on their Borg system. Kubernetes is the industry standard orchestration technology. There is a steep learning curve but it's very powerful at scale, with features like auto-scaling and self-healing clusters. The basic architecture of a cluster (or mine at least) is a master server and several nodes that do work as orchestrated by the master.
- I wanted to use a 'lite' version of k8s because resources on this build are a little tight. [k3s](https://k3s.io/) makes it possible to run on systems with as little as 512MB of RAM. Other options are 'full-fat' k8s or other distributions like Openshift or Tanzu but we're aiming for minimizing overhead here. It's not recommended to use k3s in a production environment, but for a sandbox like this, it works fine. There are other lite distributions of k8s but k3s is considered the simplest to set up from my research into this.

- Raspberry Pi's main headache (or advantage) is their CPU architecture. As they have ARM cpus, there are difficulties running software designed for x86 systems. This may not be the case for long because it looks like ARM is going to take over in the next 5-10 years. 

  

<h3>Setting up the cluster:</h3>

- Flashed [Raspberry Pi OS Lite](https://www.raspberrypi.org/downloads/raspberry-pi-os/) on all of the SD cards. Boot up the pi's.
- Changed their hostnames to make them easier to manage.
- I kept the default username and password just for ease of use. It goes without saying that this is a bad idea but it's just running on my home network so who cares.

- Enabled passwordless SSH access. This is trivial to do on Linux -> Linux with `ssh-copy-id` but Windows -> Linux is a tad bit harder. WSL helps, but luckily my new Macbook came about this time so that made it much easier.
- I chose k3s for orchestration, and used [k3sup](https://github.com/alexellis/k3sup) to install and configure the master and nodes. This is a very simple tool that can set up the entire cluster in ~10 commands,  I highly recommend it.
  - Manually installing and configuring the cluster is not very difficult. However, automation is the name of the game. This creates less opportunities for mistakes and lets me be lazy too.
- One important thing to do is `scp` your /.kube/config file onto your local machine. This allows you to run kubectl commands such as `kubectl get pods` without sshing into your master every time you want to run a command.
- Troubleshooting some weird issues with the k3s-agent.service on one of my nodes, simply uninstalling and reinstalling did the trick.

<h3> Running some apps:</h3>

- This is where things get interesting. There's a million articles like "How to deploy XYZ software to Kubernetes". However, most of these will not work as the container images they pull are usually based on x86. Being an ARM based platform, these are incompatible. However, I am far from the first person to have this problem and quite a few of them have documented their journey.
- Kubernetes Dashboard
  - Made by the team that makes Kubernetes, this actually is compatible with ARM. The install is fairly straightforward, but doesn't offer the most utility. The graphs and charts are nice, but I couldn't get the deployments via the dashboard to work and running it can be a pain. So...

![](img/dashboard2.png)

- Prometheus, Grafana, and AlertManager.

  - You might think you could just google `install prometheus on kubernetes` and get the steps to install - you would be wrong. That would would bring you to a CoreOS/kube-prometheus repo, and this would work fine on a full-fat Kubernetes install. However the container images that repo pulls are x86, and won't work on ARM processors. This leads you to use the carlosedp/cluster-monitoring repo, designed for cross-architecture clusters. Just clone the repo, edit the config file, and follow the steps to build the manifests, and you have Prometheus, Grafana, and Alertmanager running.



  ![ingress](img/prometheus-ingress.png)



  ![prometheus](img/prometheus2.png)



  ![grafana](img/grafana.png)



  ![alertmanager](img/alertmanager.png)



- Anyway, now it's time to have fun. I installed a minecraft server! It runs smooth enough. If anyone wants to come over and play Minecraft feel free, my parents said it's ok.

![](img/minecraft_building_world.png)

​		![](img/gaming.png)



<h3>What's next:</h3>

- Dive deeper with some of the apps I've installed. Set up some Grafana dashboards, AlertManager notifications, etc.
- It's one thing to run applications other people built, and it another to build it yourself. So next I would like to build something simple like a web server from the ground up. To build on that, I'm also interested in technologies like GitOps and Chaos Engineering so I might try to sprinkle in some of that once I get a handle on the infra.
- A technology that I find interesting is serverless computing, so I'd like to get a project like openFaaS running.
- Because I won't be using this cluster 99% of the time, I'd like it to be useful when I'm not tinkering on it. There are projects to get Folding@Home running in Kubernetes so I'd like to do that as well.
