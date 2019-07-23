1. create mongo db for the api-server application
#Imagine you already has installed mongodb
#create database:
use api-server
#create a user
db.createUser(
   {
     user: "api-server",
     pwd: "api-server-2019!",
     roles: [ "readWrite" ]
   }
)

2. login in mongo cli
db.auth( <username>, <password> )

3. change password
db.changeUserPassword("api-server","otherpassword");

4. drop user
use api-server
db.dropUser("api-server", {w: "majority", wtimeout: 5000})


#############################################Develope server part(backend)#######################################
#make sure you already install golang(1.11+) and set GOROOT AND GOPATH correctly, this project use go module
cd backend folder
go build github.com/api-server

#if missing package please use "go get package_missing" to download it

#finally run "go build github.com/api-server" command
#After run the command, we will see following:

ERROR: logging before flag.Parse: I1110 18:14:52.033903   97860 settings.go:50] Warning: Setting preproduction environment due to lack of GO_ENV value
I1110 18:14:52.058886   97860 server.go:28] work dir:  D:\goWork

#the server runs on port 80.


#the mongodb configuration for backend
vuetify-example/backend/settings/pre.json for development
vuetify-example/backend/settings/prod.json for production

#Please set the system variable GO_ENV to "prod" when in production environment
windows: set GO_ENV=prod
linux: export GO_ENV=prod

#package the executable file, in backend folder run "go build", after success, there is a file generated:
windos: api-server.exe
linux: api-server

# then we can run it directly with or without system varialbe "GO_ENV=prod"

