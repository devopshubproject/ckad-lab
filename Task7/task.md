* The application has an endpoint, /started , that will indicate if it can accept traffic by
returning an HTTP 200. If the endpoint returns an HTTP 500, The application has
not yet finished initialization

* The application has another endpoint /healthz that will indicate if the application is
still working as expected by returning an HTTP 200. If the endpoint returns an HTTP
500 the application is no longer responsive

* Configure the liveness-pod Pod provide to use these endpoints

* The probes should use port 8080