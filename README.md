# AAS Agent: the FIWARE IoT Agent for AAS

[![FIWARE IoT Agents](https://nexus.lab.fiware.org/static/badges/chapters/iot-agents.svg)](https://www.fiware.org/developers/catalogue/)
[![License: AGPL](https://img.shields.io/badge/License-AGPL_v3-blue.svg)](https://opensource.org/licenses/AGPL-3.0)
[![Docker badge](https://img.shields.io/badge/quay.io-fiware%2Fiotagent--aas-grey?logo=red%20hat&labelColor=EE0000)](https://quay.io/repository/fiware/iotagent-aas)
[![Support badge](https://img.shields.io/badge/support-stackoverflow-orange)](https://stackoverflow.com/questions/tagged/fiware+iot)<br/>
[![Documentation badge](https://img.shields.io/readthedocs/iotagent-aas.svg)](https://iotagent-aas.rtfd.io/)
[![CI](https://github.com/Engineering-Research-and-Development/iotagent-aas/workflows/CI/badge.svg)](https://github.com/Engineering-Research-and-Development/iotagent-aas/actions?query=workflow%3ACI)
[![Coverage Status](https://coveralls.io/repos/github/Engineering-Research-and-Development/iotagent-aas/badge.svg?branch=master)](https://coveralls.io/github/Engineering-Research-and-Development/iotagent-aas?branch=master)
[![OpenSSF Best Practices](https://www.bestpractices.dev/projects/9735/badge)](https://www.bestpractices.dev/projects/9735)
![Status](https://nexus.lab.fiware.org/static/badges/statuses/full.svg)
[![Join the chat at https://gitter.im/iotagent-aas/community](https://badges.gitter.im/iotagent-aas/community.svg)](https://gitter.im/iotagent-aas/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
<br/> <img align="right" width="150" src="/docs/images/iotagent-logo.png" />

An Internet of Things Agent accepting data from AAS devices. This IoT Agent is designed to be a bridge between the AAS
(Asset Administration Shell) and the
[NGSI](https://swagger.lab.fiware.org/?url=https://raw.githubusercontent.com/Fiware/specifications/master/OpenAPI/ngsiv2/ngsiv2-openapi.json)
interface of a context broker.

The intended level of complexity to support these operations should consider a limited human intervention (mainly during
the setup of a new AAS endpoint), through the mean of a parametrization task (either manual or semi-automatic, using a
text-based parametrization or a simple UI to support the configuration) so that no software coding is required to adapt
the agent to different AAS devices.

It is based on the [IoT Agent Node.js Library](https://github.com/telefonicaid/iotagent-node-lib). Further general
information about the FIWARE IoT Agents framework, its architecture and the common interaction model can be found in the
library's GitHub repository.

This project is part of [FIWARE](https://www.fiware.org/). For more information check the
[FIWARE Catalogue entry for the IoT Agents](https://github.com/Fiware/catalogue/tree/master/iot-agents).

| :books: [Documentation](https://iotagent-aas.rtfd.io) | <img style="height:1em" src="https://quay.io/static/img/quay_favicon.png"/> [quay.io](https://quay.io/repository/fiware/iotagent-aas) | :mortar_board: [Academy](https://fiware-academy.readthedocs.io/en/latest/iot-agents/idas) | :dart: [Roadmap](https://github.com/Engineering-Research-and-Development/iotagent-aas/blob/master/roadmap.md) |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |


## Contents

-   [Background](#background)
-   [Install](#getting-started---install)
    -   [Docker install](#docker---recommended)
    -   [NPM Install](#npm)
-   [Usage](#usage)
-   [API](#api)
-   [Testing](#testing)
-   [Quality Assurance](#quality-assurance)
-   [License](#license)

## Background

### Positioning in the overall F4I Reference Architecture

The F4I AAS Agent is based on the reference implementation of the FIWARE Backend Device Management Generic Enabler,
IDAS, delivered by Telefonica I+D. IDAS provides a collection of Agents - i.e., independent processes that are typically
executed in the proximity of IoT devices and that are responsible for bridging a specific IoT protocol to the NGSI
standard (e.g. the IDAS distribution includes off-the-shelf Agents for LwM2M and MQTT). To this end, IDAS links the NGSI
southbound API of the FIWARE Orion Context Broker to the northbound API of the IoT application stack, by providing a
software library (the IoT Agent Lib depicted in the previous figure) for developing custom Agents that may extend the
bridging capabilities of IDAS to other protocols. The F4I IDAS AAS Agent makes use of this framework to integrate
AAS-based devices in a publish-subscribe system based on the FIWARE Orion Context Broker.

## Getting Started - Install

Currently two options are available to install the Agent:

### Docker - Recommended

We suggest using a **Docker-first** approach in order to avoid issues related to your environment configuration.
Moreover, using this approach you will be provided with main components: OCB, Mongo, Agent instances.

A step-by-step tutorial is available
[here](https://github.com/Engineering-Research-and-Development/iotagent-aas/blob/master/docs/aas_agent_tutorial.md)

### npm

Before launching the Agent you must install Orion Context Broker (Be aware to choose the correct version, please use
_orion_ if it's needed to test the Agent with NGSI v2 otherwise use _orion-ld_ in case of NGSI-ld test.) and a AAS
Server. After that you must tell the Agent how to interact with these components by using config.js file. Once
configuration is complete you can execute these commands to run the Agent.

```console
$ npm install
$ node bin/iotagent-aas
```

Further Information about how to install the AAS IoT Agent can be found at the corresponding section of the
[Installation & Administration Guide](https://iotagent-aas.readthedocs.io/en/latest/installation_and_administration_guide).

## Usage

Information about how to use the IoT Agent can be found in the
[User & Programmers Manual](https://iotagent-aas.readthedocs.io/en/latest/user_and_programmers_manual).

### Administration Services

Administration services are reachable at port specified by api-port property (config.js).

|     |  Service   |                          Description                          |
| --- | :--------: | :-----------------------------------------------------------: |
| GET | `/version` | Returns information about version, name and agent description |

### Poll commands

Poll commands can be enabled switching polling property to true (config.js). Once enabled poll command, you can
customize the polling Daemon Frequency and Expiration time still in the (config.js). The polling-commands-timer is
referred to the feature developed, that consist in the execution of the older polling command periodically (if exists)
ed delete it in case of success.

## API

Apiary reference for the Configuration API can be found
[here](http://docs.telefonicaiotiotagents.apiary.io/#reference/configuration-api) More information about IoT Agents and
their APIs can be found in the IoT Agent Library [documentation](https://iotagent-node-lib.rtfd.io/).

## Testing

For test purpose can create an AAS server using the code in the following
[GitHub repository](https://github.com/Engineering-Research-and-Development/opc-ua-car-server/)

Firstly edit the [config.js](conf/config.js) in order to set Northbound (NGSI) and Southbound (AAS) settings.

Further information about configuration properties can be found [here](docs/howto.md)

For checking current status of the Agent, send a request to /version service
(`http://{agent-ip-address}:api-port/version`)

### Secure connection with an AAS Server

AAS Agent will automatically generate key pairs and certificates (persisted in `iotagent-aas/certificates`) to establish
a secure connection to the AAS Server.

### How to get access to the advanced API and Documentation topics

Documentation about the AAS Administration API can be found [here](https://iotagentaas.docs.apiary.io/)

## Quality Assurance

The **IoT Agent for AAS** project is part of [FIWARE](https://fiware.org/) and has been rated as follows:

-   **Version Tested:**
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Version&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.version&colorB=blue)
-   **Documentation:**
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Completeness&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.docCompleteness&colorB=blue)
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Usability&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.docSoundness&colorB=blue)
-   **Responsiveness:**
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Time%20to%20Respond&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.timeToCharge&colorB=blue)
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Time%20to%20Fix&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.timeToFix&colorB=blue)
-   **FIWARE Testing:**
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Tests%20Passed&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.failureRate&colorB=blue)
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Scalability&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.scalability&colorB=blue)
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Performance&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.performance&colorB=blue)
    ![](https://img.shields.io/badge/dynamic/aas.svg?label=Stability&url=https://fiware.github.io/catalogue/json/iotagent_AAS.json&query=$.stability&colorB=blue)

---

## License

The IoT Agent for AAS is licensed under [Affero General Public License (GPL) version 3](./LICENSE).

© 2024 Engineering Ingegneria Informatica S.p.A.

The following third-party libraries are used under license

1.  [iotagent-node-lib](https://github.com/telefonicaid/iotagent-node-lib) - **AGPL** © 2014-2021 Telefonica
    Investigación y Desarrollo

The full list of third-party libraries licenses can be found
[here](https://htmlpreview.github.io/?https://github.com/Engineering-Research-and-Development/iotagent-aas/blob/master/docs/aas_agent_dependencies.html)

### Are there any legal issues with AGPL 3.0? Is it safe for me to use?

No problem in using a product licensed under AGPL 3.0. Issues with GPL (or AGPL) licenses are mostly related with the
fact that different people assign different interpretations on the meaning of the term “derivate work” used in these
licenses. Due to this, some people believe that there is a risk in just _using_ software under GPL or AGPL licenses
(even without _modifying_ it).

For the avoidance of doubt, the owners of this software licensed under an AGPL 3.0 license wish to make a clarifying
public statement as follows:

"Please note that software derived as a result of modifying the source code of this software in order to fix a bug or
incorporate enhancements is considered a derivative work of the product. Software that merely uses or aggregates (i.e.
links to) an otherwise unmodified version of existing software is not considered a derivative work, and therefore it
does not need to be released as under the same license, or even released as open source."
