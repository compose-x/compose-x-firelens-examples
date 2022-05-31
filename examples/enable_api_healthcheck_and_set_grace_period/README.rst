
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
Enable HTTP API healthcheck and set grace period
################################################


.. literalinclude:: docker-compose.yaml

This configuration, although very simple, will automatically generate the following configuration

.. code-block::

    [SERVICE]
        HTTP_Server  On
        HTTP_Listen  0.0.0.0
        HTTP_PORT    2020
        Health_Check On
        # customize error and retry thresholds and evaluation period as desired
        HC_Errors_Count 5
        HC_Retry_Failure_Count 5
        HC_Period 5

    [SERVICE]
        Flush 1
        Grace 45

It will also have updated the healthcheck method for the ``log_router`` container and use ``curl -sq http://127.0.0.1:2020/api/v1/health  || exit 1``
to perform the healthcheck.
