# hrbacx: A High-Performance, Multi-Backend Hierarchical RBAC Service

**hrbacx** is a flexible and powerful Hierarchical Role-Based Access Control (HRBAC) service written in Go. It provides a simple REST API for managing roles, permissions, and user assignments, with support for multiple database backends.

## Features

*   **Hierarchical Roles:** Model complex organizational structures with parent-child role relationships.
*   **Multiple Database Backends:** Choose the database that fits your needs. Supported backends include:
    *   PostgreSQL
    *   MySQL
    *   Nebula Graph
    *   Redis
*   **Simple REST API:** Easily integrate `hrbacx` with your existing applications using a straightforward JSON-based API.
*   **High Performance:** Built with Go and optimized for speed, `hrbacx` can handle demanding workloads.
*   **Easy to Deploy:** Run `hrbacx` as a standalone service or deploy it in a Docker container.

## Architecture

`hrbacx` is built with a clean and modular architecture:

*   **Go Backend:** The core of the service is a Go application built with the [Gin](https://gin-gonic.com/) web framework.
*   **Database Layer:** A flexible database layer uses [GORM](https://gorm.io/) for SQL databases and dedicated clients for Nebula Graph and Redis.
*   **REST API:** A simple set of API endpoints for managing your RBAC policies.

## Getting Started

### Prerequisites

*   [Go](https://golang.org/doc/install) (version 1.23 or later)
*   [Docker](https://docs.docker.com/get-docker/)

### Installation and Running

1.  **Clone the repository:**

    ```bash
    git clone https://github.com/skyrocketOoO/hrbacx.git
    cd hrbacx
    ```

2.  **Start a database backend:**

    Use the `Makefile` to start your chosen database in a Docker container:

    ```bash
    # For PostgreSQL
    make run-postgres

    # For MySQL
    make run-mysql

    # For Redis
    make run-redis
    ```

3.  **Run the server:**

    Start the `hrbacx` server, specifying your chosen database:

    ```bash
    go run main.go server -d <database>
    ```

    Replace `<database>` with `postgres`, `mysql`, or `redis`. The server will be available at `http://localhost:8080`.

## API Endpoints

*   `POST /addLeader`: Create a hierarchical relationship between roles.
*   `POST /assignPermission`: Assign a permission to a role.
*   `POST /assignRole`: Assign a role to a user.
*   `POST /checkPermission`: Check if a user has a specific permission.
*   `POST /clearAll`: Clear all roles, permissions, and assignments.

## Configuration

You can configure the `hrbacx` server using command-line flags:

*   `-p, --port`: The port to run the server on (default: `8080`).
*   `-d, --database`: The database backend to use (`postgres`, `nebula`, `mysql`, `redis`; default: `postgres`).
*   `-e, --env`: The environment (`dev` or `prod`; default: `dev`).
*   `-a, --automigrate`: Enable or disable automatic database migrations (default: `false`).

## Future Work

*   Expanded test cases and integration with Grafana for monitoring.
*   Implementation of different graph traversal methods (CTE, BFS, DFS).
*   A C function for PostgreSQL for even higher performance.
*   A pure key-value store implementation.

## License

This project is licensed under the [MIT License](LICENSE).
