### **30 Common System Design Questions for SRE/DevOps Interviews (with Answers)**  

System design interviews for **SRE/DevOps** roles focus on **scalability, reliability, observability, automation, and infrastructure management**. Below are 30 common questions and their answers.

---

## **1. How would you design a highly available system?**  
- Use **load balancers** for traffic distribution.  
- Deploy services across **multiple availability zones (AZs)**.  
- Implement **auto-scaling** for horizontal scaling.  
- Use **database replication** and **failover strategies**.  
- Monitor uptime with **health checks** and **alerting systems**.  

---

## **2. How do you ensure zero-downtime deployments?**  
- Use **rolling updates** or **blue-green deployments**.  
- Implement **canary releases** for gradual rollouts.  
- Use **feature flags** to enable/disable features dynamically.  
- Deploy using **Kubernetes StatefulSets** or **immutable infrastructure**.  

---

## **3. How do you scale a database?**  
- **Vertical scaling** (increase RAM/CPU).  
- **Horizontal scaling** (sharding, read replicas).  
- **Caching** with Redis/Memcached.  
- Use **NoSQL** (e.g., Cassandra) for high write loads.  
- Implement **partitioning** for large datasets.  

---

## **4. How would you design a logging system for a distributed application?**  
- Centralize logs using **ELK (Elasticsearch, Logstash, Kibana)** or **Loki**.  
- Use **structured logging** (JSON format).  
- Implement **log rotation** and **retention policies**.  
- Use **Fluentd or Filebeat** for log shipping.  
- Store logs in **object storage (S3, GCS)** for long-term analysis.  

---

## **5. How would you design an observability stack for a microservices system?**  
- **Metrics:** Prometheus/Grafana.  
- **Logging:** ELK, Loki, or Splunk.  
- **Tracing:** OpenTelemetry, Jaeger, Zipkin.  
- **Alerting:** Prometheus Alertmanager, PagerDuty.  
- **Dashboards:** Grafana, Datadog.  

---

## **6. How do you prevent cascading failures in a distributed system?**  
- **Circuit breakers** (e.g., Hystrix, Envoy).  
- **Rate limiting and throttling**.  
- **Load shedding** (drop less important requests).  
- **Timeouts and retries** with exponential backoff.  
- **Bulkheading** (isolate failures to specific components).  

---

## **7. What is the CAP theorem, and how does it impact system design?**  
- **Consistency**: Every read gets the latest write.  
- **Availability**: System responds even if some nodes fail.  
- **Partition Tolerance**: System continues to operate if network partitions occur.  
- **Trade-offs**: CP (strong consistency, low availability) vs. AP (high availability, eventual consistency).  

---

## **8. How do you handle sudden traffic spikes?**  
- Use **auto-scaling** (Kubernetes HPA, AWS ASG).  
- Implement **CDN caching** (Cloudflare, Akamai).  
- **Queue requests** using Kafka/RabbitMQ.  
- **Rate limiting** to prevent abuse.  

---

## **9. How do you design a multi-region system?**  
- Deploy services in **multiple regions** with global load balancing.  
- Use **database replication** across regions.  
- Implement **active-active** or **active-passive** failover.  
- Use **geo-DNS** for regional routing.  

---

## **10. How do you handle stateful applications in Kubernetes?**  
- Use **Persistent Volumes (PVs)** and **Persistent Volume Claims (PVCs)**.  
- Use **StatefulSets** instead of Deployments.  
- Implement **backup and disaster recovery strategies**.  

---

## **11. How do you design a CI/CD pipeline for a microservices architecture?**  
- Use **GitHub Actions, GitLab CI, or Jenkins**.  
- Implement **containerized builds** (Docker, BuildKit).  
- Automate **testing (unit, integration, security scans)**.  
- Deploy using **Helm, ArgoCD, FluxCD**.  

---

## **12. How do you reduce cold start times for serverless functions?**  
- **Provisioned concurrency** (AWS Lambda).  
- Keep functions **warm** with scheduled pings.  
- Use **lightweight runtimes** (Node.js, Golang).  

---

## **13. How would you design a global load balancer?**  
- Use **AWS Route 53, Google Cloud Load Balancer**.  
- Implement **GeoDNS routing**.  
- Use **Anycast IPs** for nearest-region traffic.  

---

## **14. How do you design a self-healing infrastructure?**  
- **Health checks and auto-restarts**.  
- **Auto-scaling** to replace unhealthy instances.  
- **Chaos engineering** (test resilience).  

---

## **15. How do you migrate a monolithic application to microservices?**  
- Identify **domain boundaries**.  
- Implement **API gateways**.  
- Use **event-driven communication (Kafka, RabbitMQ)**.  

---

## **16. How do you prevent DDoS attacks?**  
- **WAF (Web Application Firewall)**.  
- **Rate limiting and CAPTCHA**.  
- **Cloudflare/Akamai protection**.  

---

## **17. How do you manage secrets in a DevOps environment?**  
- Use **HashiCorp Vault, AWS Secrets Manager, or Kubernetes Secrets**.  

---

## **18. How do you implement blue-green deployments in Kubernetes?**  
- Deploy **two versions** and switch traffic using **Ingress or service selectors**.  

---

## **19. How do you detect configuration drift?**  
- Use **Terraform drift detection** (`terraform plan`).  
- Implement **AWS Config, Kubernetes OPA/Gatekeeper**.  

---

## **20. How do you store and access container logs?**  
- Use **Fluentd, Filebeat, or Promtail**.  
- Send logs to **ELK, Loki, or Datadog**.  

---

## **21. What are the challenges in designing a distributed database?**  
- **Consistency vs. availability trade-off**.  
- **Data replication and sharding**.  

---

## **22. How do you implement rate limiting?**  
- Use **Redis-based counters**.  
- Implement **Envoy, Nginx, or API Gateway**.  

---

## **23. How do you design a monitoring system?**  
- Use **Prometheus for metrics**.  
- Implement **Grafana dashboards**.  
- Use **Alertmanager for alerts**.  

---

## **24. How do you handle rolling restarts of services?**  
- Use **Kubernetes rolling updates**.  
- **Drain traffic from nodes before restarting**.  

---

## **25. How do you ensure data consistency across microservices?**  
- Use **distributed transactions (SAGA, 2PC)**.  
- Implement **event-driven architecture**.  

---

## **26. What are service meshes, and why use them?**  
- Examples: **Istio, Linkerd**.  
- **Features**: Traffic control, observability, security.  

---

## **27. How do you deploy applications across multiple cloud providers?**  
- Use **Terraform** for multi-cloud infrastructure.  
- Implement **Kubernetes federation**.  

---

## **28. How do you secure inter-service communication?**  
- **Mutual TLS (mTLS)** with Istio.  
- **JWT authentication** for APIs.  

---

## **29. What is chaos engineering, and why is it important?**  
- **Testing failures in production** to improve resilience.  
- Tools: **Gremlin, Chaos Monkey**.  

---

## **30. How do you design a failover mechanism for an application?**  
- **Active-passive or active-active setup**.  
- **Global load balancers and health checks**.  

---

### **Final Thoughts**  
These **30 system design questions** focus on **scalability, resilience, observability, and automation**, which are essential for **SRE/DevOps** roles. **Practice explaining concepts with real-world examples!** 🚀