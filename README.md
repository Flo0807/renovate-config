# Renovate Config

This repository contains [Renovate](renovatebot.com) base configurations.

## Usage

### Base Configuration

To use the base configuration, add the following to your renovate configuration file:

```json
{
  "extends": ["github>Flo0807/renovate-config//base"]
}
```

### Elixir Debian Configuration

Use this configuration if you are using Debian as your base image.

To use the Elixir Debian configuration, add the following to your renovate configuration file:

```json
{
  "extends": ["github>Flo0807/renovate-config//elixir-debian"]
}
```

The `elixir-debian` configuration groups Elixir, Erlang and Debian dependencies updates together in one Pull Request as they are often used to construct the Elixir Docker image e.g. `hexpm/elixir:${ELIXIR_VERSION}-erlang-${OTP_VERSION}-debian-${DEBIAN_VERSION}`.

This allows you to update the image in one go and test the changes in a single PR.

Make sure to update your Dockerfile so Renovate can detect the versions you are using.

```Dockerfile
# renovate: datasource=hexpm-bob depName=elixir
ARG ELIXIR_VERSION=1.18.1
# renovate: datasource=github-tags depName=erlang packageName=erlang/otp versioning=regex:^(?<major>\d+?)\.(?<minor>\d+?)(\.(?<patch>\d+))?$ extractVersion=^OTP-(?<version>\S+)
ARG OTP_VERSION=27.2
# renovate: datasource=docker depName=debian packageName=debian
ARG DEBIAN_VERSION=bullseye-20241223-slim

ARG BUILDER_IMAGE="hexpm/elixir:${ELIXIR_VERSION}-erlang-${OTP_VERSION}-debian-${DEBIAN_VERSION}"
ARG RUNNER_IMAGE="debian:${DEBIAN_VERSION}"
```

### Elixir Ubuntu Configuration

Use this configuration if you are using Ubuntu as your base image.

To use the Elixir Ubuntu configuration, add the following to your renovate configuration file:

```json
{
  "extends": ["github>Flo0807/renovate-config//elixir-ubuntu"]
}
```

The `elixir-ubuntu` configuration groups Elixir, Erlang and Ubuntu dependencies updates together in one Pull Request as they are often used to construct the Elixir Docker image e.g. `hexpm/elixir:${ELIXIR_VERSION}-erlang-${OTP_VERSION}-ubuntu-${UBUNTU_VERSION}`.

This allows you to update the image in one go and test the changes in a single PR.

Make sure to update your Dockerfile so Renovate can detect the versions you are using.

```Dockerfile
# renovate: datasource=hexpm-bob depName=elixir
ARG ELIXIR_VERSION=1.18.1
# renovate: datasource=github-tags depName=erlang packageName=erlang/otp versioning=regex:^(?<major>\d+?)\.(?<minor>\d+?)(\.(?<patch>\d+))?$ extractVersion=^OTP-(?<version>\S+)
ARG OTP_VERSION=27.2
# renovate: datasource=docker depName=ubuntu versioning=ubuntu
ARG UBUNTU_VERSION=jammy-20240808

ARG BUILDER_IMAGE=hexpm/elixir:${ELIXIR_VERSION}-erlang-${OTP_VERSION}-ubuntu-${UBUNTU_VERSION}
ARG RUNNER_IMAGE=ubuntu:${UBUNTU_VERSION}
```