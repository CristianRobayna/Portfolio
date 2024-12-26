# Airbnb Price Analysis in Zurich
## Project Overview

This project analyzes Airbnb prices in Zurich using data sourced from [Inside Airbnb](https://insideairbnb.com/zurich/). The analysis was performed using Power BI, focusing on key factors that affect accommodation pricing. The dataset includes three primary tables: **calendar**, **listing**, and **review**. These were combined and transformed using Power Query to derive meaningful insights.

The goal of the analysis is to understand the pricing trends and factors that influence Airbnb accommodation costs in Zurich, with a specific focus on location, property type, and other relevant factors such as ratings and room availability.

## Key Features

- **Price by Area:** Analysis of the average price per area in Zurich's 12 districts (Kreis).
- **Accommodation Count by Area:** Number of Airbnb listings available in each district.
- **Score by Area:** Breakdown of average guest ratings by district.
- **Price by Property Type:** Analysis of pricing variations based on property types (entire home, private room, shared room).
- **Price by Zone:** Mapping of price trends across different zones in Zurich.
- **Bedroom Percentage per Zone:** Analysis of how the distribution of bedrooms varies across different zones.

## Tools Used

- **Power BI:** Data visualization and interactive report generation.
- **Power Query (in Power BI):** Used for data transformation, including cleaning and merging datasets.
- **Inside Airbnb Data:** Data from [Inside Airbnb](https://insideairbnb.com/zurich/) for Zurich, including calendar, listing, and review information.

## Data Sources

The data used in this project was sourced from Inside Airbnb's Zurich dataset, which provides publicly available Airbnb listing data, including:

- **Listing Data:** Details of Airbnb listings (e.g., price, location, property type).
- **Calendar Data:** Availability and price details for each listing over time.
- **Review Data:** Guest reviews and ratings for each listing.

You can access the data directly at [Inside Airbnb Zurich](https://insideairbnb.com/zurich/).

## Data Cleaning and Transformation

The raw data required preprocessing to make it suitable for analysis. Key transformations included:

- **Price Column Transformation:** The price column was initially stored as text (due to the dollar sign and use of periods instead of commas). This was transformed using Power Query to convert the price to a numerical format by:
    - Removing the dollar sign.
    - Replacing periods with commas.
    - Converting the column to a number type for accurate analysis.
- **Merging Databases:** The three datasets (calendar, listing, and review) were connected using the **ID** field to create a unified dataset for analysis.
- **Handling Missing Data:** Any missing or incomplete data were handled, ensuring the analysis remained robust and accurate.

## Analysis Insights

### 1. **Price by Area (Kreis)**

- The analysis showed that Wintherthur (Kreis 1) have significantly higher prices compared to suburban districts.
- Price variation across the 12 districts of Zurich was visualized using Power BI maps and charts.

### 2. **Accommodation Count per Area**

- The number of listings varies widely across districts. Central Zurich (Kreis 1, Kreis 2) has a less density of listings, while some outlying areas have more listings available. This is counting the Kreis as same a region and not counting the area of them, which could cause more density in Kreis 1 and Kreis 2 which are smaller than other Kreis.

### 3. **Price by Property Type**

- **Entire Homes and Entire serviced apartment** are priced significantly higher than **Private Rooms** and **Entire rental unit**.

### 4. **Price per Zone**

- Zones closer to key landmarks such as Lake Zurich, the University of Zurich, and Bahnhofstrasse are more expensive compared to other areas. 

### 5. **Score per Area**

- Guest ratings varied across areas, with certain districts having higher average ratings. This was analyzed in relation to price to see if better-rated accommodations also tended to be more expensive.

### 6. **Percentage of Bedrooms per Zone**

- The analysis showed varying distributions of listings with different numbers of bedrooms across Zurich. This insight helps understand the general accommodation offerings in each zone.

## Visualizations

The Power BI report contains the following key visualizations:

- **Map Visualizations** for price and accommodation distribution across the 12 districts.
- **Bar Charts** comparing average prices by property type and area.
- **Line Graphs** showing price trends over time.
- **Heat Maps** illustrating pricing patterns across Zurich zones.
- **Pie Charts** representing bedroom distribution across areas.

## Future Enhancements

- **Dynamic Price Prediction:** Implement machine learning algorithms to predict future pricing trends based on variables like location, property type, and seasonality.
- **Guest Feedback Analysis:** Integrate guest reviews to assess how guest satisfaction impacts pricing, especially for highly-rated listings.
- **Comparison with Other Cities:** Expand the analysis to include comparison with Airbnb pricing in other Swiss cities or international locations.

## Contribution

Contributions are welcome! If you have suggestions or improvements for this analysis, feel free to open an issue or submit a pull request.

## Acknowledgments

- Thanks to [Inside Airbnb](https://insideairbnb.com/zurich/) for providing the dataset.
- Thanks to Power BI for enabling intuitive data visualization.
- Data preprocessing tools in Power Query and DAX were instrumental in transforming the raw data for analysis.
