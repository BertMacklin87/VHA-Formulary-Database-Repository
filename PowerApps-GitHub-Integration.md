# Power Apps Teams Integration with GitHub Data

## Quick Setup Guide

### Step 1: Upload Data to GitHub
1. Create a new GitHub repository: `vha-formulary-db`
2. Upload the CSV files from this folder
3. Make repository public (or private with access tokens)

### Step 2: Connect Power Apps Teams to GitHub CSV

#### In Power Apps Teams:
1. **Add Data Source**
2. **Select "Web"** connector
3. **URL**: `https://raw.githubusercontent.com/YOUR_USERNAME/vha-formulary-db/main/station_589_formulary.csv`
4. **Authentication**: Anonymous (for public repos)

#### Connection Settings:
```
Data Source Type: Web
URL: [GitHub Raw CSV URL]
File Type: CSV
Headers: Yes
Delimiter: Comma
```

### Step 3: Power Apps Formulas for GitHub Data

#### Gallery Items (Search Results):
```powerquery
Filter(
    station_589_formulary,
    StartsWith(
        Upper(MedicationName),
        Upper(MedicationSearchBox.Text)
    )
)
```

#### Status Color Formula:
```powerquery
Switch(
    ThisItem.FormularyStatus,
    "NATIONAL FORMULARY", RGBA(40, 167, 69, 1),    // Green
    "LOCAL FORMULARY", RGBA(255, 193, 7, 1),       // Yellow  
    "NON-FORMULARY", RGBA(220, 53, 69, 1),         // Red
    RGBA(108, 117, 125, 1)                         // Gray (Unknown)
)
```

#### Status Icon Formula:
```powerquery
Switch(
    ThisItem.FormularyStatus,
    "NATIONAL FORMULARY", "✅",
    "LOCAL FORMULARY", "⚠️",
    "NON-FORMULARY", "❌",
    "❓"
)
```

### Step 4: App Interface Design

#### Main Screen Controls:
1. **Text Input**: MedicationSearchBox
2. **Gallery**: SearchResults (connected to filtered data)
3. **Label**: Status display with color coding

#### Gallery Template:
```
┌─────────────────────────────────────────┐
│ [Icon] MEDICATION NAME                  │
│ Status: [Formulary Status]              │ 
│ Station: [Station] | Updated: [Date]    │
└─────────────────────────────────────────┘
```

### Step 5: Real-time Search

#### OnChange for Search Box:
```powerquery
If(
    Len(MedicationSearchBox.Text) >= 2,
    Set(
        FilteredMedications,
        Filter(
            station_589_formulary,
            MedicationSearchBox.Text in MedicationName
        )
    )
)
```

## Advanced Features

### Multi-Station Support:
```powerquery
// Combine multiple station CSVs
Union(
    station_589_formulary,
    station_590_formulary,
    station_591_formulary
)
```

### Offline Capability:
```powerquery
// Cache data locally in Power Apps
ClearCollect(
    LocalFormulary,
    station_589_formulary
)
```

### Data Refresh:
```powerquery
// Refresh button OnSelect
Refresh(station_589_formulary);
Set(LastRefresh, Now())
```

## Deployment Steps

### 1. Create GitHub Repository
```bash
# Create new repo on GitHub
# Upload CSV files
# Get raw file URLs
```

### 2. Test Connection
- Verify CSV loads in Power Apps
- Test search functionality
- Validate data display

### 3. Share with Team
- Publish Power Apps to Teams channel
- Add team members
- Test access permissions

### 4. Maintenance Schedule
- **Weekly**: Export fresh VHA CDW data
- **Upload**: New CSV files to GitHub
- **Verify**: Power Apps automatically refreshes

## Benefits of This Approach

✅ **No VHA CDW connection issues**
✅ **Works in Teams Power Apps** 
✅ **Easy data updates via GitHub**
✅ **Version control for formulary data**
✅ **Shareable with entire team**
✅ **Works offline after initial load**
✅ **No database administration needed**

## GitHub Repository Structure
```
vha-formulary-db/
├── README.md
├── station_589_formulary.csv
├── station_590_formulary.csv
├── update_scripts/
│   └── export_from_cdw.sql
└── power_apps_templates/
    └── formulary_checker_template.msapp
```

## Success Metrics
- ✅ Power Apps loads GitHub CSV data
- ✅ Search returns accurate results
- ✅ Status colors display correctly
- ✅ Team members can access app
- ✅ Data updates propagate automatically