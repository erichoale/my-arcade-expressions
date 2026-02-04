Arcade Script – Facility Information HTML Formatter
Overview
This Arcade script formats facility information into a clean, styled HTML table for use in ArcGIS pop‑ups. It applies conditional formatting to highlight missing or important information, styles the facility name and website link, and ensures consistent presentation across all records.

This expression is ideal for web maps, dashboards, and field applications where users need a readable, visually structured summary of facility attributes.

Purpose
Retrieve key facility attributes from the feature.

Apply conditional formatting to highlight missing or important values.

Style the facility name, website link, and notes for improved readability.

Output a fully formatted HTML table for display in a pop‑up.

How It Works
1. Retrieve Attribute Values
The script pulls the following fields from the feature:

Name

Address

Phone

Link (website)

Mammals

Bird

Amphibian_Reptile

Notes

These values are stored in variables for later formatting.

2. Conditional Formatting Rules
Address
If the address equals
"Address not provided, contact facility for information."  
it is displayed in bold to draw attention.

Mammals, Birds, Reptiles
If any of these fields contain "No", the value is bolded to emphasize the absence of that animal type.

Notes
Always bolded for visibility.

3. Additional Styling
Name
Displayed in dark red and bold:

Code
<span style='color:darkred;'><b>Name</b></span>
Website
Rendered as a clickable hyperlink with blue, underlined text:

Code
<a href='URL' style='color:blue; text-decoration:underline;'>URL</a>
4. HTML Table Construction
The script returns an object with:

Code
type: "text"
text: "<table>...</table>"
The table includes rows for:

Name

Address

Phone

Website

Mammals

Birds

Reptiles

Notes

Each row uses consistent padding and spacing for readability.

5. Final Output
The expression returns a fully formatted HTML table ready for display in an ArcGIS pop‑up.

Example Output (Rendered)
Name: Dark red, bold  
Address: Bold if missing
Phone: Plain text
Website: Clickable blue hyperlink
Mammals/Birds/Reptiles: Bold if "No"  
Notes: Always bold

Displayed in a structured table layout.

Use Cases
Wildlife facility directories

Shelter or rescue organization maps

Environmental resource maps

Public information dashboards

Any pop‑up requiring clean, styled attribute presentation
