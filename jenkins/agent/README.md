# About the Agent Image

Installed:
- Kubectl
- Helm
- Docker

## Setting up nodes for an agent

Docker must be installed on the node, with a docker group gid 999 setup. 

`groupadd docker`
`usermod -aG docker root`

## TODO

- Agent is all-in-one bundle with --privileged mode active. Need to work on a Docker in Docker type solution that can run without privilege. Issues so far were ARM64 compatibility (need to build myself?)
    - This also includes volume forwarding the /var/run/docker.sock from host to child container = not ideal.
    - Sysbox?