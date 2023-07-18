# Airline-Customer-Value-Analysis

## Data Preprocessing

1. There is a column with the wrong data type
   
- 'FFP_DATE' (object -> date)
- 'FIRST_FLIGHT_DATE' (object -> date)
- 'LAST_FLIGHT_DATE' (object-> date)
- 'LOAD_TIME' (object -> date)
- 'Age' -> (float -> int)

2. There are invalid values such as
   
- column with date format value, there are several rows added with time format 00:00:00 -> changed to date only
- data contains dots on 'WORK_CITY' and 'WORK PROVINCE' -> changed to 'others'.

3. Clean up data according to standard procedures for flight datasets

- Records where the ticket price (SUM_YR_1,SUM_YR_2) contains the value 0, and the average discount (avg_discount) is non-zero, and where the total mileage (SEG_KM_SUM) is more than zero.
- It is assumed that the user has no travel history.

## Feature Selection

- FFP_DATE (Frequent Flyer Program Join Date)
- LOAD_TIME (Date Data fetched)
- FLIGHT_COUNT (Number of Passenger Flights)
- avg_discount (Average Discount Passenger Gets)
- SEG_KM_SUM (Total Distance (km) of Flights Taken)
- LAST_TO_END (Last Flight Time Distance to Last Flight Order)

## Data Preprocessing After Feature Selection

- OUTLIER: avg_discount
- TRANSFORMASI LOG: TIME_MONTH, LAST_TO_END, FLIGHT_COUNT, SEG_KM_SUM

## Modeling

- From the output results, the number of clusters that have a balanced composition with each cluster member and taking into account the average silhouette score of each cluster is 4 clusters.
  Although 5 clusters have a higher average silhouette score than 4 clusters, 5 clusters have fewer cluster member compositions than 4 clusters, so this model is more efficient if 4 clusters are used.
- Visualization result uses 2 PCA variable:
  
  ![image](https://github.com/nunuufdlh01/Airline-Customer-Value-Analysis/assets/89932073/ac249e04-b8de-4910-8053-133ae22b7ae9)

- Clustering result table:

  <p style="text-align: center;">
Tabel - Akumulasi Hasil Nilai LRFMC pada Setiap Cluster
</p> 

|  Cluster  | High Value | Average Value | Low Value |
| :-------- | :--------: | :-----------: | :-------: |
| **Cluster 0** | R |  | L F M C |
| **Cluster 1** |  | L F M C | R |
| **Cluster 2** | L F M | C | R |
| **Cluster 3** | R C | L | F M |

![image](https://github.com/nunuufdlh01/Airline-Customer-Value-Analysis/assets/89932073/d48f7f65-012c-4be6-928e-13336517ae16)


## Clustering Interpretation

- Cluster 0: Group of new passengers whose airline use is low, has just become a membership,
the use of low discounts, and the travel distance is still small.

- Cluster 1: Medium passenger group (potential loyal passengers) with length of membership, frequency
use of airlines, travel mileage, and use of discounts which are not high nor are they high
low (medium), as well as the time span from the time of the last flight to the last order made
pretty low.

- Cluster 2: Loyal passenger groups with long-standing airline memberships, frequent users
airlines, and the distance traveled is already very high. Even though the use of the discount
classified as medium, recency/time span from the time of the last flight to the last order
done low.

- Cluster 3: Medium passenger group with long membership on medium airlines (neither new nor new
too long since joining to use the airline), the use of a fairly high discount on
this passenger group with the time span from the time of the last flight to the last order
carried out is quite high, as well as the activity of using airlines is low and the mileage of the trip is still high
low (It is likely that this passenger group will use the airline if there is a promo. If there is no promo, then
the possibility of not making transactions at the airline).

## Business Recommendations

- Cluster 0: Needs even better treatment so that this group can be a member of the airline longer and
more often use the airline. The treatment that can be given to this group is delivery
personalized campaigns or promos for various airline flight programs sent via personal email
passengers.

- Cluster 1 : Using medium-distance airlines with the last flight time span and
the time of the last order is close together, allowing this group if it is given more treatment it will remain
using airlines, recency remains low, and makes the frequency of transactions and mileage increase.
That way, this group of passengers can become loyal passengers. Recommendations that can be given, namely by
granting of price discounts if the passenger flies more than one flight at a time
and/or inviting friends/colleagues on the same flight and awarding points for each possible flight
exchanged into a special voucher if the points collected meet the existing conditions.

- Cluster 2: This group has been using airlines for a long time with quite a lot of transactions and mileage
high travel. This group should be given treatment so that they feel that the airline
value their loyalty. The recommendations given can be in the form of sending a thank you
use airlines faithfully to personal emails and can also be in the form of awarding points that can be redeemed
with discount vouchers and/or affiliate product offers from airlines.

- Cluster 3: It's quite rare to use airlines and the mileage is still small with the old membership
moderate enough and this group is happy to make transactions if there is a discount given. Possible recommendations
given is sending a personal email in the form of the airline's longing for the transaction made and in the form of
delivery of promo voucher codes in the form of discounts for future flights within a certain time limit
This passenger can immediately redeem the voucher.
