---
title: Python Passport OCR
excerpt: ''
---
## Passport data structure
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\nmindee_client = Client(passport_api=\"your_passport_api_key_here\")\n\npassport_data = mindee_client.parse_passport(\"/path/to/file\")",
      "language": "python"
    }
  ]
}
[/block]
### Document level prediction

The document attribute is the passport object constructed by gathering all the pages into a single document. It can reveal useful if you have a pdf of two pages, each of them containing  different side of the passport.
[block:code]
{
  "codes": [
    {
      "code": "passport_data.passport # returns a unique object from class Passport",
      "language": "python"
    }
  ]
}
[/block]
### Page level prediction

For multi pages pdf, the 'pages' attribute is a list of Passport objects, each object is constructed using a unique page of the pdf
[block:code]
{
  "codes": [
    {
      "code": "passport_data.passports # [Passport, Passport ...] ",
      "language": "python"
    }
  ]
}
[/block]
 ### Raw HTTP response
[block:code]
{
  "codes": [
    {
      "code": "passport_data.http_response # full HTTP request object",
      "language": "python"
    }
  ]
}
[/block]
Contains the full Mindee API HTTP response object in JSON format


## Extracted passport fields

Each Passport object contains a set of different fields.
 

To access a passport object, you need to create a **mindee.Client **and call the Client.parse_passport method:
[block:code]
{
  "codes": [
    {
      "code": "from mindee import Client\n\n# Instantiate your client\nmindee_client = Client(passport_token=\"your_api_key_here\")\n\n# Call the Mindee passport endpoint and parse the result\npassport_data = mindee_client.parse_passport(\"/path/to/my/file\")",
      "language": "python"
    }
  ]
}
[/block]
  

Whatever the field type, each of them contains the four following attributes:
> **value**: (Str or Float depending on the field type), corresponds to the field value. Set to None if the >field was not extracted.
> **probability**: (Float), confidence score of the field prediction.
> **bbox**: (Array[Float]), contains the relative vertices coordinates of the bounding box containing the > field in the image. If the field is not written, the bbox is an empty array. 
>r **econstructed**: (Bool), True if the field was reconstructed using other fields.


### Passport's owner data
 

**passport.given_names**: List of passport's owner given names

[block:code]
{
  "codes": [
    {
      "code": "# To get the list of names\ngiven_names = passport_data.passport.given_names\n\n# Loop on each given name\nfor given_name in given_names:\n\n   # To get the name string\n   name = given_name.value",
      "language": "python"
    }
  ]
}
[/block]
 

**passport.surname**: Passport's owner surname

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport's owner surname (string)\nsurname = passport_data.passport.surname.value",
      "language": "python"
    }
  ]
}
[/block]
**passport.gender**: Passport's owner gender (M / F)


[block:code]
{
  "codes": [
    {
      "code": "# To get the passport's owner gender (string among {\"M\", \"F\"}\ngender = passport_data.passport.gender.value",
      "language": "python"
    }
  ]
}
[/block]
**passport.full_name**: Reconstructed Passport's owner full name from surname and given_names

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport's owner full name (string)\nfull_name = passport_data.passport.full_name.value",
      "language": "python"
    }
  ]
}
[/block]
 
**passport.birth_place**: Passport's owner birth place

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport's owner birth place (string)\nbirth_place = passport_data.passport.birth_place.value",
      "language": "python"
    }
  ]
}
[/block]
 
Dates
 

Each date field comes with an extra attribute:

> **date_object**: (Datetime), datetime object from python datetime.date library
 

**passport.birth_date**: Passport's owner date of birth

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport's owner date of birth (string)\nbirth_date = passport_data.passport.birth_date.value",
      "language": "python"
    }
  ]
}
[/block]
 

**passport.expiry_date**: Passport expiry date

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport expiry date (string)\nexpiry_date = passport_data.expiry_date.value",
      "language": "python"
    }
  ]
}
[/block]
 

**passport.issuance_date**: Passport date of issuance

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport date of issuance (string)\nissuance_date = passport_data.passport.issuance_date.value",
      "language": "python"
    }
  ]
}
[/block]
### Passports metadata
 

**passport.mrz1**: Passport first line of machine readable zone

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport  first line of machine readable zone (string)\nmrz1 = passport_data.passport.mrz1.value",
      "language": "python"
    }
  ]
}
[/block]

**passport.mrz2**: Passport second line of machine readable zone

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport second line of machine readable zone (string)\nmrz2 = passport_data.passport.mrz2.value",
      "language": "python"
    }
  ]
}
[/block]
 

**passport.mrz**: Reconstructed passport full machine readable zone from mrz1 and mrz2

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport full machine readable zone (string)\nmrz = passport_data.passport.mrz.value",
      "language": "python"
    }
  ]
}
[/block]

**passport.id_number**: Passport identification number

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport id number (string)\nid_number = passport_data.passport.id_number.value",
      "language": "python"
    }
  ]
}
[/block]
**passport.country**: Passport country code

[block:code]
{
  "codes": [
    {
      "code": "# To get the passport country code (string)\ncountry_code = passport_data.passport.country_code.value",
      "language": "python"
    }
  ]
}
[/block]