# walmart_sales_report
these repo is to showcase the sales and prediction analysis of walmart sales dataset 
# 🛒 Walmart Sales Analytics Dashboard

A full-stack Python analytics application for exploring, visualising, and forecasting Walmart retail sales across 45 stores (Feb 2010 – Oct 2012).

---

## 📌 Overview

This project transforms a raw Walmart weekly sales CSV dataset into an interactive analytics dashboard with a REST API backend and a Python-native web frontend. It covers KPI reporting, store benchmarking, holiday impact analysis, feature correlation, and machine learning-based sales forecasting — all in pure Python.

---

## 🏗️ Architecture

```
Walmart_Sales.csv
       │
       ▼
┌─────────────────────┐        HTTP / JSON        ┌──────────────────────────┐
│   FastAPI Backend   │ ◄────────────────────────► │   Streamlit Frontend     │
│   (port 8000)       │                            │   (port 8501)            │
│                     │                            │                          │
│  data_loader.py     │                            │  6 interactive pages     │
│  ├─ Pandas/NumPy    │                            │  Plotly charts           │
│  └─ scikit-learn    │                            │  httpx API client        │
│  models.py          │                            └──────────────────────────┘
│  main.py            │
└─────────────────────┘
```

---

## 📂 Project Structure

```
walmart_sales/
├── Walmart_Sales.csv          # Source dataset (6,435 rows, 45 stores)
├── requirements.txt           # Python dependencies
├── run.py                     # One-command launcher (starts both servers)
├── Walmart_Sales_Report.docx  # Project report (this document)
├── README.md                  # This file
├── backend/
│   ├── __init__.py
│   ├── data_loader.py         # All Pandas data processing & aggregations
│   ├── models.py              # Pydantic response schemas
│   └── main.py                # FastAPI app with 8 REST endpoints
└── frontend/
    └── app.py                 # Streamlit dashboard (6 pages)
```

---

## 📊 Dataset

| Field | Type | Description |
|-------|------|-------------|
| `Store` | Integer | Store identifier (1–45) |
| `Date` | Date | Week ending date (DD-MM-YYYY) |
| `Weekly_Sales` | Float | Total store sales in USD |
| `Holiday_Flag` | 0/1 | 1 = holiday week (Super Bowl, Labour Day, Thanksgiving, Christmas) |
| `Temperature` | Float (°F) | Average regional temperature |
| `Fuel_Price` | Float ($/gal) | Regional fuel cost |
| `CPI` | Float | Consumer Price Index |
| `Unemployment` | Float (%) | Regional unemployment rate |

**Size:** 6,435 records · 45 stores · 143 weeks · 8 columns

---

## 🚀 Quick Start

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Launch (both servers at once)

```bash
python run.py
```

| Service | URL |
|---------|-----|
| 🌐 Dashboard | http://localhost:8501 |
| ⚙️ API | http://localhost:8000 |
| 📖 API Docs | http://localhost:8000/docs |

### 3. Or run separately

```bash
# Backend only
uvicorn backend.main:app --reload --port 8000

# Frontend only
streamlit run frontend/app.py
```

---

## 🔌 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/kpis` | Overall KPI summary |
| `GET` | `/api/trend?store=N` | Weekly sales trend (all or per store) |
| `GET` | `/api/stores` | All stores ranked by total sales |
| `GET` | `/api/holiday` | Holiday vs non-holiday sales |
| `GET` | `/api/correlation` | Pearson correlation matrix |
| `GET` | `/api/scatter/{feature}` | Feature vs sales scatter data |
| `GET` | `/api/forecast?store=N&weeks_ahead=12` | Linear regression forecast |

All endpoints return JSON. Interactive Swagger docs available at `/docs`.

---

## 📈 Dashboard Pages

| Page | Key Features |
|------|-------------|
| **📊 Overview** | 4 KPI cards, Top-10 store bar chart, all-store sales area trend, dataset stats |
| **📈 Sales Trends** | Store filter, weekly line chart, 4-week rolling average, monthly bar chart |
| **🏪 Store Comparison** | Total & avg sales bar charts, full data table across all 45 stores |
| **🎉 Holiday Impact** | Holiday vs non-holiday bar + donut chart, +7.84% avg sales uplift |
| **🔥 Correlation** | Pearson heatmap (5×5), OLS scatter plot for any feature vs sales |
| **🔮 Forecast** | Linear regression with historical fit + N-week ahead forecast chart & table |

---

## 📦 Tech Stack

| Layer | Library | Version |
|-------|---------|---------|
| Backend API | FastAPI | 0.111.0 |
| API Server | Uvicorn | 0.29.0 |
| Data Processing | Pandas | 2.2.2 |
| Numerics | NumPy | 1.26.4 |
| ML / Forecast | scikit-learn | 1.4.2 |
| Charts | Plotly | 5.22.0 |
| Frontend UI | Streamlit | 1.35.0 |
| HTTP Client | httpx | 0.27.0 |
| Validation | Pydantic | 2.7.1 |

> 100% Python — no JavaScript, HTML, or CSS required.

---

## 📋 Key Findings

- **$6.74B** total revenue across all 45 stores (2010–2012)
- **Store 20** is the top performer at $301.4M cumulative sales
- **Holiday weeks** generate **+7.84%** higher average sales than non-holiday weeks
- **Unemployment** has the strongest (negative) correlation with sales (r = −0.106)
- **2011** was the peak revenue year at $2.45B

---

## 📄 Project Report

A full project report with metrics, analysis, and findings is available in [`Walmart_Sales_Report.docx`](Walmart_Sales_Report.docx).

---

## 📝 License

This project is for educational and analytical, project  purposes. Dataset sourced from public Walmart sales data (Kaggle).
