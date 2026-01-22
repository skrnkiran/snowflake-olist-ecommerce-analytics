# snowflake-olist-ecommerce-analytics
Production-grade Snowflake data warehouse analyzing Olist Brazilian e-commerce dataset (994K rows across 9 CSVs). Features medallion architecture, S3 external stages + Snowpipe, star schema modeling, RLS/masking security, clustering optimization, and supply chain KPIs.<br/>

🎯 Business Value
Olist serves 3K+ Brazilian cities. This pipeline delivers:<br/>
Seller performance tracking (OTIF, delivery delays)<br/>
Revenue leakage analysis (late delivery impact)<br/>
Product category margins (freight % optimization)<br/>
Customer concentration risk (state-level)<br/>
Supply chain efficiency (revenue per delivery day)<br/>

ER Diagram<br/>
![ERdiagram](https://github.com/user-attachments/assets/ade7945a-4f2c-4eee-a147-3b9f704a3e4b)

Data Workflow:<br/>
<img width="1185" height="345" alt="image" src="https://github.com/user-attachments/assets/f0557f04-1df3-4041-8766-86bb8da6980e" />

📈 Supply Chain KPIs Delivered:<br/>

| KPI               | Formula                            | Value          | Business Impact     |
| ----------------- | ---------------------------------- | -------------- | ------------------- |
| OTIF Rate         | AVG(on_time_delivery_flag)         | 78.2%          | Delivery SLA target |
| Avg Delivery      | AVG(actual_delivery_days)          | 11.2 days      | Benchmark           |
| Late Revenue Risk | SUM(total_revenue) WHERE delay > 0 | R$1.2M         | Cost optimization   |
| Freight %         | freight_value/price                | 23.5%          | Margin analysis     |
| Revenue/Day       | total_revenue/delivery_days        | Seller ranking |                     |


🛠️ Tech Stack

| Layer     | Technology                |               
| --------- | ------------------------- | 
| Storage   | AWS S3                    | 
| Ingestion | External Stage + Snowpipe |
| Warehouse | Snowflake                 | 
| Security  | RLS + Masking             |
| Modeling  | Star Schema               | 






