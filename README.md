# Deploy containers using Elastic Container Service and CloudFormation

ECS and Fargate give you a lot of control over how you want to deploy containers, and how you would like them to be networked and accessed. This repository contains CloudFormation templates to help you setup architecture AWS ECS on AWS Fargate.

To get started use the AWS CLI to execute the following command. This will create a role that enables ECS on your account, so the following reference templates will work properly:

```
aws iam create-service-linked-role --aws-service-name ecs.amazonaws.com
```

### Privately networked service, with public load balancer

This is a service protected inside a private subnet, with no direct internet access. Because the service does not have public IP address it must initiate outbound connections through a NAT Gateway, which communicates to the external internet on the service's behalf. However, you may still want to give the public limited access to the service via a load balancer which is public.

![private subnet public lb](images/private-subnet-public-lb.png)

__Fargate hosted:__

1. Deploy the [Fargate cluster with public subnet](cluster/ecs-cluster-fargate-vpc.yml)
2. Deploy the [external, public ALB](ingress/alb.yml) ingress
3. Deploy the [private subnet, public load balanced Fargate service template](service/service.yml)


## 📚 Examples
- React SPA SSG: [git@github.com:jim9527/REACT-SPA-SSG.git](https://github.com/jim9527/REACT-SPA-SSG)  
