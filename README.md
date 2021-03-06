[![Build](https://github.com/jthomperoo/custom-pod-autoscaler/workflows/main/badge.svg)](https://github.com/jthomperoo/custom-pod-autoscaler/actions)
[![codecov](https://codecov.io/gh/jthomperoo/custom-pod-autoscaler/branch/master/graph/badge.svg)](https://codecov.io/gh/jthomperoo/custom-pod-autoscaler)
[![go.dev](https://img.shields.io/badge/go.dev-reference-007d9c?logo=go&logoColor=white&style=flat)](https://pkg.go.dev/github.com/jthomperoo/custom-pod-autoscaler)
[![Go Report
Card](https://goreportcard.com/badge/github.com/jthomperoo/custom-pod-autoscaler)](https://goreportcard.com/report/github.com/jthomperoo/custom-pod-autoscaler)
[![Documentation
Status](https://readthedocs.org/projects/custom-pod-autoscaler/badge/?version=latest)](https://custom-pod-autoscaler.readthedocs.io/en/latest)
[![License](https://img.shields.io/:license-apache-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)

<p>This project is supported by:</p>
<p>
  <a href="https://www.digitalocean.com/">
    <img src="https://opensource.nyc3.cdn.digitaloceanspaces.com/attribution/assets/SVG/DO_Logo_horizontal_blue.svg" width="201px">
  </a>
</p>

# Custom Pod Autoscaler

This is the Custom Pod Autoscaler (CPA) code and base images.

The CPA is part of the [Custom Pod Autoscaler Framework](https://custom-pod-autoscaler.readthedocs.io/en/stable).

## What is it?

A Custom Pod Autoscaler is a Kubernetes autoscaler that is customised and user created. Custom Pod Autoscalers are
designed to be similar to the Kubernetes Horizontal Pod Autoscaler. The Custom Pod Autoscaler framework allows easier
and faster development of Kubernetes autoscalers.
A Custom Pod Autoscaler can be created by using this project, extending the Docker base images provided and inserting
your own logic; see the
[examples for more information](https://github.com/jthomperoo/custom-pod-autoscaler/tree/v1.0.1/example).

## Features

- Supports any language, environment and framework; the only requirement is it must be startable by a shell command
or HTTP request.
- Supports all configuration options of the Horizontal Pod Autoscaler (downscale stabilisation, sync period etc.)
- Allows fast and easy prototyping and development.
- Abstracts away all complicated Kubernetes API interactions.
- Exposes a HTTP REST API for integration with wider systems/manual intervention.
- Can write autoscalers with limited Kubernetes API or lifecycle knowledge.
- Configuration at build time or deploy time.
- Allows scaling to and from zero.
- Can be configured without master node access, can be configured on managed providers such as EKS or GKE.

## How does it work?
A Custom Pod Autoscaler has a base program (defined in this repository) that handles interacting with user logic, for
example by using shell commands and piping data into them.
When developing a Custom Pod Autoscaler you define logic for two stages:

* Metric gathering - collecting or generating metrics; can be calling metrics APIs, running calculations locally,
making HTTP requests.
* Evaluating metrics - taking these gathered metrics and using them to decide how many replicas a resource should have.

These two pieces of logic are all the custom logic required to build a Custom Pod Autoscaler, the base program will
handle all Kubernetes API interactions for scaling/retrieving resources.

## Getting started

Check out [this getting started guide for a quick start for
developers](https://custom-pod-autoscaler.readthedocs.io/en/stable/user-guide/getting-started).

## More information

See the [wiki for more information, such as guides and
references](https://custom-pod-autoscaler.readthedocs.io/en/stable/).

## Developing this project
### Environment
Developing this project requires these dependencies:

* [Go](https://golang.org/doc/install) >= `1.13`
* [Golint](https://github.com/golang/lint)
* [Docker](https://docs.docker.com/install/)

To view docs locally, requires:

* [mkdocs](https://www.mkdocs.org/)

### Commands

* `make` - builds the CPA binary.
* `make docker` - builds the CPA base images.
* `make lint` - lints the code.
* `make unittest` - runs the unit tests.
* `make vendor` - generates a vendor folder.
* `make doc` - hosts the documentation locally, at `127.0.0.1:8000`.
