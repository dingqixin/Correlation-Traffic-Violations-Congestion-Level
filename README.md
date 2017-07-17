# Correlation: Traffic Violations & Congestion Level
In large cities, for example Chicago, traffic is one of the most important issues in daily life. Traffic violations, such as overspeed and running red lights, can result in serious injuries and deaths. By studying the correlation between the traffic violations and congestion level, hopefully we can get some insights on reducing traffic violations and improve road safety condition.

## Team Member
* Arun Sugumar
* Zichao Wu
* Xiaoxin Xu
* Lijiu Liang
* Qixin Ding

## Note
The time overlap of these four datasets is 2014.7.1 ~ 2014.12.31. Red light violation has 48959 entries that falls within that time range while speed violation has 16318 entries.

## Current Available Datasets
Detailed PDF Description: [Download](https://data.cityofchicago.org/api/assets/3F039704-BD76-4E6E-8E42-5F2BB01F0AF8)

### Traffic Violation (Historical Data):

#### Red Light Violation (2014.7.1~2014.12.31): [Link](https://data.cityofchicago.org/Transportation/Red-Light-Camera-Violations/spqx-js37)
- Contains the violation count for each red light camera at each intersection.
Columns: Intersection/address, violation date, violation count, location (lat coord, long coord)

#### Red Light Violation Trimmed (2014.11.25~2014.12.31)(10355 Rows):
- Same as above, but only contains data from 11.25. It should be used when analyzing the relationship between violation and segment data.

#### Speed Camera Violation (2014.7.1~2014.12.31): [Link](https://data.cityofchicago.org/Transportation/Speed-Camera-Violations/hhkd-xvj4)
- Contains the violation count for each red light camera at each intersection.
Columns: Intersection/address, violation date, violation count, location (lat coord, long coord)

#### Speed Camera Violation Trimmed (2014.11.25~2014.12.31)(3699 Rows)
- Same as above, but only contains data from 11.25. It should be used when analyzing the relationship between violation and segment data.

---
### Traffic Congestion (Historical Data):

- The Chicago Traffic Tracker estimates traffic congestion on Chicago’s arterial streets (nonfreeway streets) in real-time by continuously monitoring and analyzing GPS traces received from Chicago Transit Authority (CTA) buses. Two types of congestion estimates are produced every 10 minutes: 1) by Traffic Segments and 2) by Traffic Regions or Zones.

- There is much volatility in traffic **segment** speed. However, the congestion estimates for the **traffic regions** remain consistent for relatively longer period. **Speed on individual arterial segments can fluctuate from heavily congested to no congestion and back in a few minutes**.

#### Traffic Congestion History Estimate by Region (2014.11.1~2014.12.31)(702312 Rows, 6 Cols): [Link](https://data.cityofchicago.org/Transportation/Chicago-Traffic-Tracker-Historical-Congestion-Esti/emtn-qqdi)
- A traffic region is comprised of two or three community areas with comparable traffic patterns.
29 regions are created to cover the entire city (except O’Hare airport area).

- Column description:

	- DATE: the date of observation

	- REGION_ID: Unique arbitrary number to represent each region. See [Regions With ID Dataframe](https://data.cityofchicago.org/Transportation/Chicago-Traffic-Tracker-Congestion-Estimates-by-Re/t2qc-9pjd).

	- NUMBER OF READS: Number of GPS probes received(or used) for estimating the speed for that segment.

	- SPEED: Estimated congestion level. Although expressed in miles per hour, this value is more a reflection of the congestion level in the region than it is indicative of the average raw speed vehicles are traveling within the region.

	- ID: A hash ID representing unique rows.

#### Traffic Congestion History Estimate by Traffic Segment (2014.11.25~2014.12.31)(3291634 Rows, 6 Cols): [Link](https://data.cityofchicago.org/Transportation/Chicago-Traffic-Tracker-Historical-Congestion-Esti/77hq-huss)
- Congestion by Traffic Region gives the average traffic condition for all arterial street segments within a region.

- Columns:

	- DATE: the date of observation, same as above

	- SPEED: Same as above. this value is compared to a 0-9, 10-20, and 21 & over scale to display heavy, medium, and free flow conditions for the traffic segment. Segments which has insufficient

	- SEGMENT_ID: We can use SEGMENT_ID to identify the location of each observation. See the [Road Segments With ID Dataframe](https://data.cityofchicago.org/Transportation/Chicago-Traffic-Tracker-Congestion-Estimates-by-Se/n4j6-wkkf/data)

		- So the segment id could be expanded to several other useful columns:
Street name, direction, from street, to street, street heading, comments (we can eliminate those rows with “outside city limits”), start/end longitude & latitude, current speed (drop rows with -1?). The “last updated” column is irrelevant because street is always there. Street doesn’t quite change with date

	- ID: same as above. Unique arbitrary number to represent each region. See http://bit.ly/103beCf for the geographic location of each region.
