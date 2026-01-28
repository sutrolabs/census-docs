# CSV Datasets

CSV datasets allow you to upload and use CSV (Comma-Separated Values) files directly in Census. This feature is particularly useful when you need to work with data that isn't stored in your data warehouse or when you want to quickly test a sync without setting up complex data infrastructure.

{% hint style="warning" %}
CSV Datasets have been deprecated and are no longer available in new Census accounts.&#x20;

* **July 1, 2026**: Existing datasets become read-only; no new datasets can be created.
* **August 1, 2026**: Datasets will be deleted, as will any data remaining in Census-managed S3\
  storage.

Customers can work with support to migrate their data to another object storage.
{% endhint %}

## Key Benefits of CSV Datasets

* **No Data Warehouse Required** - Use Census without connecting to a data warehouse
* **Quick Testing** - Rapidly prototype and test syncs before implementing in production
* **Supplemental Data** - Add data that may not exist in your primary data sources
* **Simple Collaboration** - Share and collaborate on datasets using familiar CSV files
* **Easy Migration Path** - Start with CSV files and seamlessly transition to basic datasets as you scale

## Getting Started

To create your first CSV dataset:

1. Prepare your CSV file with clean, well-structured data
2. Navigate to the Datasets section in Census
3. Click "New Dataset" and select "CSV Dataset"
4. Upload your file and configure as needed
5. Click "Create Dataset" to finalize

## Creating CSV Datasets

### File Requirements

Census accepts CSV files with the following specifications:

* File format: `.csv` (comma-separated values)
* Maximum file size: 100MB
* Character encoding: UTF-8
* First row must contain column headers

Example of a valid CSV file:

```csv
id,first_name,last_name,email,company,title,created_at
1,John,Doe,john.doe@example.com,Acme Inc,CEO,2023-01-15
2,Jane,Smith,jane.smith@example.com,XYZ Corp,CTO,2023-02-20
3,Robert,Johnson,robert.j@example.com,123 Industries,VP Sales,2023-03-05
```

## Working with CSV Datasets

### Data Types

During the upload process, you can manually set the data type for each column in your CSV dataset:

* **Text** - For string values
* **Integer** - For whole numbers without decimals
* **Float** - For decimal numbers
* **Date** - For calendar dates (e.g., 2023-01-15)
* **Timestamp** - For specific points in time (e.g., 2023-01-15 12:00:00)
* **Boolean** - For true/false values

Setting the correct data type for each column ensures proper handling of your data when using it in syncs and helps Census validate the data during import.

### Refreshing Data

CSV datasets are static by default, but you can update them by:

1. Navigating to the dataset details page
2. Clicking "Update Dataset"
3. Uploading a new CSV file
4. Confirming the update

This action completely replaces the existing dataset with the new file.

## Use Cases for CSV Datasets

<details>

<summary>Quick Prototyping</summary>

CSV datasets provide an excellent way to test and prototype your data workflows without making changes to your production data warehouse:

* Test new sync configurations with sample data before implementing in your warehouse
* Validate field mappings and transformations with controlled test data
* Experiment with different data structures and formats to find the optimal approach
* Create proof-of-concept syncs to demonstrate value before investing in full implementation

</details>

<details>

<summary>One-time Data Loads</summary>

For data that doesn't need regular updates, CSV datasets offer a straightforward solution:

* Upload customer lists for one-time marketing campaigns or outreach
* Import event attendees or webinar registrants for specific follow-up activities
* Load historical data for backfilling systems or analytics
* Import lead lists from trade shows or other offline events
* Upload contest or promotion participants for special communications

</details>

<details>

<summary>Supplemental Reference Data</summary>

CSV datasets are perfect for reference data that complements your warehouse data:

* Upload product catalogs or price lists that change infrequently
* Import geographic or demographic reference data for segmentation
* Add mapping tables for code translations or categorizations
* Import industry benchmarks or standards for comparison
* Upload postal code or region mappings for territory management

</details>

<details>

<summary>Data Enrichment</summary>

Enhance your existing data with additional information from external sources:

* Combine CSV data with warehouse data using Census's data enrichment features
* Upload third-party data that isn't available in your warehouse
* Add manual classifications or segments created by business teams
* Import scoring data or rankings from external systems
* Add supplemental attributes for more precise targeting

</details>

## Best Practices for CSV Datasets

CSV files are a simple but powerful way to bring data into Census. Here are some tips to help you work effectively with CSV datasets:

* **Include a unique identifier column** whenever possible to make updates and syncs more reliable
* **Set types for your columns** to ensure proper parsing and avoid errors
* **Use consistent date formats** (we require YYYY-MM-DD) to ensure proper date parsing
* **Document the source and purpose** of each CSV dataset for your team
* **Keep backups of your uploaded files** in case you need to reference or restore them
* **Check your column headers** to ensure they're clear, consistent, and don't contain special characters
* **Preview your data** after upload to verify it was parsed correctly

Remember that CSV datasets are best for relatively static data or one-time imports. For data that changes frequently, consider setting up a basic dataset with automated refreshes instead.

## Limitations

* Maximum file size: 100MB
* Not suitable for real-time data that changes frequently
* Manual refresh process required for updates
* Limited to tabular data formats

For more information on working with datasets in Census, see our [core concepts documentation](../core-concepts/datasets.md).
