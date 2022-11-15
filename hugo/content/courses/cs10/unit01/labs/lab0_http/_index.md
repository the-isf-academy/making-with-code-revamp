---
title: "0. HTTP"
type: lab
# draft: true
---


# HTTP: How Computers Communicate

The Internet may be humanity's most profound invention. A global
network of computers talking to one another, making it possible for people all
over the world to interact. In this lab, we will start learning about *how*
computers talk with one another. 

{{< aside "FYI" >}}
**All actions on the Internet are composed of HTTP Requests.** 

 - Every time you access a website, it triggers a series of HTTP Requests depending on its complexity. 
 - Every time a client requests information from a server, the request is recorded along with the status code.

{{<expand "An Analogy to better understand HTTP Requests" >}}
It can be tricky to understand how HTTP functions because it’s difficult to examine what your browser is actually doing. (And perhaps also because we explained it using acronyms that may be new to you.) Let’s review what we learned by using an analogy that could be more familiar to you.

Imagine the internet is a town. You are a client and your address determines where you can be reached. Businesses in town, such as Codecademy.com, serve requests that are sent to them. The other houses are filled with other clients like you that are making requests and expecting responses from these businesses in town. This town also has a crazy fast mail service, an army of mail delivery staff that can travel on trains that move at the speed of light.

Suppose you want to read the morning newspaper. In order to retrieve it, you write down what you need in a language called HTTP and ask your local mail delivery staff agent to retrieve it from a specific business. The mail delivery person agrees and builds a railroad track (connection) between your house and the business nearly instantly, and rides the train car labeled “TCP” to the address of the business you provided.

Upon arriving at the business, she asks the first of several free employees ready to fulfill the request. The employee searches for the page of the newspaper that you requested but cannot find it and communicates that back to the mail delivery person.

The mail delivery person returns on the light speed train, ripping up the tracks on the way back, and tells you that there was a problem “404 Not Found.” After you check the spelling of what you had written, you realize that you misspelled the newspaper title. You correct it and provide the corrected title to the mail delivery person.

This time the mail delivery person is able to retrieve it from the business. You can now read your newspaper in peace until you decide you want to read the next page, at which point, you would make another request and give it to the mail delivery person.

*Source: [https://www.codecademy.com/articles/http-requests](https://www.codecademy.com/articles/http-requests)*

{{</expand>}}

{{< /aside >}}

### New Vocabulary

- **HTTP** stands for "**Hypertext Transfer Protocol**." It's a set of rules for how
  computers ask each other for content, and how they reply. 
- **JSON** stands for **JavaScript Object Notation**. It is the standard file format for exchanging data over the internet. The syntax mimics dictionaries by using `key` and `value` pairs. 
<<<<<<< HEAD
=======
- ***API** stands for **Application Programming Interface**. It is software that allows computers to communicate with each other. An `API` often provides `JSON`. 
>>>>>>> cs9_unit00

---

## [0] Set Up

{{< code-action >}} **Install `httpie`.** We will be using this command-line software throughout the unit to interact with websites in a new way. 
```shell
brew install httpie
```

{{< code-action "Check it install correctly." >}} You see a verison number appear.
```shell
httpie --version
```

---


## [1] HTTP GET

Every time you visit a URL, your computer opens a connection with the server at that address and uses **HTTP** to send and recieve the content. 

### [GET Request]

Communication starts when one computer (the client) sends a *request* to another computer (the server). For example, by visiting "cs.fablearn.org" you initiate
a `GET` request to recieve the *Making with Code* homepage from the server. 

A `GET` request contains following: 

```shell
GET / HTTP/1.1
Host: cs.fablearn.org
```

{{< figure src="images/courses/cs10/unit00/00_http_get.png" width="100%" alt-text="An HTTP GET request" >}}


### [GET Response]

Once the request has been recieved by the server, it responds by sending the client a HTTP *response*. If a successful connection has been made, the server sends the content to the client. 

Here's an example of a HTTP response to a successful `GET` request to the course website:

  ```shell {linenos=table}
  HTTP/1.1 200 OK                                 // This is the response
  Content-Length: 2081                            // I am sending a lot
  Content-Type: text/html                         // I am sending HTML
  Date: Tue, 18 Aug 2020 19:23:28 GMT             // This is when I sent it
  Last-Modified: Tue, 18 Aug 2020 15:46:28 GMT    // There is new content
  
  <!DOCTYPE html>                                 // Here it comes!
  <html lang="en">                                // Here is your webpage
      . . . 
  <p><em>Making with Code</em> is a new, old 
  approach to teaching computer science 
  based in Constructionism.</p>
      . . .
  ```
- `200` (line 1) is the response status code. 
- `Content-Length` (line 2), `Content-Type`(line 3), `Date`(line 4), and `Last-Modified`(line 5) are response headers. They provide
  more detail about what is being requested and what is being sent back. For example, the `Content-Type` tells your computer what
  type of data is being recieved. For "cs.fablearn.org", your computer recieves the HTML, Javacsript, CSS, and image files that make
  up the homepage of the site. 
- `<!DOCTYPE html>` (line 7) is the beginning of the content sent with the response. This is the HTML of the course website which your
  browser then renders as a webpage.

{{< figure src="images/courses/cs10/unit00/00_http_response.png" width="100%" alt-text="An HTTP response" >}}

### [Status Codes]
Status codes are used to signal how the communication between the client and the server is going.

**Common HTTP Status Codes**
- `200` means success.
- `300` means you're looking in the wrong place
- `400` means you did something wrong.
- `404` means the resource requested could not be found 
- `500` means, "Sorry, the server broke!" 

<<<<<<< HEAD

{{< checkpoint >}}

Follow the instructions on the worksheet to before moving onto the next section. 
=======
### [Using HTTPIE]

With the new tool we installed on your computer, `httpie`, we can send HTTP `GET` requests from our terminal. 

{{< code-action >}} **Make a request to the cs.fablearn.org site:**
```shell
http get https://cs.fablearn.org
```
> You should be seeing something very similar to what you see in Chrome. 
>
> If you see an error, try: `cs.fablearn.org` or `http://cs.fablearn.org`

{{< checkpoint >}}

{{< write-action >}}**Complete the section, `0. csfablearn`, of the worksheet.** You will need to:
- Right click and click "Inspect"
- Select "Network" from the top toolbar in the developer tools
- Hard refresh the page with "Command + Shift + R"

>>>>>>> cs9_unit00

{{< /checkpoint >}}

--- 

## [2] HKO

<<<<<<< HEAD
add example

add 



{{< checkpoint >}}

Follow the instructions on the worksheet before moving onto the next section. 

{{< /checkpoint >}}





add deliverables
=======
You may have noticed that our site is pretty simple. That's because the data being sent is primarily text. **Our site is not hooked up to a database.**

**We're now going to look at a website that utilizes a database, the [Hong Kong Observatory](https://www.hko.gov.hk/en/index.html).**

### [API]

The HKO provides an open `API` that allows anyone to access their weather database. We are going to use `HTTP Requests` to access this database. 

`API` stands for **Application Programming Interface**. It is software that allows computers to communicate with each other. An `API` often provides `JSON`. 

{{< look-action "Open the documentation from the HKO:" >}} [API Documentation](https://www.hko.gov.hk/en/weatherAPI/doc/files/HKO_Open_Data_API_Documentation.pdf). We will use this throughout today's lab. 

### [JSON]

**JSON** stands for **JavaScript Object Notation**. It is the standard file format for exchanging data over the internet. The syntax mimics dictionaries by using `key` and `value` pairs. 

{{< code-action >}}**Let's start by making a simple `http get` request to recieve `JSON` from the HKO.**
```shell
http get https://data.weather.gov.hk/weatherAPI/opendata/weather.php\? dataType==flw
```

{{< look-action >}} **Should recieve `JSON` that looks like this.** However, the information will differ depending which day and time you make the request.
```shell
{
    "fireDangerWarning": "",
    "forecastDesc": "Mainly fine. Very hot with isolated showers in the afternoon. Moderate easterly winds, occasionally fresh offshore.",
    "forecastPeriod": "Weather forecast for this afternoon and tonight",
    "generalSituation": "A ridge of high pressure is bringing generally fine weather to the coast of southeastern China. Besides, showers triggered by high temperatures are affecting the coast of Guangdong.",
    "outlook": "Mainly fine tomorrow. Sunny periods and a few showers on the Mid-Autumn Festival and the following couple of days.",
    "tcInfo": "At noon, Tropical Storm Muifa was centred about 1100 kilometres south-southeast of Okinawa. It is forecast to move northwest at about 12 kilometres per hour across the seas east of the Philippines.",
    "updateTime": "2022-09-08T15:45:00+08:00"
}
```
> Notice how it looks exactly like a dictionary with `key` and `value` pairs. 

### [Making HTTP Requests]

This lab will require you to make a series of `http requests` to the HKO API. Note the format:
```shell
http get https://data.weather.gov.hk/weatherAPI/opendata/weather.php\? dataType==flw
```
> - `http get` - tells the Terminal you are making a `get` request 
> - `https://data.weather.gov.hk/weatherAPI/opendata/weather.php` - tells the Terminal which address you'd like to make the request to
> - `dataType==flw` - this tells the API what type of data you'd like to recieve. In this instance, `flw` provies the Local Weather Forecast.


{{< checkpoint >}}

{{< write-action >}}**Complete the section, `1. HKO API`, of the worksheet to further explore `http requests`, `JSON`, and `APIs`.**

You will need to use the [HKO API Documentation](https://www.hko.gov.hk/en/weatherAPI/doc/files/HKO_Open_Data_API_Documentation.pdf) to make specific `http requests`. 

{{< /checkpoint >}}


## [2] ISF Energy Database

The ISF Energy Database keep historical and current data about the school's energy usage. This includes XYZ thing. 

{{< code-action >}}**Let's start by making a `http get` request to the ISF Energy Database API.**
```shell
http -A bearer -a 0SoXGdHjZb0iktf5dT9fMeAn4XwGyk get https://v4.en-trak.com/apis/usages/isf/total/ date==2022-07-15 period=day
```
> `-A bearer -a 0SoXGdHjZb0iktf5dT9fMeAn4XwGyk` - this API requires users to use an authentication token

{{< checkpoint >}}

{{< write-action >}}**Complete the section, `2. ISF Energy Database API`, of the worksheet to further explore `http requests`, `JSON`, and `APIs`.**

You will need to use the [HKO API Documentation](https://www.hko.gov.hk/en/weatherAPI/doc/files/HKO_Open_Data_API_Documentation.pdf) to make specific `http requests`. 

{{< /checkpoint >}}

---

## [3] Deliverables


{{< deliverables >}}  

**Once you've successfully completed the worksheet be sure to fill out [this Google form](https://docs.google.com/forms/d/e/1FAIpQLSf-RzRIb6y3cFRbOj1uFjbmmPakYu2TI1A4UZzOBQdjEDGYCg/viewform?usp=sf_link).**

{{< /deliverables >}}

---

## [4] Extension

Now that you've had succifient practice accessing APIs, it's time to explore what type of APIs exist. 

{{< code-action "Explore an API of your choosing." >}} Here are some suggestions:
- [Joke API](https://sv443.net/jokeapi/v2/)
- [ZenQuotes API](https://premium.zenquotes.io/zenquotes-documentation/)
- [Wikipedia API](https://www.mediawiki.org/wiki/API:Main_page)
>>>>>>> cs9_unit00
