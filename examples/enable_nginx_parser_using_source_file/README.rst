
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
Enable HTTP API healthcheck and set grace period
################################################


.. literalinclude:: docker-compose.yaml

In this example, we are going to let FireLens automatically configure the delivery_stream settings.

But we are using NGINX, and there is a `pre-built NGINX parser`_ that would allow us to format into JSON attributes, the
different fields of the log. We also want to retain the metadata data that FireLens will add to our logging (task_id etc).

To also demonstrate with further settings, we have also added a modify filter that will change the field ``ecs_task_arn``
and instead use ``task_id`` in our logging format.

The following configuration will be generated and used to tell FireLens to extend the configuration.

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
        Grace 30

    [SERVICE]
        Parsers_File /fluent-bit/parsers/parsers.conf

    [FILTER]
        Name modify
        Match frontend-firelens*
        Rename ecs_task_arn task_id

    [FILTER]
        Name parser
        Match frontend-firelens*
        Parser nginx
        Key_Name log
        Reserve_Data True

The resulting logs will be something like

.. code-block:: json

    {
        "agent": "ApacheBench/2.3",
        "code": "200",
        "container_id": "8e1fe6c0477eb3d34474372ad8004742dc9692c4d83b07cbb66a67b99b23385b",
        "container_name": "/ecs-web-38-web-e0a9b288b085b1c9ef01",
        "ecs_cluster": "ANewCluster",
        "ecs_task_definition": "web:38",
        "host": "-",
        "method": "GET",
        "path": "/",
        "referer": "-",
        "remote": "192.168.12.31",
        "size": "615",
        "source": "stdout",
        "task_id": "arn:aws:ecs:eu-west-1:374709687836:task/ANewCluster/c810b9e024e54a31852ca448f3929d9c",
        "user": "-"
    }

.. _pre-built NGINX parser: https://github.com/fluent/fluent-bit/blob/master/conf/parsers.conf
