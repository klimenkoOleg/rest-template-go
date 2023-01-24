# The RESTful API Template Project [Golang]

[Join our slack](https://speakeasy-dev.slack.com/archives/C03QVDNMCMT) if you need any help with the template, or just want to chat about APIs!

![speakeasy-logo](https://user-images.githubusercontent.com/6267663/180816984-254daaec-a8e3-4c47-ac11-6c6d52a5e390.png)

<p align="center">
  <a href='http://makeapullrequest.com'><img alt='PRs Welcome' src='https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=shields'/></a>
  <a href='https://join.slack.com/t/speakeasy-dev/shared_invite/zt-1df0lalk5-HCAlpcQiqPw8vGukQWhexw'><img alt="Join Slack Community" src="https://img.shields.io/badge/slack%20community-join-blue"/></a>
  <a href='https://goreportcard.com/report/github.com/speakeasy-api/rest-template-go'><img alt='Go Report Card' src='https://img.shields.io/badge/go%20report-A+-brightgreen.svg?style=flat'/></a>
</p>


## How To Use This Repo

This repo is intended to be used by Golang developers seeking to understand the building blocks of a simple and well-constructed REST API service. We have built a simple CRUD API which exhibits the characteristics we expect our own developers to apply to the APIs we build at Speakeasy:

- **Entity-based**: The resources available should represent the domain model. Each resource should have the CRUD methods implemented (even if not all available to API consumers). In our template, we have a single resource defined (users.go). However other resources could be easily added by copying the template and changing the logic of the service layer.
- **Properly Abstracted**: The Transport, service, and data layers are all cleanly abstracted from one another. This makes it easy to make apply updates to the API endpoints
- **Consistent**: It's important that consumers of a service have guaranteed consistency across the entire range of API endpoints and methods. In this service, responses are consistently formatted whether successfully returning a JSON object or responding with an error code. All the service's methods use shared response (http.go) and error (errors.go) handler functions to ensure consistency.
- **Tested**: We believe that a blend of unit and integration testing is important for ensuring that the service maintains its contract with consumers. The service repo therefore contains a collection of unit and integration tests for the various layers of the service.
- **Explorable**: It is important for developers to be able to play with an endpoint in order to understand it. We have provided Postman collections for testing out the REST endpoints exposed by the service. That's why there is a `Bootstrap Users` collection that can be run using the `Run collection` tool in Postman that will create 100 users to test the search endpoint with.

This repo can serve as an educational tool, or be used as a foundation upon which developers can build their own basic API scaffolding to turn API development into a consistent and marignally easier activity.

## Getting Started

### Prerequisites

- Go 1.18 (should still be backwards compatible with earlier versions)

### Running locally

1. From root of the repo
2. Run `docker-compose up` will start the dependencies and server on port 8080

### Running via docker

1. From root of the repo
2. Run `docker-compose up` will start the dependencies and server on port 8080

### Postman

The collections will need an environment setup with `scheme`, `port` and `host` variables setup with values of `http`, `8080` and `localhost` respectively.

### Run tests

Some of the integration tests use docker to spin up dependencies on demand (ie a postgres db) so just be aware that docker is needed to run the tests.

1. From root of the repo
2. Run `go test ./...`
### Dependencies list

There are libraries used as a dependency for the template project.
Let me remind, to install a dependency, one need to execute:
`go get -u go.uber.org/zap`

1. `go.uber.org/zap` - blazing fast, structured, leveled logging in Go.
2. `github.com/caarlos0/env/v6` - a simple and zero-dependencies library to parse environment variables into structs.
3. `github.com/go-playground/validator/v10` - Package validator implements value validations for structs and individual fields based on tags.
Usage example:
```
// User contains user information
type User struct {
FirstName      string     `validate:"required"`
LastName       string     `validate:"required"`
Age            uint8      `validate:"gte=0,lte=130"`
Email          string     `validate:"required,email"`
FavouriteColor string     `validate:"iscolor"`                // alias for 'hexcolor|rgb|rgba|hsl|hsla'
Addresses      []*Address `validate:"required,dive,required"` // a person can have a home and cottage...
}
```
4. `gopkg.in/yaml.v2` - YAML support for the Go language.
5. `github.com/golang-migrate/migrate/v4` - Database migrations written in Go. Use as CLI or import as library.
6. `github.com/jmoiron/sqlx` - sqlx is a library which provides a set of extensions on go's standard database/sql library. The sqlx versions of sql.DB, sql.TX, sql.Stmt, et al. all leave the underlying interfaces untouched, so that their interfaces are a superset on the standard ones. This makes it relatively painless to integrate existing codebases using database/sql with sqlx.
7. `github.com/lib/pq` - A pure Go postgres driver for Go's database/sql package.
8. `github.com/gorilla/mux`
9. `go.opentelemetry.io/contrib/instrumentation/net/http/otelhttp`
10. `go.opentelemetry.io/otel/exporters/stdout/stdouttrace`
11. `github.com/golang/mock/gomock`
12. `github.com/stretchr/testify/assert`
13. `github.com/AlekSi/pointer`
14. 