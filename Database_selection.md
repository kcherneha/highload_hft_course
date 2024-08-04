### Selection of Data Storage Models for HFT Market Maker System

### 1. Snapshots (Cassandra)
#### Requirements:
- **High Write Throughput**: Frequent updates to store real-time snapshots.
- **Horizontal Scalability**: Ability to handle increasing data volume and transaction rates.
- **High Availability**: Ensure data is available even during node failures.

#### Key Purpose:

To store real-time snapshots of the market data, including the state of order books, trades, and other financial information. Details:

1. **Real-Time Market State Storage**:
   - The snapshots database captures the current state of the market at any given moment, including the latest prices, trade volumes, and the order book depth.

2. **High Write Throughput**:
   - In an HFT environment, data about trades and order book changes is generated at a very high rate.

3. **Disaster Recovery and Fault Tolerance**:
   - By capturing the state of the market at frequent intervals, the snapshots database aids in quick recovery in case of system failures. Cassandra’s replication features ensure that data is available even if some nodes fail.

4. **Data Analysis and Backtesting**:
   - Snapshots of market data can be used to backtest trading algorithms against recent market conditions. This helps in refining strategies based on near-real-time historical data.

#### Justification for Choosing Cassandra:

- **Scalability**: Cassandra is highly scalable, making it capable of handling the large volumes of data generated by HFT operations.
- **Availability**: With its decentralized architecture, Cassandra ensures high availability and fault tolerance, which are critical for an HFT system that requires continuous uptime.
- **Write Optimization**: The database is optimized for high-speed write operations, aligning with the need to frequently update the market state.


### 2. Historical Data (Time Series DB or again Cassandra - see p.4)
#### Requirements:
- **Time-Based Data**: Efficient storage and retrieval of time-series data.
- **High Insertion Rate**: Capable of handling a high rate of incoming data points.
- **Query Efficiency**: Optimized for queries over specific time ranges.

#### Key Purpose:
For future analytics and reviewing algorithms of trading.

#### Storage Model:
**Time Series Database (InfluxDB, TimescaleDB)**

#### Justification:
- **Optimized for Time-Series Data**: Time-series databases are specifically designed to handle sequential, time-stamped data, making them ideal for historical market data.
- **High Insertion Rate**: They can handle large volumes of data points with minimal latency.
- **Efficient Queries**: These databases provide optimized functions for querying and analyzing time-series data, such as rollups, aggregations, and downsampling.

### 3. Payment and Settlement Systems (RDBMS) - if needed for us (maybe in scope of this project will be implemented by outer HFT-board actor)
#### Requirements:
- **Transactionality**: Ensure ACID (Atomicity, Consistency, Isolation, Durability) properties for financial transactions.
- **Relational Data**: Manage relationships between different entities (e.g., accounts, transactions).

#### Storage Model:
**Relational Database Management System (PostgreSQL, MySQL)**

#### Justification:
- **ACID Compliance**: RDBMS provides strong transactional guarantees necessary for financial operations.
- **Relational Data Handling**: Ideal for managing complex relationships between entities and enforcing data integrity.
- **Mature Ecosystem**: Well-established tools and practices for backup, recovery, and security.

### Summary
#### Selected Storage Models:
- **Snapshots**: Apache Cassandra (NoSQL Column-Family Database)
- **Historical Data**: InfluxDB or TimescaleDB (Time Series Database)
- **Payment and Settlement Systems**: PostgreSQL or MySQL (Relational Database Management System)