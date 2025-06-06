# AWS Networking Components: Key Differences

| Feature           | NAT Gateway                                  | Internet Gateway                        | Transit Gateway                                  | Direct Connect                                    | VPC Endpoint                   |
|-------------------|----------------------------------------------|-----------------------------------------|--------------------------------------------------|---------------------------------------------------|-------------------------------|
| **Primary Use**   | Allow private subnets to access internet     | Enable VPC to communicate with internet | Central hub to connect VPCs and on-prem networks | Dedicated private network link from on-prem to AWS | Private connection to AWS services |
| **Type**          | Managed AWS service                          | Managed AWS resource                    | Managed AWS service                              | Physical connection/service                        | Managed AWS service            |
| **Direction**     | Outbound only (from private subnet)          | Inbound & outbound                      | Both                                             | Both                                              | Both (depends on endpoint)     |
| **Typical Use**   | Allow EC2 in private subnet to reach internet| Allow public subnet/EC2 to be reachable | Connects multiple VPCs, VPNs, DX, on-prem        | Secure, high-speed on-prem to AWS                  | Access S3, DynamoDB, or PrivateLink services from VPC |
| **Internet Access**| Yes (outbound for private subnets)          | Yes (public subnets, bi-directional)    | No (does not provide direct internet access)      | No (private, not for internet)                     | No                            |
| **Pricing**       | Hourly + data processed                      | Free                                    | Hourly + data processed                          | Port-hourly + data transfer usage                  | Interface: hourly + data, Gateway: free             |
| **Managed by AWS?**| Yes                                         | Yes                                     | Yes                                              | Yes (but requires physical setup)                  | Yes                          |
| **Common Example**| Private EC2 downloading updates              | Hosting a public website                | Multi-VPC, multi-account networking              | Hybrid cloud, low-latency workloads                | Secure S3 access without internet gateway           |
| **AWS Service Example** | NAT Gateway in a private subnet        | Attach IGW to VPC, route via IGW        | Attach VPCs/VPNs/DX to TGW                       | Set up DX at AWS location, connect to VPC          | S3 Gateway Endpoint, Interface Endpoint for SNS     |

---

## **Quick Reference**

- **NAT Gateway:**  
  Enables outbound internet for private subnets. No inbound connections allowed. Managed, scalable, and charged per hour and per GB.

- **Internet Gateway (IGW):**  
  Allows VPC resources (in public subnets) to reach and be reached from the internet. Free resource.

- **Transit Gateway (TGW):**  
  Central router to interconnect multiple VPCs, VPNs, and Direct Connect. Used for large, complex, multi-VPC or hybrid networks.

- **Direct Connect (DX):**  
  Dedicated physical link from your data center to AWS. Bypasses the public internet for performance/security.

- **VPC Endpoint:**  
  Connects your VPC privately to AWS services (like S3, DynamoDB) without internet/NAT gateway. Two types:
    - **Gateway Endpoint:** Free, for S3/DynamoDB.
    - **Interface Endpoint:** Paid, for most other AWS services (via PrivateLink).

---

**Summary Table:**

| Component         | Internet Access | On-premises/Private | Use Case                             |
|-------------------|----------------|---------------------|--------------------------------------|
| NAT Gateway       | Outbound only  | No                  | Private subnet → internet            |
| Internet Gateway  | In/Out         | No                  | Public subnet ↔ internet             |
| Transit Gateway   | No             | Yes                 | Multi-VPC, hybrid networks           |
| Direct Connect    | No             | Yes                 | On-premises ↔ AWS via private link   |
| VPC Endpoint      | No             | Yes (AWS services)  | Private VPC ↔ AWS service            |
