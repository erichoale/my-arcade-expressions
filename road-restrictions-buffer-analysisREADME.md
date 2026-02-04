Arcade Script – Road Restriction Buffer Analysis
Overview
This Arcade script evaluates road restriction features that fall within a buffer around the current feature. It clips each intersecting restriction segment to the buffer, measures the length of the restricted portion, filters out short segments, and returns a formatted summary of road names, restriction types, and intersecting mileage. A total mileage value is appended at the end.

This expression is ideal for pop‑ups, dashboards, and analytical map layers where users need to understand which road restrictions affect a specific location.

Purpose
Identify road restriction features within a defined distance of a feature.

Clip each restriction to the buffer area and measure only the portion inside.

Exclude segments shorter than a minimum threshold.

Return a readable list of road names, restriction types, and segment lengths.

Provide a total mileage value for all qualifying restricted segments.

How It Works
1. Buffer Creation
A buffer of 10 meters is created around the current feature ($feature).

The buffer is converted to a polygon for geometric operations.

2. Load the Road Restrictions Layer
The script accesses the Road Restrictions layer using FeatureSetByName().

It retrieves all features that intersect the buffer.

3. Clip Restriction Segments
For each intersecting restriction:

The geometry is clipped to the buffer using Intersection().

Empty or invalid intersections are skipped.

4. Measure Segment Lengths
The clipped segment length is measured in feet.

Segments shorter than 100 feet are ignored.

Remaining segments are converted to miles and rounded to three decimals.

5. Build Output Entries
Each qualifying segment is added to the output list in the format:

Code
ROADNAME – RESOLUTION (X.XXX mi)
Where:

ROADNAME = name of the road

RESOLUTION = type or description of the restriction

X.XXX mi = length of the restricted portion inside the buffer

6. Total Mileage Calculation
All qualifying segment lengths are summed.

A final entry is appended:

Code
Total: X.XXX mi
7. Final Output
All entries are concatenated into a single string separated by |.

Parameters
Name	Value	Description
bufferDistance	10	Distance around the feature
bufferUnit	meter	Units for the buffer
minLengthFeet	100	Minimum clipped segment length to include
Road Restrictions	—	Source layer containing restriction features
Example Output
Code
Main St - Weight Limit (0.125 mi) | Oak Rd - Height Restriction (0.204 mi) | Total: 0.329 mi
Use Cases
Identifying road restrictions affecting an incident or planned work area

Pop‑ups showing nearby restrictions for routing or planning

Operational dashboards summarizing restricted road mileage

Field apps needing quick visibility into impacted road segments
