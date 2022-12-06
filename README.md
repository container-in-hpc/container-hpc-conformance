# Common HPC Container Initiative

This initiative has two goals:
1. Collect best-practices on how to build a container for HPC use cases
1. Define a set of labels/annotations to describe what execution environment is expected and what the container guarantees.

### Build Best-Practices

To define the labels and build a common understanding around them, the community needs to get an overview of how containers are build in different sites and user communities.

While some containers are accessible through different container registries, the artefact with which the container is build is mostly hidden. We want to change that so that we can learn from each other.

**Call for Participation #1**: Please provide an artefact on how a container is build along with the actual container image. 

#### Common Entrypoint

In order to use containers from different authors we need to define rules on what an entrypoint is meant to do. In other words, what happens when a container is started without arguments (w/o `CMD`)?

- It drops into an interactive shell
- it shows `--help` to inform the user how to use the container.

And what happens if a user (or scheduler) overwrites the `ENTRYPOINT`? Are all bets off in terms of usability?

-> [Entrypoint.md](Entrypoint.md)

### Annotations

Downloading a potentially huge container image as a black box and learn afterwards that it does not work on the execution environment, with the scheduler at hand or with the use-case in mind is frustrating.

This initiative thrives to help with that by defining a set of annotations for container images to assist end users, admins and container builders. 
1. **Container Expectations**: Drive an automated assesement whether a given container will work on a given execution environment.
1. **Container Tweaking**: Today, it is hard to take a container build by someone else and tweak it so that it works on a different environment. The annotations will provide artifacts (Dockerfile, ideally a higher level artifact like a spack environment, HPCCM recipies) to allow for adjustments.
1. **Container Documentation**: Links to resources in line with what the [opencontainers/image-spec](https://github.com/opencontainers/image-spec/blob/main/annotations.md). So that someone else is able to find a hello-world on how to use the container and guardrails on what not to expect.

### Container Dimmensions

Dealing with containers (or apps in general) in HPC has multiple dimensions: **Reproducibility**, **Performance**, **Portability**

Within the initiative we will need to define different levels for some dimensions to manage expectations of the end users and the container provider.

By using annotations a container its coordinates within these dimensions. E.g.

|               | Portability | MPI Type | Network type/ABI | libc | Kernel ABI |
| ------------- | ------------- | ------- | ------ | ---- |
| gromacs/mpich:2021.5@sha256:abc | medium | OpenMPI 4.3 | libfabric 1.15 | glibc 2.12 | 5.4 |


#### Reproducibility (initial take)

We do not allow for compromises on reproducibility. This dimension is strict.

#### Portability

A container should be clear about its portability limitations, so that a user is aware of what to expect. A hightly optimized container for a given system (HPE/Cray XC40 ABC) is welcome as long as it makes sure everyone understands the purpose and does not try to make it work on a MacBook Pro.

To convey the information of protability annotations are used.

In order to make this work it is paramount to get the input of **SysAdmins**. The community of system providers need to agree on a set of annotations themselves so that the expectations are set from both directions...

#### Performance

The performance of a container should not drop below a certain threshold (e.g. 30%) of the native, optimized performance. We recognize that containers with sub-par performance are better than no container at all.
