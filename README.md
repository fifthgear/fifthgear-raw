#Fifth Gear RAW API - **PRE SEPT 1st 2015 Version**

**NOTE: [Official Fifth Gear API Documentation has moved here. http://docs.infifthgear.com/api](http://docs.infifthgear.com/api)**

The [Fifth Gear](http://infifthgear.com) API acts as the secure bridge between our software and your ecommerce platform, allowing it to automatically send us orders that are downloaded and fulfilled in our warehouses.  Additionally, you can request your supply chain data from our system that will help you efficiently run your business, including inventory quantities, item attributes, order status, tracking numbers, and more.  Our API can seamlessly integrate with any ecommerce platform, removing the chance for any unnecessary changes.              
Below is conceptual documentation related to the types of data that can be automatically requested from our system.  Each number represents a different request, signifying a different interaction, or bridge, between your system and ours.  

1. **Item lookup** - your ecommerce platform can request different attributes of a specific product and our system will return the following details and more.
      - **Product** - name, category, description, item attributes, UPC codes, personalization information, model numbers and model attributes, related items, unit of measurement, alias item numbers, item type (physical or virtual), special order item status, and more.   
      - **Pricing** - retail pricing, promotional pricing, discounts, and even more customization.  
      - **Ecommerce Logic** - Availability status, inventory, gift card information, gift status, return policies, drop ship status, shipping information, sales price text.
      - **Kitting** - kitting information, required components, pricing, ID numbers, kit grouping data.

2. **Item Inventory Lookup** - your ecommerce platform can request the available quantity on hand (inventory less quantity on sales order) of a specific item, as well as the next available date and active/inactive status.

3. **Item Inventory Bulk Lookup** - your ecommerce platform can make a request to return the quantity available over a range of consecutively numbered items for easy item lookup. 

4.  **Export Item Personalization Data** - if you offer any sort of personalization items in your product line, your ecommerce platform can request the possible personalization(s) associated with each product.  Our system will return one or more template input options, their specific template identifiers, names, and customer prompts for typing in their desired customization.  For example, if your product offers an engraving option for the customer's name and birth place, those would be two different templates returned or submitted with all of their respective information included.

5.  **Order Status Lookup by Reference Number** - by submitting an order reference number, our system can return shipping details such as the date the order was shipped, the web order number, our system's order number, the customer's number, the ship status, the SKU, and the item name.  Additionally, there will be carrier specific details such as carrier name, the tracking number, and the quantity shipped. 

6. **Order Status Bulk Lookup** - This API will give you the current order status for all orders loaded into our system by the external website(s).  Any orders created directly in our CRM module will not be included in the data set returned from this API.

7. **Cart Submit** - This is the mechanism through which your ecommerce platform will submit orders to our warehouse management system.  Alternatively, your ecommerce platform can request information from past orders to display, such as in the case of when a customer logs in and views their order history.  The following information and more is transmitted through this action:

   - **Customer information** - name, email, customer number, and fax.
   -  **Shipping information** - shipping price, address, gift address, organization, and carrier. 
   -  **Order information** - discounts, items, price, currency type, comments, order type, date, order number, and source code.
   - **Billing** - Billing can be handled in one of two ways.  Your company can settle the transaction on your side before sending the prepaid order over to our warehouse system for shipping, or we can process and settle the transaction for you.
      - **Prepaid** - check number, check date, and order amount.
      - **Fifth Gear processes transaction** - credit card information including: card holder, billing address, authorization amount, CVV, authorization status, reference number, and authorization processor.  



--------------------

##Base API URL 

- **TEST** https://commerceservicestest.infifthgear.com/v2.0/CommerceServices.svc/Rest
- **PRODUCTION** https://commerceservices.infifthgear.com/v2.0/CommerceServices.svc/Rest

--------------------

##Authentication
For all requests you must provide a CompanyID, Username and Password. If you are unaware of these values please contact your Client Success Manager. 

--------------------

##Example Request and Response

In this example we will be looking up the inventory levels for a specific item in our warehouses.

**POST:** https://commerceservicestest.infifthgear.com/v2.0/CommerceServices.svc/Rest/ItemInventoryLookup

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
Lookup the item details for a given sku. Includes pricing, product attributes, available to purchase qty, categories, description, personalization data and more.

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
            "SalesName": "Product Name",
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
Look up the current inventory qty, back order status and total sku's on hand for any sku in our warehouse. 

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
Lookup available inventory for a range of skus. 

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

    {
      "OperationRequest": {
        "Arguments": null,
        "Errors": null,
        "HTTPHeaders": null,
        "RequestId": null,
        "RequestProcessingTime": 236
      },
      "Response": {
        "DateShipped": "20140119",
        "ExternalCustomerNumber": null,
        "ExternalOrderNumber": null,
        "OrderNumber": "corp-2333471118",
        "ShipmentStatus": [],
        "Status": "Shipped",
        "TrackingDetails": {
          "CarrierURL": "www.fedex.com",
          "TrackingData": [
            {
              "ItemName": null,
              "ItemNumber": "SKU1",
              "LineDateShipped": null,
              "LineStatus": "NotYetShipped",
              "QtyShipped": "1.0000",
              "TrackingNumber": "12345123451234512345"
            }
          ],
          "TrackingUrl": "http://fedex.com/Tracking?ascend_header=1&clienttype=dotcom&cntry_code=us&language=english&tracknumbers=",
          "TrackingUrlSeperator": ""
        }
      }
    }


--------------------

##OrderStatusBulkLookup
This API will give you the current order status for all orders loaded into our system by the external website(s).  Any orders created directly in our CRM module will not be included in the data set returned from this API.

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


    {
      "OperationRequest": null,
      "Response": {
        "Statuses": [
          {
            "DateShipped": null,
            "ExternalCustomerNumber": "",
            "ExternalOrderNumber": "ord-1034561",
            "OrderNumber": "10",
            "ShipmentStatus": [
              {
                "ShipmentNumber": null,
                "Status": null,
                "TrackingDetails": {
                  "CarrierURL": "",
                  "TrackingData": [
                    {
                      "ItemName": "AdultShinyCap&Gown-Red-51",
                      "ItemNumber": "GS-CGAS-RED-51",
                      "LineDateShipped": null,
                      "LineStatus": null,
                      "QtyShipped": "6.0000",
                      "TrackingNumber": "911978371406530"
                    }
                  ],
                  "TrackingUrl": "",
                  "TrackingUrlSeperator": ""
                }
              }
            ],
            "Status": "Closed",
            "TrackingDetails": {
              "CarrierURL": null,
              "TrackingData": [],
              "TrackingUrl": null,
              "TrackingUrlSeperator": null
            }
          },
          {
            "DateShipped": null,
            "ExternalCustomerNumber": "",
            "ExternalOrderNumber": "ord-100002",
            "OrderNumber": "133",
            "ShipmentStatus": [
              {
                "ShipmentNumber": null,
                "Status": null,
                "TrackingDetails": {
                  "CarrierURL": "",
                  "TrackingData": [
                    {
                      "ItemName": "AdultMatteCap&Gown-Black-45",
                      "ItemNumber": "GS-CGAM-BLK-45",
                      "LineDateShipped": null,
                      "LineStatus": null,
                      "QtyShipped": "3.0000",
                      "TrackingNumber": "911978371438562"
                    },
                    {
                      "ItemName": "AdultMatteCap&Gown-Black-51",
                      "ItemNumber": "GS-CGAM-BLK-51",
                      "LineDateShipped": null,
                      "LineStatus": null,
                      "QtyShipped": "12.0000",
                      "TrackingNumber": "911978371438562"
                    }
                  ],
                  "TrackingUrl": "",
                  "TrackingUrlSeperator": ""
                }
              }
            ],
            "Status": "Closed",
            "TrackingDetails": {
              "CarrierURL": null,
              "TrackingData": [],
              "TrackingUrl": null,
              "TrackingUrlSeperator": null
            }
          },
          {
            "DateShipped": null,
            "ExternalCustomerNumber": "",
            "ExternalOrderNumber": "Ord3",
            "OrderNumber": "Test-157",
            "ShipmentStatus": [
              {
                "ShipmentNumber": null,
                "Status": null,
                "TrackingDetails": {
                  "CarrierURL": "",
                  "TrackingData": [],
                  "TrackingUrl": "",
                  "TrackingUrlSeperator": ""
                }
              }
            ],
            "Status": "Cancelled",
            "TrackingDetails": {
              "CarrierURL": null,
              "TrackingData": [],
              "TrackingUrl": null,
              "TrackingUrlSeperator": null
            }
          }
        ],
        "TotalOrderResults": 3
      }
    }


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
The Cart submit accepts two types of payment : **Credit and Cash**. Cash transaction will automatically be loaded into Fifth Gear without requiring any credit card data.

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
