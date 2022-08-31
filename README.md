## Uffizzi Starter App - Establish an On-demand Uffizzi Environment in 2 steps
=========

## 1. Fork this Repo
## 2. Open a PR of `double-dogs` branch against `main` in your fork

The PR will trigger a series of [jobs](https://github.com/UffizziCloud/uffizzi-2-step-starter-app/blob/main/.github/workflows/uffizzi-environment.yml) with Uffizzi Github Action's re-useable [workflow](https://github.com/marketplace/actions/create-preview-environment) being utilized to create an on-demand environment for this example micro-services application.  The environment URL and Uffizzi Dashboard URL will be posted as a comment in your PR when the workflow completes.

-New commits will update the environment.  
-Merging or Closing the PR will delete the environment.  
-The environment is set to `delete` in 1hr 

The environment is defined by [docker-compose](https://github.com/UffizziCloud/uffizzi-2-step-starter-app/blob/main/docker-compose.template.yml).

From within the Uffizzi Dashboard you can view logs and events, manage projects, manage teams, set RBAC, set SSO, and establish password protected URLs.

**Note-** Running this workflow will create a free Uffizzi Platform account under the Github account from which it is initiated.  Each account receives 10,000 preview minutes per month for free.  If you exceed the free tier threshold your services will be paused until you provide a credit card.  Users are not liable for paid services unless they authorize billing.

Using Uffizzi for Crypto-mining, bots and other unauthorized activities is strictly prohibited per the user policy.  Users who break the service agreement are at risk of being banned from future use.  

Architecture
-----

![Architecture diagram](architecture.png)

* A front-end web app in [Python](/vote) or [ASP.NET Core](/vote/dotnet) which lets you vote between two options
* A [Redis](https://hub.docker.com/_/redis/) or [NATS](https://hub.docker.com/_/nats/) queue which collects new votes
* A [.NET Core](/worker/src/Worker), [Java](/worker/src/main) or [.NET Core 2.1](/worker/dotnet) worker which consumes votes and stores them in…
* A [Postgres](https://hub.docker.com/_/postgres/) or [TiDB](https://hub.docker.com/r/dockersamples/tidb/tags/) database backed by a Docker volume
* A [Node.js](/result) or [ASP.NET Core SignalR](/result/dotnet) webapp which shows the results of the voting in real time


Notes
-----

The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.

This isn't an example of a properly architected perfectly designed distributed app... it's just a simple 
example of the various types of pieces and languages you might see (queues, persistent data, etc), and how to 
deal with them in Docker at a basic level. 
