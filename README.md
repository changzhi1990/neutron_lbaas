# New two extensions for Neutron LBaaS v2

## Extension 1：Configure sub processes in HAProxy
HAProxy can use `cpu-map` to configure one or more subprocess
and we can set binding relationship between each subprocess and
physical CPU, example:

            cpu-map 1 2
            cpu-map 2 4
            cpu-map 3 6
            cpu-map 4 8
            cpu-map 5 10

These configuration shows that five subprocess(1 2 3 4 5) binds its own
physical CPU(2 4 6 8 10).

Adding a new configuration named "cpu_binding" in configure file
lbaas_agent.ini .

all           All process will see this instance. This is the default. It
              may be used to override a default value.

odd           This instance will be enabled on processes 1,3,5,...63. This
              option may be combined with other numbers.

even          This instance will be enabled on processes 2,4,6,...64. This
              option may be combined with other numbers. Do not use it
              with less than 2 processes otherwise some instances might be
              missing from all processes.

## Extension 2：Configure http-keep-alive in frontend and backend
HAProxy can configure http-keep-alive in both frontend and backend.
In Neutron LBaaS v2, named "listener" and "pool". 

In this extension, we can specify "keep-alive" when creating HTTP listeners
and HTTP pools. If we do that, listeners and pools will have "option http-keep-alive"
configuration.
