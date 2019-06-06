.. _get-list-node-service-events:

List node service events
~~~~~~~~~~~~~~~~~~~~~~~~

.. code::

    GET /v1.0/{account}/loadbalancers/{loadBalancerId}/nodes/events

Lists node service events.

Lists events associated with the activity between the node and the load
balancer. The events report errors found with the node. The ``detailedMessage``
provides the detailed reason for the error. The events can be processed as
JSON, XML, and ATOM. This call has pagination and a list limit of 100 events.
Events are stored for 90 days.


The following table shows the possible response codes for this operation:

+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|200                       |Success                  |Request succeeded.       |
+--------------------------+-------------------------+-------------------------+
|400                       |Bad Request              |The request is missing   |
|                          |                         |one or more elements, or |
|                          |                         |the values of some       |
|                          |                         |elements are invalid.    |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |You are not authorized   |
|                          |                         |to complete this         |
|                          |                         |operation. This error    |
|                          |                         |can occur if the request |
|                          |                         |is submitted with an     |
|                          |                         |invalid authentication   |
|                          |                         |token.                   |
+--------------------------+-------------------------+-------------------------+
|404                       |Not Found                |The requested item was   |
|                          |                         |not found.               |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+
|422                       |ImmutableEntity          |This fault is returned   |
|                          |                         |when a user attempts to  |
|                          |                         |modify an item that is   |
|                          |                         |not currently in a state |
|                          |                         |that allows              |
|                          |                         |modification. For        |
|                          |                         |example, load balancers  |
|                          |                         |in a status of           |
|                          |                         |PENDING_UPDATE,BUILD, or |
|                          |                         |DELETED may not be       |
|                          |                         |modified.                |
+--------------------------+-------------------------+-------------------------+
|500                       |Load Balancer Fault      |The load balancer has    |
|                          |                         |experienced a fault.     |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The service is not       |
|                          |                         |available.               |
+--------------------------+-------------------------+-------------------------+

Request
-------

The following table shows the URI parameters for the request:

+--------------------------+-------------------------+-------------------------+
|Name                      |Type                     |Description              |
+==========================+=========================+=========================+
|{account}                 |String                   |The ID for the tenant or |
|                          |                         |account in a multi-      |
|                          |                         |tenancy cloud.           |
+--------------------------+-------------------------+-------------------------+
|{loadBalancerId}          |String                   |The ID for the load      |
|                          |                         |balancer.                |
+--------------------------+-------------------------+-------------------------+

This operation does not accept a request body.

Response
--------


**Example List node service events: JSON response**

.. code::

    {"nodeServiceEvents":[
        {
            "detailedMessage":"Node is ok",
            "nodeId":373,
            "id":7,
            "type":"UPDATE_NODE",
            "description":"Node '373' status changed to 'ONLINE' for load balancer '323'",
            "category":"UPDATE",
            "severity":"INFO",
            "relativeUri":"/406271/loadbalancers/323/nodes/373/events",
            "accountId":406271,
            "loadbalancerId":323,
            "title":"Node Status Updated",
            "author":"Rackspace Cloud",
            "created":"2019-02-12T09:23:36Z"
        },
        {
            "detailedMessage":"Invalid HTTP response received; premature end of headers",
            "nodeId":373,
            "id":8,
            "type":"UPDATE_NODE",
            "description":"Node '373' status changed to 'OFFLINE' for load balancer '323'",
            "category":"UPDATE",
            "severity":"INFO",
            "relativeUri":"/406271/loadbalancers/323/nodes/373/events",
            "accountId":406271,
            "loadbalancerId":323,
            "title":"Node Status Updated",
            "author":"Rackspace Cloud",
            "created":"2019-02-12T09:28:36Z"
        }
    ],
    "links": [
        {
            "otherAttributes": {},
            "href": "http://localhost:8080/528830/loadbalancers/nodes/events?offset=4&limit=2",
            "rel": "next"
        },
        {
            "otherAttributes": {},
            "href": "http://localhost:8080/528830/loadbalancers/nodes/events?offset=0&limit=2",
            "rel": "previous"
        }
    ]}

**Example List node service events: XML response**

.. code::

    <nodeServiceEvents>
        <nodeServiceEvent nodeId="373" detailedMessage="Node is ok" id="7"
                          loadbalancerId="323" accountId="406271" author="Rackspace Cloud" title="Node Status Updated"
                          description="Node '373' status changed to 'ONLINE' for load balancer '323'" type="UPDATE_NODE"
                          category="UPDATE" severity="INFO" relativeUri="/406271/loadbalancers/323/nodes/373/events"
                          created="2019-02-12T09:23:36Z"/>
        <nodeServiceEvent nodeId="373" detailedMessage="Invalid HTTP response received; premature end of headers" id="8"
                          loadbalancerId="323" accountId="406271" author="Rackspace Cloud" title="Node Status Updated"
                          description="Node '373' status changed to 'OFFLINE' for load balancer '323'" type="UPDATE_NODE"
                          category="UPDATE" severity="INFO" relativeUri="/406271/loadbalancers/323/nodes/373/events"
                          created="2019-02-12T09:28:36Z"/>
        <atom:link
            href="http://localhost:8080/528830/loadbalancers/nodes/events?offset=4&limit=2"
            rel="next"/>
        <atom:link
            href="http://localhost:8080/528830/loadbalancers/nodes/events?offset=0&limit=2"
            rel="previous"/>
    </nodeServiceEvents>

**Example List node service events: ATOM response**

.. code::

    <?xml version='1.0' encoding='UTF-8'?>
    <feed xmlns="http://www.w3.org/2005/Atom">
        <link rel="next" href="http://127.0.0.1:8080/pub/406271/loadbalancers/323/nodes/events.atom?page=2"/>
        <title type="text">Node Service Feed</title>
        <id>406271-loadbalancers-323-nodeservice</id>
        <author>
            <name>Rackspace Cloud</name>
        </author>
        <entry>
            <title type="text">Node Status Updated</title>
            <summary type="text">Node '373' status changed to 'ONLINE' for load balancer '323'</summary>
            <author>
                <name>Rackspace Cloud</name>
            </author>
            <link href="http://127.0.0.1:8080/pub/406271/loadbalancers/323/nodes/373/events"/>
            <id>406271-loadbalancers-323-nodes-373-events-20123041018230</id>
            <category term="UPDATE"/>
            <updated>2019-02-12T09:23:36Z</updated>
            <content type="text">Node is ok</content>
        </entry>
        <entry>
            <title type="text">Node Status Updated</title>
            <summary type="text">Node '373' status changed to 'OFFLINE' for load balancer '323'</summary>
            <author>
                <name>Rackspace Cloud</name>
            </author>
            <link href="http://127.0.0.1:8080/pub/406271/loadbalancers/323/nodes/373/events"/>
            <id>406271-loadbalancers-323-nodes-373-events-20123041122250</id>
            <category term="UPDATE"/>
            <updated>2019-02-12T09:28:36Z</updated>
            <content type="text">Details: Invalid HTTP response received; premature end of headers</content>
        </entry>
    </feed>
