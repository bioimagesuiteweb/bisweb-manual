# BioImage Suite's File Server

Applications run from the browser are only able to access a local filesystem at a fairly primitive level — the user must select an item to load manually and confirm that they want the browser to load it. The interface is so limited for security reasons, as if the browser could inspect the file system without any check, it would be trivial for a malicious script to download private files and send them to an arbitrary destination. 

This restriction would be particularly onerous when running image processing pipelines that require saving and loading dozens of images at each step: the user would need to accept the request for each file manually and drag it into the application. The BioImage Suite file server is designed to circumvent this limitation by uploading and downloading data from the server through a trusted link. 

The server itself is a [Node](https://nodejs.org/en/) process that you must connect and authenticate with before the server will accept data. We will cover how to run the server and configure BioImage Suite to use it as its source in the sections below.


    cd ~/<NAME OF FOLDER CONTAINING BIOIMAGE SUITE>/bisweb/js/bin
    node bisfileserver.js <OPTIONS>

The options for the file server are as follows:

Flag | Description | 
-|-
 -p, --port <port_number> | Which port the server will listen on. This will be the number that follows the colon in the hostname when connecting to the server.
 --readonly | If this flag is specified, the server will not accept requests to write files. 
--insecure | If this flag is set, the server will not ask for a One-Time Password when you connect. As the name suggests, setting this flag may undermine the security of the files on your system, __use with care__.
--verbose | Prints more detailed information from the server while it's running. 
--ipaddr <host_name> | Which host to connect to. Note that BioImage Suite may not support hosts besides 'localhost', i.e. your own computer. If this is not specified, the host name will be set to 'localhost'.
--tmpdir <directory_name> | Which temporary directory to use, i.e. where the server will default to saving. 
--config <file_name> | Whether the script that starts the BioImage Suite file server should read from a config file that may specify many options on the command line. This is helpful if you have a complex ipaddr, tmpdir, etc.
--createconfig | Takes the options currently written on the command line, saves them in a file, then exits. For example, you might create a config file that will run in insecure mode by writing `node bisfileserver.js --insecure --createconfig`.
-h, --help | Prints the help file for the file server.







    