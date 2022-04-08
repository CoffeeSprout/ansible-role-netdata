coffeesprout.netdata
===================

Install and configure netdata for FreeBSD, RHEL based systems and Debian using the package manager.
We disable ACLK by default
Optionally you might want to disable  the default alarms...

    netdata_enable_stock_health_configuration: "yes"

Role Variables
--------------



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    #Simple deployment that is accessible from other than local host; Also disable online callbacks
    - hosts: servers
      roles:
      - role: coffeesprout.netdata
        netdata_bind_address: 0.0.0.0
        

    #Another simple deployment but with Teams enabled
    - hosts: servers
      roles:
      - role: coffeesprout.netdata
        netdata_health_alarm_notify:
        - option: "SND_MSTEAMS"
          value: "YES"
        - option: "MSTEAMS_WEBHOOK_URL"
          value: "https://outlook.office.com/webhook/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX@XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/IncomingWebhook/[XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX]/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
        - option: "DEFAULT_RECIPIENT_MSTEAMS"
          value: "Channel name"

    #Deployment with PostgreSQL plugin included
     - hosts: server
       roles:
       - role: coffeesprout.netdata
         netdata_pythond_plugins:
         - postgres
         netdata_postgresql_user: monitoring-user
         netdata_postgresql_password: "{{ monitoring_password }}"
         netdata_postgresql_tcp: True
         netdata_bind_address: "{{ ansible_default_ipv4.address }}"

    #Simple deployment that is accessible from other than local host; Simple deployment without alarms
    - hosts: servers
      roles:
      - role: coffeesprout.netdata
        netdata_bind_address: 0.0.0.0
        netdata_enable_stock_health_configuration: "no"

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
: