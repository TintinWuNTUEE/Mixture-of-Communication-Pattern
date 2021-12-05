# Mixture-of-Communication-Pattern

## Environment
- python 3.8.10
- grpc
## Run Project
- Install project dependencies
```bash
$ sudo apt-get install protobuf-compiler

$ sudo apt-get install build-essential make

$ pip3 install -r requirements.txt
```
- Compile server
```bash
$ cd rest_server 
$ make
$ cd fib_server 
$ make
$ cd log_server
$ make
```
- start docker(under main dir)
```
$ docker run -d -it -p 1883:1883 --name con -v $(pwd)/mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto
```
- stop docker(under main dir)
```
docker stop con
```
- Start the gRPC
```bash
$ cd fib_server
$ python3 server.py --ip 0.0.0.0 --port 8080
```
- Start the REST server
```bash
cd rest_server 
python3 manage.py migrate
python3 manage.py runserver
```
- start log server
```bash
cd log_server
python3 server.py --ip localhost --port 8888
```

- POST
```bash
curl -X POST -H "Content-Type: application/json" http://127.0.0.1:8000/rest/fibonacci/ -d "{\"order\":\"$(Input)\"}"
```
- GET
```bash
curl http://localhost:8000/rest/logs
```