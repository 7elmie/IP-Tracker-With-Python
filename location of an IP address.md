Get your tools ready

To accomplish this goal, we'll be using two APIs mentioned below:

ipify: This API will help us know the IP address from where the request is coming.
ipapi: This API will help us fetch location information for a particular IP address.
To interact with these APIs, we'll be using the requests library in Python. If you're new to APIs, make sure you check out this tutorial to learn about them.

## You can install this library using the pip command like this :
    $ pip install requests

Once the library is installed, we're good to go!

## Get Location Information
As we discussed, we'll first fetch our IP address from the first API. 
Then we'll make use of this IP address to fetch location information for this particular IP address. 
So, we'll have two functions : 
   
    import requests
    
    def get_ip():
        response = requests.get('https://api64.ipify.org?format=json').json()
        return response["ip"]

    def get_location():
        ip_address = get_ip()
        response = requests.get(f'https://ipapi.co/{ip_address}/json/').json()
        location_data = {
            "ip": ip_address,
            "city": response.get("city"),
            "region": response.get("region"),
            "country": response.get("country_name")
        }
        return location_data
    print(get_location())


In the above code, we have two functions – get_ip() and get_location(). 
Let's discuss each of them separately.

    get_ip() function
As per the API documentation of ipify, we need to make a GET request on https://api.ipify.org?format=json 
to get a JSON response that looks like this:

    {
      "ip": "117.214.109.137"
    }


We store this response in a response variable which is nothing but a sort of Python dictionary with one key-value pair. 
So we returned the value of the key ip as response["ip"].

    get_location() function
As per the API documentation of ipapi, we need to make a GET request on https://ipapi.co/{ip}/{format}/ to get location information for a particular IP address. 
{ip} is replaced by the IP address and {format} can be replaced with any of these – json, jsonp, xml, csv, yaml.


This function internally calls the get_ip() function to get the IP address and then makes a GET request on the URL with the IP address. 
This API returns a JSON response that looks like this:

    {
        "ip": "117.214.109.137",
        "version": "IPv4",
        "city": "Gaya",
        "region": "Bihar",
        "region_code": "BR",
        "country": "IN",
        "country_name": "India",
        "country_code": "IN",
        "country_code_iso3": "IND",
        "country_capital": "New Delhi",
        "country_tld": ".in",
        "continent_code": "AS",
        "in_eu": false,
        "postal": "823002",
        "latitude": 24.7935,
        "longitude": 85.012,
        "timezone": "Asia/Kolkata",
        "utc_offset": "+0530",
        "country_calling_code": "+91",
        "currency": "INR",
        "currency_name": "Rupee",
        "languages": "en-IN,hi,bn,te,mr,ta,ur,gu,kn,ml,or,pa,as,bh,sat,ks,ne,sd,kok,doi,mni,sit,sa,fr,lus,inc",
        "country_area": 3287590,
        "country_population": 1352617328,
        "asn": "AS9829",
        "org": "National Internet Backbone"
    }
    


We get a whole lot of data in the response. You can use whatever works for you. For this tutorial, we'll just be using  city, region and country. 
That's why we created a dictionary called location_data and stored all the data inside it and returned the same.

At last, we call the get_location() function and print the output. Our output will look like this:

    {
      "ip": "117.214.109.137", 
      "city": "Gaya", 
      "region": "Bihar", 
      "country": "India"
    }


## Conclusion
In this article, we learned how we can interact with web services to get location information for a particular IP address.
