## Notes of each Step Taken

### STEP 1: Create an Azure Storage Credential
Before Databrick can talk to ADLS Gen2, it needs a connection
1. In Databricks workspace, click **Catalog** in the sidebar
2. Select **External Locations** and then click **Storage Credentials.**
3. Click **Create credential**
4. Give it a name (e.g., cred-giftmapote_storage)
5. Select **Azure Managed Identity** (Recommended for seniority/security) or **Service Principal**

### STEP 2: Register the External Location
Tell Unity Catalog exactly which folder this credential can access. 
1. In the **Catalog** menu, click **External Locations > Create location.**
2. **Location Name:** `fraud_sentinel_landing`
3. **URL**: `abfss://fraud-sentinel@giftmapote2ete.dfs.core.windows.net/.
4. **Storage Credential:**Select the one created in Step 1 (`cred_giftmapote_storage`)
5. Click **Create**

### STEP 3: Test the Access
