# ShipStation Fulfillment Dashboard

B2B order fulfillment analytics dashboard built with Streamlit and BigQuery.

## Features

- **KPI Cards**: Orders, fulfillment rate, avg days to ship, pending orders, shipping cost
- **Order Volume Trend**: 90-day trend with 7-day moving average
- **Fulfillment Rate Chart**: Daily fulfillment percentage vs target
- **Carrier Mix**: Donut chart showing carrier distribution
- **State Distribution**: Top states by order volume
- **Shipping Cost Analysis**: Average cost by carrier
- **Recent Orders Table**: Last 7 days of orders

## Data Source

Data comes from `mart_shipstation` dataset in BigQuery:
- `fct_order_shipment` - Denormalized order + shipment fact table
- `dim_daily_fulfillment` - Daily aggregations
- `dim_carrier_performance` - Carrier-level metrics
- `dim_state_distribution` - Geographic distribution

## Local Development

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Ensure you have GCP credentials configured:
```bash
gcloud auth application-default login
```

3. Run the dashboard:
```bash
streamlit run app.py
```

## Deployment (Streamlit Cloud)

1. Push to GitHub
2. Connect repo to Streamlit Cloud
3. Configure secrets in Streamlit Cloud dashboard:

```toml
[gcp_service_account]
type = "service_account"
project_id = "artful-logic-475116-p1"
private_key_id = "..."
private_key = "..."
client_email = "..."
client_id = "..."
auth_uri = "https://accounts.google.com/o/oauth2/auth"
token_uri = "https://oauth2.googleapis.com/token"
auth_provider_x509_cert_url = "https://www.googleapis.com/oauth2/v1/certs"
client_x509_cert_url = "..."
```

## Data Refresh

- Dashboard data is cached for 5 minutes (TTL=300)
- Source data syncs daily from ShipStation via Airbyte
- Mart tables can be refreshed on-demand via BigQuery
