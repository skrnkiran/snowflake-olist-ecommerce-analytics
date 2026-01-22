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



```mermaid
erDiagram
    FACT_ORDER_LINE ||--o{ DIM_CUSTOMER : "places"
    FACT_ORDER_LINE ||--o{ DIM_SELLER : "sold_by" 
    FACT_ORDER_LINE ||--o{ DIM_PRODUCT : "contains"
    
    FACT_ORDER_LINE {
        string order_id PK
        string order_item_id
        string product_id FK
        string seller_id FK
        string customer_id FK
        float price
        float freight_value
        float total_revenue
        timestamp order_purchase_ts
        int actual_delivery_days
        int delivery_delay_days
        boolean on_time_delivery_flag
    }
    
    DIM_CUSTOMER {
        string customer_id PK
        string customer_unique_id
        int customer_zip_code_prefix
        string customer_city
        string customer_state
    }
    
    DIM_SELLER {
        string seller_id PK
        int seller_zip_code_prefix
        string seller_city
        string seller_state
    }
    
    DIM_PRODUCT {
        string product_id PK
        string product_category_name_english
        float product_weight_g
        float product_length_cm
        float product_height_cm
        float product_width_cm
    }


