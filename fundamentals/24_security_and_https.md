# Security and HTTPS

### Some terms before beginning
- Man in the middle attack
	- an attack in which the attacker intercepts a line as communication that is thought to be private
	- this actor can intercept and mutate an IP packet on its way from a client to a server
	- MITM attacks are the primary threat that encryption and HTTPS aim to defend against
- Symmetric Encryption
	- relies only a single key to both encrypt and decrypt data
	- key must be known to all parties involved in communications
	- and therefore typically be shared between the parties at one point or another
	- tend to be faster than asymmetric
	- most widly used here in *Advanced Encryption Standard* or AES
- Asymmetric Encrytion
	- also known as public key encrytion
	- relies on two keys, a public and private key, to encrypt and decrypt data
	- keys are generated using crytographic algo's and are mathematically connected
	- this means that data encrypted with the public key can only be decrypted with the private key
	- the private key must be kept secure
	- the public one can be openly shared
	- tend to be slower than symmetric
- AES
	- Advanced Encryption Standard
	- widely used that has three symmetric-key algo's
	- gold standard in encrytion and is used by the NSA to encrypt top secret info
- HTTPS
	- HTTP secure
	- required servers to have trusted certifications (SSL certificates)
	- uses the Transport Layer Security (TLS), a security protocol built on top of TCP, to encrypt data communicated between a client and server
- TLS
	- *Transport Layer Security*
	- over which HTTP runs in order to achieve secure communication online
	- HTTP over TLS == HTTPS
- SSL Certificate
	- digital certificate granted to a server by a certificate authority
	- contains the servers public key, which is used as part of the TLS handshake process in an HTTPS connection
	- this cert effectively confirms that a public key belongs to the server claiming it belongs to them
	- crucial defense against MITM attackes
- TLS handshake
	- process through which a client and a server communicating over HTTPS exchange encrytion-related information and establish a secure connection
	- Steps are
		- client sends a *client hello*
		- server responds with a *server hello*, as well as its SSL cert (which has the public key)
		- client verfies that the cert was issued by a cert authority and sends a premaster secret (random bytes) this time encrypted with the public key to the server
		- the client and the server use the client hello, server hello, and premaster secret to then generate the same symmetric encryption session keys. these are used to encrypt and decrypt all data communicated during the remainder of the connection

### Getting into it
Don't nessesarily need this in an interview - unlikley to need to know lots
Good to be familar with - things can lead here based on the interview question
Very complex field, you either an expert or not :)

MITM attack - someone can intercept the ip packets between client and server
Don't assume comms are private, not nessesarily
This is at the core of what we're trying to mitigate against
HTTPS = HTTP secure
Why is it secure? That's what this video is about

Encryption - turn message (from client) into a (seemingly) random chars
Its no longer readable, but can be decrypted (by server)
This would return the original message

There is symmetric and asymmetric encryption
Symmetric relies on symmetric key algo's, which rely on one key to encrypt and decrypt
AES is typcally used here, its a spec of encryption
This is very very faster, much more so then asymmetric
Relies on one key - so must be shared between client and server
Can be ok - can be tough
Key needs to be shared across a secure connection, otherwise MITM possibility

Asymmetric (public key encryption)
Rely on a pair of keys to encrypt and decrypt
Generated together - public and private keys
If you encrypt using public, it can only be decrypted by private
Make the public key "public"
Keep private "private"
Thus, anyone can encrypt, but only you can decrypt
It's slower than symmetric (maybe algos are more complex?)

TLS handshake / SSL certificate
HTTP on top of TLS == HTTPS
With HTTPS, comms are encrypted with TLS
before TLS, it was SSL (certificates)
when client and server make a connection, they go through a TLS handshake
	1. client sends client hello (random string of bytes)
	2. server responds with server hello (like client hello) and ssl cert. this contains the servers public key
	3. client generates the pre-master secret, encrypted using the public key, sends to server
	4. session (only used for this session) keys are then generated (using hello's, secret). this allows for symmetric encryption

This is vulnerable because - MITM when server sends public key to client
That can be intercepted, and replaced / processed / manipulated in some way by a bad acter
How does cleint know the public key it's being given from the server is good?
It's the SSL cert - "client can trust this server's public key"
issueer of cert is trustworthy
Trusted 3rd party signs the certificate allows client to know the server is who they say they are
