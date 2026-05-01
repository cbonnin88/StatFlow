# StatFlow: Automated A/B Testing & Analytics Pipeline 📊

An end-to-end Python data pipeline that extracts live e-commerce data from a REST API, processes it with high-performance Polars, and automates statistical A/B testing using SciPy and Statsmodels.

## 🚀 Overview

Many A/B testing tutorials rely on static CSVs and manual pandas calculations. This project was built to simulate a **production-grade Analytics Engineering workflow**. It connects to a live API endpoint, cleans dirty data on the fly, applies robust statistical tests (accounting for unequal variances), and outputs interactive visualizations for stakeholders.

**Key Features:**
*   **Live API Extraction:** Pulls real-time cart data using the `requests` library.
*   **High-Speed Transformation:** Uses `polars` instead of pandas for memory-efficient feature engineering.
*   **Automated Experimentation:** Routes binary metrics (Conversion Rate) to a Z-Test and continuous metrics (Revenue) to Welch's T-Test.
*   **Interactive Visualizations:** Generates stakeholder-ready charts using `plotly`.

## 🛠️ Tech Stack

*   **Data Manipulation:** `polars` (for speed and lazy-evaluation principles), `numpy`
*   **Statistical Engine:** `scipy` (Welch's T-Test), `statsmodels` (Proportions Z-Test)
*   **Visualization:** `plotly`
*   **Data Ingestion:** `requests` (REST API)

## 🏗️ Pipeline Architecture

1.  **Extraction (The "E" in ELT):** Connects to the public DummyJSON API (`/carts`) to pull a live JSON payload of user shopping carts.
2.  **Transformation (Polars):** 
    *   Unpacks the nested JSON array.
    *   Dynamically assigns users to `Control` or `Variant` groups based on User ID logic.
    *   Engineers a continuous metric (`revenue`) and a binary metric (`converted`, defined as having >4 items in the cart).
3.  **Analysis (Stats Engine):**
    *   Calculates relative uplift and 95% statistical significance.
    *   Uses **Welch's T-Test** for revenue, as it does not incorrectly assume equal variances between the control and variant groups.
4.  **Visualization:** Compiles the mathematical outputs into an interactive Plotly dashboard (Box Plots for distribution analysis, Bar Charts for conversion rates).

## 💻 How to Run Locally

Because this project points to a free, public API, you can clone and run this pipeline immediately without needing any API keys or `.env` files.

**1. Clone the repository:**
```bash
git clone [https://github.com/YourUsername/StatFlow.git](https://github.com/YourUsername/StatFlow.git)
cd StatFlow
