# Arsitektur Infrastruktur Cloud

Diagram ini menunjukkan rancangan infrastruktur jaringan privat, subnet publik, subnet aplikasi, hingga database utama[cite: 3]:

```mermaid
flowchart TD
    User([Mahasiswa / Dosen / Staff]) --> DNS[DNS + CDN + WAF]
    
    subgraph VPC ["VPC Cloud Kampus - Jaringan Privat"]
        subgraph Public ["Public Subnet"]
            Bastion["Bastion / VPN Admin"]
            NAT["NAT Gateway"]
            ALB["Application Load Balancer"]
        end

        DNS --> ALB

        subgraph PrivateApp ["Private Subnet - Aplikasi"]
            Web1["Web/App Server AZ-1 (Autoscale)"]
            Web2["Web/App Server AZ-1 (Container)"]
            Web3["Web/App Server AZ-2 (Container)"]
            Cache["Cache Redis"]
        end

        ALB --> Web1 & Web2 & Web3
        Web1 & Web2 & Web3 --> Cache

        subgraph PrivateData ["Private Subnet - Data"]
            DB["DB Utama Managed SQL"]
            Replica["Read Replica"]
        end

        Web1 & Web2 & Web3 --> DB
        Cache --> DB
        DB --> Replica
    end
