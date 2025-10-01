# VHA Formulary Database Repository

## Overview

This repository contains VHA medication formulary data in CSV format for use with Power Apps and other applications.

## Data Structure

### Files

- `station_589_formulary.csv` - Station 589 formulary data
- `station_XXX_formulary.csv` - Additional stations as needed

### CSV Format

```csv
MedicationName,FormularyStatus,NonFormularyFlag,NationalFormularyFlag,StationNumber,LastUpdated
"METFORMIN HCL 500 MG TABLET","NATIONAL FORMULARY","N","Y",589,"10/01/2025"
"LISINOPRIL 10 MG TABLET","NATIONAL FORMULARY","N","Y",589,"10/01/2025"
```

## Usage

### For Power Apps Teams Integration:

1. Upload CSV files to this repository
2. Use GitHub raw file URLs as data source
3. Connect Power Apps to GitHub CSV via web connector

### Data Sources Available:

- **Station 589**: `https://raw.githubusercontent.com/YOUR_USERNAME/vha-formulary-db/main/station_589_formulary.csv`
- Add more stations as needed

## Power Apps Connection Steps:

1. In Power Apps (Teams), go to Data Sources
2. Select "Web" or "Import from web"
3. Use the raw GitHub CSV URL
4. Power Apps will automatically parse the CSV

## Data Updates:

- Export fresh data from VHA CDW monthly
- Upload updated CSV files to repository
- Power Apps will automatically refresh data

## Security Notes:

- This repository can be private if needed
- No sensitive patient data included
- Only medication names and formulary status
- Station-specific data segregated by file

## API Endpoint (Future):

Consider converting to REST API for real-time updates:

```
GET /api/formulary/{station}/{medication}
GET /api/formulary/{station}/all
```
