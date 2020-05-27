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

An API token is required for most routes. Tokens are passed in a header like `Authorization: token`.  Or as a curl request: `curl -H "Authorization: token" https://bienapi.xyz`. 

Get a token using the `/token` route, see below.

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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

con <- HttpClient$new("https://bienapi.xyz")
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

