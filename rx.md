SparcPharma Search JSON Service Guide
=============================================	

## Document Overview

This document is an Implementation Guide to aid in understanding the proper use of JSON wrapper for the SparcPharma Search Service.

This service is an entity service in inventory of web services. As an entity service, the operations of this service are typically useful for assisting in the automation of multiple business processes. 

This Implementation Guide contains information useful to “consumers” of the operations of this service. This information is intended to supplement the detailed input, headers and JSON response associated with this service. For each service operation, this document includes a description of the operation functions, the Request and Response messages, the pre-conditions, the post-conditions, and the error messages. 

## SparcPharma Search JSON Service
This is a JSON Web service that can be consumed by different applications. Service operations and parameters are defined in the following sections.

### Service Overview
#### Purpose
This SparcPharma Search JSON Service is classified as an "Entity" service in that it contains business logic that is associated with a business entity (i.e., a "Sparc Pharma") which can be re-used for a number of different business processes.

#### Service URL Address
 - End Point: **http://api.sparcpharma.com/api**
 - Domain: **api.sparcpharma.com**
 - Server IP: **159.203.149.70**

Consumers will be using the same URL for UAT and Production. To differentiate between UAT and Production, the end-point expect a mode data (either passed as query string or passed as post form data)

 - *mode=uat* - default value
 - *mode=live*

#### Security
SparcPharma Search JSON Service supports post method only. This service expects following two mandatory headers to be passed with each call.

1. *rx-auth-header*
1. *rx-header-client-ref*

You will receive the values of these headers during the on-boarding process.

## Service Operations
Following operations are supported.

### 1. GetDrugInfo
http://api.sparcpharma.com/api/

*Required headers*
 - *rx-auth-header*
 - *rx-header-client-ref*
 
*Required post data*
 - **action**=GetDrugInfo
 - **gsn**=3775 - GCN Sequence Number.

**Sample Post Request**

        http://api.sparcpharma.com/api/?action=GetDrugInfo&gsn=3775
        rx-auth-header:*********************
        rx-header-client-ref:*********************   
   
**Sample Response**

		{
		  "msg": "success",
		  "result": {
		    "brandName": "ALPRAZOLAM",
		    "genericName": "ALPRAZOLAM",
		    "drugDescription": "USES:  Alprazolam is used to treat anxiety and panic disorders...",
		    "administerInstructions": "HOW TO USE:  Read the Medication Guide provided by your pharmacist...",
		    "contraindications": "PRECAUTIONS:  Before taking alprazolam, tell your doctor...",
		    "disclaimer": "IMPORTANT: HOW TO USE THIS INFORMATION:  This is a summary...",
		    "interactions": "DRUG INTERACTIONS:  See also Warning section...",
		    "missedDoseInfo": "MISSED DOSE:  If you miss a dose...",
		    "sideEffects": "SIDE EFFECTS:  See also Warning section. Drowsiness...",
		    "storageInfo": "STORAGE:  Store at room temperature away from light and moisture..."
		  }
		}
		
**No record found**

		{
		  "msg": "success",
		  "result": {

		  }
		}

### 2. FindDrugByName
http://api.sparcpharma.com/api/

*Required headers*
 - *rx-auth-header*
 - *rx-header-client-ref*
 
*Required post data*
 - **action**=FindDrugByName
 - **prefixText**=pro -  Drug search text of at least 3 character
 - **recordCount**=10 - Optional - default value = 10
 
**Sample Post Request**

        http://api.sparcpharma.com/api/?action=FindDrugByName&prefixText=pro
        rx-auth-header:*********************
        rx-header-client-ref:*********************   
   
**Sample Response**

		{
		  "msg": "success",
		  "result": [
		    "PRO COMFORT ALCOHOL PADS",
		    "PRO COMFORT INSULIN SYRINGE",
		    "PRO COMFORT LANCET",
		    "PRO COMFORT PEN NEEDLE",
		    "PRO COMFORT SPACER-ADULT MASK"
		  ]
		}

**No record found**

		{
		  "msg": "success",
		  "result": {

		  }
		}

### 3. GetPharmacyDrugPricing
http://api.sparcpharma.com/api/

*Required headers*
 - *rx-auth-header*
 - *rx-header-client-ref*
 
*Required post data*
 - **action**=GetPharmacyDrugPricing
 - **zipCode**=92131 -  Zip code of search location for closest pharmacies
 - **drugName**=ALPRAZOLAM INTENSOL - Drug name

**Sample Post Request**

        http://api.sparcpharma.com/api/?action=GetPharmacyDrugPricing&zipCode=92131&drugName=ALPRAZOLAM INTENSOL
        rx-auth-header:*********************
        rx-header-client-ref:*********************   
   
**Sample Response**

		{
		  "msg": "success",
		  "result": {
		    "drugs": [
		      {
			"pharmacy": {
			  "name": "RITE AID PHARMACY 05661",
			  "streetAddress": "8985 MIRA MESA BOULEVARD",
			  "city": "SAN DIEGO",
			  "state": "CA",
			  "zipCode": "92126-2716",
			  "latitude": 32.9139498,
			  "longitude": -117.13006,
			  "hoursOfOperation": "11018208223082240822508226082270918",
			  "phone": "8585663490",
			  "npi": "1376559666",
			  "chainCode": "181",
			  "distance": 3.89
			},
			"drug": {
			  "ndcCode": "781107705",
			  "brandGenericIndicator": "G",
			  "gsn": "3774",
			  "drugRanking": 1,
			  "quantity": 30,
			  "quantityRanking": 1
			},
			"pricing": {
			  "price": 4.50,
			  "priceBasis": "MAC",
			  "usualAndCustomaryPrice": 23.99,
			  "macPrice": 4.50,
			  "awpPrice": 26.17
			}
		      }
		    ],
		    "drugForms": [
		      {
			"form": "TABLET",
			"gsn": "3774",
			"isSelected": true,
			"ranking": 1
		      }
		    ],
		    "drugNames": [
		      {
			"drugName": "ALPRAZOLAM",
			"brandGenericIndicator": "G",
			"isSelected": true
		      }
		    ],
		    "drugQuantities": [
		      {
			"quantity": 30,
			"quantityUom": "TABLET",
			"gsn": "3774",
			"isSelected": true,
			"ranking": 1
		      }
		    ],
		    "drugStrengths": [
		      {
			"strength": "0.5 mg",
			"gsn": "3774",
			"isSelected": true,
			"ranking": 1
		      }
		    ]
		  }
		}

**No record found**

		{
		  "msg": "success",
		  "result": {

		  }
		}

### 4. GetPharmacies
http://api.sparcpharma.com/api/

*Required headers*
 - *rx-auth-header*
 - *rx-header-client-ref*
 
*Required post data*
 - **action**=GetPharmacies
 - **zipCode**=92131 -  Zip code of search location for closest pharmacies

**Sample Post Request**

        http://api.sparcpharma.com/api/?action=GetPharmacies&zipCode=92131
        rx-auth-header:*********************
        rx-header-client-ref:*********************   
   
**Sample Response**

		{
		  "msg": "success",
		  "result": {
		    "pharmacies": [
		      {
			"name": "VONS PHARMACY #4018",
			"streetAddress": "10016 SCRIPPS RANCH BLVD ",
			"city": "SAN DIEGO",
			"state": "CA",
			"zipCode": "92131-1222",
			"latitude": 32.9030914,
			"longitude": -117.100461,
			"hoursOfOperation": "10917209213092140921509216092170917",
			"npi": "1891724811",
			"chainCode": "227",
			"distance": 2.02
		      }
		    ]
		  }
		}

**No record found**

		{
		  "msg": "success",
		  "result": {

		  }
		}

## Errors

In case of any error, you will get 401 HTTP Status Code.

### Client reference not passed

		{
		    "msg": "Client reference is not provided."
		}
		
### Authentication header not passed/Invalid authentication header

		{
		    "msg": "Invalid autehntication header"
		}

### Invalid client reference

		{
		    "msg": "Could not authenticate the client reference, please connect with your administrator."
		}
		
