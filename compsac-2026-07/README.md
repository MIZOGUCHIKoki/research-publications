# Implementation and Execution Environment
To evaluate and formally verify the proposed protocol, we constructed a containerized execution environment utilizing Docker. The formal verification was conducted using the Tamarin Prover. The environment configuration and the step-by-step execution procedure are described below.

## 1. Environment Setup
The verification environment is containerized using `Dockerfile` and `docker-compose.yml` to ensure reproducibility. The following command builds the Docker image and initializes the container in the background:

```bash
$ docker-compose up -d --build
```

## 2. Attaching to the Container
To interact with the isolated environment, an interactive bash session is established within the running container named tamarin:
```bash
$ docker exec -it tamarin /bin/bash
```

## 3. Formal Verification Execution
The protocol specification model defined in main.spthy is formally verified by executing the Tamarin Prover with bounded model checking capabilities. The verification command is executed as follows:

```bash
[root@.... tamarin] tamarin-prover +RTS -N120 -M400g -RTS --prove --bound=5 main.spthy
```
Depending on the underlying hardware architecture, the GHC runtime options (`+RTS` ... `-RTS`) and verification constraints must be configured appropriately:
- `N120`: Specifies the number of processors/cores allocated for parallel execution (set to 120 cores in this setup).

- `M400g`: Imposes a strict threshold on the maximum memory allocation to prevent out-of-memory errors (limited to 400 GB in this setup).

- `-bound=5`: Restricts the maximum depth of the proof search space to 5 steps to ensure termination within a finite bound.