# CSV Datasets

CSV datasets allow you to upload and use CSV (Comma-Separated Values) files directly in Census. This feature is particularly useful when you need to work with data that isn't stored in your data warehouse or when you want to quickly test a sync without setting up complex data infrastructure.

## Key Benefits of CSV Datasets

- **No Data Warehouse Required** - Use Census without connecting to a data warehouse
- **Quick Testing** - Rapidly prototype and test syncs before implementing in production
- **Supplemental Data** - Add data that may not exist in your primary data sources
- **Simple Collaboration** - Share and collaborate on datasets using familiar CSV files
- **Easy Migration Path** - Start with CSV files and seamlessly transition to warehouse datasets as you scale

## Creating CSV Datasets

### File Requirements

Census accepts CSV files with the following specifications:

- File format: `.csv` (comma-separated values)
- Maximum file size: 100MB
- First row must contain column headers
- UTF-8 encoding recommended
- Common delimiters supported (comma, tab, semicolon)

Example of a valid CSV file:

```csv
id,first_name,last_name,email,company,title,created_at
1,John,Doe,john.doe@example.com,Acme Inc,CEO,2023-01-15
2,Jane,Smith,jane.smith@example.com,XYZ Corp,CTO,2023-02-20
3,Robert,Johnson,robert.j@example.com,123 Industries,VP Sales,2023-03-05
```

### Upload Process

To create a CSV dataset:

1. Navigate to the Datasets section in Census
2. Click "New Dataset" and select "CSV Dataset"
3. Upload your CSV file by dragging and dropping or using the file browser
4. Review the preview to ensure your data is parsed correctly
5. Configure column data types if needed
6. Name your dataset and add a description
7. Click "Create Dataset" to finalize

## Working with CSV Datasets

### Data Types

Census automatically detects data types for your CSV columns, but you can manually adjust them if needed:

- **Text** - For string values
- **Number** - For numeric values (integers or decimals)
- **Boolean** - For true/false values
- **Date/Time** - For date and timestamp values
- **JSON** - For structured data in JSON format

### Refreshing Data

CSV datasets are static by default, but you can update them by:

1. Navigating to the dataset details page
2. Clicking "Update Dataset"
3. Uploading a new CSV file with the same schema
4. Confirming the update

### Schema Changes

When updating a CSV dataset, Census handles schema changes as follows:

- **New columns** - Added to the dataset
- **Removed columns** - Preserved in the dataset but marked as deprecated
- **Data type changes** - Detected and may require confirmation

## Use Cases for CSV Datasets

### Quick Prototyping

- Test new sync configurations without modifying your warehouse
- Validate mappings and transformations with sample data
- Experiment with different data structures

### One-time Data Loads

- Upload lists of customers for one-time campaigns
- Import event attendees for specific marketing activities
- Load historical data for backfilling systems

### Supplemental Reference Data

- Upload product catalogs or price lists
- Import geographic or demographic reference data
- Add mapping tables for code translations

### Data Enrichment

- Combine CSV data with warehouse data using Census's data enrichment features
- Upload third-party data that isn't available in your warehouse
- Add manual classifications or segments to existing data

## Best Practices for CSV Datasets

CSV files are a simple but powerful way to bring data into Census. Here are some tips to help you work effectively with CSV datasets:

- **Include a unique identifier column** whenever possible to make updates and syncs more reliable
- **Set types for your columns** to ensure proper parsing and avoid errors
- **Use consistent date formats** (we require YYYY-MM-DD) to ensure proper date parsing
- **Document the source and purpose** of each CSV dataset for your team
- **Keep backups of your uploaded files** in case you need to reference or restore them
- **Check your column headers** to ensure they're clear, consistent, and don't contain special characters
- **Preview your data** after upload to verify it was parsed correctly

Remember that CSV datasets are best for relatively static data or one-time imports. For data that changes frequently, consider setting up a warehouse dataset with automated refreshes instead.

## Limitations

- Maximum file size: 100MB
- Not suitable for real-time data that changes frequently
- Manual refresh process required for updates
- Limited to tabular data formats

## Getting Started

To create your first CSV dataset:

1. Prepare your CSV file with clean, well-structured data
2. Navigate to the Datasets section in Census
3. Click "New Dataset" and select "CSV Dataset"
4. Upload your file and configure as needed
5. Start using your CSV dataset in syncs

For more information on working with datasets in Census, see our [core concepts documentation](../core-concepts/datasets.md).
