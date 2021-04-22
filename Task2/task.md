• Create a secret named app-secret with a Key/value pair:key1/value1

• Start an nginx Pod named nginx-secret using container image nginx, and add an
environment variable exposing the value of the secret key key1, using
MY_VARIABLE as the name for the Secret key key1, Using MY_VARIABLE as the
name for the environment variable inside the Pod