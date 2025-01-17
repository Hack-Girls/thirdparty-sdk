# Mojaloop Thirdparty SDK
[![Git Commit](https://img.shields.io/github/last-commit/mojaloop/thirdparty-sdk.svg?style=flat)](https://github.com/mojaloop/thirdparty-sdk/commits/master)
[![Git Releases](https://img.shields.io/github/release/mojaloop/thirdparty-sdk.svg?style=flat)](https://github.com/mojaloop/thirdparty-sdk/releases)
[![CircleCI](https://circleci.com/gh/mojaloop/thirdparty-sdk.svg?style=svg)](https://circleci.com/gh/mojaloop/thirdparty-sdk)

> This package provides a Thirdparty (PISP) SDK that interfaces between a Mojaloop API compliant switch and a Thirdparty backend platform that does not natively implement the Mojaloop API.

The API between the SDK and the Thirdparty backend is synchronous HTTP while the interface between the SDK and the switch is native Mojaloop Third Party API.

This package exemplifies the use of the Mojaloop SDK Standard Components for TLS, JWS and ILP and is should be use together with [mojaloop/sdk-scheme-adapter](https://github.com/mojaloop/sdk-scheme-adapter)


## Quick Start
> The steps shown below illustrate setting up the Mojaloop Thirdparty SDK locally and how to run Inbound  and Outbound API services listening on `localhost`

1. Clone repo
   ```bash
   git clone git@github.com:mojaloop/thirdparty-sdk.git
   ```
2. Install dependencies
   ```bash
   npm install
   ```
3. Modify the hosts to setup local DNS for Redis
   ```bash
   127.0.0.1 redis
   ```
4. Start Redis container through docker-compose in a separate terminal window
   ```bash
   docker-compose up redis
   ```
5. Start Inbound API server 
   ```bash
   npm run start:inbound
   ```
   then visit in your web browser http://localhost:4005/health
   
   In case to start the test environment
   ```bash
   NODE_ENV=test npm run start:inbound
   ```
6. Start Outbound API server
   ```bash
   npm run start:outbound
   ```
   then visit in your web browser http://localhost:4006/health

   In case to start the test environment
   ```bash
   NODE_ENV=test npm run start:outbound
   ```

## Inbound & Outbound API
> This package delivers implementation Inbound and Outbound API services which will be used by Thirdparty to integrate with `Mojaloop Switch`

### Inbound API
  `Inbound API` service is called by `Mojaloop Switch`.  
  Its responsibility is to forward calls to `Thirdparty Backend` or help to deliver synchronous response for calls initiated by `Thirdparty backend` on `Outbound API`

### Outbound API
  `Outbound API` service is used by `Thirdparty backend` to make a call to `Mojaloop Switch`  
  Its responsibility is to transform asynchronous Mojaloop API native interface's set of calls to a synchronous call.

## Integration Test
   To run integration tests, first start `docker-compose` in root folder

   ```bash
   docker-compose build && docker-compose up
   ```
   
   then start `docker-compose` inside `docker` folder in a separate window.
   ```bash
   cd docker
   docker-compose build && docker-compose up
   ```

   then start `docker-compose` inside `docker/contract` folder in a separate window.
   ```bash
   cd docker/contract
   docker-compose build && docker-compose up
   ```

   Finally run the following command to execute tests
   ```bash
   npm run test:integration
   ```

# Contribution
Read the [contributing.md](./contributing.md) doc
