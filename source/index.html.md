---
title: IKDB API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell


includes:
  - errors

search: true
---

# Welcome to the IKDB
<img width="600" src="http://thecatapi.com/api/images/get?format=src&type=gif">
Welcome to the Internet Kitten Database (IKDB). The IKDB houses millions of records of kittens ages 0-5 years old. The kittens have first and last name as well as
date of birth, color, and gender

# Caching


The IKDB uses server side caching. If a request is slow it is because the query is not in the cache. Once cached you can
expected better response times. The default cache is 10 minutes.



# Pagination

All list-type API that could potentially contain multiple records will return results in a paginated response. Pagination control is via the query string. The default pagination controls are thus:

Parameter | Description
--------- | -----------
perPage | Returns the desired number of results per page. Defaults to 100 unless otherwise stated
page | Specify which page to start on. Default to 1

# Kittens

## Get All Kittens


```shell
curl "http://localhost:7177/kittens"
```



> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "firstName": "Maddison",
            "lastName": "Anderson",
            "dob": "2015-01-10 23:09:24",
            "color": "Gainsboro",
            "gender": "m",
            "created_at": "2017-10-24 15:27:36",
            "updated_at": "2017-10-24 15:27:36"
        }
     ],
    "current_page": 1,
    "first_page_url": "http://localhost:7177/kittens?page=1",
    "from": 1,
    "last_page": 6500,
    "last_page_url": "http://localhost:7177/kittens?page=6500",
    "next_page_url": "http://localhost:7177/kittens?page=2",
    "path": "http://localhost:7177/kittens",
    "per_page": 100,
    "prev_page_url": null,
    "to": 100,
    "total": 650000
}
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://localhost:7177/kittens`


### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
filters[age] | null | Set to a positive integer to find kittens of this age. Note that kittens less than 1 year are considered age 0
filters[maxAge] | null | Set to a positive integer to find kittens with this maximum age. Note that maxAge is inclusive of the current age. If a kitten is 4.5 years old then maxAge=4 will match that kitten
filters[gender] | null | Set to either `m` for male or `f` for female
filters[color] | null | There are over 150 colors including `Teal`, `RosyBrown`, `Olive` and `Navy`. 
filters[firstName] | null | Set to a string to find kittens with first names starting with the string
filters[lastName] | null | Set to a string to find kittens with last names starting with the string


This endpoint retrieves all kittens without filters

### HTTP Request

`GET http://localhost:7177/kittens`


This endpoint retrieves all kittens 2 years old with color Teal
### HTTP Request

`GET http://localhost:7177/kittens?filters[age]=2&filters[color]=Teal`



This endpoint finds a very specific special kitty
### HTTP Request

`GET http://localhost:7177/kittens?filters[age]=0&filters[color]=Olive&filters[firstName]=Alex&filters[gender]=f`

