# dtrust-reconu

Open source developer resources for digital trust --  Ressources de développement open source à l'intention du réseau de confiance numérique

## Verifiable Credential Wallet - Portefeuille numérique d'attestations vérifiables

- [Aries Mobile Agent React Native / Aries Bifold](https://github.com/hyperledger/aries-mobile-agent-react-native)
- [Aries Framework JavaScript](https://github.com/hyperledger/aries-framework-javascript)
- [Aries Framework JavaScript Extensions](https://github.com/hyperledger/aries-framework-javascript-ext)

## Ledger Networks - Réseaux de registres

### CANdy Dev Ledger - Registres du réseau de la couche dev CANdy

- [Ledger Browser - Navigateur du registre](https://candy-dev.idlab.org/)
- [Ledger Monitor - Moniteur du registre](https://candy.uptime.neoterictech.ca/)
- [Genesis files - Fichiers Genesis](./CANdy/dev)
- [Ledger Node Deployment Scripts - Scripts de déploiement des nœuds du registre](https://github.com/CQEN-QDCE/Candy)

### CANdy Test and Production Ledgers - Registres du réseau des couches de tests et de production CANdy

To Be Added - À ajouter

### Developer Local Ledger - Registre local pour les développeurs

- [von-network](https://github.com/bcgov/von-network)

## Verifiable Credential Issuers / Verifiers - Émetteurs / consommateur d'attestations vérifiables

### Demo Environments / Environnements de démonstration

### [CANdy - Unverified Person Issuer / Émetteur de personne non vérifié (`prod`)](https://openvp-candy-dev.vonx.io/)

A test issuer from the BC Gov of an "unverified person." In this proof of concept issuer, there is no authentication
prior to the issuing a credential -- anyone can use the web service to just ask for an unverified person verifiable credential!
The user fills in "unverified" data into a form and on completion, an "unverified" credential is issued to the user's wallet.

AnonCreds technical details:

- Ledger: [CANdy-Dev](CANdy/dev/README.md)
- Ledger identifiers for proof request restrictions:
  - Schema Creator: [`9wVuYYDEDtpZ6CYMqSiWop`](https://candy-dev.idlab.org/browse/domain?page=1&query=9wVuYYDEDtpZ6CYMqSiWop&txn_type=1)
  - Schema: [`9wVuYYDEDtpZ6CYMqSiWop:2:unverified_person:0.1.0`](https://candy-dev.idlab.org/browse/domain?page=1&query=9wVuYYDEDtpZ6CYMqSiWop&txn_type=101)
  - Issuer: [`9wVuYYDEDtpZ6CYMqSiWop`](https://candy-dev.idlab.org/browse/domain?page=1&query=9wVuYYDEDtpZ6CYMqSiWop&txn_type=1)
  - Issuer Cred Def: [`9wVuYYDEDtpZ6CYMqSiWop:3:CL:23:default`](https://candy-dev.idlab.org/browse/domain?page=1&query=9wVuYYDEDtpZ6CYMqSiWop&txn_type=102)

The following is a proof request an ACA-Py verifier controller could use to request claims from an Unverified Person credential. In the following:

- The JSON is the body of a call to the `/present-proof-2.0/send-request` admin endpoint.
- Only the `given_names` and `family_name` claims are requested.
- The use of "names" in the requested attributes ensures that the claims must be sourced from the same verifiable credential.
- The request uses the `cred_def_id` restriction which means the claims from a credential must come from the identified CredDef from the identified Issuer.

``` jsonc

{
  "comment": "Unverified person proof request",
  "connection_id": "<fill in with connection>",
  "presentation_request": {
    "indy": {
      "name": "First Name, Last Name from the Unverified Person verifiable credential",
      "version": "1.0",
      "requested_attributes": {
        "0_name_uuid": {
          "names": [ "given_names", "family_name" ],
          "restrictions": [
            {
              "cred_def_id": "9wVuYYDEDtpZ6CYMqSiWop:3:CL:23:default"
            }
          ]
        }
      }
    }
  }
}

```

Although we don't have direct instructions on how to experiment with a verifier (yet!), those that want to use an "unverified person" credential can follow
these steps. These familiar with ACA-Py can skip by steps 1-3 -- they are for those new to ACA-Py.

1. Use the basic ACA-Py [Alice/Faber demo](https://github.com/hyperledger/aries-cloudagent-python/tree/main/demo#the-alicefaber-python-demo)
2. Learn about the ACA-Py Open API for a controller with the [Alice/Faber OpenAPI Demo](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AriesOpenAPIDemo.md)
3. Run the [Alice/Faber demo with a mobile wallet app](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AliceGetsAPhone.md)
4. Use the Trinsic Wallet, update the settings to use the CANdy Dev ledger (instructions to be added...), and then get an Unverified Person credential from the [Issuer](https://openvp-candy-dev.vonx.io/).
5. Redo the [Alice/Faber demo with a mobile wallet app](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AliceGetsAPhone.md) to the point where you have a connection between Faber and Alice's Trinsic Mobile app.
6. Follow the ACA-Py Open API instructions using the [Faber Open API to request a proof from Alice](https://github.com/hyperledger/aries-cloudagent-python/blob/main/demo/AriesOpenAPIDemo.md#requestingpresenting-a-proof) using the proof request JSON above.

We know -- it's lot. Look for an update soon with more precise instructions!

## Interoperability - Interpérabilité

- [Interoperability Test Status - Statuts des tests d'interopérabilité](https://aries-interop.info)
- [Aries Interop Profiles](https://github.com/hyperledger/aries-rfcs/tree/main/concepts/0302-aries-interop-profile)
- [Aries Interop Profile 2.0](https://github.com/hyperledger/aries-rfcs/tree/main/concepts/0302-aries-interop-profile#aries-interop-profile-version-20)
