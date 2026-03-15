# Hospitality Industry: Revenue Optimization Analysis for a Multi-City Hotel Chain

## The Challenge
Atliq Hotels operates multiple hotels across several cities, providing room and hospitality services to customers. The key challenge was to identify hotels with low occupancy rates across different cities and understand the factors affecting their performance. Previously, the company relied on manual analysis and traditional reporting methods, which were not effective in identifying patterns across large booking datasets. Therefore, the objective was to use data analytics to analyze booking patterns, improve booking efficiency, and optimize overall revenue.

---


# The Solution

To address the revenue decline and low occupancy challenges, I developed a **data analytics solution using Power BI** to analyze hotel performance across multiple cities. First, I collected booking, revenue, customer rating, and hotel capacity datasets. The raw data was cleaned by handling missing values, standardizing formats, and detecting outliers to ensure reliable analysis. Next, I designed a **Star Schema data model** to efficiently structure the data. In this model, the **fact tables store booking and revenue information**, while the **dimension tables contain supporting details such as city, date, and room category**. This approach improves query performance and simplifies analytical reporting.

After building the data model, I created **business KPIs using DAX formulas** to monitor hotel performance and identify revenue opportunities. These KPIs track important hospitality metrics such as:

- Occupancy Rate  
- ADR (Average Daily Rate)  
- RevPAR (Revenue per Available Room)  
- Cancellation Rate  
- Realisation Rate  
- Booking Contribution by Platform  
- Week-over-Week Revenue Growth  

Using these metrics, I developed an **interactive Power BI dashboard** that enables analysis at:

- City Level
- Property Level
- Booking Platform Level

The dashboard helps identify underperforming hotels, analyze booking platform performance, and monitor revenue trends.

To ensure transparency and reproducibility, I also documented **all KPI formulas used in the analysis**.

---

# Results

### Identification of Underperforming Properties
The dashboard highlights cities and hotels with low occupancy rates, enabling targeted improvement strategies.

### Revenue Leakage Detection
The analysis quantified revenue losses caused by **cancellations and no-shows**, helping identify inefficiencies in the booking process.

### Booking Channel Performance Insights
The analysis compared **Online Travel Agencies (OTAs) and direct bookings**, helping evaluate how commission costs impact profitability.

### Demand Pattern Discovery
The analysis revealed clear differences between **weekday and weekend demand**, helping inform dynamic pricing and promotional strategies.

---

# Key Achievements

### Built an End-to-End Hospitality Revenue Analytics Dashboard
Developed a complete workflow from data cleaning and modeling to interactive dashboard creation.

### Implemented a Star Schema Data Model
Structured the dataset using a star schema to improve query performance and simplify business analysis.

### Created 25+ Business KPIs Using DAX
Developed metrics including:

- Occupancy %
- ADR
- RevPAR
- Realisation %
- Week-over-Week Revenue Change
- Booking Contribution by Platform

(**All KPIs and Formulas are listed on below of this page**)

---

# Key insights discovered from the analysis include:

- Some cities consistently show **lower occupancy rates**, indicating demand imbalance.
- **OTA platforms generate higher booking volume**, but commission costs affect profitability.
- **Weekend demand is significantly higher than weekday demand**, suggesting opportunities for weekday promotions.
- **Cancellations and no-shows lead to revenue leakage**, highlighting the need for improved booking policies.

---

# Business Impact

By implementing the insights and strategies identified from the analysis, the hotel business can significantly improve operational performance and profitability.

### Profit Growth Opportunity
Applying data-driven pricing strategies and demand-based promotions can potentially **increase the overall profit rate by up to 30%**.

### Reduction in OTA Booking Cancellations
Improving booking policies such as partial advance payments, reminder notifications, and flexible rescheduling options can **reduce OTA booking cancellations by approximately 25%**.

### Dynamic Pricing Strategy
Using key metrics such as **ADR and RevPAR**, the business can adjust room prices based on demand patterns (weekday vs weekend) to maximize revenue.

### Improved Booking Efficiency
Monitoring occupancy rates and booking platform performance enables better allocation of rooms and marketing strategies.

### Real Time Monitoring
The Power BI dashboard allows hotel management to continuously monitor key KPIs such as **Occupancy %, Revenue, ADR, RevPAR, and Realisation %**, helping them make faster and more informed business decisions.

---

# Tools & Technologies

- Power BI
- DAX
- Power Query
- Data Modeling (Star Schema)
- Exploratory Data Analysis (EDA)

---

# Dashboard

https://app.powerbi.com/groups/me/reports/d4af6be0-a1d9-4c71-93f1-9cba3e437f56/ReportSectionce2063a216d8e001051e?experience=power-bi

---

# Author

**Mathan Ponraj**

Junior Data Scientist | Data Analyst  
Skills: Python, SQL, Machine Learning, Power BI, Data Analytics

---

# Key Metrics and Formulas

## Core Performance Metrics

### 1. Revenue  
Total realized revenue from bookings.
```DAX
Revenue = SUM(fact_bookings[revenue_realized])
```

### 2. Total Bookings  
Total number of bookings recorded.
```DAX
Total Bookings = COUNT(fact_bookings[booking_id])
```

### 3. Total Capacity  
Total available rooms across all hotels.
```DAX
Total Capacity = SUM(fact_aggregated_bookings[capacity])
```

### 4. Total Successful Bookings  
Total successfully occupied rooms.
```DAX
Total Successful Bookings = SUM(fact_aggregated_bookings[successful_bookings])
```

### 5. Occupancy %  
Percentage of rooms occupied out of total capacity.
```DAX
Occupancy % = DIVIDE([Total Successful Bookings], [Total Capacity], 0)
```

### 6. Average Rating  
Average customer rating.
```DAX
Average Rating = AVERAGE(fact_bookings[ratings_given])
```

### 7. No of Days  
Total number of days in selected period.
```DAX
No of Days = DATEDIFF(MIN(dim_date[date]), MAX(dim_date[date]), DAY) + 1
```

### 8. Total Cancelled Bookings
```DAX
Total Cancelled Bookings =
CALCULATE([Total Bookings], fact_bookings[booking_status] = "Cancelled")
```

### 9. Cancellation %
```DAX
Cancellation % =
DIVIDE([Total Cancelled Bookings], [Total Bookings])
```

### 10. Total Checked Out
```DAX
Total Checked Out =
CALCULATE([Total Bookings], fact_bookings[booking_status] = "Checked Out")
```

### 11. Total No Show Bookings
```DAX
Total No Show Bookings =
CALCULATE([Total Bookings], fact_bookings[booking_status] = "No Show")
```

### 12. No Show Rate %
```DAX
No Show Rate % =
DIVIDE([Total No Show Bookings], [Total Bookings])
```

### 13. Realisation %
Percentage of bookings successfully completed.
```DAX
Realisation % =
1 - ([Cancellation %] + [No Show Rate %])
```
### 14. Booking % by Platform
Percentage contribution of each booking platform (OTA vs Direct).
```DAX
Booking % by Platform =
DIVIDE(
    [Total Bookings],
    CALCULATE([Total Bookings], ALL(fact_bookings[booking_platform]))
) * 100
```

### 15. Booking % by Room Class
Contribution of each room category.
```DAX
Booking % by Room Class =
DIVIDE(
    [Total Bookings],
    CALCULATE([Total Bookings], ALL(dim_rooms[room_class]))
) * 100
```




### 16. ADR (Average Daily Rate)
Average revenue earned per booked room.
```DAX
ADR = DIVIDE([Revenue], [Total Bookings], 0)
```

### 17. RevPAR (Revenue Per Available Room)
Revenue generated per available room.
```DAX
RevPAR = DIVIDE([Revenue], [Total Capacity])
```

### 18. DBRN (Daily Booked Room Nights)
Average rooms booked per day.
```DAX
DBRN = DIVIDE([Total Bookings], [No of Days])
```

### 19. DSRN (Daily Sellable Room Nights)
Average rooms available for sale per day.
```DAX
DSRN = DIVIDE([Total Capacity], [No of Days])
```

### 20. DURN (Daily Utilized Room Nights)
Average rooms successfully utilized per day.
```DAX
DURN = DIVIDE([Total Checked Out], [No of Days])
```

### 21. Revenue WoW Change %
```DAX
Revenue WoW Change % =
VAR selv =
    IF(HASONEFILTER(dim_date[wn]),
       SELECTEDVALUE(dim_date[wn]),
       MAX(dim_date[wn]))
VAR revcw =
    CALCULATE([Revenue], dim_date[wn] = selv)
VAR revpw =
    CALCULATE([Revenue],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1))
RETURN
DIVIDE(revcw, revpw, 0) - 1
```
### 22. Occupancy WoW Change %

```DAX
Occupancy WoW Change % =
VAR selv =
    IF(
        HASONEFILTER(dim_date[wn]),
        SELECTEDVALUE(dim_date[wn]),
        MAX(dim_date[wn])
    )
VAR curr_week =
    CALCULATE([Occupancy %], dim_date[wn] = selv)
VAR prev_week =
    CALCULATE(
        [Occupancy %],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1)
    )
RETURN
DIVIDE(curr_week, prev_week, 0) - 1
```

### 23. ADR WoW Change %

```DAX
ADR WoW Change % =
VAR selv =
    IF(
        HASONEFILTER(dim_date[wn]),
        SELECTEDVALUE(dim_date[wn]),
        MAX(dim_date[wn])
    )
VAR curr_week =
    CALCULATE([ADR], dim_date[wn] = selv)
VAR prev_week =
    CALCULATE(
        [ADR],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1)
    )
RETURN
DIVIDE(curr_week, prev_week, 0) - 1
```

### 24. RevPAR WoW Change %

```DAX
RevPAR WoW Change % =
VAR selv =
    IF(
        HASONEFILTER(dim_date[wn]),
        SELECTEDVALUE(dim_date[wn]),
        MAX(dim_date[wn])
    )
VAR curr_week =
    CALCULATE([RevPAR], dim_date[wn] = selv)
VAR prev_week =
    CALCULATE(
        [RevPAR],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1)
    )
RETURN
DIVIDE(curr_week, prev_week, 0) - 1
```

### 25. Realisation WoW Change %

```DAX
Realisation WoW Change % =
VAR selv =
    IF(
        HASONEFILTER(dim_date[wn]),
        SELECTEDVALUE(dim_date[wn]),
        MAX(dim_date[wn])
    )
VAR curr_week =
    CALCULATE([Realisation %], dim_date[wn] = selv)
VAR prev_week =
    CALCULATE(
        [Realisation %],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1)
    )
RETURN
DIVIDE(curr_week, prev_week, 0) - 1
```


### 26. DSRN WoW Change %

```DAX
DSRN WoW Change % =
VAR selv =
    IF(
        HASONEFILTER(dim_date[wn]),
        SELECTEDVALUE(dim_date[wn]),
        MAX(dim_date[wn])
    )
VAR curr_week =
    CALCULATE([DSRN], dim_date[wn] = selv)
VAR prev_week =
    CALCULATE(
        [DSRN],
        FILTER(ALL(dim_date), dim_date[wn] = selv - 1)
    )
RETURN
DIVIDE(curr_week, prev_week, 0) - 1
```

---

---

