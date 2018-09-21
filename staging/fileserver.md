# BioImage Suite's File Server

Applications run from the browser are only able to access a local filesystem at a fairly primitive level — the user must select an item to load manually and confirm that they want the browser to load it. The interface is so limited for security reasons, as if the browser could inspect the file system without any check, it would be trivial for a malicious script to download private files and send them to an arbitrary destination. 

This restriction would be particularly onerous when running image processing pipelines that require saving and loading dozens of images at each step: the user would need to accept the request for each file manually and drag it into the application. The BioImage Suite file server is designed to circumvent this limitation by uploading and downloading data from the server through a trusted link. 

The server itself is a [Node](https://nodejs.org/en/) process that you must connect and authenticate with before the server will accept data. We will cover how to run the server and configure BioImage Suite to use it as its source in the sections below.

