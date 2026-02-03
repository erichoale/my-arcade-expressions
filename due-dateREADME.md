Arcade Expression: Due vs. Not Due
Reference Page for Web Maps
Purpose
This Arcade expression evaluates whether a task or inspection is Due or Not Due based on:

A starting date (COUNT_DATE)

A frequency in months (FREQ)

Today’s date

It allows you to symbolize features dynamically without creating additional fields in your dataset.

Expression
arcade
var countdate = $feature.COUNT_DATE;
var frequencymonths = $feature.FREQ;
var dueDate = DateAdd(countdate, frequencymonths, "months");

var today = Now();
return IIf(dueDate < today, "Due", "Not Due");
How the Expression Works
1. Retrieve the last completed date
arcade
var countdate = $feature.COUNT_DATE;
Pulls the date of the last completed task.

2. Retrieve the frequency (in months)
arcade
var frequencymonths = $feature.FREQ;
Reads how often the task should recur.

3. Calculate the next due date
arcade
var dueDate = DateAdd(countdate, frequencymonths, "months");
Adds the frequency to the last completed date to determine the next scheduled date.

4. Get today’s date
arcade
var today = Now();
Captures the current date/time.

5. Compare dates and return a status
arcade
return IIf(dueDate < today, "Due", "Not Due");
If the due date has passed → "Due"

Otherwise → "Not Due"

Using This Expression for Symbology in Web Maps
Arcade expressions can act as virtual fields, letting you symbolize features without modifying your underlying data.

Steps in ArcGIS Online / Enterprise Web Maps
Open your layer

Go to Styles

Choose a style such as Types (Unique symbols)

Under Field, select Expression

Paste the Arcade expression

Save the expression

Apply symbology to the resulting categories:

Due

Not Due

Benefits
No need to create or maintain a “DueStatus” field

Automatically updates every day

Responds instantly to changes in COUNT_DATE or FREQ

Keeps your data clean while still enabling powerful visualization

Why Use Arcade for This
Arcade allows you to compute values dynamically at draw time. This is ideal for date‑based logic like due dates, which change over time and shouldn’t require constant database updates.
