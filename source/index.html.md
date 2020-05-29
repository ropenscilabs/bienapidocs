---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - r

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the BIEN API!

We have examples for Shell, Ruby, and R. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

An API token is required for most routes. Tokens are passed in a header like `Authorization: token`, for example: `curl -H "Authorization: token" https://bienapi.xyz`. 

Get a token using the [/token](#token) route.

<aside class="notice">
You must get your own personal API key.
</aside>


# Heartbeat

List all API routes

<aside class="notice">
No API key required for this route.
</aside>

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
res = con.get '/heartbeat'
res.body
```

```shell
curl https://bienapi.xyz/heartbeat
```

```r
library(crul)
con <- HttpClient$new("https://bienapi.xyz")
con$get("heartbeat")
```

> The above command returns JSON structured like this:

```json
{
  "routes": [
    "/token/?",
    "/authorized/?",
    "/?",
    "/heartbeat/?",
    "/list/?",
    "/list/country/?",
    "/plot/metadata/?",
    "/plot/protocols/?",
    "/traits/?",
    "/traits/family/?",
    "/traits/family/:id/?",
    "/occurrence/species/?",
    "/occurrence/genus/?",
    "/occurrence/family/?",
    "/occurrence/count/?",
    "/taxonomy/species/?",
    "/phylogeny/?",
    "/meta/version/?",
    "/meta/politicalnames/?",
    "/ranges/list/?",
    "/ranges/species/?",
    "/ranges/genus/?",
    "/ranges/spatial/?",
    "/stem/species/?",
    "/stem/genus/?",
    "/stem/family/?",
    "/stem/datasource/?"
  ]
}
```

`GET https://bienapi.xyz/heartbeat`


# Token

Get an API key/token

<aside class="notice">
No API key required for this route.
</aside>

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
res = con.get '/token'
res.body
```

```shell
curl https://bienapi.xyz/token
```

```r
library(crul)
con <- HttpClient$new("https://bienapi.xyz")
con$get("token")
```

> The above command returns JSON structured like this:

```json
{
  "email": "foo@bar.com",
  "token": "<token>"
}
```


`GET https://bienapi.xyz/token`


# Species lists

## Extract species lists

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/list'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/list"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("list")
```

> The above command returns JSON structured like this:

```json
{
  "count": 331065,
  "returned": 10,
  "data": [
    {
      "species": "Aa achalensis"
    },
    {
      "species": "Aa argyrolepis"
    },
    {
      "species": "Aa calceata"
    }
  ],
  "error": null
}
```


`GET https://bienapi.xyz/list`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at

## Extract species lists by country

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/list/country'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/list/country?country=Canada"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("list/country", query = list(country = "Canada"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 1,
  "returned": 10,
  "data": [
    {
      "species_by_political_division_id": null,
      "scrubbed_species_binomial": "Abelia grandiflora",
      "country": "Canada",
      "is_new_world": 1,
      "is_cultivated_observation": null,
      "is_cultivated_in_region": 0
    },
    {
      "species_by_political_division_id": null,
      "scrubbed_species_binomial": "Abelia xgrandiflora",
      "country": "Canada",
      "is_new_world": 1,
      "is_cultivated_observation": null,
      "is_cultivated_in_region": 0
    }
  ],
  "error": null
}
```


`GET https://bienapi.xyz/list/country`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
country_code | NULL | country code
cultivated | false | return cultivated records as well?
only_new_world | false | return only records from the New World?
limit | 10 | number of results to return
offset | 0 | record number to start at



# Plot

## Plot Metadata

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/plot/metadata'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/plot/metadata"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("plot/metadata")
```

> The above command returns JSON structured like this:

```json
{
  "count": 631121,
  "returned": 10,
  "data": [
    {
      "plot_metadata_id": 2183
    },
    {
      "plot_metadata_id": 2204
    }
  ],
  "error": null
}
```


`GET https://bienapi.xyz/plot/metadata`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
fields | NULL | fields to return, by dafault all are returned
limit | 10 | number of results to return
offset | 0 | record number to start at

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Plot Metadata protocols

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/plot/protocols'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/plot/protocols"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("plot/metadata/protocols")
```

> The above command returns JSON structured like this:

```json
{
  "count": 1,
  "returned": 9,
  "data": [
    {
      "sampling_protocol": "",
      "plot_metadata_id": null
    },
    {
      "sampling_protocol": "0.1 ha  transect, stems >= 2.5 cm dbh",
      "plot_metadata_id": null
    }
  ],
  "error": null
}
```

<!-- <aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside> -->


`GET https://bienapi.xyz/plot/protocols`





# Ranges

## Range: list

List available range maps


```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/ranges/list'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/ranges/list"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("ranges/list")
```

> The above command returns JSON structured like this:

```json
{
  "count": 98829,
  "returned": 10,
  "data": [
    {
      "species": "Aa_argyrolepis",
      "gid": 1
    },
    {
      "species": "Aa_colombiana",
      "gid": 2
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/ranges/list`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at


## Range: species

Range maps for a given species

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/ranges/species', {:species => "Abies lasiocarpa"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/ranges/species?species=Abies%20lasiocarpa"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("ranges/species", query = list(species = "Abies lasiocarpa"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 1,
  "returned": 1,
  "data": [
    {
      "species": "Abies_lasiocarpa",
      "gid": 90,
      "st_astext": "MULTIPOLYGON(((-107.75178470368 28.3154733778057, ..."
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/ranges/species`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
species | NULL | a species name (binomial: "genus epithet")
match_names_only | false | check for range maps for the taxa specified w/o downloading range data

## Ranges: genus

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/ranges/genus', {:genus => "Abies"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/ranges/genus?genus=Abies"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("ranges/genus", query = list(genus = "Abies"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 29,
  "returned": 29,
  "data": [
    {
      "species": "Abies_alba",
      "gid": 73,
      "st_astext": "MULTIPOLYGON(((-77.0940591727373 38.9862810126957, ...)))"
    },
    {
      "species": "Abies_amabilis",
      "gid": 74,
      "st_astext": "MULTIPOLYGON(((-119.61169766459 33.3287672107037, ...)))"
    },
    {
      "species": "Abies_balsamea",
      "gid": 75,
      "st_astext": "MULTIPOLYGON(((-84.0403833648593 35.4759177778039, ...)))"
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/ranges/genus`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
genus | NULL | a genus name
match_names_only | false | check for range maps for the taxa specified w/o downloading range data


## Ranges: spatial

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/ranges/spatial', {:wkt => "POLYGON((-114.03 34.54,-112.67 34.54,-112.67 33.19,-114.03 33.19,-114.03 34.54))"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/ranges/spatial?wkt=POLYGON((-114.03 34.54,-112.67 34.54,-112.67 33.19,-114.03 33.19,-114.03 34.54))"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("ranges/spatial", query = list(wkt = "POLYGON((-114.03 34.54,-112.67 34.54,-112.67 33.19,-114.03 33.19,-114.03 34.54))"))
```

> The above command returns JSON structured like this:

```json
{
  "fix": "me"
}
```

`GET https://bienapi.xyz/ranges/spatial`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
wkt | NULL | xx
species_names_only | false | xx
crop_ranges | false | xx








# Stem

## Stem: species

Extract stem data for a species

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/stem/species', {:species => "Abies amabilis"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/stem/species?species=Abies%20amabilis"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("stem/species", query = list(species = "Abies amabilis"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 15619,
  "returned": 10,
  "data": [
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 70784983,
      "datasource_id": 65,
      "datasource": "FIA",
      "dataset": "U.S. Forest Inventory and Analysis (FIA) National Program",
      "dataowner": "Greg Reams",
      "latitude": "48.603513",
      "longitude": "-121.069843",
      "is_new_world": 1
    },
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 70785003,
      "datasource_id": 65,
      "datasource": "FIA",
      "dataset": "U.S. Forest Inventory and Analysis (FIA) National Program",
      "dataowner": "Greg Reams",
      "latitude": "45.351508",
      "longitude": "-121.847807",
      "is_new_world": 1
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/stem/species`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
species | NULL | a species name (binomial: "genus epithet")


## Stem: genus

Extract stem data for a genus

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/stem/genus', {:genus => "Tovomita"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/stem/genus?genus=Tovomita"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("stem/genus", query = list(genus = "Tovomita"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 460,
  "returned": 10,
  "data": [
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 63198198,
      "datasource_id": 42,
      "datasource": "TEAM",
      "dataset": "Manaus",
      "dataowner": "Eduardo Eler",
      "latitude": "-2.9289898",
      "longitude": "-59.9468382",
      "is_new_world": 1
    },
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 63348187,
      "datasource_id": 42,
      "datasource": "TEAM",
      "dataset": "Manaus",
      "dataowner": "Eduardo Eler",
      "latitude": "-2.9289898",
      "longitude": "-59.9468382",
      "is_new_world": 1
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/stem/genus`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
genus | NULL | a genus name



## Stem: family

Extract stem data for a family

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/stem/family', {:family => "Marantaceae"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/stem/family?family=Marantaceae"
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("stem/family", query = list(family = "Marantaceae"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 30,
  "returned": 10,
  "data": [
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 75556961,
      "datasource_id": 14,
      "datasource": "SALVIAS",
      "dataset": "Gentry Transect Dataset",
      "dataowner": "James S. MIller"
    },
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 75556961,
      "datasource_id": 14,
      "datasource": "SALVIAS",
      "dataset": "Gentry Transect Dataset",
      "dataowner": "James S. MIller"
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/stem/family`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
family | NULL | a family name


## Stem: datasource

Extract stem data for a datasource

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/stem/datasource', {:datasource => "SALVIAS"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/stem/datasource?datasource=SALVIAS" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("stem/datasource", query = list(datasource = "SALVIAS"))
```

> The above command returns JSON structured like this:

```json
{
  "count": 188628,
  "returned": 10,
  "data": [
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 31795391,
      "datasource_id": 33,
      "datasource": "SALVIAS",
      "dataset": "La Selva Secondary Forest Plots",
      "dataowner": "Susan Letcher",
      "latitude": "10.399",
      "longitude": "-84.0995"
    },
    {
      "analytical_stem_id": null,
      "taxonobservation_id": 31795391,
      "datasource_id": 33,
      "datasource": "SALVIAS",
      "dataset": "La Selva Secondary Forest Plots",
      "dataowner": "Susan Letcher",
      "latitude": "10.399",
      "longitude": "-84.0995",
      "plot_name": "LSSFP_26"
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/stem/datasource`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
datasource | NULL | a datasource name







# Traits

## Traits: list

List all available types of trait data

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/traits'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/traits" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("traits")
```

> The above command returns JSON structured like this:

```json
{
  "count": 1,
  "returned": 10,
  "data": [
    {
      "id": null,
      "trait_name": "diameter at breast height (1.3 m)"
    },
    {
      "id": null,
      "trait_name": "flower color"
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/traits`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at



## Traits: family

Extract all trait data for given families

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/traits/family', {:family => "Poaceae"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/traits/family?family=Poaceae" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("traits/family", query = list(family = "Poaceae"))
```

> The above command returns JSON structured like this:

```json
{
  "fix": "me"
}
```

`GET https://bienapi.xyz/traits/family`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at







# Occurrences

## Occurrences: species

Extract occurrence data for a given species

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/occurrence/species', {:species => "Pinus contorta"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/occurrence/species?species=Pinus%20contorta" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("occurrence/species", query = list(species = "Pinus contorta"))
```

> The above command returns JSON structured like this:

```json
{
  "count": null,
  "returned": 3,
  "data": [
    {
      "taxonobservation_id": 42841561,
      "datasource_id": 85,
      "datasource": "VegBank",
      "dataset": "Glacier National Park",
      "dataowner": "Steve Cooper",
      "latitude": "48.682812748",
      "longitude": "-113.583088685",
      "date_collected": "2000-07-11",
      "scrubbed_species_binomial": "Pinus contorta"
    },
    {
      "taxonobservation_id": 42898022,
      "datasource_id": 85,
      "datasource": "VegBank",
      "dataset": "Glacier National Park",
      "dataowner": "Steve Cooper",
      "latitude": "48.682812748",
      "longitude": "-113.583088685",
      "date_collected": "2000-07-11",
      "scrubbed_species_binomial": "Pinus contorta"
    }
  ],
  "error": null
}
```

<aside class="warning">
The count (number of records found) is not being reported for now. Hoping to fix that soon. 
</aside>

<aside class="notice">
More paremeters will be added, e.g., `cultivaed`, `only_new_world`, etc.
</aside>

`GET https://bienapi.xyz/occurrence/species/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
species | NULL | a species name (binomial: "genus epithet")


## Occurrences: genus

Extract occurrence data for a given genus

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/occurrence/genus', {:genus => "Pinus"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/occurrence/genus?genus=Pinus" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("occurrence/genus", query = list(genus = "Pinus"))
```

> The above command returns JSON structured like this:

```json
{
  "count": null,
  "returned": 4,
  "data": [
    {
      "taxonobservation_id": 38103840,
      "datasource_id": 85,
      "datasource": "VegBank",
      "dataset": "Glacier National Park",
      "dataowner": "Steve Cooper",
      "latitude": "48.506137075",
      "longitude": "-113.369232885",
      "date_collected": "2000-08-17",
      "scrubbed_genus": "Abies",
      "scrubbed_species_binomial": "Abies lasiocarpa"
    },
    {
      "taxonobservation_id": 37449270,
      "datasource_id": 85,
      "datasource": "VegBank",
      "dataset": "Glacier National Park",
      "dataowner": "Steve Cooper",
      "latitude": "48.576218428",
      "longitude": "-113.826884591",
      "date_collected": "2000-08-02",
      "scrubbed_genus": "Abies",
      "scrubbed_species_binomial": "Abies lasiocarpa"
    }
  ],
  "error": null
}
```

<aside class="warning">
The count (number of records found) is not being reported for now. Hoping to fix that soon. 
</aside>

<aside class="notice">
More paremeters will be added, e.g., `cultivaed`, `only_new_world`, etc.
</aside>

`GET https://bienapi.xyz/occurrence/genus/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
genus | NULL | a genus name (e.g., Pinus)


## Occurrences: family

Extract occurrence data for a given species

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/occurrence/family', {:family => "Pinaceae"}
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz/occurrence/family?family=Pinaceae" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("occurrence/family", query = list(family = "Pinaceae"))
```

> The above command returns JSON structured like this:

```json
{
  "count": null,
  "returned": 2,
  "data": [
    {
      "taxonobservation_id": 53172406,
      "datasource_id": 21,
      "datasource": "VegBank",
      "dataset": "Southwest GAP, Nevada",
      "dataowner": "Lisa Hahn",
      "latitude": null,
      "longitude": null,
      "custodial_institution_codes": null,
      "collection_code": null,
      "date_collected": "2002-09-18",
      "scrubbed_family": "Pinaceae",
      "scrubbed_species_binomial": "Pinus flexilis"
    },
    {
      "taxonobservation_id": 57033225,
      "datasource_id": 65,
      "datasource": "FIA",
      "dataset": "U.S. Forest Inventory and Analysis (FIA) National Program",
      "dataowner": "Greg Reams",
      "latitude": null,
      "longitude": null,
      "custodial_institution_codes": null,
      "collection_code": null,
      "date_collected": "2004-06-18",
      "scrubbed_family": "Pinaceae",
      "scrubbed_species_binomial": "Pinus monophylla"
    }
  ],
  "error": null
}
```

<aside class="warning">
The count (number of records found) is not being reported for now. Hoping to fix that soon. 
</aside>

<aside class="notice">
More paremeters will be added, e.g., `cultivaed`, `only_new_world`, etc.
</aside>

`GET https://bienapi.xyz/occurrence/family/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
limit | 10 | number of results to return
offset | 0 | record number to start at
family | NULL | a family name (e.g. Pinaceae)








# Citations

## Citations: traits

Extract citation data for a trait

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/meta/citations/traits/20024404/'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz//meta/citations/traits/20024404/" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("/meta/citations/traits/20024404/")
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": null,
      "source": null,
      "url_source": null,
      "source_citation": null,
      "access": "public",
      "project_pi": "Greg Reams",
      "project_pi_contact": null,
      "citation_bibtex": "\"@MISC{noauthor_2013-mm,\n  title        = \"Forest Inventory and Analysis National Program\",\n  year         =  2013,\n  howpublished = \"\\url{http://www.fia.fs.fed.us/}\",\n  note         = \"Accessed: 2013-1-19\"\n}\""
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/meta/citations/traits/:id/`

## Citations: occurrences

Extract citation data for an occurrence

```ruby
require 'faraday'

con = Faraday.new(url: "https://bienapi.xyz")
con.headers[:authorization] = ENV["BIEN_API_KEY"]
res = con.get '/meta/citations/occurrence/22/'
res.body
```

```shell
curl -H 'Authorization: '"$BIEN_API_KEY"'' \
  "https://bienapi.xyz//meta/citations/occurrence/22/" | jq .
```

```r
library(crul)
auth <- list(Authorization = Sys.getenv('BIEN_API_KEY'))
con <- HttpClient$new("https://bienapi.xyz", headers = auth)
con$get("/meta/citations/occurrence/22/")
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "observation_type": "plot",
      "datasource_id": 22,
      "source_name": "Badlands National Park",
      "source_fullname": "Badlands National Park",
      "source_type": "data owner",
      "proximate_provider_name": "VegBank",
      "proximate_provider_datasource_id": 1439,
      "primary_contact_firstname": "Jim",
      "primary_contact_lastname": "Von Low",
      "access_level": "public",
      "locality_error_added": true,
      "locality_error_details": "Reduced precision, selected plots only. Coordinate precision as been reduced to protect endangered species and/or hide locality of private land. Reduction in precision for each plot, if any, is indicated in column coord_uncertainty_m"
    },
    {
      "observation_type": "plot",
      "datasource_id": 1439,
      "source_name": "VegBank",
      "source_type": "proximate provider",
      "proximate_provider_name": "VegBank",
      "proximate_provider_datasource_id": 1439,
      "source_url": "http://vegbank.org/",
      "source_citation": "\"@ARTICLE{Peet2012-qw,\n title = \"{VegBank}: a permanent, open-access archive for vegetation plot\n data\",\n author = \"Peet, Robert K and Lee, Michael T and Jennings, Michael D and\n Faber-Langendoen, Don\",\n journal = \"Biodivers. Ecol.\",\n volume = 4,\n pages = \"233--241\",\n year = 2012\n}\"",
      "access_conditions": "acknowledge",
      "access_level": "public",
      "locality_error_added": false,
      "locality_error_details": "Reduced precision, selected plots only. Coordinate precision as been reduced to protect endangered species and/or hide locality of private land. Reduction in precision for each plot, if any, is indicated in column coord_uncertainty_m"
    }
  ],
  "error": null
}
```

`GET https://bienapi.xyz/meta/citations/occurrence/:id/`
