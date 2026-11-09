# Wording

* A **user account** is identified by an email adress and allows access to the web service.
* A **link** is a pair of input and output ports that allows exchanging of data (or only the output side can be used). A side set to TCP server is a port on links.remoteredirect.com that devices connect to, see [Input side and output side of a link](../remoteredirect-local.md#input-side-and-output-side-of-a-link).
* An **account** can manage one to many links and is associated with one to many user accounts.
* Links can be shared between one and many accounts.
* A **scene script** is a piece of Scriban script that can be defined per scene and defines what data is output to the display board
* An **account script** is a piece of javascript code that can query external APIs and make the data available in link scripts.
