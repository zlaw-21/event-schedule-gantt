
## Table of Contents
- [Introduction](#introduction)
- [The Problem of the *Flyer*](#the-problem-of-the-flyer)
- [The Tutorial](#the-tutorial)
- [The Visualization & Solution](#the-visualization--solution)
  

## Introduction
Arcade Music Fest, a newly recurring music festival in Covington, KY, debuted the weekend of August 8th, bringing together local musicians from the Cincinnati area to perform across eight venues along the historic Pike Street corridor. The festival’s official schedule was provided as a static flyer that listed performance times and locations, but its dense layout made it difficult for attendees to quickly compare overlapping sets or plan transitions between venues. This project aimed to transform that unstructured flyer into a clear, minute-level Gantt chart in Excel for the Saturday lineup, delivering a visual schedule that enhanced readability, improved planning, and could be adapted for other multi-venue or time-based events.


## The Problem of *The Flyer*
<img src="/images/AMF%20Artist%20Schedule.avif" alt="AMF Artist Schedule" width="50%" height="50%">

While the flyer provided strong branding and visual appeal, it lacked utility and readability for Type-A festival goers who wanted to plan their experience in detail. The dense layout made it difficult to quickly compare set times across eight venues, spot potential overlaps, or identify gaps in the schedule. Without an interactive or structured digital version, attendees had no efficient way to organize their time, creating a cognitive load similar to a high-stakes chess endgame where every move must be planned several steps ahead.

To resolve this, I fell on my early career Scrum Master training and aimed to build a minute-level Gantt chart to visualize the lineup for easy side-by-side time analysis of venue schedules. Gantt charts have been historically used in project management communities to understand simultaneous processes, but have fallen out of favor in Agile communities due to their rigidity. For this use case in particular, the rigidity is exactly what we need to help festival goers plan their experience and make split second decisions at the event.


## The Tutorial
At a high level, the goal is to build a stacked bar chart that uses both calculations and formatting to mimic the look and utility of a Gantt chart. The approach is simple: for each row of data, we’ll layer bars onto the chart by adding additional series for each timeslot, gradually building out the full visualization.

Before starting, be sure to pull the template spreadsheet I put together for quick data entry [here](https://github.com/zlaw-21/event-schedule-gantt/blob/main/gantt_chart_template.xlsx).

**Step One: Format Static values and Series 1 to build the foundation.**

To get started, enter the data for Stage and Series 1.
- Stage represents the timeline, in our case, concert venues.
- Series 1 should include Artist, Start Time, End Time, and Duration.
    - Artist: Name of the event.
    - Start Time: Start time of the event. Ensure this is in the "Time" data format.
    - End Time: End time of the event. Ensure this is in the "Time" data format.
    - Duration: ```End Time - Start Time``` of the event. Ensure this is in the "Time" data format.

NOTE: Excel handles timeframes in a slightly less intuitve way than one might expect at first glance. 

``` =7:55:00 PM - 7:00:00 PM ``` returns 12:55:00 AM when in the Time format, and 0.0381944444444445 when in General or Number formats. This is because Excel converts a 24 hour period to a value of 1.0. In our case, 55 minutes equates to 3.81944444444445% of one day. To explore this further, see this great article written by Dave Bruns over at ExcelJet [here](https://exceljet.net/formulas/calculate-hours-between-two-times).

**Step Two: Build the chart's foundation and first series.**

Foundation:
- First, select all Start Time values in Series 1 -> Insert -> 2D Stacked Bar
- Then, right click the new chart area -> Select Data -> Edit Horizontal Category Label
- From here, select the data for Stage and then right click the y-axis -> Format Axis -> Select Categories in reverse order
- Lastly right click the x-axis -> Format Axis -> Set Label Position to High

Now that the foundation is built, our chart should appear as a single horizontal bar chart with correct x and y axis formatting. From here, we will add the finishing touches to the first series.

First Series:
- Right click anywhere in the chart area -> Select Data -> Add Series -> Rename to "Duration 1" and Select all cells under the Series 1 duration column
- Next, right click the left most bar on the graph -> Format data series -> Select No fill and No line
- Lastly, right click the x-axis -> Axis Options -> Set Min Bounds to .75 and Max to 1 -> Set Major Units to 0.02083333333

NOTE: When updating Bounds and Unit values, match the input values to the scale that you want to be displayed on your visualization based upon the Min and Max values of the dataset. 

For this example, .75 = 6:00 PM, 1 = 12:00 AM, and 0.02083333333 = 30 minutes/12:30 AM. For quick minute-level calculations, you can use ```Total # of Minutes / 1440``` to get a quick and exact value.

**Step Three: Add all consecutive data series to the template and chart.**

To begin, add the rest of your series data to the template. You can add as many as you need and have different counts for each timeline. Just ensure that all unused cells are  empty to prevent visualization bugs.

All additional series should include:
- Artist: *See Step One*
- Start Time: *See Step One*
-  **Diff from Previous:** ```Current Series Start Time - Previous Series End Time``` to add the gaps between each performance/event.
- End Time: *See Step One*
- Duration: *See Step One*

To add each additional series to the chart:
- First, Right click the chart area -> Select Data -> Add Series -> Rename to "Diff From Prev 2" and select all data from the Diff from Previous column
- Next, right click the left most bar on the graph -> Format data series -> Select No fill and No line
- Then, Right click the chart area -> Select Data -> Add Series -> Rename to "Duration 2" and select all data from the Diff from Previous column
- Repeat this process for each additional series you want visualized on the chart

**Step Four: Format your chart.**

At this step, your Gantt chart is now complete and every further decision should be based on getting the right aesthetics. For my visualization, I went with colors and formatting options that aligned with the design choices of the original flyer and festival branding.

Some quick tips to get you started:
- To add labels to each bar directly, right click a series bar -> Add Data Labels -> Label Options -> Value From Cells -> Select all series Artists -> Uncheck Value
- To increase the vertical thickness of all bars, right click any series bar -> Format Data Series -> Series Options -> Adjust Gap Width to the desired size
- To adjust a series or individual bar color, right click any series bar (double click for single selection) -> Format Data Series -> Fill & Line -> Select the desired fill color


## The Visualization & Solution





