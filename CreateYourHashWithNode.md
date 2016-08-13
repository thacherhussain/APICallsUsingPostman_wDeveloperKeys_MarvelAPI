Another option

Rather than using random webpages to find a hash tool, you can use node right in your terminal. And then test your GET calls from Postman.

###Two ways to create your hash
Below I've outlined two ways to create your hash. If you have Node.js installed on your computer and feel comfortable using the terminal, using Node to create your hash is the best option. Likewise, if you don't know if you have node installed, or don't feel as comfortable with the command line, we can also create a hash using a web tool.

####Using a web tool to create your hash

####Using Node to create your hash
Using your developer keys and a chosen timestamp of '123456789', you can now create your hash to be used with the API call.

From your terminal type `node` -- you should then see `>` on the left hand side of the terminal. Below is what the input and output will look like for node.

**Set the Variables**

`> var private = 'YOUR PRIVATE KEY'`

`undefined`

`> var public = 'YOUR PUBLIC KEY'`

`undefined`

`> var ts = '123456789'`

`undefined`

**Create the hash**

`crypto.createHash('md5').update(`${ts}${private}${public}`).digest('hex');`

`'YOUR HASH'`

**Type `.exit` to exit node.**

Now that you have all the pieces, we can make a test call using Postman.
