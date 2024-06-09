# Learning

    p.p1 {margin: 0.0px 0.0px 14.0px 0.0px; font: 14.0px Monaco} p.p2 {margin: 0.0px 0.0px 14.0px 0.0px; text-align: center; font: 33.0px Monaco} p.p3 {margin: 0.0px 0.0px 14.0px 0.0px; font: 14.0px Monaco; min-height: 19.0px} p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; font: 14.0px Monaco; -webkit-text-stroke: #000000} p.p5 {margin: 0.0px 0.0px 14.0px 0.0px; font: 14.0px Monaco; -webkit-text-stroke: #000000; min-height: 19.0px} p.p6 {margin: 0.0px 0.0px 14.0px 0.0px; font: 14.0px Monaco; -webkit-text-stroke: #000000} p.p7 {margin: 0.0px 0.0px 14.0px 0.0px; font: 12.0px Monaco; -webkit-text-stroke: #000000} p.p8 {margin: 0.0px 0.0px 0.0px 0.0px; font: 14.0px Monaco; -webkit-text-stroke: #000000; min-height: 19.0px} span.s1 {font-kerning: none} span.Apple-tab-span {white-space:pre}

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

GCP

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————————

  

VM: Machine with hardware(machine type) and software(boot disk image: public or custom)

e2-medium-2 : <machine family>-<No of vCPUs>

  

Instance Template: Template with pre-populated machine config to launch new vm quickly

Image: You can create image of running vm boot disk, and create a template with the image and launch new vm using template quickly

? Reduce latency for installing softwares…

  

Instance Groups:

1\. MIG: Instance of same/identical type(config) created using a TEMPLATE, instance template is must

Features: auto healing, auto scaling, managed release

Types: Stateful, Stateless

Config: Name, Instance template, Location(single/multiple zones, distrib shape), Auto-Scaling(Mode: on, scale-out, off| Min, Max Instances | Signal(Metrics for scale(LB, cpu etc))), Init Period(check for autoscale), Scale-in-controls(Don’t scale-in more than 10 vms in 10 mins), Instance Lifecyle(Auto-Healing: HC), Port-Mapping

2\. UMIG: Instances could be of diff type(config)

Features: auto healing, scaling, MR Not available 

  

Updating MIG:

1\. Rolling update - Gradual update of instances in an instance group to the new instance template 

\- Specify new template: (OPTIONAL) Specify a template for canary testing 

\- Specify how you want the update to be done: 

When should the update happen? 

Start the update immediately (Proactive) or when instance group is resized later(Opportunistic) 

How should the update happen? 

Maximum surge: How many instances are added at any point in time? 

Maximum unavailable: How many instances can be offline during the update? 

2\. Rolling Restart/replace: Gradual restart or replace of all instances in the group 

\- No change in template BUT replace/restart existing VMs 

\- Configure Maximum surge, Maximum unavailable and What you want to do? (Restart/Replace)

  

  

Question: diff b/w backend service and backend

Resiliency: ability to provide expected behaviour even if some part of the provider fails.

Question: 

  

gcloud:

gcloud <group> <subgroup> <actions> …

Ex- 

gcloud compute instances list

gcloud compute zones list

gcloud compute regions list

gcloud compute machine-types list

gcloud compute machine-types list --filter=“zone:asia-south1-a”

gcloud compute machine-types list --filter=“zone:(asia-south1-a asia-south1-b)”

  

Container Orchestration:

Features:

1\. Auto-Scaling

2\. Service Discovery

3\. Load Balancer

4\. Self Healing

5\. Zero downtime deployments

  

GCP Compute Managed Services

Compute Engine: IAAS, GKE: CAAS, App Engine: PAAS(CAAS, Serverless), Cloud Funtion: FAAS(Serverless), Cloud Run: CAAS(Serverless)

  

App Engine:

one app per project

app:

 service1:

  version1: traffic 0.3

  version2: traffic 0.7

 service2:

  version1: traffic 0.4

  version2: traffic 0.6

 …

cd default-service

gcloud app deploy

gcloud app services list

gcloud app versions list

gcloud app instances list

gcloud app deploy --version=v2

gcloud app versions list

gcloud app browse

gcloud app browse --version 20210215t072907

gcloud app deploy --version=v3 --no-promote

gcloud app browse --version v3

gcloud app services set-traffic split=v3=.5,v2=.5

gcloud app services set-traffic splits=v3=.5,v2=.5

watch curl https://melodic-furnace-304906.uc.r.appspot.com/

gcloud app services set-traffic --splits=v3=.5,v2=.5 --split-by=random

cd ../my-first-service/

gcloud app deploy

gcloud app browse --service=my-first-service

gcloud app services list

gcloud app regions list
