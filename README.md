## Introduction

The nextstrain project is an attempt to make flexible informatic pipelines and visualization tools to track ongoing pathogen evolution as sequence data emerges. The nextstrain project derives from [nextflu](https://github.com/blab/nextflu), which was specific to influenza evolution.

nextstrain is comprised of three components:

* [fauna](https://github.com/nextstrain/fauna): database and IO scripts for sequence and serological data
* [augur](https://github.com/nextstrain/augur): informatic pipelines to conduct inferences from raw data
* [auspice](https://github.com/nextstrain/auspice): web app to visualize resulting inferences

## fauna

*Definition: The animals of a given region or period considered as a whole. Also, prophetic Roman deity.*

The fauna database stores viral sequences and serological data in [rethinkdb](RETHINKDB.md). The current database and scripts is designed around influenza and Zika viruses.

### vdb

The [virus database (vdb)](vdb/) is used to store viral information in an organized schema. This allows easy storage and querying of viruses which can be downloaded in formatted fasta or json files.

### tdb

The [titer database (tdb)](tdb/) is used to store titer measurements in an organized schema. This allows easy storage and downloading of all measurements in the database.

## Install

Clone the repo and load submodules:

    git clone https://github.com/nextstrain/fauna.git
    git submodule update --init --recursive

Install Python modules needed to run upload/download scripts:

    pip install -r requirements.txt

Install Chateau Web UI:

    npm install

Backup and restore functionality requires the rethinkdb command line utility. This can be installed by following instructions [here](http://www.rethinkdb.com/docs/install/). With Homebrew, you can just do:

    brew install rethinkdb

## Chateau

[Chateau](https://github.com/nextstrain/chateau/) allows easy web access to the database. To run, do the following:

#### For remote rethink instance

1. Set environment variables `RETHINK_HOST` and `RETHINK_AUTH_KEY`.
2. Run with `npm run chateau` from directory `fauna/`.
3. Go to `http://localhost:3000/`.

#### For local rethink instance

2. Run with `npm run chateau-local` from directory `fauna/`.
3. Go to `http://localhost:3001/`.

Chateau configurations are stored in [`config.js`](config.js) for remote server and [`config_local.js`](config_local.js) for local server.

## Docker

Build a Docker image for fauna:

    docker build -t nextstrain/fauna:latest .

Push image to the Docker Hub:

    docker push nextstrain/fauna:latest

Run a shell from within the container:

    docker run --env-file environment_docker.env -t -i nextstrain/fauna /bin/bash

## License and copyright

Copyright 2016 Trevor Bedford and Charlton Callender.

Source code to nextstrain is made available under the terms of the [GNU Affero General Public License](LICENSE.txt) (AGPL). nextstrain is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more details.
