# snowflake-olist-ecommerce-analytics
Production-grade Snowflake data warehouse analyzing Olist Brazilian e-commerce dataset (994K rows across 9 CSVs). Features medallion architecture, S3 external stages + Snowpipe, star schema modeling, RLS/masking security, clustering optimization, and supply chain KPIs.<br/>

🎯 Business Value
Olist serves 3K+ Brazilian cities. This pipeline delivers:<br/>
Seller performance tracking (OTIF, delivery delays)<br/>
Revenue leakage analysis (late delivery impact)<br/>
Product category margins (freight % optimization)<br/>
Customer concentration risk (state-level)<br/>
Supply chain efficiency (revenue per delivery day)<br/>

PROJECT WORKFLOW:
```mermaid
flowchart TD
    A[1 Clone Repo<br/>git clone ...] 
    A --> B[2 Setup Snowflake<br/>2 Warehouses<br/>3 Databases]
    B --> C[3 S3 Stage<br/>@OLIST_S3_STAGE<br/>s3_integration]
    C --> D[4 Upload CSVs<br/>9 Files → S3<br/>994K rows]
    D --> E[5 Bronze Load<br/>COPY INTO x9<br/>OLIST_RAW.MYSCHEMA]
    E --> F[6 Silver Cleanse<br/>TRY_TO_*<br/>OLIST_STAGE.PUBLIC]
    F --> G[7 Gold Schema<br/>FACT + 3 DIMs<br/>OLIST_MART.PUBLIC]
    G --> H[8 Security<br/>RLS + Masking]
    H --> I[9 Clustering<br/>Performance Opt]
    I --> J[✅ Supply Chain KPIs<br/>Live SQL Queries]
    
    classDef setup fill:#e3f2fd
    classDef ingest fill:#e8f5e8
    classDef model fill:#fff3e0
    classDef secure fill:#fce4ec
    classDef live fill:#f3e5f5
    
    class A,B,C setup
    class D,E ingest
    class F,G model
    class H,I secure
    class J live



