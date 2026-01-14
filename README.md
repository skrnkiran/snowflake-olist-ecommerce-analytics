# snowflake-olist-ecommerce-analytics



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


