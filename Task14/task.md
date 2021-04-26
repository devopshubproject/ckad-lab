* Create a Persistent Volume named pv, access mode ReadWriteMany, storage class name shared, 512MB of storage capacity and the host path /data/config.

* Create a Persistent Volume Claim named pvc that requests the Persistent Volume in step 1. The claim should request 256MB. Ensure that the Persistent Volume Claim is properly bound after its creation.

* Mount the Persistent Volume Claim from a new Pod named app with the path /var/app/config. The Pod uses the image nginx.

* Check the events of the Pod after starting it to ensure that the Persistent Volume was mounted properly.