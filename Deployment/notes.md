# IAAS --- infrastructure as a service
1. VMs (Virtual Machines)
2. Storage (Block, Object, File)
3. Networking (VPC, Subnets, Routing, Firewalls)
4. Load Balancers (ELB, ALB, NLB, GSLB)

## examples - 
- AWS EC2
- Azure VMs
- GCP Compute Engine
- Microsoft Azure 
- Oracle

# concurrency --- all daily active users on website
# RPS --- requests per second on website (2-5% average)


# Users 

## 1k - 10k users
- Tools: render, vercel, entry level cloud providers
- Bottlenecks: CPU/Memory, DB Stress, RAM
- Scaling: Vertical Scaling
- improve: DB connection 
- Cache: Redis/memcached
- Load balancers: AWS ELB, NGINX


## 10k - 100k users
- Tools: AWS, Azure, GCP, kubernetes
- Bottlenecks: every request hits DB
- Scaling: Horizontal Scaling
- improve: cdn(content delivery network), caching layer, read replicas, DB indexing,  

## 100k - 1M users
- Tools: AWS/GCP/Azure, message broker(SQS/RabbitMQ), Node worker, distributed monolith, sharding, read replicas, caching layer, cdn
- Bottlenecks: sync processing, not scalable, DB writes, Network latency
- improve: async processing, message queue  
- Monitoring: Prometheus, Grafana, ELK Stack

