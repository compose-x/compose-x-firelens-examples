
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
Declare FireLens with FireHose Delivery Stream
################################################

Very simple example where you set the driver to ``awsfirelens`` and the `FireHose plugin`_ options.
Compose-X will automatically deal with IAM permissions to enable everything for the plugin to work properly.

.. warning::

    When using this method, you will have to ensure the IAM permissions for your Task Role are set properly.
    You can use the ``x-iam`` section to grant access to the delivery stream.

.. tip::

    We highly recommend that you use `x-kinesis_firehose.Lookup`_ to let Compose-X automatically set the IAM permissions.

.. literalinclude:: docker-compose.yaml

.. code-block:: yaml

    LogConfiguration:
      LogDriver: awsfirelens
      Options:
        Name: kinesis_firehose
        delivery_stream: my-firehose-stream
        region: us-east-1

.. _FireHose plugin: https://docs.fluentbit.io/manual/pipeline/outputs/firehose
.. _x-kinesis_firehose.Lookup: https://docs.compose-x.io/syntax/compose_x/firehose.html
