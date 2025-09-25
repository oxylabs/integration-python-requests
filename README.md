# Proxy Integration With Python Requests

[![Oxylabs promo code](https://raw.githubusercontent.com/oxylabs/product-integrations/refs/heads/master/Affiliate-Universal-1090x275.png)](https://oxylabs.io/pages/gitoxy?utm_source=877&utm_medium=affiliate&groupid=877&utm_content=integration-python-requests-github&transaction_id=102f49063ab94276ae8f116d224b67)

[![](https://dcbadge.limes.pink/api/server/Pds3gBmKMH?style=for-the-badge&theme=discord)](https://discord.gg/Pds3gBmKMH) [![YouTube](https://img.shields.io/badge/YouTube-Oxylabs-red?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@oxylabs)

- [Installing requests](#installing-requests)
- [Configuring proxies](#configuring-proxies)
- [Configuring session proxies](#configuring-session-proxies)
- [Testing proxy connection](#testing-proxy-connection)
- [Rotating proxies with Python Requests](#rotating-proxies-with-python-requests)

## Installing requests

Installing the Python Requests library is straightforward. Open your integrated development environment’s (IDE) Python command terminal and execute the following `pip` command:

```pip install requests```

On a Windows device, use the following command:

```python -m pip install requests```

Once installed, you can import the Requests library by using the following statement:

```import requests```

## Python Requests code example
The Python Requests module supports different methods to send HTTP requests, including `GET`, `POST`, and `PUT`. For the sake of demonstration, the following code snippet uses the `requests.get()` method to send an HTTP GET request to `http://httpbin.org/ip`.

```
import requests

response = requests.get("http://httpbin.org/ip")

print("Response: ", response)

print("Response Status Code:", response.status_code)

print("Response data in Content format:\n", response.content)

print("Response data in Text format:\n", response.text)

print("Response data in JSON format:\n", response.json())
```
The above code sends an HTTP GET request and stores the `response` in the response object. Next, it prints `status_code` and the received content in different formats. 

## Configuring proxies
You can provide your proxy IP and proxy authentication credentials within the `get()` function. Python Requests proxy integration is a three-step procedure.

**Step 1:** Assuming that you have already installed the Python Requests library, you must first import the Requests library before using any of its functionalities:

```import requests```

**Step 2:** Create a dictionary variable containing all the information about your proxy endpoint, including the proxy address, port number, and proxy authentication credentials:

```
proxies = {
    "PROTOCOL": "PROXY_TYPE://USERNAME:PASSWORD@PROXY_ADDRESS:PORT_NUMBER"
}
```

Here, **USERNAME** and **PASSWORD** are your Oxylabs sub-user’s credentials. The request **PROTOCOL** can be `HTTP` or `HTTPS` and isn’t necessarily the same as the **PROXY_TYPE**.

### Residential Proxies
The following code demonstrates creating a dictionary with one Residential Proxy endpoint for an HTTP request, and another for HTTPS:

```
proxies = {
    "http": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777",
    "https": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777"
}
```

Here, you can use country-specific entries. For example, if you enter gb-pr.oxylabs.io instead of PROXY_ADDRESS and 20000 instead of PORT, you’ll acquire a United Kingdom exit node. Please refer to our [documentation](https://developers.oxylabs.io/proxies/residential-proxies/location-settings/country-specific-entry-nodes) for a complete list of country-specific entry nodes and sticky session details.

### Datacenter Proxies

If you've purchased a dedicated proxy through our sales team, you’ll have to choose an IP address from the acquired list. You can refer to our [documentation](https://developers.oxylabs.io/proxies/dedicated-datacenter-proxies/enterprise/proxy-lists) for more details. 

If you used the self-service dashboard instead, the port number corresponds with the sequential number of the IP address from the obtained list – more details are available in our [documentation](https://developers.oxylabs.io/proxies/dedicated-datacenter-proxies/self-service/proxy-list).

### Shared Datacenter Proxies

You can also use country-specific entries with Shared Datacenter Proxies. For instance, if you enter `dc.fr-pr.oxylabs.io` in place of **PROXY_ADDRESS** and `42000` instead of **PORT**, you’ll have a French exit node. Please refer to our [documentation](https://developers.oxylabs.io/proxies/shared-datacenter-proxies/select-country) for the entire list of country-specific entries.

**Step 3:** The last step is to send an HTTP request using a method of your `choice—get()`, `post(), or `put()` —and pass the `proxies` dictionary along the target URL.

The following code sends a GET request to `http://httpbin.org/ip` by using the Residential Proxy server configuration described in **step 2.** It further prints the response in different formats:

```
response = requests.get("http://httpbin.org/ip", proxies=proxies)

print("Response: ", response)

print("Response Status Code:", response.status_code)

print("Response data in Content format:\n", response.content)

print("Response data in Text format:\n", response.text)

print("Response data in JSON format:\n", response.json())
```

## Configuring session proxies
Some scraping targets require a session for HTTP communications. In this case, you need to configure proxies with the request session you create. 

The following code demonstrates creating a request session and configuring a residential proxy:

```
import requests

session_obj = requests.Session()
session_obj.proxies = {
    "http": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777",
    "https": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777"
}

response = session_obj.get("http://httpbin.org/ip")

print("Response: ", response)

print("Response Status Code:", response.status_code)

print("Response data in Content format:\n", response.content)

print("Response data in Text format:\n", response.text)

print("Response data in JSON format:\n", response.json())
```

As you can see, first, you have to create a new request session and store it in `session_obj`. Next, you must set the `proxies` property with one of the proxy endpoints.

The configured `session_obj` is then used to generate a GET request to `http://httpbin.org/ip`. Lastly, the code prints the returned response in different formats.

## Testing proxy connection
You can test your proxy server settings by sending a GET request to `http://httpbin.org/ip`.

Use the following code to test the proxy connectivity. Don’t forget to use your Oxylabs sub-user’s username and password:

```
import requests

proxies = {
   "http": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777",
   "https": "http://USERNAME:PASSWORD@pr.oxylabs.io:7777"
}

response=requests.get("http://httpbin.org/ip", proxies=proxies)

print("Response Status Code", response.status_code)

print("Response data in Content format:\n", response.content)
```

If the status code is `200 `and the output IP differs from your actual network IP address, then your proxy server is configured correctly.

## Rotating proxies with Python Requests

Unlike Residential and Shared Datacenter Proxies,  Dedicated Datacenter Proxies don’t have an in-built rotation feature, but they can be implemented with our Proxy Rotator. With this tool, you can easily automate the rotation of our Dedicated Datacenter Proxies. Alternatively, Python Requests proxy rotation can be achieved in Python. Unfortunately, the Requests library doesn’t have a built-in rotation feature, but you can still rotate proxies using the following two methods.

### Selecting a proxy endpoint randomly from a proxy list

This straightforward process involves creating a list of proxy endpoints and randomly selecting one before every new HTTP request. 

Assuming you have a [proxy list](https://developers.oxylabs.io/proxies/dedicated-datacenter-proxies/proxy-lists), you can use the following code to rotate the proxies from the given proxy list:

```
import requests
import random

proxies = (
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_1:10000",
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_2:20000",
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_3:30000",
                    .
                    .
                    .
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_N:100000"
)

for i in range(len(proxies)):
    random_proxy = random.choice(proxies)
    proxy = {"http": random_proxy, "https": random_proxy}

    response = requests.get("http://httpbin.org/ip", proxies=proxy)

    print("Proxy used: ", random_proxy)
    print("Response Status Code", response.status_code)
    print("Response data in Text format:\n", response.text)
```

The above code creates a list of proxy endpoints and uses `random.choice(`) which returns a randomly selected element from the specified sequence, in our case proxies. Each call to the `choice()` method randomly selects a new proxy, which is then used to create the proxy dictionary for the subsequent HTTP request. 

The for loop in this code makes four different `GET` requests to `http://httpbin.org/ip`. It uses a random proxy endpoint from the proxies for each new HTTP request. 

The `choice()` method can select the same proxy endpoint multiple times. Each value from the given range is always equally likely in each `choice()` call. Thus, there can be a possibility of repeating the same endpoints several times in consecutive HTTP requests.

### Iterating over the proxy list

The randomness in the previous proxy-rotation scheme makes it non-deterministic. However, you might want to use a more deterministic rotating technique. You can do that by using a pattern similar to the round-robin.

In this scheme, you create a list of proxy endpoints and iterate over the list indices until you reach the end of the list. Thanks to modular arithmetics, the next value of `i` is mapped to the 0th index. It goes on until the `for` loop completes all of its iterations.

The following code provides the implementation of this method:

```
import requests

proxies = (
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_1:10000",
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_2:20000",
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_3:30000",
                    .
                    .
                    .
    "http://USERNAME:PASSWORD@PROXY_ADDRESS_N:100000"
)

for index in range(len(proxies)):
    proxy = {"http": proxies[index], "https": proxies[index]}
    response = requests.get("http://httpbin.org/ip", proxies=proxy)

    print("Proxy used: ", proxies[index])
    print("Response Status Code", response.status_code)
    print("Response data in Text format:\n", response.text)
```

The `for` loop makes as many HTTP requests as the length of the `proxies` list. It maps all the values of `index` between **0** and the **length-1**. Thus, ensuring a smooth rotation of proxies.

For a more detailed guide on proxy integration with Python requests, please check our [website](https://oxylabs.io/resources/integrations/python-requests). 




