# Tailscale Docker Image

## About

The Tailscale official image will not work if the iptables variant used by the container and the underlying host is different.

For instance, Raspberry Pi OS uses `iptables-nft` while the current official image uses `iptables-legacy`. As such, the rules are not being propagated properly to the host.

The image created by this repository uses `iptables-nft` by default.

If you are deploying Tailscale in a Kubernetes cluster via the [operator](https://tailscale.com/kb/1236/kubernetes-operator), you can update the operator's deployment with the following to use a custom image:

```yaml
- name: PROXY_IMAGE
  value: ghcr.io/elroy-haw/tailscale:vX.Y.Z
```

## References

- https://github.com/tailscale/tailscale/issues/5621
- https://github.com/zyclonite/tailscale-docker
