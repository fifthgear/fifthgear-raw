#Fifth Gear RAW API - **WORKING DRAFT**


This document covers the guidelines for interacting with a specific clients Warehouse Platform. This is a living document and is currently about 70% complete.

--------------------

##Base API URL 

- **TEST** https://commerceservices.infifthgear.com/test/v2.0/CommerceServices.svc/Rest
- **PRODUCTION** https://commerceservices.infifthgear.com/v2.0/CommerceServices.svc/Rest

--------------------

##Authentication
For all requests you must provide a CompanyID, Username and Password. If you are unaware of these values please contact your Client Success Manager. 

--------------------

##Example Request and Response

In this example we will be looking up the inventory levels for a specific item in our warehouses.

**POST:** https://commerceservices.infifthgear.com/test/v2.0/CommerceServices.svc/Rest/ItemInventoryLookup

**Headers** 

- Username  
- Password
- Content-Type: text/json

**Raw Body**: 
    
    {"CompanyId":"CompanyID", "Request": "SKU123" }

The raw body is comprised of a JSON object that contains a CompanyID and a Request. The request might be a simple string value, or in other cases might be a complex data structure (as it is while placing an order).  

**Response**:

    {
        "OperationRequest": null,
        "Response": {
            "AvailableToPurchaseQuantity": 196,
            "BackOrderAvailableDate": "12/26/2013",
            "ItemNumber": "ZK001",
            "Status": 0,
            "TotalSKUs": 0
        }
    }

--------------------

#General Notes

#### Dates
All dates need to be passed in the .NET serialized date format. You can learn more about creating this format here: http://stackoverflow.com/questions/17315394/how-to-format-a-php-date-in-net-datacontractjsonserializer-format

#### HTTPS
All requests MUST be sent through HTTPS

--------------------

#API Calls
We offer the following calls to your Fifth Gear Warehouse.

- **ItemLookup** - access details on any product
- **ItemInventoryLookup** - find the current inventory levels for a given product
- **ItemInventoryBulkLookup** - find the current inventory levels for all products (with a range)
- **ExportItemPersonalizationData** - returns an array of personalization options for a given product
- **OrderStatusLookupByRefNumber** - Track the status of a single order
- **OrderStatusBulkLookup** - Track the status of multiple orders at once
- **CartSubmit** - Place an order!

--------------------

##ItemLookup##
#### URL
 /v2.0/CommerceServices.svc/Rest/ItemLookup


#### Request

    {
        "CompanyId":"CompanyID", 
        "Request": "SKU123" // SKU of the item you're looking for
    }

#### Response

    {
        "OperationRequest": null,
        "Response": {
            "AdditionalSalesPriceText": null,
            "Attributes": null,
            "AvailableToPurchaseQuantity": 196,
            "BasePromotionPrice": 55,
            "BaseRetailPrice": 55,
            "BaseShopperPromotionPrice": 0,
            "Category": "Tote",
            "DefaultPricePercentage": 0,
            "DefaultQuantity": 0,
            "Description": "Zaggo Care System includes the ZaggoCare Guide Book, the pre-assembled tote bag and brochure. ",
            "EMailIDForEGC": null,
            "FormattedDescription": null,
            "GiftCardMessage": null,
            "GiftCardRecipientName": null,
            "GiftCardSendertName": null,
            "GiftCertificateAmount": 0,
            "GiftItemID": null,
            "IsBasePromotionPriceSet": false,
            "IsConfigKit": false,
            "IsDoNotPurchaseActive": false,
            "IsDoNotSellActive": false,
            "IsDropShipItem": false,
            "IsFixedGiftCertificate": false,
            "IsKitPriceDependentOnComponent": false,
            "IsMandatoryKitComponent": false,
            "IsMustForShipping": false,
            "IsPersonalizable": 1,
            "IsPredefinedKit": false,
            "IsSOI": false,
            "IsSelectedKitComponent": false,
            "IsSeries": false,
            "IsStaticKit": false,
            "ItemAttribute": null,
            "ItemNumberAlias": null,
            "KitGroupID": null,
            "KitGroups": [],
            "KitPriceDifference": 0,
            "ModelAttributeValues": [],
            "ModelAttributes": [],
            "ModelItemNumber": null,
            "Number": "ZK001",
            "PersonalizationValues": null,
            "PersonalizedText": null,
            "PromotionPrices": [
                {
                    "Name": null,
                    "Value": "55.000000"
                }
            ],
            "RelatedItems": null,
            "ReturnPolicy": null,
            "SalesName": "ZaggoCare System",
            "SelectedAttributes": [],
            "SelectedQuantity": 0,
            "SelectedUOMData": null,
            "SeriesItemAttributes": null,
            "Status": "Active",
            "TaglineDescription": null,
            "TemplateNumber": null,
            "TemplateVersion": 0,
            "TotalAvailableQuantity": 0,
            "Type": "Physical Item",
            "UOMDetails": null,
            "UPCValue": null
        }
    }


--------------------

##ItemInventoryLookup##

#### URL
 /v2.0/CommerceServices.svc/Rest/ItemInventoryLookup

### Request

    {
        "CompanyId":"CompanyID", 
        "Request": "SKU123" // SKU of the item you're looking for
    }

### Response

    {
        "OperationRequest": null,
        "Response": {
            "AvailableToPurchaseQuantity": 196,
            "BackOrderAvailableDate": "12/26/2013",
            "ItemNumber": "ZK001",
            "Status": 0,
            "TotalSKUs": 0
        }
    }

--------------------

##ItemInventoryBulkLookup##

#### URL
 /v2.0/CommerceServices.svc/Rest/ItemInventoryBulkLookup


#### Request

    {
        "CompanyId":"CompanyID", 
        "Request": {
            "startRange" : 1, // Starting index
            "endRange" : 3 // Ending Index.
        }
    }

#### Response

    {
        "OperationRequest": null,
        "Response": {
            "ItemInventories": [
                {
                    "AvailableToPurchaseQuantity": 6,
                    "ExternalItemNumber": null,
                    "ItemNumber": "Test Item"
                },
                {
                    "AvailableToPurchaseQuantity": 0,
                    "ExternalItemNumber": null,
                    "ItemNumber": "FG-SS-M-Knit.1.1"
                },
                {
                    "AvailableToPurchaseQuantity": 4,
                    "ExternalItemNumber": null,
                    "ItemNumber": "FG-SS-M-Knit.1.2"
                }
            ],
            "TotalSKUResults": 0
        }
    }

--------------------

##ExportItemPersonalizationData##

#### URL
/v2.0/CommerceServices.svc/Rest/ExportItemPersonalizationData

#### Request

    {
        "CompanyId":"CompanyID", 
        "Request": "SKU123" // SKU of the item you're looking for
    }

#### Response

    {
        "OperationRequest" : null,
        "Response" : {
            "ExportPersonalization": [
              {
                "Is_Default": true,
                "Is_Response_Required": true,
                "Item_ID": "76c59887-b679-412a-92c2-fae59a0dd578",
                "Item_Number": "WP-136",
                "List_ID": "c19418be-28cc-41e8-a08b-b3053d3cd1ec",
                "Response_Size": "0",
                "Response_Type": "List",
                "Sort_Order": 1,
                "TemplateLineListName": "Year 71-72",
                "TemplateLineListNumber": "PLN-41",
                "TemplateLineListValues": "1971",
                "TemplateLineNumber": "1",
                "TemplateName": "Name to Print",
                "TemplateNumber": "62",
                "TemplatePrompt": "Your Full Name",
                "TemplateSequence": "1"
              },
              {
                "Is_Default": true,
                "Is_Response_Required": true,
                "Item_ID": "76c59887-b679-412a-92c2-fae59a0dd578",
                "Item_Number": "WP-136",
                "List_ID": null,
                "Response_Size": "10",
                "Response_Type": "String",
                "Sort_Order": 1,
                "TemplateLineListName": null,
                "TemplateLineListNumber": null,
                "TemplateLineListValues": null,
                "TemplateLineNumber": "3",
                "TemplateName": "Birth City",
                "TemplateNumber": "62",
                "TemplatePrompt": "Your Birth City",
                "TemplateSequence": "2"
              }
            ]
        }
    }

--------------------

##OrderStatusLookupByRefNumber

####URL
/v2.0/CommerceServices.svc/Rest/OrderStatusLookupByRefNumber

#### Request

    {
        "CompanyId":"CompanyID", 
        "Request": "OrderRefNumber" // Order Reference Number
    }

#### Response

   COMING SOON


--------------------

##OrderStatusBulkLookup

####URL
/v2.0/CommerceServices.svc/OrderStatusBulkLookup

#### Request

    {
        "CompanyId":"CompanyID", 
        "Request": {
            "FromDate" : /Date(1387721954000-0500)/,  // .NET Datetime String 
            "ToDate" : /Date(1388067628000-0500)/, 
            "StartRange" : 1,
            "EndRange" : 10
        }
    }

#### Response

   COMING SOON


--------------------

## CartSubmit

#### URL
/v2.0/CommerceServices.svc/Rest/CartSubmit

#### Request

    {
      "CompanyId": "ZC",
      "Request": {
        "BillingAddress": {
          "Address1": "9100 Purdue Road",
          "Address2": "Suite 400",
          "City": "Indianapolis",
          "CountryCode": 231, // Fifth Gear Country Code
          "Email": null,
          "Fax": "",
          "IsGiftAddress": false,
          "Organization": null,
          "PhoneNumber": null,
          "PostalCode": "46268",
          "StateOrProvinceCode": 23 // Fifth Gear State Code
        },
        "Charges": [
          {
            "Amount": 13, // Dollar amount for shipping charges
            "ChargeCode": "Shipping Charges"
          }
        ],
        "CountryCode": 231, // Fifth Gear Country Code
        "CurrencyCode": 154, // Fifth Gear Dollar Code - 154 = USD
        "Customer": {
          "CustomerNumber": "",
          "FirstName": "Bob",
          "LastName": "Van Der Konkle",
          "MiddleName": "",
          "RefCustomerNumber": "",
          "Email": "van@xyz.zyx"
        },
        "Discounts": [],
        "Items": [
          {
            "ShipTo": 1, // Ships to the first index of the shiptos array
            "Amount": 55, // Dollar amount for the item
            "ItemNumber": "ZK001",
            "Quantity": 1,
            "Discounts": [],
            "ParentLineNumber": 0,
            "GroupName": null,
            "LineNumber": 1,
            "Comments": null
          }
        ],
        "OrderType": "internet",
        "OrderDate": "/Date(1383312895000-0500)/",  // .NET Datetime String format
        "OrderMessage": "",
        "OrderReferenceNumber": "corp-767444d5d2", // Unique Order Reference ID - must be unique
        "Payment": {
          "IsOnAccountPayment": "false",
          "RedeemablePayments": [],
          // CASH PAYMENT
          "CashPayment": {
            "Amount": 68,
            "ChequeNumber": 10001,
            "ChequeDate": "/Date(1383312895000-0500)/"
          },
          /// CREDIT CARD PAYMENT
          "CreditCardPayments" : [
           {
            "HolderName" : "Bob Van Der Konkle",
            "AddressZip" : "46268",
            "AuthorizationAmount" : 10000, // Total Amount of changes
            "CVV" : 123,
            "ExpirationMonth" : 04,
            "ExpirationYear" : 2014,
            "IsAuthorizationAmountSpecified" : true,
            "AuthorizationCode" : null,
            "AuthorizationProcessor" : "Authorize.net",
            "OrderReferenceNumber" : null,
            "TransactionReferenceNumber" : null
           }
          ]

        },
        "ShipTos": [
          {
            "CarrierAccountNumber": "",
            "ExternalShipCode": "FXG",
            "Recipient": {
              "FirstName": "Bob",
              "LastName": "Van Der Konkle",
              "MiddleName": ""
            },
            "ShipLineID": 1,
            "ShippingAddress": {
              "Address1": "1234 Pine View Dr",
              "Address2": "",
              "City": "Carmel",
              "CountryCode": 231,
              "Email": null,
              "Fax": "",
              "IsGiftAddress": false,
              "Organization": null,
              "PhoneNumber": null,
              "PostalCode": "46032",
              "StateOrProvinceCode": 23
            },
            "ShippingMethodCode": "XC" // Shipping codes can be obtained from your Client Success Manager
          }
        ],
        "Source": "",
        "SourceCode": ""
      }
    }

##### Payments
The Cart submit accepts two types of payment : Credit and Cash. 

** Don't want Fifth Gear to process the order? Use a Cash transaction **

    "Payment": {
      "IsOnAccountPayment": "false",
      "RedeemablePayments": [],
      "CashPayment": {
        "Amount": 68,
        "ChequeNumber": 10001,
        "ChequeDate": "/Date(1383312895000-0500)/"
      }
    }

#### Response

    {
        "OperationRequest" : null,
        "Response" : {
                "OrderReceipt": "4d341e8b-f425-499a-a9a4-79f800d8c0d7",
                "OrderStatus": "NotYetShipped",
                "OrderReferenceNumber": "ord-7HG9IB32F",
                "OrderStatusMessage": "Not Yet Shipped"
        }

    }
