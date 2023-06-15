# Exhibits

This is a the app to control all public TVs in our office space including noc wall TV. We uses an app named **Exhibit** [documentation](https://exhibit.readthedocs.io/en/latest/) to manage the app. 

The TV directly pulls the configuration via Kandji blueprint named **Common TV** then the URL in app configuration calls the lambda function named **Display-TV** located in **Cogo-IT** account. The lambda function parse the config from **settings.json** to sent the correct csv files to each TV. Refer to the diagram below for system reference.

<img src="https://user-images.githubusercontent.com/109532993/236540762-53edf8cd-f5ce-4b6c-a538-686f4f5f5eaf.png" width="600" height="600">

### How to update display settings
As setting configurations are controlled by **settings.json** simply modify the settings to pull from different CSVs located in the CSV folder. _Be sure to follow the following format in the settings.json or else it will error._

### Display Video and Image Format
Please be sure the video and image size is 1920 x 1080 or else the display won't show. It will go into an endless loop!!!! Current images are stored in `cogo-dashboard/images` s3 bucket under `cogo-IT

### settings.json Format
**Fields**  
`default_panic-` (REQUIRED) : set to `true` to turn all screens into panic mode and displays the `default_panic_url-`   
`default_panic_url-` (REQUIRED) : default URL to the csv file to be displayed when panic mode is activated   
`default_url-` (REQUIRED) : default URL to the csv file to be display when there're no confirguration specified for the TV  
`url` : Specific URL for individual TV. If not specified the TV will display `default_url-`  
`panic-` (REQUIRED) : Set to `true` to set the individual TV to panic mode  
`panic_url` : Specific panic URL for individual TV. If not specified the TV will display `default_panic_url-`      


```
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
        "Noc2" : {
            "panic-": true
        }
    }
}
```
        
### CSV Format  
Use the following format for CSV files. Be sure that the image link is accessible via HTTPS and not extra space or line in the CSV files. For more details on the configuration visit documentation [here](https://exhibit.readthedocs.io/en/latest/playlist/). 

```
Name,URL,Duration,UpdateInterval,StartOn,EndBy,Cache
Exhibit01,https://cogo-dashboards.s3.us-east-1.amazonaws.com/noc1/noc1-2023.05.05-12.00.01.png,0:00:10,1:00:00,1/1/18 0:00,12/31/30 23:59,no
```
