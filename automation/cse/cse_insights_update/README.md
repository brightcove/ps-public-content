# Purpose
`cse_insights_update.py` script can be used to list and update CSE Insights.

# Variables
```
optional arguments:
  -h, --help                show this help message and exit
  -test                     test mode (no change applied)
  -env ENV                  Sumo Logic Environment (default: "us2")
  -tag TAG                  new TAG to apply
  -comment COMMENT          new COMMENT to apply
  -status STATUS            new STATUS to apply
  -resolution RESOLUTION    new RESOLUTION to apply

required arguments:
  -accessid ACCESSID        Sumo Logic API Access ID
  -accesskey ACCESSKEY      Sumo Logic API Access KEY
  -filter FILTER            CSE Insight filter (ex: '-status="closed" -tag="custom"')
```

# Examples
## List (no action) non-closed insights with tag CUSTOM
```
python3 cse_insights_update.py -accessid XXXXX -accesskey XXXXX -filter '-status:"closed" +tag:"CUSTOM"' -test
```

## Add tag NEWTAG to non-closed insights without tag CUSTOM
```
python3 cse_insights_update.py -accessid XXXXX -accesskey XXXXX -filter '-status:"closed" -tag:"CUSTOM"' -tag 'NEWTAG'
```

## Using the us2 endpoint, close all non-closed insights with tag CUSTOM with resolution "No Action", Add tag NEWTAG, add comment, in us2 environment
```
python3 cse_insights_update.py -env=us2 -accessid XXXXX -accesskey XXXXX -filter '-status:"closed" +tag:"CUSTOM"' -tag 'NEWTAG' -comment 'NEWCOMMENT' -status 'closed' -resolution 'No Action'
```

## Close all non-closed insights as duplicates (e.g. alert flood)
```
python3 cse_insights_update.py -accessid XXXXX -accesskey XXXXX -filter '-status:"closed" -tag:"CUSTOM"' -comment 'Valid traffic that has since been tuned out. Closing out.' -status 'closed' -resolution 'Duplicate'
```
### Just new insights, w/o any tag
```
python3 cse_insights_update.py -accessid XXXXX -accesskey XXXXX -filter '+status:"new"' -comment 'Valid traffic that has since been tuned out. Closing out.' -status 'closed' -resolution 'No Action'
```
