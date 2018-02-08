# CouchDBCRUDExamples

## General instructions
Get couchDB from http://docs.couchdb.org/en/latest/install/unix.html#installation-using-the-apache-couchdb-convenience-binary-packages

Get the docker couchDb image from: https://hub.docker.com/_/couchdb/

Start a container with the image using:
```sh
$ docker run -p 5984:5984 -d couchdb //forwards the containers port 5984, so you can access it on your localhost
```

If you are using a debian based system you can also write:
```sh
sudo apt-get install couchdb-bin -y //NOTICE the repo dosen't host the newest version.
```

CouchDB communicate over simple http requests, this means that curl is an excelent tool for interacting with your
database from the shell.

CouchDB uses port 5984 as default - this guide assumes your couchDB instance is hosted on localhost

## CREATE
### STEP 1
Create a database to store your documents

```sh
curl -X PUT http://127.0.0.1:5984/person //creates the people database
{"ok":true}
```

### STEP 2
create a person document
```sh
curl -X PUT http://127.0.0.1:5984/person/1 -d '{"username" : "Møller"}' //input, gives Møller the id 1
{"ok":true,"id":"1","rev":"1-7cafe18bdf0e85baa9a35a36c6b4fd1f"} //output if succesful
```


## READ
Reads the person document from the above step.
```sh
curl http://127.0.0.1:5984/people/1 //input, ask for Id no. 1
{"_id":"1","_rev":"1-dfa783e23c0290b414e9f6500f907074","username":"Møler"} //output
```

## UPDATE
Updates Møller:
```sh
curl -X PUT http://127.0.0.1:5984/person/1/ -d '{"username" : "Møller Von Gokkenstein" , "_rev" : "1-dfa783e23c0290b414e9f6500f907074"}'
{"ok":true,"id":"2","rev":"1-a98316408dd0e46ae99636f3d1243e1c"}
```

## DELETE
We're fucking tired of Møller and his shit, so we've dicided to delete him!
```sh
curl -X DELETE http://127.0.0.1:5984/person/1?rev=1-a98316408dd0e46ae99636f3d1243e1c
{"ok":true,"id":"1","rev":"2-89425da99ad03484350a9bd286e5d372"}
```
and that's it - Møller Von Gottenstein is finaly gone!


Good luck have fun!
