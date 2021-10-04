# network

## Prerequisites
- docker and docker-compose are installed

## Customizing
- IP_ADDRESS - Insert your own (public or private) ip-address. This will be used for the endpoint of the aries-agent to make it available from your wallet, and for downloading the tails-file from the tails-server to your wallet

- COMPANY_AGENT_GENESIS_URL - Add your company agent genesis url

- COMPANY_SCHEMA_ID - Add your company schema id

- HOTEL_CONTROLLER_AGENT_RECIPIENTKEY - Add hotel agent reception key

- HOTEL_AGENT_MASTERID_CREDENTIAL_DEFINITION_IDS - Add hotel credential definiton id

- HOTEL_AGENT_CORPORATEID_SCHEMA_IDS - Add hotel schema id

- HOTEL_CONTROLLER_AGENT_CORPORATEID_ISSUER_DIDS - Add hotel agent issuer DIDS


Check agent logs to find the above information

    Sample Schema

    ```
    {
      "schema_id": "xxxx",
      "schema": {
        "ver": "1.0",
        "id": "xxxx",
        "name": "corporateID",
        "version": "1.0",
        "attrNames": [
          "firmStreet",
          "firmName",
          "firmSubject",
          "firstName",
          "firmPostalcode",
          "lastName",
          "firmCity"
        ],
        "seqNo": 95
      }
    }
    ```

    Sample DID:

    ```
    {
      "service": [{
        "id": "did:example:123456789abcdefghi#did-communication",
        "type": "did-communication",
        "priority" : 0,
        "recipientKeys" : [ "did:example:123456789abcdefghi#1" ],
        "routingKeys" : [ "did:example:123456789abcdefghi#1" ],
        "accept": [
          "didcomm/aip2;env=rfc587",
          "didcomm/aip2;env=rfc19"
        ],
        "serviceEndpoint": "https://agent.example.com/"
      }]
    }
    ```

For more information check the following url :

    ```
    https://github.com/hyperledger/aries-rfcs/blob/master/features/0067-didcomm-diddoc-conventions/README.md
    ``

- HOTEL_CONTROLLER_INTEGRATIONSERVICE_APIKEY - Add hotel integration service Api key

- HOTEL_INTEGRATIONSERVICE_SMBSERVERCREDENTIALS_SERVERNAME -Add samba server url


## Start Application using the images from the DockerHub registry

To start the company application, run:

```
export IP_ADDRESS={private-ip-address} && docker-compose -f docker-compose-company_registry.yml up -d
```

Add your ip address in export command and run the above command.


To start the hotel application, run:

```
export IP_ADDRESS={private-ip-address} && docker-compose -f docker-compose-hotel_registry.yml up -d
```

Add your ip address in export command and run the above command.

## Stop Application

To stop it and remove the company container, run:

```
docker-compose -f docker-compose-company_registry.yml down
```

To stop it and remove the hotel container, run:

```
docker-compose -f docker-compose-hotel_registry.yml down
```

For more information refer to corresponding repository README.MD file

## Troubleshooting
- In total, there should be containers running afterward:
  - two agents (one for the company and one for the hotel)
  - two controllers (one for the company and one for the hotel)
  - two mongodbs (one for the company and one for the hotel)
  - one tails-server for the company

Moreover, next to the 5 repositories (company-controller, ...) there should be two mounted repositories, namely .indy_client_{hotel, company} which contain a few files each.
