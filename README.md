# athletic_sales_analysis: Module 5

    # Import Libraries and Dependencies

    import pandas as pd

    # Read the CSV files into DataFrames

    csv_path_2020 = 'Resources/athletic_sales_2020.csv'
    csv_path_2021 = 'Resources/athletic_sales_2021.csv'

    # Display the 2020 sales DataFrame

    df_athletic_sales_2020 = pd.read_csv(csv_path_2020)
    print(df_athletic_sales_2020)

    # Display the 2021 sales DataFrame

    df_athletic_sales_2021 = pd.read_csv(csv_path_2021)
    print(df_athletic_sales_2021)

    # Check the 2020 sales data types

    data_types_2020 = df_athletic_sales_2020.dtypes
    print(data_types_2020)

    # Check the 2021 sales data types

    data_types_2021 = df_athletic_sales_2021.dtypes
    print(data_types_2021)

    # Combine the 2020 and 2021 sales DataFrames on the rows and reset the index

    combined_sales_df = pd.concat([df_athletic_sales_2020, df_athletic_sales_2021], ignore_index=True)
    print("Combined DataFrame of 2020 and 2021 sales:")
    print(combined_sales_df)

    # Check if any values are null

    null_values = combined_sales_df.isnull().any()
    if null_values.any():
    print("Columns with null values:")
    print(null_values[null_values])
    else:
    print("No null values found in the DataFrame.")

    # Check the data type of each column

    combined_data_types = combined_sales_df.dtypes
    print("Data types of each column:")
    print(combined_data_types)

    # Convert the "invoice_date" to a datetime datatype

    combined_sales_df['invoice_date'] = pd.to_datetime(combined_sales_df['invoice_date'])
    print("Data types after conversion:")
    print(combined_sales_df.dtypes)

    # Confirm that the "invoice_date" data type has been changed

    combined_sales_df['invoice_date'] = pd.to_datetime(combined_sales_df['invoice_date'])
    print("Data types after conversion:")
    print(combined_sales_df.dtypes)

    # Show the number products sold for region, state, and city

    # Rename the sum to "Total_Products_Sold"

    products_grouped_df = combined_sales_df.groupby(['region', 'state', 'city']).size().reset_index(name='Total_Products_Sold')

    # Show the top 5 results

    products_top_5_results = products_grouped_df.sort_values(by='Total_Products_Sold', ascending=False).head(5)
    print("Top 5 results - Number of products sold for region, state, and city:")
    print(products_top_5_results)

    # Show the number products sold for region, state, and city

    products_pivot_table = pd.pivot_table(combined_sales_df,
                                values='units_sold',
                                index=['region', 'state', 'city'],
                                aggfunc='sum')

    # Rename the "units_sold" column to "Total_Products_Sold"

    pivot_table = products_pivot_table.rename(columns={'units_sold': 'Total_Products_Sold'})

    # Show the top 5 results

    top_5_results = pivot_table.sort_values(by='Total_Products_Sold', ascending=False).head(5)
    print("Top 5 results - Number of products sold for region, state, and city:")
    print(top_5_results)

    # Show the total sales for the products sold for each region, state, and city

    # Rename the "total_sales" column to "Total Sales"

    units_sold_df = combined_sales_df.groupby[['region', 'state', 'city']]('total_sales').sum().reset_index(name='Total Sales')

    # Show the top 5 results

    top_5_sales = units_sold_df.nlargest(5, 'Total Sales')
    print("Total sales for products sold in each region, state, and city:")
    print(top_5_sales)

    # Show the total sales for the products sold for each region, state, and city

    pivot_df = pd.pivot_table(combined_sales_df, values='total_sales',
                            index=['region', 'state', 'city'],
                            aggfunc='sum').reset_index()

    # Optional: Rename the "total_sales" column to "Total Sales"

    pivot_df = pivot_df.rename(columns={'total_sales': 'Total Sales'})

    # Show the top 5 results

    top_5_sales = pivot_df.nlargest(5, 'Total Sales')
    print(top_5_sales)

    # Show the total sales for the products sold for each retailer, region, state, and city

    # Rename the "total_sales" column to "Total Sales"

    grouped_sales = combined_sales_df.groupby[['retailer', 'region', 'state', 'city']]('total_sales').sum().reset_index()
    grouped_sales = grouped_sales.rename(columns={'total_sales': 'Total Sales'})

    # Show the top 5 results

    top_5_sales = grouped_sales.nlargest(5, 'Total Sales')
    print(top_5_sales)

    # Show the total sales for the products sold for each retailer, region, state, and city

    pivot_df = pd.pivot_table(combined_sales_df,
                            values='total_sales',
                            index=['retailer', 'region', 'state', 'city'],
                            aggfunc='sum').reset_index()

    # Optional: Rename the "total_sales" column to "Total Sales"

    pivot_df = pivot_df.rename(columns={'total_sales': 'Total Sales'})

    # Show the top 5 results

    top_5_sales = pivot_df.nlargest(5, 'Total Sales')
    print(top_5_sales)

    # Filter the sales data to get the women's athletic footwear sales data

    womens_athletic_footwear_sales = combined_sales_df[combined_sales_df['product'].str.contains("Women's Athletic Footwear")]
    print(womens_athletic_footwear_sales)

    # Show the total number of women's athletic footwear sold for each retailer, region, state, and city

    # Rename the "units_sold" column to "Womens_Footwear_Units_Sold"

    grouped_sales = womens_athletic_footwear_sales.groupby[['retailer', 'region', 'state', 'city']]('units_sold').sum().reset_index()
    grouped_sales = grouped_sales.rename(columns={'units_sold': 'Womens_Footwear_Units_Sold'})

    # Show the top 5 results

    top_5_results = grouped_sales.nlargest(5, 'Womens_Footwear_Units_Sold')
    print(top_5_results)

    # Show the total number of women's athletic footwear sold for each retailer, region, state, and city

    pivot_df = pd.pivot_table(womens_athletic_footwear_sales,
                            values='units_sold',
                            index=['retailer', 'region', 'state', 'city'],
                            aggfunc='sum').reset_index()

    # Rename the "units_sold" column to "Womens_Footwear_Units_Sold"

    pivot_df = pivot_df.rename(columns={'units_sold': 'Womens_Footwear_Units_Sold'})

    # Show the top 5 results

    top_5_results = pivot_df.nlargest(5, 'Womens_Footwear_Units_Sold')
    print(top_5_results)

    # Create a pivot table with the 'invoice_date' column is the index, and the "total_sales" as the values

    womens_athletic_footwear_sales.loc[:, 'invoice_date'] = pd.to_datetime(womens_athletic_footwear_sales['invoice_date'])
    pivot_df = pd.pivot_table(womens_athletic_footwear_sales,
                            values='total_sales',
                            index='invoice_date',
                            aggfunc='sum')

    # Optional: Rename the "total_sales" column to "Total Sales"

    pivot_df = pivot_df.rename(columns={'total_sales': 'Total Sales'})

    # Show the table

    top_10_sales = pivot_df.sort_values(by='Total Sales', ascending=False).head(10)
    print(top_10_sales)

    # Resample the pivot table into daily bins, and get the total sales for each day

    daily_sales = pivot_df.resample('D').sum()

    # Sort the resampled pivot table in descending order on "Total Sales"

    daily_sales = daily_sales.rename(columns={'total_sales': 'Total Sales'})
    top_10_days = daily_sales.sort_values(by='Total Sales', ascending=False).head(10)
    print(top_10_days)

    # Resample the pivot table into weekly bins, and get the total sales for each week

    weekly_sales = pivot_df.resample('W').sum()

    # Sort the resampled pivot table in descending order on "Total Sales"

    weekly_sales = weekly_sales.rename(columns={'total_sales': 'Total Sales'})
    weekly_sales_sorted = weekly_sales.sort_values(by='Total Sales', ascending=False)
    top_10_weeks = weekly_sales_sorted.head(10)
    print(top_10_weeks)
