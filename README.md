##Learning API GET Calls with Developer Keys using Postman and the Marvel API

When using APIs sometimes you will sometimes need to obtain/use developer keys. When using these to access information from an API you will usually have to include the public key and a hashed version of the private key plus some other variable(s).

###Getting Started with an API
A pretty safe bet to find the information for any API is to just google the company name followed by "API" or "Developer Portal". In this case we're going to use the Marvel API as an example.

After finding the [Marvel Developer Portal](http://developer.marvel.com/) we see that we need developer keys to access the API, this also means that our calls to the Marvel API will have to be signed with our keys. After creating a developer account with Marvel, I'm able to access my public and private developer keys.

Reading the docs I'm able to see what is required to make a GET call to the API.

Per the Marvel API docs, the formula to construct a valid call is as follows:
* A user with a public key of "1234" and a private key of "abcd" could construct a valid call as follows: `http://gateway.marvel.com/v1/public/comics?ts=1&apikey=1234&hash=ffd275c5130566a2916217b101f26150`
* The three parts that will be specific to our developer keys are at the end of the call:
  * `ts=1` (timestamp)
  * `apikey=1234` (public key)
  * `hash=ffd275c5130566a2916217b101f26150`
    * The hash value is a "hashed" or obfuscated version of (ts)(private key)(public key) using the md5 hash.

**Optional Note (if you're interested) Quick note on developer keys and hashing:** Hashing, or A cryptographic hash function, is a mathematical algorithm that maps data of arbitrary size to a bit string of a fixed size (a hash function) which is designed to also be one-way function, that is, a function which is infeasible to invert. [Hash Functions on wikipedia](https://en.wikipedia.org/wiki/Cryptographic_hash_function)

There is a lot more to this, but this is all you need to know for this exercise is that you're going to use your public key, private key, and a timestamp to create a hash to be used in your API call to the Marvel API.

###Using a web tool to create your hash
From the Marvel API documentation we know that our GET request needs to be in the following format:
* A user with a public key of "1234" and a private key of "abcd" could construct a valid call as follows: `http://gateway.marvel.com/v1/public/comics?ts=1&apikey=1234&hash=ffd275c5130566a2916217b101f26150`

Right now you have three of the four needed parts to make an API call -- you have your public and private keys, and your timestamp value (the Marvel API doesn't give specific restrictions on the format of the timestamp so it can be an integer, such as `1`, used below)

To test that you are doing it correctly put in these test values
* timestamp = 1
* private key = abcd
* public key = 1234

Using a web-based md5 hash tool found [here](http://www.md5hashgenerator.com/). If you have Node.js installed you can also use node to create your hash (find details on this in the other markdown file in this directory)

The Hash generation formula given to us from the Marvel API is: (timestamp)(private key)(public key). Therefore, the value we enter into the text box on the md5 site to be hashed is `1abcd1234`

The generated hash is shown at the top of the page. This is the hash that is generated for the values above:
`hash=ffd275c5130566a2916217b101f26150`

Use your timestamp, private and public keys to generate your timestamp now.

Now that you have all the pieces, we can make a test call using Postman.

###Getting Started with Postman
**[Postman Docs](https://www.getpostman.com/)**

You can use the web-based or desktop version of Postman -- these direction were written based on the desktop version, but the functionality between tools is the same for what we are doing here.

###Testing GET requests with Postman
We can build a request in Postman by first selecting "GET", putting  the beginning of the url `http://gateway.marvel.com/v1/public/characters/1011396`
in the text box -- here I've chosen to look up character 1011396, you can look up the different types of calls you can make in the Marvel API docs.

Next press the "Params" button. For each of the parameters required by the Marvel API, add a param key and value. Then click "Send" -- and the results of your call (whether information or error) will be shown in the window below.

You can customize how you view the data in Postman using the options listed above the text window with the call results. To view your results as formatted JSON, make sure you have selected the "pretty" button and JSON from the dropdown, from the selections available at the top of the body section.

Here's a snapshot of what that call would look like:

![alt text](http://i.imgur.com/gaSUpP5.png "Postman Screenshot")
