# MCC-Based Merchant Categorization Analysis

## 🎯 Key Improvement: Using NPCI MCC Standards

Based on the [NPCI RuPay Merchant Category Code reference](https://www.npci.org.in/what-we-do/rupay/merchant-category-code), implementing MCC-based categorization will significantly improve merchant classification accuracy.

## 📊 Current Situation Analysis

From the data exploration, I found:

1. **MCC Data Availability**: ~100% coverage
   - Direct `mcccode` column exists in the data
   - MCC codes also embedded in JSON fields within merchant/payee columns
   - Sample MCCs found: 5541 (gas stations), 4900 (utilities), 5812 (restaurants), 4814 (telecom), 5411 (grocery), etc.

2. **Current Name-based Issues**:
   - High "Others" category (~47.7% of transactions)
   - Inconsistent categorization of similar merchants
   - Difficulty categorizing smaller/regional merchants

## 🏷️ NPCI MCC-Based Categories 
POS Merchant Category Codes - June 2025
MCC
MCC Description
Category
5541
Service Stations (without Ancillary services)
High Transacting
5411
Grocery Stores, Supermarkets
High Transacting
5921
Package Stores, Beer, Wine, Liquor
High Transacting
5812
Eating Places and Restaurants
High Transacting
4111
Local/Suburban Commuter Passngr Transport/Ferries
High Transacting
5311
Department Stores
High Transacting
9399
Government Services, Not Elsewhere Classified
High Transacting
5912
Drug Stores and Pharmacies
High Transacting
8062
Hospitals
High Transacting
5699
Miscellaneous Apparel and Accessory Stores
High Transacting
5813
Drinking Places (Alcoholic Bev) - Bars, Taverns
Medium Transacting
5651
Family Clothing Stores
Medium Transacting
7011
Lodging - Hotels, Motels, Resorts
Medium Transacting
5944
Jewellery, Watches, Clocks and Silverware Stores
Medium Transacting
5814
Fast Food Restaurants
Medium Transacting
5691
Men's and Women's Clothing Stores
Medium Transacting
5732
Radio, Television and Stereo Stores
Medium Transacting
4814
Telecommunication Services
Medium Transacting
4812
Telecomm Equipment including Telephone Sales
Medium Transacting
5462
Bakeries
Medium Transacting
5661
Shoe Stores
All Other Categories
5722
Household Appliance Stores
All Other Categories
5499
Misc Food/Convenience Stores/Speciality Markets
All Other Categories
8299
Schools and Educational Services
All Other Categories
4900
Utilities-Electric/Gas/Heating Oil/Sanitary/Water
All Other Categories
7832
Motion Pictures Theatres
All Other Categories
5511
Auto and Truck Dealers (new and used) Sales, Service
All Other Categories
5047
Dental/Laboratory/Medical/Ophthalmic Hospital Supp
All Other Categories
5137
Men's, Women's, And Children's Uniforms
All Other Categories
5441
Candy, Nut, Confectionery Stores
All Other Categories


ECOM Merchant Category Codes - June 2025
MCC
MCC Description
Category
9399
Government Services, Not Elsewhere Classified
High Transacting
4900
Utilities-Electric/Gas/Heating Oil/Sanitary/Water
High Transacting
5411
Grocery Stores, Supermarkets
High Transacting
5699
Miscellaneous Apparel and Accessory Stores
High Transacting
4112
Passenger Railways
High Transacting
4814
Telecommunication Services
High Transacting
5399
Miscellaneous General Merchandise Stores
High Transacting
5814
Fast Food Restaurants
High Transacting
6540
Debit Card to wallet Credit
High Transacting
8220
Colleges, Universities, Professional Schools and Jr
High Transacting
5816
Digital Goods: Games
Medium Transacting
6300
Insurance - Sales and Underwriting
Medium Transacting
8299
Schools and Educational Services
Medium Transacting
6513
Real Estate Agents and Managers - Rentals
Medium Transacting
4784
Toll and Bridge Fees
Medium Transacting
9311
Tax Payments
Medium Transacting
6012
Financial Institutions - Merchandise and Services
Medium Transacting
5262
Marketplaces
Medium Transacting
4722
Travel Agencies
Medium Transacting
5499
Misc Food/Convenience Stores/Speciality Markets
Medium Transacting
8211
Elementary and Secondary Schools
All Other Categories
4899
Cable/Satellite/Other Pay Television/ Radio Srvcs
All Other Categories
5817
Digital Good - Applications (Excluding Games)
All Other Categories
7832
Motion Pictures Theatres
All Other Categories
5691
Men's and Women's Clothing Stores
All Other Categories
4812
Telecomm Equipment including Telephone Sales
All Other Categories
4131
Bus Lines
All Other Categories
7399
Business Services, Not Elsewhere Classified
All Other Categories
5732
Radio, Television and Stereo Stores
All Other Categories
5311
Department Stores
All Other Categories





## 💡 Expected Improvements

Implementing MCC-based categorization should:

1. **Reduce "Others" category** from ~47.7% to likely <10%
2. **Improve accuracy** of merchant classification
3. **Enable better RFM analysis** with cleaner category distributions
4. **Standardize categorization** using industry standards
5. **Better segment high-value categories** like Government/Utilities (high transaction volume)

## 🔧 Implementation Strategy

1. **Extract MCC codes** from multiple columns:
   - Direct `mcccode` column
   - JSON embedded codes in `merchant`, `payee`, `payeeparticulars`

2. **Apply NPCI mapping** to create standardized categories:
   - Food & Dining (5812, 5814, 5813, 5811, 5462)
   - Grocery & Supermarkets (5411, 5499, 5441)
   - Fuel & Transportation (5541, 4111, 4112, 4121, 4214)
   - Government & Utilities (9399, 4900)
   - Healthcare & Medical (8062, 5912, 5047, etc.)
   - And 10+ other precise categories

3. **Maintain fallback** to name-based categorization for edge cases

## 📈 Business Impact

This will enable:
- **More precise user segmentation** by actual spending categories
- **Better recommendation targeting** based on industry-standard categories
- **Improved RFM analysis** with cleaner category distributions
- **Regulatory compliance** with NPCI standards
- **Better cross-category insights** for banking/fintech analysis

