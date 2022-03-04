---
title: Commercial General Liability Section OCR
excerpt: ''
hidden: false
---
This article describes how to build an OCR API that extracts data from the Commercial General Liability Section using our deep learning engine. If you want to automate your workflow, this article is for you. 

**Prerequisites**
> 1. You’ll need a free account. [Sign up](https://platform.mindee.com/signup) and confirm your email to login.
> 2. You’ll need at least 20 Commercial General Liability Section images or pdfs to train your OCR.

## Define your Commercial General Liability Section use case
 

First, we’re going to define what fields we want to extract from your **Commercial General Liability Section. 

** 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a73bf8b-capture-decran-2021-01-25-a-210733.png",
        "capture-decran-2021-01-25-a-210733.png",
        447,
        615,
        "#edecec"
      ],
      "caption": ""
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ad69124-capture-decran-2021-01-25-a-210738.png",
        "capture-decran-2021-01-25-a-210738.png",
        447,
        615,
        "#f1f1f2"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6a451cf-capture-decran-2021-01-25-a-210743.png",
        "capture-decran-2021-01-25-a-210743.png",
        447,
        615,
        "#f4f4f4"
      ],
      "caption": "Commercial Liability Section key data extraction"
    }
  ]
}
[/block]
**General Information**
> Agency
> Carrier
> Agency Customer ID
> Policy Number
> Effective Date
> Applicant
> NAIC Code
> Date
 

**Coverages**
> Property Damage Deductibles
> Bodily Injury Deductibles per claim
> Bodily Injury Deductibles per occurrence
 

**Limits**
> General Aggregate Limit
> Products & Completed Operations Aggregate
> Personal & Advertising Injury
> Each Occurrence
> Damage to Rented Premises (each occurrence)
> Medical Expense (any other person)
> Employee Benefit
 

**Premium**
> Premises Operations Premium
> Products Premium
> Other Premium
> Total Premium
 

**Schedule of Hazards**
> Loc #
> Haz #
> Classification
> Class Code
> Premium basis
> Exposure
> Terr
> Premops Rate
 

**Claims Made**
> Proposed Retroactive Date
> Entry Date
 

**Employee Benefits Liability**
> Deductible per Claim
> Number of Employees
> Number of Employees covered
> Retroactive Date
 

**Contractors**
> Paid to Subcontractor
> % of work subcontracted
> Number of Full Time Staff
> Number of Part-Time Staff
 

**Products / Completed Operations**
> Product
> Annual Gross Sales
> Number of Units
> Time to Market
> Expected Life
> Intended Use
> Principal Component
 

​​​​​​​**Additional Interest / Certificate Recipient**
> Name
> Address 
> Rank
> Reference
 

That’s it for our use case. Feel free to add any other relevant data to fit your requirements. 

 

 

## Deploy your API
 

Once you have defined the list of fields you want to extract from your Commercial General Liability Section, head over to the platform and press the ‘**Create a new API**’ button.


[block:html]
{
  "html": "You land now on the setup page. <a \n   href=\"https://mindee-public-website.s3.amazonaws.com/blog/2021/01/25/ilovepdf_merged-4.pdf\"\n   target=\"_blank\">Here is the image</a> you can use to set up the API. For instance, my setup is as follows:"
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9ea52a1-Capture_decran_2021-04-09_a_14.56.50.png",
        "Capture d’écran 2021-04-09 à 14.56.50.png",
        1123,
        454,
        "#f8f9fa"
      ],
      "caption": "Set up your model"
    }
  ]
}
[/block]
Once you’re ready, click on the “**next**” button. We are going to specify the data types for each of the fields we want our API to extract.


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/60df790-Capture_decran_2021-04-09_a_14.56.56.png",
        "Capture d’écran 2021-04-09 à 14.56.56.png",
        1123,
        454,
        "#fbfbfd"
      ],
      "caption": "Define your model"
    }
  ]
}
[/block]
To move forward, you have two possibilities:

**Upload a json config**
Copy the following JSON into a file and upload it on the interface


[block:code]
{
  "codes": [
    {
      "code": "{\n  \"problem_type\": {\n    \"classificator\": { \"features\": [], \"features_name\": [] },\n    \"selector\": {\n      \"features\": [\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"agency\",\n          \"public_name\": \"Agency\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"carrier\",\n          \"public_name\": \"Carrier\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"agency_customer_id\",\n          \"public_name\": \"Agency Customer ID\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"policy_number\",\n          \"public_name\": \"Policy Number\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"effective_date\",\n          \"public_name\": \"Effective Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"applicant\",\n          \"public_name\": \"Applicant\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"naic_code\",\n          \"public_name\": \"NAIC Code\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"date\",\n          \"public_name\": \"Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"property_damage_deductibles\",\n          \"public_name\": \"Property Damage Deductibles\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"bodily_injury_deductibles_per_claim\",\n          \"public_name\": \"Bodily Injury Deductibles per claim\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"bodily_injury_deductibles_per_occurrence\",\n          \"public_name\": \"Bodily Injury Deductibles per occurrence\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"general_aggregate_limit\",\n          \"public_name\": \"General Aggregate Limit\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"products_completed_operations_aggregate\",\n          \"public_name\": \"Products & Completed Operations Aggregate\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"personal_advertising_injury\",\n          \"public_name\": \"Personal & Advertising Injury\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"each_occurrence\",\n          \"public_name\": \"Each Occurrence\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"damage_to_rented_premises_each_occurrence\",\n          \"public_name\": \"Damage to Rented Premises (each occurrence)\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"medical_expense_any_other_person\",\n          \"public_name\": \"Medical Expense (any other person)\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"employee_benefit\",\n          \"public_name\": \"Employee Benefit\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"premises_operations_premium\",\n          \"public_name\": \"Premises Operations Premium\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"products_premium\",\n          \"public_name\": \"Products Premium\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"other_premium\",\n          \"public_name\": \"Other Premium\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"total_premium\",\n          \"public_name\": \"Total Premium\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"loc\",\n          \"public_name\": \"Loc #\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"haz\",\n          \"public_name\": \"Haz\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"classification\",\n          \"public_name\": \"Classification\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"class_code\",\n          \"public_name\": \"Class Code\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"premium_basis\",\n          \"public_name\": \"Premium basis\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"exposure\",\n          \"public_name\": \"Exposure\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"terr\",\n          \"public_name\": \"Terr\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"premops_rate\",\n          \"public_name\": \"Premops Rate\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"proposed_retroactive_date\",\n          \"public_name\": \"Proposed Retroactive Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"convention\": \"US\" } },\n          \"handwritten\": false,\n          \"name\": \"entry_date\",\n          \"public_name\": \"Entry Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"deductible_per_claim\",\n          \"public_name\": \"Deductible per Claim\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"number_of_employees\",\n          \"public_name\": \"Number of Employees\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"number_of_employees_covered\",\n          \"public_name\": \"Number of Employees covered\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": {} },\n          \"handwritten\": false,\n          \"name\": \"retroactive_date\",\n          \"public_name\": \"Retroactive Date\",\n          \"semantics\": \"date\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"paid_to_subcontractor\",\n          \"public_name\": \"Paid to Subcontractor\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"of_work_subcontracted\",\n          \"public_name\": \"% of work subcontracted\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"number_of_full_time_staff\",\n          \"public_name\": \"Number of Full Time Staff\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": 1 } },\n          \"handwritten\": false,\n          \"name\": \"number_of_part_time_staff\",\n          \"public_name\": \"Number of Part-Time Staff\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"product\",\n          \"public_name\": \"Product\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"annual_gross_sales\",\n          \"public_name\": \"Annual Gross Sales\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"number_of_units\",\n          \"public_name\": \"Number of Units\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"time_to_market\",\n          \"public_name\": \"Time to Market\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"expected_life\",\n          \"public_name\": \"Expected Life\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"intended_use\",\n          \"public_name\": \"Intended Use\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"principal_component\",\n          \"public_name\": \"Principal Component\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": 0 } },\n          \"handwritten\": false,\n          \"name\": \"name\",\n          \"public_name\": \"Name\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"address\",\n          \"public_name\": \"Address\",\n          \"semantics\": \"word\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"is_integer\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"rank\",\n          \"public_name\": \"Rank\",\n          \"semantics\": \"amount\"\n        },\n        {\n          \"cfg\": { \"filter\": { \"alpha\": -1, \"numeric\": -1 } },\n          \"handwritten\": false,\n          \"name\": \"reference\",\n          \"public_name\": \"Reference\",\n          \"semantics\": \"word\"\n        }\n      ],\n      \"features_name\": [\n        \"agency\",\n        \"carrier\",\n        \"agency_customer_id\",\n        \"policy_number\",\n        \"effective_date\",\n        \"applicant\",\n        \"naic_code\",\n        \"date\",\n        \"property_damage_deductibles\",\n        \"bodily_injury_deductibles_per_claim\",\n        \"bodily_injury_deductibles_per_occurrence\",\n        \"general_aggregate_limit\",\n        \"products_completed_operations_aggregate\",\n        \"personal_advertising_injury\",\n        \"each_occurrence\",\n        \"damage_to_rented_premises_each_occurrence\",\n        \"medical_expense_any_other_person\",\n        \"employee_benefit\",\n        \"premises_operations_premium\",\n        \"products_premium\",\n        \"other_premium\",\n        \"total_premium\",\n        \"loc\",\n        \"haz\",\n        \"classification\",\n        \"class_code\",\n        \"premium_basis\",\n        \"exposure\",\n        \"terr\",\n        \"premops_rate\",\n        \"proposed_retroactive_date\",\n        \"entry_date\",\n        \"deductible_per_claim\",\n        \"number_of_employees\",\n        \"number_of_employees_covered\",\n        \"retroactive_date\",\n        \"paid_to_subcontractor\",\n        \"of_work_subcontracted\",\n        \"number_of_full_time_staff\",\n        \"number_of_part_time_staff\",\n        \"product\",\n        \"annual_gross_sales\",\n        \"number_of_units\",\n        \"time_to_market\",\n        \"expected_life\",\n        \"intended_use\",\n        \"principal_component\",\n        \"name\",\n        \"address\",\n        \"rank\",\n        \"reference\"\n      ]\n    }\n  }\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**Or build your data model manually**
Using the interface, add up to your data model each field.

In our example, here are the different field configurations we used:

**General Information**
  * **Agency**: type String that never contains numeric characters. 
  * **Carrier**: type String that never contains numeric characters. 
  * **Agency Customer ID**: type String without specifications. 
  * **Policy Number**: type String without specifications. 
  * **Effective Date**: type Date with US format. 
  * **Applicant**: type String that never contains numeric characters. 
  * **NAIC Code**: type Number without specifications. 
  * **Date**: type Date with US format. 
 

**Coverages**
  * **Property Damage Deductibles**: type Number without specifications. 
  * **Bodily Injury Deductibles per claim**: type Number without specifications. 
  * **Bodily Injury Deductibles per occurrence**: type Number without specifications. 
 

**Limits**​​​​​​​
  * **General Aggregate Limit**: type Number without specifications. 
  * **Products & Completed Operations Aggregate**: type String without specifications.
  * **Personal & Advertising Injury**: type String without specifications.
  * **Each Occurrence**: type String without specifications.
  * **Damage to Rented Premises (each occurrence):** type String without specifications.
  * **Medical Expense (any other person)**: type String without specifications.
  * **Employee Benefit**: type String without specifications.
 

​​​​​​​**Premium**
  * **Premises Operations Premium**: type Number without specifications. 
  * **Products Premium**: type Number without specifications. 
  * **Other Premium**: type Number without specifications. 
  * **Total Premium**: type Number without specifications. 
 

​​​​​​​**Schedule of Hazards**
  * **Loc #**: type Number without specifications. 
  * **Haz #**: type Number without specifications. 
  * **Classification**: type String that never contains numeric characters. 
  * **Class Code**: type Number without specifications. 
  * **Premium basis**: type String that never contains numeric characters. 
  * **Exposure**: type Number without specifications. 
  * **Terr**: type Number without specifications. 
  * **Premops Rate**: type Number that is always an integer. 
 

​​​​​​​**Claims Made**
  * **Proposed Retroactive Date**: type Date with US format. 
  * **Entry Date**: type Date with US format. 
 

​​​​​​​**Employee Benefits Liability**
  * **Deductible per Claim**: type Number without specifications. 
  * **Number of Employees**: type Number without specifications. 
  * **Number of Employees covered**: type Number without specifications. 
  * **Retroactive Date**: type Date with US format. 
 

​​​​​​​**Contractors**
  * **Paid to Subcontractor**: type Date with US format. 
  * **% of work subcontracted**: type Number that is always an integer. 
  * **Number of Full Time Staff**: type Date with US format. 
  * **Number of Part-Time Staff**: type Date with US format. 
 

​​​​​​​**Products / Completed Operations**
  * **Product**: type String that never contains numeric characters. 
  * **Annual Gross Sales**: type Number without specifications. 
  * **Number of Units**: type Number without specifications. 
  * **Time to Market**: type Number without specifications. 
  * **Expected Life**: type Number without specifications. 
  * **Intended Use**: type String that never contains numeric characters. 
  * **Principal Component**: type String that never contains numeric characters. 
 

​​​​​​​**Additional Interest / Certificate Recipient**
  * **Name**: type String that never contains numeric characters. 
  * **Address**: type String without specifications. 
  * **Rank**: type Number without specifications. 
  * **Reference**: type String without specifications. 
 

 

Once you’re done setting up your data model, press the **Start training your model** button at the bottom of the screen.

 

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fe50d72-Capture_decran_2021-04-09_a_15.04.53.png",
        "Capture d’écran 2021-04-09 à 15.04.53.png",
        1120,
        629,
        "#fbfbfc"
      ],
      "caption": "Ready to train model"
    }
  ]
}
[/block]
 
 
## Train your Commercial General Liability Section OCR
 

 


 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2793cf3-Capture_decran_2021-04-09_a_15.08.29.png",
        "Capture d’écran 2021-04-09 à 15.08.29.png",
        1318,
        770,
        "#ebecf0"
      ],
      "caption": "Train your model"
    }
  ]
}
[/block]
 

You’re all set! 

 

Now is the time to train your Commercial General Liability Section deep learning model in the Training section of our API. This use case is quite well templated and you should get very high performances with the first training (20 data annotated) :)

 

In a few hours (minutes if you're fast), you’ll get your first model trained and will be able to use your custom OCR API for parsing the Commercial General Liability Section in your application.


To get more information about the training phase, please refer to the  [Getting Started tutorial](doc:build-your-first-document-parsing-api). If you have any question regarding your use case, feel free to reach out on our chat!