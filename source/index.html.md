---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Specs Database API! You can use our API to access Specs Database API endpoints, which can get information on various watch specs, brands, models and model numbers in application's database.

We have language bindings in Shell and Ruby. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

You also can use [Specs Client](https://github.com/crownandcaliber/specs_client) - it is ruby client for accessing to the Specs Database.

# Authentication

> To authorize, use this code:

```ruby
client = Specs::Client.new(username, password)
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -u username:password
```

> Make sure to replace `username` and `password` with your API key.

Specs Database uses API username and password to allow access to the API.

Specs Database expects for the API username and password to be included in all API requests to the server that looks like the following:

`-u username:password`

<aside class="notice">
You must replace <code>username</code> and <code>password</code> with your personal API credentials.
</aside>

# Watch specs

## Search Watch Specs

```ruby
client = Specs::Client.new(username, password)
client.search('Submariner')
```

```shell
curl "http://example.com/api/v1/search"
  -u username:password -d "term=Submariner"
```

> The above command returns JSON structured like this:

```json
[
  {
    "ccspec_number": "CCS-BRE-1-YUX-1",
    "name": "Aerospace Avantage E79362",
    "brand_name": "Avantage",
    "model_name": "Aerospace",
    "model_number": "E79362",
    "thumb" : "/placeholder.jpg"
  },
  {
    "ccspec_number": "CCS-ROL-114200-EED-0",
    "name": "Air-King 114200",
    "brand_name": "Rolex",
    "model_name": "Air-King",
    "model_number": "114200",
    "thumb" : "/placeholder.jpg"
  }
]
```

This endpoint allows to search Watch Specs by keyword(s).

### HTTP Request

`GET http://example.com/api/v1/search`

### Query Parameters

Parameter | Description
--------- | -----------
term | Keyword(s) for the searching

## Get a Specific Watch Spec

```ruby
client = Specs::Client.new(username, password)
client.ccspec.show('CCS-BRE-1-SDD-1')
```

```shell
curl "http://example.com/api/v1/ccspecs/CCS-BRE-1-SDD-1"
  -u username:password
```

> The above command returns JSON structured like this:

```json
{
  "ccspec" {
    "name":"Breguet Submariner I30-JK",
    "brand_name":"Breguet",
    "model_name":"Submariner",
    "model_number":"I30-JK",
    "thumb":"/placeholder.jpg",
    "ccspec_number":"CCS-BRE-1-SDD-1",
    "alternate_reference_numbers":[],
    "description":"",
    "years_released":"",
    "years_stopped":"",
    "water_resistance":10,
    "jewels":"559",
    "base_caliber":"215 PS",
    "manuf_caliber":"test",
    "movement_type":"Automatic",
    "case_back":"Hinged",
    "bezel_insert_colors":["0-60 (Dive)"],
    "case_size":23333.0,
    "crystal_materials":["Mineral"],
    "lug_width":14.0,
    "case_materials":["Aluminium"],
    "bezel_materials":["18k Rose"],
    "case_shape":"Oblong",
    "band_materials":["18k Rose"],
    "dial_colors":["Amber","Anthracite/Black Sub","Ardoise"],
    "power_reserve":"",
    "case_thickness":44.0,
    "gender":"Women",
    "model_pictures":["/placeholder.jpg"]}
  }
}
```

This endpoint retrieves a specific watch spec.

### HTTP Request

`GET http://example.com/api/v1/ccspecs/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The Watch Spec number

## Get a list by brand ID or name

```ruby
  client = Specs::Client.new(username, password)
  #with brand name
  client.ccspecs.by_brand_id("Breguet")
  #with brand ID
  client.ccspecs.by_brand_id("115")
```

```shell
  #with brand name
  curl "http://example.com/api/v1/ccspecs/"
    -u username:password -d brand_id=Breguet

  #with brand ID
  curl "http://example.com/api/v1/ccspecs/"
    -u username:password -d brand_id=115
```


> The above command returns JSON structured like this:

```json
{
  "ccspecs": [
    {
      "ccspec_number": "CCS-BRE-1-YUX-1",
      "name": "Aerospace Breguet E79362",
      "brand_name": "Breguet",
      "model_name": "Aerospace",
      "model_number": "E79362",
      "thumb" : "/placeholder.jpg"
    },
    {
      "ccspec_number": "CCS-ROL-114200-EED-0",
      "name": "Air-King 114200",
      "brand_name": "Breguet",
      "model_name": "Air-King",
      "model_number": "114200",
      "thumb" : "/placeholder.jpg"
    }
  ]

}
```

This endpoint returns Watch Specs by the brand ID or name.

### HTTP Request

`GET http://example.com/api/v1/ccspecs/`

### URL Parameters

Parameter | Description
--------- | -----------
brand_id | The brand ID or name

## Get a list by model ID or name

```ruby
  client = Specs::Client.new(username, password)
  #with model name
  client.ccspecs.by_model_id("Breguet")

  #with model ID
  client.ccspecs.by_model_id("25")
```

```shell
  #with model name
  curl "http://example.com/api/v1/ccspecs/"
    -u username:password -d model_id=Breguet
  #with model ID
  curl "http://example.com/api/v1/ccspecs/"
    -u username:password -d model_id=25
```


> The above command returns JSON structured like this:

```json
{
  "ccspecs": [
    {
      "ccspec_number": "CCS-BRE-1-YUX-1",
      "name": "Aerospace Breguet E79362",
      "brand_name": "Breguet",
      "model_name": "Aerospace",
      "model_number": "E79362",
      "thumb" : "/placeholder.jpg"
    },
    {
      "ccspec_number": "CCS-ROL-114200-EED-0",
      "name": "Air-King 114200",
      "brand_name": "Breguet",
      "model_name": "Air-King",
      "model_number": "114200",
      "thumb" : "/placeholder.jpg"
    }
  ]

}
```

This endpoint returns Watch Specs by the model ID or name.

### HTTP Request

`GET http://example.com/api/v1/ccspecs/`

### URL Parameters

Parameter | Description
--------- | -----------
model_id | The model ID or name

## Get a list by model number ID

```ruby
  client = Specs::Client.new(username, password)
  client.ccspecs.by_model_number_id("105")
```

```shell
  curl "http://example.com/api/v1/ccspecs/"
    -u username:password -d model_number_id=25
```


> The above command returns JSON structured like this:

```json
{
  "ccspecs": [
    {
      "ccspec_number": "CCS-BRE-1-YUX-1",
      "name": "Aerospace Breguet E79362",
      "brand_name": "Breguet",
      "model_name": "Aerospace",
      "model_number": "E79362",
      "thumb" : "/placeholder.jpg"
    },
    {
      "ccspec_number": "CCS-ROL-114200-EED-0",
      "name": "Air-King 114200",
      "brand_name": "Breguet",
      "model_name": "Air-King",
      "model_number": "114200",
      "thumb" : "/placeholder.jpg"
    }
  ]

}
```

This endpoint returns Watch Specs by the model number ID.

### HTTP Request

`GET http://example.com/api/v1/ccspecs/`

### URL Parameters

Parameter | Description
--------- | -----------
model_number_id | The model number ID

## Create Watch Spec

```ruby
  params = {
    "analog_digital" => 'Analog',
    "band_materials" => ["Stainless Steel"],
    "bezel_materials" => ["Titanium"],
    "case_back" => "Steel",
    "case_materials" => ["Stainless Steel"],
    "case_size" => "42.0",
    "crystal_materials" => ["Diamond"],
    "dial_colors" => ["Black"],
    "gender" => "Men",
    "model_name" => "50s Presidents",
    "model_number" => "210150.278LF",
    "movement_type" => "Automatic",
    "brand_name" => "Vulcain"
  }

  client = Specs::Client.new(username, password)
  client.ccspecs.create(params)
```

```shell

  curl "http://example.com/api/v1/ccspecs/"
    -X POST
    -u username:password
    -d "{ \"ccspec\": { \"analog_digital\": \"Analog\", \"band_materials\": [\"Stainless\"]}, /
      { \"bezel_materials\": [\"Titanium\"], \"case_back\": \"Steel\" } }" \
```


> The above command returns JSON structured like this:

```json
{
  status: "success"
}
```

This endpoint creates new Watch Spec.

### HTTP Request

`GET http://example.com/api/v1/ccspecs/`

### Ccspec params

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
brand_name | String | Yes | Brand name
model_name | String | Yes | Model name
model_number | String | Yes | Model number
gender | String | Yes | Gender
movement_type | String | Yes | Movement type
case_size | Float | Yes | Case size
case_materials | Array | Yes | Case materials
band_materials | Array | Yes | Band materials
bezel_materials | Array | Yes | Bezel materials
dial_colors | Array | Yes | Dial colors
crystal_materials | Array | Yes | Crystal materials
case_back | String | Yes | Case back
analog_digital | String | Yes | Type of display
name | String | No | Name
alternate_reference_numbers | Array | No | Alternate reference numbers
merchandising_name | String | No | Merchandising name
description | String | No | Description
check_for | String | No | Check for
style | String | No | Style
case_shape | String | No | Case shape
case_thickness | Float | No | Case thickness
lug_width | Float | No | Lug width
water_resistance | Float | No | Water resistance
bracelet_name | String | No | Bracelet name
bezel_insert_colors | Array | NO | Bezel insert colors
bezel_insert_materials | Array | NO | Bezel insert materials
bezel_features | Array | NO | Bezel features
diamond_dial | Boolean | No | Diamond dial
complications | Array | NO | Complications
calendar_type | String | NO | Calendar type
manuf_caliber | String | NO | Manufacturer caliber
base_caliber | String | NO | Base caliber
power_reserve | String | NO | Power reserve
jewels | String | NO | Jewels
manuf_diamonds | Boolean | NO | Manufacturer diamonds
years_released | String | NO | Years released
years_stopped | String | NO | Years stopped

# Brands

## List of all brands

```ruby
client = Specs::Client.new(username, password)
client.brands.all
```

```shell
curl "http://example.com/api/v1/brands/"
  -u username:password
```

> The above command returns JSON structured like this:

```json
{
  "brands":
  [
    { "id":165,
      "name":"Rolex",
      "alternate_spellings":["1"]
    },
    {
      "id":152,
      "name":"Breguet",
      "alternate_spellings":["111"]
    }
  ]
}
```

This endpoint returns list of a all brands.

### HTTP Request

`GET http://example.com/api/v1/brands`

## Get brand by an ID or name

```ruby
client = Specs::Client.new(username, password)
#return brand by ID
client.brands.by_id("20")

#return brand by name
client.brands.by_name("Rolex")
```

```shell
#return brand by ID
curl "http://example.com/api/v1/brands/20"
  -u username:password -d

#return brand by name
curl "http://example.com/api/v1/brands/Rolex"
  -u username:password -d
```

> The above command returns JSON structured like this:

```json
{
  "brand":
    {
      "id":49,
      "name":"Rolex",
      "alternate_spellings":["Rollex","Roolex"]
    }
}
```

This endpoint returns brand by ID or name.

### HTTP Request

`GET http://example.com/api/v1/brands/ID`

Parameter | Description
--------- | -----------
ID | Brand ID or name

# Models

## Get model by an ID or name

```ruby
client = Specs::Client.new(username, password)
#return model by ID
client.model.by_id("25")

#return model by name
client.model.by_name("Submariner")
```

```shell
#return model by ID
curl "http://example.com/api/v1/models/25"
  -u username:password -d

#return model by name
curl "http://example.com/api/v1/models/Submariner"
  -u username:password -d
```

> The above command returns JSON structured like this:

```json
{
  "model":
    {
      "id":739,
      "name":"Submariner",
      "brand_id":151,
      "brand_name":"King-Dooley"
    }
}
```

This endpoint returns model by ID or name.

### HTTP Request

`GET http://example.com/api/v1/models/ID`

Parameter | Description
--------- | -----------
ID | Model ID or name

## Get a list by brand ID or name

```ruby
client = Specs::Client.new(username, password)
#return models by  brand ID
client.models.by_brand_id("20")

#return models by name
client.models.by_brand_name("Rolex")
```

```shell
#return models by ID
curl "http://example.com/api/v1/models"
  -u username:password -d brand_id=25

#return models by name
curl "http://example.com/api/v1/models"
  -u username:password -d brand_id=Rolex
```

> The above command returns JSON structured like this:

```json
{
  "models":
    [
      {
        "id":737,
        "name":"Submariner",
        "brand_id":5
      },
      {
        "id":747,
        "name":"Daytona",
        "brand_id":5
      }
    ]
}
```

This endpoint returns list of a models by brand ID or name.

### HTTP Request

`GET http://example.com/api/v1/models`

Parameter | Description
--------- | -----------
brand_id | Brand ID or name

# Model Numbers

## Get a list by brand ID or name

```ruby
client = Specs::Client.new(username, password)
#return model numbers by  brand ID
client.model_numbers.by_brand_id("20")

#return model numbers by name
client.model_numbers.by_brand_name("Rolex")
```

```shell
#return model numbers by brand ID
curl "http://example.com/api/v1/model_numbers"
  -u username:password -d brand_id=25

#return model numbers by brand name
curl "http://example.com/api/v1/model_numbers"
  -u username:password -d brand_id=Rolex
```

> The above command returns JSON structured like this:

```json
{
  "model_numbers":
    [
      {
        "id":25,
        "model_number":"CCS-RL-39-1",
        "brand_id":25,
        "model_id":737
      },
      {
        "id":29,
        "model_number":"CCS-RL-26-0",
        "brand_id":25,
        "model_id":747
      }
  ]
}
```

This endpoint returns list of a model numbers by brand ID or name.

### HTTP Request

`GET http://example.com/api/v1/model_numbers`

Parameter | Description
--------- | -----------
brand_id | Brand ID or name

## Get a list by model ID or name

```ruby
client = Specs::Client.new(username, password)
#return model numbers by model ID
client.model_numbers.by_model_id("39")

#return model numbers by model name
client.model_numbers.by_model_name("Submariner")
```

```shell
#return model numbers by model ID
curl "http://example.com/api/v1/model_numbers"
  -u username:password -d model_id=39

#return model numbers by model name
curl "http://example.com/api/v1/model_numbers"
  -u username:password -d model_id=Submariner
```

> The above command returns JSON structured like this:

```json
{
  "model_numbers":
    [
      {
        "id":25,
        "model_number":"CCS-RL-39-1",
        "brand_id":25,
        "model_id":39
      },
      {
        "id":29,
        "model_number":"CCS-RL-26-0",
        "brand_id":25,
        "model_id":39
      }
  ]
}
```

This endpoint returns list of a model numbers by model ID or name.

### HTTP Request

`GET http://example.com/api/v1/model_numbers`

Parameter | Description
--------- | -----------
model_id | Model ID or name

# Global Values

## List of all global values

```ruby
client = Specs::Client.new(username, password)
client.global_values.all
```

```shell
#all global values
curl "http://example.com/api/v1/global_values/"
  -u username:password
```

> The above command returns JSON structured like this:

```json
{
  "attributes":
    {
      "gender":["Men","Women","Unisex"],
      "style":["Sport","Classic"],
      "case_shape":["Cushion","Cushion-y round?","Oblong","Octagon","Other"],
      "case_materials":["18k Rose","18k White","18k Yellow","Aluminium","Bi Color","Black Ceramic"]
    }
}
```

This endpoint returns list of all global values.

### HTTP Request

`GET http://example.com/api/v1/global_values`

## Get a global value by name

```ruby
client = Specs::Client.new(username, password)
client.global_values.by_name("gender")
```

```shell
#all global values
curl "http://example.com/api/v1/global_values/gender"
  -u username:password
```

> The above command returns JSON structured like this:

```json
{
  "attribute": ["Men","Women","Unisex"]
}
```

This endpoint returns a certain global value.

### HTTP Request

`GET http://example.com/api/v1/global_values/ID`

Parameter | Description
--------- | -----------
ID | Global value name
