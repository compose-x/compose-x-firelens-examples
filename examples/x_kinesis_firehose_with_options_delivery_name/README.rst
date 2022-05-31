
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X, FireHose, S3

################################################
Enable HTTP API healthcheck and set grace period
################################################


.. literalinclude:: docker-compose.yaml

With this example, Compose-X is going to do the following:

* Find the KMS key that already exists in the account to use it with any other resources
* Create a new S3 bucket
* Create a new Delivery Stream that will be used by the `more-logs` container, and configure to deliver to the new bucket
* Lookup and find the details of the ``delivery-stream-output-bucket`` Delivery Stream

For both services, ``more-logs`` and ``random-logs`` (here in the family called ``web``), the value for `delivery_stream`
will be set accordingly the the name of the respective delivery stream, so will the ``region`` property.

And on top of all that, Compose-X will create all of the necessary IAM policies to grant the service access to the
delivery streams.

The resulting configuration will look like (for random-logs container in the ``web`` family)

.. code-block::

    [INPUT]
        Name forward
        unix_path /var/run/fluent.sock

    [INPUT]
        Name forward
        Listen 0.0.0.0
        Port 24224

    [INPUT]
        Name tcp
        Tag firelens-healthcheck
        Listen 127.0.0.1
        Port 8877

    [FILTER]
        Name record_modifier
        Match *
        Record ecs_cluster ANewCluster
        Record ecs_task_arn arn:aws:ecs:eu-west-1:374709687836:task/ANewCluster/f97a679f6c0d46fd9ca6a4547e169a24
        Record ecs_task_definition web:5

    @INCLUDE /compose_x_rendered/firelens.conf

    [OUTPUT]
        Name null
        Match firelens-healthcheck

    [OUTPUT]
        Name kinesis_firehose
        Match random-logs-firelens*
        delivery_stream PUT-S3-g6B0t
        region eu-west-1
