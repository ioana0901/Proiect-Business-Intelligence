# Business-Intelligence Project
-3rd year project- 

## Analysis of data on retail trade in Bacău County

### 1. Business Scenario<br>


In this project I will analyze data on the field of retail trade in Bacău County. <br>
The field of activity studied has the CAEN code 47 and refers to retail trade, except for motor vehicles and motorcycles. <br>
In the project I will use 8 data sets:
<ul>
<li> 4 files (csv type) containing the lists of companies registered in ONRC until 2019. From here I will extract the Unique Identification Code (CUI), the name of the companies and the data regarding the localities where the companies have their headquarters; li>
<li> For each year (2016, 2017, 2018, 2019) 2 files (text type) containing data on companies that have submitted long, short balance sheets and annual reports; </li>
</ul>

### 2. Data Cleaning and Processing

a. Loading the data in Tableau Prep <br>
![image](https://user-images.githubusercontent.com/63421754/124277848-3222b700-db4e-11eb-8dae-f0ef43ce5231.png)
<br>
b.Preparation of data from files containing lists of companies that are unradiated and have a headquarters. Below are the steps I followed for the data in the set "2019-neradiate-cu-sediu_4" (I followed the same steps for the other 3 sets): <br>
-First we removed the EUID, COD_INMATRICULARE, and STARE_FRIMA attributes, as they are not needed:<br>
![image](https://user-images.githubusercontent.com/63421754/124277936-4e265880-db4e-11eb-9c93-4cf3fb179f89.png)<br>
-I then added a clean step, after which, when viewing the data, I noticed that the CUI attribute is of type number, so I converted it into string. At the same time, I removed the null values:<br>
![image](https://user-images.githubusercontent.com/63421754/124278011-64ccaf80-db4e-11eb-8bd0-c71a8e6aa2f0.png)<br>
- I did all these operations on the other 3 data sets, after which I reated a union to have them all together:<br>
![image](https://user-images.githubusercontent.com/63421754/124278081-7ada7000-db4e-11eb-9476-1eae331461d7.png)<br>
-In the above meeting I filtered the results by counties. For this, I split the ADRESA column by commas, for the last two fields:<br>
![image](https://user-images.githubusercontent.com/63421754/124278153-947bb780-db4e-11eb-880f-9d90691cf64c.png)<br>
-Then, I deleted the first split, as it contained only details about the address and in the second split I filtered by Bacău County:<br>
![image](https://user-images.githubusercontent.com/63421754/124278209-a52c2d80-db4e-11eb-948a-3efee9e7e704.png)<br>
-I made a new split of the ADRESA column by comma, for the first field to remove all the localities. I renamed the column to "localitate":<br>
![image](https://user-images.githubusercontent.com/63421754/124278262-b7a66700-db4e-11eb-9f50-f3b05eb3c6d3.png)<br>
- In the end, I removed the address column, the end result looking like this:<br>
![image](https://user-images.githubusercontent.com/63421754/124278314-c7be4680-db4e-11eb-9363-9a2d4d211ff5.png)<br>

c.Preparing data from bilant_lung files:<br>
Below are the steps I followed for the data from the “2016-bilant-lung” set (I followed the same steps for the other 3 sets): <br>
-First I converted the CUI and CAEN attribute types into string, similar to what I did with the other data set above;<br>
![image](https://user-images.githubusercontent.com/63421754/124278567-15d34a00-db4f-11eb-8168-c78d58b48d85.png)<br>
-After that, I made the union of the 4 sets:<br>
![image](https://user-images.githubusercontent.com/63421754/124278634-297eb080-db4f-11eb-893a-723887106ad7.png)<br>
I added a clean step to this union in which I filtered by CAEN code 47:<br>
![image](https://user-images.githubusercontent.com/63421754/124278678-39969000-db4f-11eb-94f5-0c6d16fb29b1.png)<br>
-I also noticed that some columns have null values that I turned into 0:<br>
![image](https://user-images.githubusercontent.com/63421754/124278762-56cb5e80-db4f-11eb-874b-791cc23cd85f.png)<br>
d.Creating a join between the two unions: <br>
-At the end, I made a join between the two unions made in the previous steps using the CUI code;<br>
![image](https://user-images.githubusercontent.com/63421754/124278831-6d71b580-db4f-11eb-9755-22ae10ae338d.png)<br>
-I added a new clean step to add one last touch to the data. I noticed that there are some fields that have null values, which I turned into 0 by using Group Values. Also, I made an automatic split on the locality column to keep only their name; <br>
- I changed the type of columns in date; <br>
- I also changed their name with the corresponding year. I renamed this column to "Year": <br>
![image](https://user-images.githubusercontent.com/63421754/124278901-837f7600-db4f-11eb-851d-c8fa3bce5bcf.png)<br>
-Finally, I added an Output to be able to further load the result in Tableau Desktop;<br>
![image](https://user-images.githubusercontent.com/63421754/124278966-985c0980-db4f-11eb-8a9e-c0c884bd3ae1.png)<br>
### 3.	Data Visualization & Analysis

In order to interpret the data, I will use Tableau Desktop. Thus, I will start by uploading the Output previously created:<br>
![image](https://user-images.githubusercontent.com/63421754/124279055-b0cc2400-db4f-11eb-95d5-0a7335ebfbf8.png)<br>
-I changed the type of the Localitate column in geographic type in City in order to make a map:<br>
![image](https://user-images.githubusercontent.com/63421754/124279128-c9d4d500-db4f-11eb-8403-2447e2712230.png)<br>
For starters, I made a map to view the location of the county and the number of companies operating in it: <br>
-I used the attributes County and CUI, using count distinct measure, in order to have the exact number of companies depending on the county:<br>
![image](https://user-images.githubusercontent.com/63421754/124279187-e113c280-db4f-11eb-8daa-ad547f418daf.png)<br>
-I added the CUI in both colors and label so that the information is as prominent as possible; <br>
-In addition, I added the county in labels, so that the information is complete;<br>
![image](https://user-images.githubusercontent.com/63421754/124283061-2639f380-db54-11eb-9185-7faf3c32b90e.png)
<br>

<li>From the map above it can be seen that in Bacău County there are 567 companies whose field of activity is retail. </li>
In order to see the distribution of companies in the cities in the county, I made a new map like the one above, but instead of the county, I used Locality.<br>

![image](https://user-images.githubusercontent.com/63421754/124284562-c8a6a680-db55-11eb-93c0-36c5deae28fc.png)<br>
<li> Thus, it is observed that most such companies are located in Bacău, in number of 219. </li>
<br> Next, to see the net income at county level during the 4 years, I made a bar graph using the attributes "Profit net" in rows and Year in columns. <br>

![image](https://user-images.githubusercontent.com/63421754/124284670-d9571c80-db55-11eb-877a-34841ff8504f.png)

<br><li>The graph shows that the highest profit was recorded in 2019. It is also noted that from 2016 to 2019 the net profit continued to increase.</li><br>

In order to be able to compare profit and loss, I created a new side-by-side graph to be able to compare the net profit and loss recorded. For this chart I used year, net loss and net profit. I also did a filter by name, which excluded the company Dedeman, as it greatly influenced the results. Last but not least, I highlighted the values of the results using <i>mark label-always show.</i><br>

![image](https://user-images.githubusercontent.com/63421754/124279879-ac543b00-db50-11eb-8675-71d7c5563ab8.png)<br>

![image](https://user-images.githubusercontent.com/63421754/124282385-706ea500-db53-11eb-89c9-509eb96e2ff9.png)<br>

<li>The graph above shows that over the 4 years, the profit has remained much higher than the loss, especially in 2019 where the difference is much larger. </li> <br>
An important role in reflecting the performance of enterprises is played by the <b> profit rate </b>, which is calculated as a percentage ratio between the sum of the profit of turnover and revenue. Thus, I added a field calculated using the formula below:<br>

![image](https://user-images.githubusercontent.com/63421754/124280258-24bafc00-db51-11eb-87b1-2d59f1fe078f.png)
<br>-I modified the axis to narrow the range shown on it:<br>

![image](https://user-images.githubusercontent.com/63421754/124280507-706da580-db51-11eb-9042-c71521d1f667.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124280391-4c11c900-db51-11eb-83db-4bea5e8a2f4e.png)
<br>
<li>The graph above shows that in 2016 and 2018 the average profit rate had the highest values, while in 2019, it decreased. </li> <br>
Furthermore, in order to find out to what extent the total assets within the companies in this field are influenced by debts, I created a new field to calculate the <b>total assets.</b>

![image](https://user-images.githubusercontent.com/63421754/124280670-a27f0780-db51-11eb-874b-53c09969d0fb.png)<br>

-Then, I used Datorii (debts) and ActiveTotale (total assets) to create a scatterplot chart, and then I added a trend line:<br>

![image](https://user-images.githubusercontent.com/63421754/124280753-bd517c00-db51-11eb-9dfb-6593db397ee3.png)
<br><li>The image above shows that there is a strong correlation (0.84) between the two variables showing that total assets are really influenced by debt. </li> <br>
Furthermore, I created a new calculated field to be able to find out the <b> rotation speed of current assets </b>:<br>

![image](https://user-images.githubusercontent.com/63421754/124280955-ebcf5700-db51-11eb-88ad-9da1d09fd2d0.png)
<br>
-I then created a new chart similar to the one showing the total assets:<br>

![image](https://user-images.githubusercontent.com/63421754/124281073-086b8f00-db52-11eb-9e2d-655bb8f99d00.png)
<br><li>From here it is observed that this coefficient has decreased over the years, which suggests that the degree of asset immobilization has increased.</li>
### 4. Dashboard
<br> Below are the dashboards created within the project. they were also used in the creation of the story.<br>
![image](https://user-images.githubusercontent.com/63421754/124281591-87f95e00-db52-11eb-8762-6d6edc4bebd1.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281647-9778a700-db52-11eb-9c5d-8e0de60df267.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281707-a8c1b380-db52-11eb-87f9-7e6b492619e8.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281744-b4ad7580-db52-11eb-80f0-78e1acefe519.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281775-c131ce00-db52-11eb-88ac-95182a35e179.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281813-cc84f980-db52-11eb-9bb8-29dc988d1e7e.png)
<br>
### 5. Story

![image](https://user-images.githubusercontent.com/63421754/124285753-e9bbc700-db56-11eb-81ff-abf7d3e809eb.png)












 













