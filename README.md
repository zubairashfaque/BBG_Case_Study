# BBG Case Study

## All code is in _BBG_Case_Study.ipynb_

### Import Libraries

- [pandas] - Used for Pandas dataframe.
- [numpy] - Used for handling Null values.
- [json] - Used for handling GET API request.
- [requests] - Used for handling GET API request.
- [gspread] - Used for handling google spread sheets.


### Loading Dataset and Doing Initial Analysis
We have 3 datasets contain following information.
- A CSV file containing a shop mapping.
- An Excel file containing orders (revenue) on date per web shop and category between February 15 - March 15, 2022.
- An Excel file containing cost data (advertising) on date per shop between February 15 - March 15, 2022.


We have observed in order dataset the column "product_category" have null values seems some data is missing. 

![image](https://user-images.githubusercontent.com/7127134/207832407-a4a4d0eb-a5ac-413a-97d0-fd9e925513a2.png)

So, we are goinmg to replace it with Unknown category.

### Identifying unwanted Values and Removing Them (Data integrity)

We also observed that in order dataset the column "discount currency" have some incorrect values so, we have to fix it keep things symmetrical.

![image](https://user-images.githubusercontent.com/7127134/207832937-0e37269a-c870-45be-aff7-76d06f1274f6.png)
![image](https://user-images.githubusercontent.com/7127134/207833059-4e7b05dc-cb3f-4c23-adf1-c47f07e6054d.png)

### Data Aggregation

Merge Cost Data with content Data to get shopewise currency information.

![image](https://user-images.githubusercontent.com/7127134/207833320-b4243388-8b8b-4538-9429-a96c84ad62a5.png)

#### Exchange API call

Exchange API call and savinf the data in data frame.

![image](https://user-images.githubusercontent.com/7127134/207833491-86f5b8f5-b089-4e56-86da-ddfe8a092e36.png)

Merge new Cost Dataframe with API call to get shop wise currency conversion rate. As we need to calculate discount in future on basis of local currency.

![image](https://user-images.githubusercontent.com/7127134/207833582-14d677a0-bbb8-45af-9c91-1c681acc21b3.png)

So, our objective is to have all discounts and revenues in EUR so we have to convert all currencies to EUR. So, in case of cost EUR normalization can be done by diving "advertising_costs (local currency)" by "conversion_rates" and placing all values in new column "Cost_in_ads_eur".

![image](https://user-images.githubusercontent.com/7127134/207833782-f3354b88-91b8-4f28-a3f1-c6268e0ab06e.png)

In order dataset we have discount in EUR or LOCAL. We have to normalize all discount in EUR. So, in first set make new column and place all EUR values in it.

To get local curency for discount merge dataframe on basis of shop ids.

To normalize discount currency we have to check whether discount currency is EUR or Local in case of EUR we will use same EUR value and in case of LOCAL we convert by dividing current value by conversion rate value. And done in the loop

![image](https://user-images.githubusercontent.com/7127134/207834090-dbf11536-d76a-4b10-b3e9-1e9b06cb32e9.png)

Now, we have to get cost of add rate in the table.

To get country code "UK, DE" split Shop_Name to two columns

Calculating each transaction by adding discount value because all discount are in nagative so will add them will do work.
![image](https://user-images.githubusercontent.com/7127134/207834262-318ec077-6668-4e59-ac8f-3da00b800ecf.png)


My understanding is that total revenue mean have to calculte revenue of a shop in provided period so for that have to group by shop ID and calculate sum. And to calculate Revenue Share we have to do same but this time group by product category and Shop id then sum of revelue after discount and first calculate total revenue each shop category.

![image](https://user-images.githubusercontent.com/7127134/207834497-7c18a3c1-8568-4bd9-91cd-48b4aae3da2b.png)

![image](https://user-images.githubusercontent.com/7127134/207834645-875b987a-17c8-4776-8e75-a759e34a29b2.png)


Final result

![image](https://user-images.githubusercontent.com/7127134/207834782-84ffe510-c6f4-43a9-bc7c-437a344f7c5b.png)


## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
