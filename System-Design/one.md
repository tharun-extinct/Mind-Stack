> <center> "Anyone can write code that works. <br> System Design is what makes it work for a million people at once." <center>

<br><br>

---

<br><br>


```mermaid

flowchart TD
    %% Define color classes based on the image
    classDef redBox fill:#ff8b8b,stroke:#fff,stroke-width:1px,color:#000;
    classDef blueBox fill:#5b9bd5,stroke:#fff,stroke-width:1px,color:#000;
    classDef greenBox fill:#70ad47,stroke:#fff,stroke-width:1px,color:#000;
    classDef brownBox fill:#c69022,stroke:#fff,stroke-width:1px,color:#000;
    classDef purpleBox fill:#a572ff,stroke:#fff,stroke-width:1px,color:#000;
    classDef orangeBox fill:#ed7d31,stroke:#fff,stroke-width:1px,color:#000;
    
    %% Top Node
    Start([System Design]):::redBox
    
    %% Section 1
    subgraph S1 [1 - Foundations]
        direction LR
        1A[What is System Design]:::blueBox --> 1B[Components]:::blueBox
        1B --> 1C[Data vs Compute<br>Intensive]:::blueBox
        1C --> 1D[Functional & Non-<br>Functional]:::blueBox
    end
    
    %% Section 2
    subgraph S2 [2 - Communication]
        direction LR
        2A[DNS]:::greenBox --> 2B[APIs]:::greenBox
        2B --> 2C[REST in Detail]:::greenBox
    end
    
    %% Section 3
    subgraph S3 [3 - Data Layer]
        direction LR
        3A[SQL]:::brownBox --> 3B[NoSQL]:::brownBox
        3B --> 3C[Cache]:::brownBox
    end
    
    %% Section 4
    subgraph S4 [4 - Scaling & Distribution]
        direction LR
        4A[Load Balancer]:::purpleBox --> 4B[Replication]:::purpleBox
        4B --> 4C[Partitioning]:::purpleBox
        4C --> 4D[CAP Theorem]:::purpleBox
    end
    
    %% Section 5
    subgraph S5 [5 - Reliability & Operations]
        direction LR
        5A[Message Queue]:::orangeBox --> 5B[Fault Tolerance]:::orangeBox
        5B --> 5C[Monitoring]:::orangeBox
    end
    
    %% Bottom Node
    End([Case Study: Streaming<br>App]):::redBox

    %% Flow connections between subgraphs
    Start --> S1
    S1 --> S2
    S2 --> S3
    S3 --> S4
    S4 --> S5
    S5 --> End

```


<br><br>



# System Design

> System = Components + Common Goal 


 

Components of System Design

1. Databases
    - No Sql
    - SQL

> To connect the DB and App - IP or HTTP or TCP

2. Application Code
    - APIs -> Endpoints

    > Get -> https://edge-op.com/login

3. Client Applications


  Client <---------> Server [Application Code] <----------> Database

4. Cache



5. Load Balancer

6. Message Queue

    Ordering 
    Inventory Update --> Delivery --> Mail /SMS

    > This is where message Broker like Kafka comes into picture (Asynchronous)

```mermaid

flowchart LR
    %% Invisible nodes to represent the incoming and outgoing floating arrows
    Incoming(( ))
    Outgoing(( ))
    
    style Incoming fill:none, stroke:none
    style Outgoing fill:none, stroke:none

    %% Main Nodes
    Incoming --> Order[Order]
    
    %% Forward and backward straight/curved white arrows
    Order --> SMS["SMS ✔"]
    SMS --> Order
    
```




7. Monitoring & Logs

- Stack trace
- Reproduce those errors in order to fix them




Types of Application

- Data Intensive Application
- Compute Intensive Application




## Data Intensive Appilcation

Data -> Store, Gather, Move, Add


Platform like Instagram Feed, Whatsapp msgs, Log processing System

Database Response
Network calls
Server 


#### Concerns

- How fast can we read the data?
- How safety are we going to store the data?

- How many users can access it simultaneously?

- what happens if Machine dies?


#### Components to improve DIA

- Databases 
- Caching
- Replication
- Sharding
- Consistency


## Compute Intensive Application

Challenge -> Heavy computation

-> CPU /GPU Bound

Examples:  
- Image Processing
- Video Rendering
- ML Model Training
- Cryptography


#### Concerns

- How fast can we compute?
- Can we parallelize this work?
- How to reduce the computational cost? (Algorithm Optimization)
- Can we use GPU instead of CPU?





