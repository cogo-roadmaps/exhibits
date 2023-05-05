# Exhibits

This is a the app to control all public TVs in our office space including noc wall TV. We uses an app named **Exhibit** [documentation](https://exhibit.readthedocs.io/en/latest/) to manage the app. 

The TV directly pulls the configuration via Kandji blueprint named **Common TV** then the URL in app configuration calls the lambda function named **Display-TV** located in **Cogo-IT** account. The lambda function parse the config from **settings.json** to sent the correct csv files to each TV. Refer to the diagram below for system reference.

DIAGRAM!!!

### How to update display settings
As setting configurations are controlled by **settings.json** simply modify the settings to pull from different CSVs located in the CSV folder. _Be sure to follow the following format in the settings.json or else it will error._

### settings.json Format
**Required Fields**

{
    "default_panic-": false,
    "default_panic_url-": "https://raw.githubusercontent.com/cogo-roadmaps/exhibits/main/csv/panic.csv",
    "default_url-": "https://raw.githubusercontent.com/cogo-roadmaps/exhibits/main/csv/commonTV.csv",
    "TV_configs": {
        "Noc1": {
            "url": "https://raw.githubusercontent.com/cogo-roadmaps/exhibits/main/csv/noc1.csv",
            "panic-": false,
            "panic_url": "https://raw.githubusercontent.com/cogo-roadmaps/exhibits/main/csv/panic.csv"
        },
        
### CSV Format  
