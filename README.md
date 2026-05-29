# Apigee API Intelligence Dashboard — Canara Bank Production

21-panel Kibana dashboard monitoring Apigee API traffic, faults, latency,
and client behaviour across 3 production indices.

## Indices
| Index | Volume |
|---|---|
| `apigee-log-customerapi-*` | ~60K docs/day |
| `apigee-log-micgw-*` | ~12–16M docs/day |
| `apigee-log-prod-*` | ~2–3M docs/day |

## 21 Panels
| # | Panel | Type |
|---|---|---|
| 1 | Total API Hits | Metric |
| 2 | 4xx Errors | Metric |
| 3 | 5xx Errors | Metric |
| 4 | Fault Transactions | Metric |
| 5 | Avg Response Time | Metric |
| 6 | API Traffic Over Time | Area chart |
| 7 | Top APIs by Hits | Horizontal bar |
| 8 | Status Code Distribution | Donut |
| 9 | Top 4xx Errors by Proxy | Table |
| 10 | Top 5xx Errors by Proxy | Table |
| 11 | Hits by Environment | Bar |
| 12 | Top Client IPs | Table |
| 13 | Top Proxies by Request Count | Horizontal bar |
| 14 | HTTP Methods Distribution | Donut |
| 15 | Top Flow Names (Operations) | Table |
| 16 | Fault Transactions by Proxy | Table |
| 17 | Top Faulty Client IPs + Error Messages | Table |
| 18 | Fault Rate by Proxy % | Horizontal bar |
| 19 | Error Message Breakdown | Bar |
| 20 | API Proxy Health Scorecard | Table |
| 21 | Fault Rate Over Time by Proxy | Multi-line |

## Import Instructions
1. Go to Kibana → Stack Management → Saved Objects
2. Click Import → select `apigee-kibana-dashboard.ndjson`
3. Select Overwrite → Import → Done
4. Open dashboards:
   - `https://<your-kibana-host>/app/dashboards#/view/apigee-canara-prod`
   - `https://<your-kibana-host>/app/dashboards#/view/apigee-canara-micgw`
   - `https://<your-kibana-host>/app/dashboards#/view/apigee-canara-customerapi`

## Key Fields (Apigee OPDK Logstash pipeline)
| Field | Usage |
|---|---|
| `fault:"true"` | Fault filter |
| `status` | HTTP status code (string) |
| `proxy-method.keyword` | HTTP verb |
| `proxyName.keyword` | API proxy name |
| `proxyClientIp.keyword` | Client IP |
| `errorMessage.keyword` | Error message |
| `flowName.keyword` | Flow/operation name |
| `environment.keyword` | Apigee environment |

## Stack
- Apigee Edge OPDK 4.53.01
- Elasticsearch + Kibana 7.17
- Logstash (syslog pipeline)
