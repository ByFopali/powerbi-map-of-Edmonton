Hi! It's a guide how to create a shape map in PowerBI. ALL FILES ARE ATTACHED TO THIS REPO, SO YOU SHOULDN'T FOLLOW FIRST 2 STEPS.

1. It’s my data about real estate in Edmonton for the start of 2025. Choose whatever you want. Download in CSV format.
https://data.edmonton.ca/City-Administration/Property-Assessment-Data-Current-Calendar-Year-/q7d6-ambg/about_data
OR
https://data.edmonton.ca/City-Administration/Residential-Assessment-Class/c7sw-npqx/data_preview

2. Download a map of Edmonton in geojson format:
https://data.edmonton.ca/City-Administration/City-of-Edmonton-Neighbourhoods/65fr-66s6/about_data
In this geojson you have to replace all "neighbourhood_number" into "neighbourhood_id" and "descriptive_name" into "neighbourhood". Save this file.
Then transform into topojson using https://mapshaper.org/

![Image](https://github.com/user-attachments/assets/b16d5438-da8a-4c12-83c2-87e06cbe64e7)

3. Next I have to clean data to get rid of the outliers (low and high prices), inconsistencies and unnecessary columns (in my case). Got something like this. (1st method)

![Image](https://github.com/user-attachments/assets/c146f250-80e6-4bd1-ac15-2ae14a39464f)

Also I tried to use SQL to extract data I need and exported it into CSV file again. (2nd method) Choose whatever method you like. Software I used is BeaverDB.

![Image](https://github.com/user-attachments/assets/e805f3fb-1652-44b7-82fc-e255eeb3d8a8)

```
SELECT
neighbourhood_id,
neighbourhood,
ROUND(AVG(assessed_value), 0) AS avg_value
FROM Residential_Assessment_Class
WHERE neighbourhood_id != '' AND assessed_value > 75000 AND assessed_value < 1000000
GROUP BY neighbourhood_id
```

4. After we prepared all data, we can visualize it. Place a “shape map” and “table” on the canvas. To activate “shape map” go to the settings → Preview features → Activate “Shape map Visual”.

![Image](https://github.com/user-attachments/assets/f97a834f-f658-4b2f-b850-d3f5e859e0c1)

5. Click the “table” and select “neighbourhood” from data on the right side. Change size as you want.

![Image](https://github.com/user-attachments/assets/2b245109-0cdf-47d9-9a74-bea1b159e130)

7. Click the “Shape map” and select “neighbourhood_id” (for Location) and “assessed_value” (for color saturation) from data on the right side. Click “assessed_value” and select  “Average”. Change size as you want.

![Image](https://github.com/user-attachments/assets/5433cc9d-6dad-4394-8da5-d8136c7b067c)

8. Now, it’s time to change the map. Click “Format your visual” (marked with red arrow below). Select “Map settings” and choose Custom map type and “Browse” then. Select json file attached to this repo or use your own. Also you can to some experiments with “Zoom”. I enabled “Auto Zoom” for more interaction.

![Image](https://github.com/user-attachments/assets/8b21eb23-94df-4f05-badb-80c03e7d376a)

9. Here we are. We see our map has changed and we can see neighbourhood name and assessed value for each neighbourhood in the Edmonton.

![Image](https://github.com/user-attachments/assets/68ded9d4-4109-4792-aa15-6755a39fbf7b)

10. Also you can change the color schema of the map in “Format your visual” → “Fill colors”

![Image](https://github.com/user-attachments/assets/0d8f5dc2-5f68-4a9d-843b-9a6553811787)

11. Next, select table and column assessed_value and choose “Average” for this field to group the data (check screenshot).

![Image](https://github.com/user-attachments/assets/38228e04-dac5-41d2-8774-85ccf2ce2d2d)

12. Then Click “Condition formatting”  → “Background color” and copy colors from map formatting. Apply these changes for “neighbourhood” and “Average of assessed_value” separately. Both of them should be based on “Average of assessed_value” and summarized by average.

![Image](https://github.com/user-attachments/assets/69c8f024-adf4-45ac-ae63-e7910dec6a12)

Result:

![Image](https://github.com/user-attachments/assets/b1156895-c881-49ba-9f4d-f431f07bd99f)

Video: https://youtu.be/ZC5vRPHUrkc
