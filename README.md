# Helm-installation

Version: 4.3.0
Installing Helm
This guide shows how to install the Helm CLI. Helm can be installed either from source, or from pre-built binary releases.

From The Helm Project
The Helm project provides two ways to fetch and install Helm. These are the official methods to get Helm releases. In addition to that, the Helm community provides methods to install Helm through different package managers. Installation through those methods can be found below the official methods.

From the Binary Releases
Every release of Helm provides binary releases for a variety of OSes. These binary versions can be manually downloaded and installed.

Download your desired version
Verify the binary. See Verifying Helm Binaries on this page.
Unpack it 
`tar -zxvf helm-v4.0.0-linux-amd64.tar.gz`

Find the helm binary in the unpacked directory, and move it to its desired destination (mv linux-amd64/helm /usr/local/bin/helm)
From there, you should be able to run the client and find charts to install: helm help.

Note: Helm automated tests are performed for Linux AMD64 only during GitHub Actions builds and releases. Testing of other OSes are the responsibility of the community requesting Helm for the OS in question.

## From Chocolatey (Windows)
Members of the Helm community have contributed a Helm package build to Chocolatey. This package is generally up to date.

`choco install kubernetes-helm`


## From Apt (Debian/Ubuntu)
Members of the Helm community have contributed an Apt package for Debian/Ubuntu. This package is generally up to date. Thanks to Buildkite for hosting the repo.

HELM_BUILDKITE_APT_KEY_ID="DDF78C3E6EBB2D2CC223C95C62BA89D07698DBC6"

sudo apt-get install curl gpg apt-transport-https --yes

curl -fsSL https://packages.buildkite.com/helm-linux/helm-debian/gpgkey > "${TMPDIR:-/tmp}/helm.gpg"

## Ensure that the key ID matches to prevent a repository compromise from establishing an attacker controlled key

`if [ "$(gpg --show-keys --with-colons "${TMPDIR:-/tmp}/helm.gpg" | awk -F: '$1 == "fpr" {print $10}' | head -n 1)" != "${HELM_BUILDKITE_APT_KEY_ID}" ]; then echo "ERROR: Unexpected Helm APT key ID: potential key compromise"; exit 1; fi
`
`cat "${TMPDIR:-/tmp}/helm.gpg" | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/helm.gpg] https://packages.buildkite.com/helm-linux/helm-debian/any/ any main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list`

`sudo apt-get update
sudo apt-get install helm
`
