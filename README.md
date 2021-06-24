# Algorithmic Hedging System

## Conceptual Architecture / Model

![Algorithmic Hedging System Conceptual Architecture](res/ConceptualArchitecture.png)

## System Behaviour

- Data Source
    - Receive data
    - Publish raw for processing
- Data Processing
    - Filter irrrelevant data
    - Extract Transform Load (ETL)
    - Enqueue/Publish as simple events for processing (ex. spot price dependence only)
    - Store in operational data store
    - Continous analysis of data store
        - Enqueue/Publish as sophisticated events for processing (ex. historical price path dependence)
- Intelligence
    - Process events based on defined strategies
    - Construct preliminary orders
    - Enqueue/Publish orders
- Order Management
    - Compare against portfolio for sizing
    - Breakout large orders?
    - Route orders to exchange OR [Execution Management]()
    - Receive orders execution
    - Update portfolio
    - Enqueue/Publish execution result?
    - Update operational data store with execution result
- Execution Management ?
    - Get orders from [Order Management]()
    - Route orders to exchange as maker
    - Chase the market until filled
    - Signal Order Management with orders execution


<!-- ## System Components

- Data Ingestion
    - Data collectors
    - Filtering
    - Data processor (ETL)
    - Store/Publish
        - Operational Database
        - Downstream production
        - Archive
        - Non-prod env.
- Data Communication
    - Message-based
- Hedging Strategies
    - Naive hedging stat
    - Variance hedging stat
    - Per hedging instrument stat (perpetuals, inverse futures, futures)
- Order Management
    - Execution
- Metrics Collector -->


### Functional Requirements

1. Get market data: aquire relevant data and clean/prepare
    - download
    - filter
    - store
    - ETL as required
    - publish
1. Define hedging strategy: specify optimal trading rules based on market conditions
    - Optimal hedging instrument to use
    - Optimal hedging strategy to use
1. Get trade information
1. Create trade orders
1. Manage pending orders
1. Route / submit orders
1. Manage submitted orders



### Non-Functional Requirements

- Scalability: ability to cope and perform under expanding workload
    - Number of data feeds
    - Number of market instruments
    - Number of hedging strategies
    - Number of users?
- Performance: amount of work accomplished per unit of time and resources
    - Memory efficient
    - Processor efficient
    - Network efficient
    - Data processing efficient
- Modifiability: ease with which changes can be implemented
    - Changes to hedging strategies
    - Changes to hedging instruments
    - Changes to data processing
- Reliability: ability to stay accurate and dependable
    - Deterministic
    - Free of bugs?
- Auditability: ability to track and report the chain of events that lead to any action taken
- Fault tolerance: ability for continous proper operation after failure
    - State recovery after fault
- Interoperability: ease with which the system is able to function with others
    - Exhchanges
    - Wallet modification


## Proposed Action Plan (phase 1)

1. Build the Data Source and Data Processing layer
1. Prototype the Intelligence layer for backtesting and validating


## Deliverables (phase 1)

1. Data Source 
    - FTX data publisher module
    - OKEx data publisher module
    - Functional message-based communication component (ZMQ, Redis, else...)
1. Data Processing
    - Functional data store
    - ETL module (ex. spike removal, ...)
    - Store in operational data store
1. Intelligence
    - Historical data analysis processing (summary stats, volatility)
    - Backtesting (workbook? script?)
