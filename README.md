# Operator-sdk-installation

## Prerequisite:
* git should be installed
* go version 1.18
install go using this command:
```bash
sudo snap install --classic go
```

## Run the script file:
```bash
bash main.sh
```
## Or do it manually using following commands:

1. Set platform information:
```bash
export ARCH=$(case $(uname -m) in x86_64) echo -n amd64 ;; aarch64) echo -n arm64 ;; *) echo -n $(uname -m) ;; esac)
export OS=$(uname | awk '{print tolower($0)}')
```
Download the binary for your platform:
```bash
export OPERATOR_SDK_DL_URL=https://github.com/operator-framework/operator-sdk/releases/download/v1.22.2
curl -LO ${OPERATOR_SDK_DL_URL}/operator-sdk_${OS}_${ARCH}
```
2. Verify the downloaded binary 
Import the operator-sdk release GPG key from keyserver.ubuntu.com:
```bash
gpg --keyserver keyserver.ubuntu.com --recv-keys 052996E2A20B5C7E
```
Download the checksums file and its signature, then verify the signature:
```bash
curl -LO ${OPERATOR_SDK_DL_URL}/checksums.txt
curl -LO ${OPERATOR_SDK_DL_URL}/checksums.txt.asc
gpg -u "Operator SDK (release) <cncf-operator-sdk@cncf.io>" --verify checksums.txt.asc
```
Make sure the checksums match:
```bash
grep operator-sdk_${OS}_${ARCH} checksums.txt | sha256sum -c -
```

2. Install the release binary in your PATH
```bash
chmod +x operator-sdk_${OS}_${ARCH} && sudo mv operator-sdk_${OS}_${ARCH} /usr/local/bin/operator-sdk
```

3. Final step:
```bash
git clone https://github.com/operator-framework/operator-sdk
cd operator-sdk
git checkout master
make install
cd
```

It should be installed successfully.
