# API Endpoints for Row Management

## **Overview of API Endpoints for Rows**

Beefree SDK provides robust APIs for managing rows. These API endpoints enable operations such as saving, retrieving, syncing, merging, and organizing rows, making them essential for maintaining design consistency and managing shared rows.

## **Row-Related API endpoints**

1. **Merge Rows API endpoints**
   * **Purpose**: Updates linked rows across multiple designs by replacing outdated content with new versions. Ideal for batch-updating designs or maintaining consistent synced rows.
2. **Synced Rows API endpoint**
   * **Purpose**: Retrieves all rows marked as "synced," ensuring centralized tracking of synced rows across templates.
3. **Index Rows API endpoint**
   * **Purpose**: Generates metadata for template rows, enabling better organization and search capabilities. Create structured catalogs of rows with attributes like categories, names, or tags.

### **Row Endpoints and Descriptions**

**Merge Rows**

**Endpoint**: `POST https://api.beefree.io/v1/{collection}/merge-rows`

{% swagger src="broken-reference" path="/v1/{collection}/merge-rows" method="post" %}
[Broken link](broken-reference)
{% endswagger %}



**Index Rows**

**Endpoint**: `POST https://api.beefree.io/v1/{collection}/merge/index`

{% swagger src="broken-reference" path="/v1/{collection}/merge-index" method="post" %}
[Broken link](broken-reference)
{% endswagger %}



**Retrieve Synced Rows**

**Endpoint**: `POST https://api.beefree.io/v1/{collection}/synced-rows`

{% swagger src="../.gitbook/assets/synced_rows_endpoint (1).yaml" path="/v1/{collection}/synced-rows" method="post" %}
[synced_rows_endpoint (1).yaml](<../.gitbook/assets/synced_rows_endpoint (1).yaml>)
{% endswagger %}



## Workflow Example

1. **Retrieve Synced Rows**: Use the `Synced Rows` endpoint to identify synced rows across designs.
2. **Modify a Synced Row**: Update the row and submit changes using the `Merge Rows` endpoint.
3. **Verify Updates**: Confirm that updates are reflected in all linked templates based on the `Merge Rows` response.
