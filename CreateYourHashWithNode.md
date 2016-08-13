###Using Node to create your hash
Rather than using a webpage based hash tool, you can use node right in your terminal.

Using your developer keys and a chosen timestamp of `123456789`, you can now create your hash to be used with the API call.

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


**For Testing**
where:
private = 'abcd'
public = '1234'
ts = '1'

Combination to be hashed: 1abcd1234
Output Hash: 'ffd275c5130566a2916217b101f26150'
