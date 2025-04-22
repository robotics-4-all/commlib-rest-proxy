# commlib-rest-proxy
Proxy REST service calls via message broker technologies (e.g. MQTT, AMQP, Redis, Kafka message brokers).

a **REST proxy**, that enables ***invocation of REST services via message brokers***. The proxy uses an RPCService to run the broker endpoint and an http client for calling REST services. An RPC call is transformed into proper, REST-compliant, http request, based on the input parameters.

<div align="center">
<img src="https://github.com/robotics-4-all/commlib-py/assets/4770702/1507cb10-00ec-49ce-8159-967c23d1ba72">
</div>

Responses from the REST services have the following **RESTProxyMessage** schema:

```python
class RESTProxyMessage(RPCMessage):
    class Request(RPCMessage.Request):
        base_url: str
        path: str = '/'
        verb: str = 'GET'
        query_params: Dict[str, Any] = {}
        path_params: Dict[str, Any] = {}
        body_params: Dict[str, Any] = {}
        headers: Dict[str, Any] = {}

    class Response(RPCMessage.Response):
        data: Union[str, Dict, int]
        headers: Dict[str, Any]
        status_code: int = 200
```

# Run with uvicorn

First create a virtual environment and install dependencies.

```sh
python -m venv myenv
pip install -r requirements.txt
```

Start the uvicorn wsgi server with 16 workers.

```py
uvicorn web_gw.api:app --host 0.0.0.0 --port 8080 --workers 16
```

# Run with Docker

First, download this repository and build the docker image using docker-cli

```sh
docker build . -t cwebgw
```
