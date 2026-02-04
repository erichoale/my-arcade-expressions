Arcade Script – Bridge Weight Restriction Lookup
Overview
This Arcade script retrieves bridge weight‑restriction information from an ArcGIS Online hosted feature layer and identifies which bridges fall within a 100‑meter buffer around the current feature. For each intersecting bridge, the script extracts key restriction attributes and formats them into a readable summary. If no bridges intersect the buffer, the script returns an empty string.

This expression is ideal for pop‑ups, proposed project analyses, routing evaluations, and any workflow where bridge weight limits near a proposed alignment need to be quickly reviewed.

Purpose
Connect to an ArcGIS Online feature layer using a Portal item ID.

Retrieve bridge attributes relevant to weight restrictions.

Identify bridges intersecting a buffered version of the current feature.

Extract and format weight‑restriction values for trucks, semi‑trailers, and full trailers.

Provide a clean, readable summary for use in pop‑ups or reports.

How It Works
1. Connect to ArcGIS Online
The script initializes a connection to the SBCountyDPW ArcGIS Online portal.

It loads a feature layer using:

Item ID: 2866169f94484a95aeedc8014bb25533

Layer index: 0

Only the necessary fields are requested:

BRIDGE_NUMBER

Weight_Rest_Truck

Weight_Rest_Semi_Trailer_Combo

Weight_Rest_Truck_Full_Trailer

2. Create a Buffer Around the Current Feature
A 100‑meter buffer is generated around $feature.

This buffer defines the search area for intersecting bridges.

3. Identify Intersecting Bridges
The script uses Intersects() to find all bridge features that fall within the buffer.

The number of intersecting features is counted.

4. Extract and Format Attribute Values
For each intersecting bridge:

Weight restriction fields are retrieved using DefaultValue() to avoid nulls.

The bridge number is also retrieved with a fallback of "N/A".

A formatted string is created:

Code
Bridge No.: <BRIDGE_NUMBER> - Truck Wt:<value> | Semi Wt:<value> | Full Wt:<value>
Each entry is appended to the output string, separated by semicolons.

5. Return the Final Output
If bridges are found, the script returns the concatenated summary string.

If none are found, the script returns an empty string.

Parameters
Name	Value	Description
bridgeItemID	2866169f94484a95aeedc8014bb25533	ArcGIS Online item containing bridge data
bridgeLayerID	0	Layer index within the item
bufferDistance	100	Distance around the feature
bufferUnit	meters	Units for the buffer
BRIDGE_NUMBER, Weight_Rest_*	—	Fields retrieved from the bridge layer
Example Output
Code
Bridge No.: 52C0123 - Truck Wt:20T | Semi Wt:28T | Full Wt:35T;
Bridge No.: 52C0456 - Truck Wt:N/A | Semi Wt:18T | Full Wt:25T;
Use Cases
Evaluating proposed road alignments for bridge weight conflicts

Pop‑ups showing nearby bridge restrictions in web maps

Field apps used for routing heavy equipment

Engineering review workflows requiring quick access to weight limits
