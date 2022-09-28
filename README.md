Ansible role: RabbitMQ
======================

Install and configure RabbitMQ.

Role Variables
--------------

```
ENTRY POINT: main - Install and configure RabbitMQ

OPTIONS (= is mandatory):

- bintray_rabbitmq_apt_key_fingerprint
        Fingerprint for RabbitMQ apt signing key from old bintray repo
        [Default: (null)]
        type: str

- erlang_apt_key_fingerprint
        Fingerprint for Erlang apt signing key
        [Default: (null)]
        type: str

- old_rabbitmq_apt_key_fingerprint
        Old fingerprint for RabbitMQ apt signing key
        [Default: (null)]
        type: str

- rabbitmq_apt_key_fingerprint
        Fingerprint for RabbitMQ apt signing key
        [Default: (null)]
        type: str

- rabbitmq_auth_mechanisms
        List of client authentication mechanisms to enable
        [Default: (null)]
        elements: str
        type: list

- rabbitmq_disabled_plugins
        List of plugins to disable
        [Default: (null)]
        elements: str
        type: list

- rabbitmq_enable_management
        If true, enable management plugin and listen for management
        connections on localhost:15672
        [Default: False]
        type: bool

- rabbitmq_enabled_plugins
        List of plugins to enable
        [Default: (null)]
        elements: str
        type: list

- rabbitmq_erlang_apt_key_fingerprint
        Fingerprint for RabbitMQ-Erlang apt signing key
        [Default: (null)]
        type: str

- rabbitmq_log_levels
        Log levels for different output types or log message
        categories, see https://www.rabbitmq.com/logging.html#log-
        outputs and https://www.rabbitmq.com/logging.html#log-message-
        categories
        [Default: [{'name': 'file', 'level': 'info'}, {'name':
        'connection', 'level': 'warning'}]]
        elements: dict
        type: list

        OPTIONS:

        = level
            Log level
            (Choices: debug, info, warning, error, critical, none)
            type: str

        = name
            Output type or message category

            type: str

- rabbitmq_monitoring_enable_cronjob
        If true, enable cron job to monitor rabbitmq queue size
        [Default: False]
        type: bool

- rabbitmq_monitoring_queue_alarm_cron_interval
        Cron interval for checking queue sizes
        [Default: 20 * * * *]
        type: str

- rabbitmq_monitoring_queue_alarm_threshold
        Maximum number of messages in a queue before triggering an
        alert
        [Default: 1000]
        type: int

- rabbitmq_tcp_listeners
        Bind addresses and ports to listen on for client connections
        [Default: ['127.0.0.1:5672', '::1:5672']]
        elements: str
        type: list

- rabbitmq_tls_cacertfile
        Path to CA certificate file
        [Default: (null)]
        type: str

- rabbitmq_tls_certfile
        Path to server certificate file
        [Default: (null)]
        type: str

- rabbitmq_tls_ciphers
        List of TLS cipher suites to enable (in openssl format)
        [Default: ['ECDHE-RSA-AES256-GCM-SHA384']]
        elements: str
        type: list

- rabbitmq_tls_keyfile
        Path to server key file
        [Default: (null)]
        type: str

- rabbitmq_tls_listeners
        List of ports to listen on for TLS connections
        [Default: (null)]
        elements: str
        type: list

- rabbitmq_tls_versions
        List of TLS versions to enable
        [Default: ['tlsv1.2']]
        elements: str
        type: list
```

Installation
------------

This role can either be installed manually with the ansible-galaxy CLI tool:

    ansible-galaxy collection install community.rabbitmq
    ansible-galaxy install git+https://github.com/wandansible/rabbitmq,main,wandansible.rabbitmq
     
Or, by adding the following to `requirements.yml`:

    roles:
      - name: wandansible.rabbitmq
        src: https://github.com/wandansible/rabbitmq

    collections:
      - name: community.rabbitmq

Roles listed in `requirements.yml` can be installed with the following ansible-galaxy command:

    ansible-galaxy install -r requirements.yml

Example Playbook
----------------

    - hosts: rabbitmq_hosts
      roles:
         - role: wandansible.rabbitmq
           become: true
           vars:
             rabbitmq_auth_mechanisms:
               - "PLAIN"
             rabbitmq_enabled_plugins:
               - "rabbitmq_shovel"
