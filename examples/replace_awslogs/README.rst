
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
Replace awslogs default driver with FireLens
################################################

.. literalinclude:: docker-compose.yaml

The user defined a familiar configuration for CloudWatch. However, they'd like to use FireLens and FluentBit
to take care of sending the logs to CloudWatch, using the cloudwatch plugin.

``x-logging.FireLens.Shorthands.ReplaceAwsLogs`` will do just that. It will also take care of making sure the
IAM Task role is granted permissions to publish to the log group.

In the resulting template, we get the following LogConfiguration for our container

.. code-block:: yaml

    LogConfiguration:
      LogDriver: awsfirelens
        Options:
          Name: cloudwatch
          auto_create_group: true
          log_group_name: a-custom-name
          log_stream_prefix: random-logs
          region: !Ref 'AWS::Region'
