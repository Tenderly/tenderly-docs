# How to set up Hardhat

First things first, we need to add Hardhat into our project. You can follow along in an empty directory \(we’ll be using yarn\):

```text
yarn add hardhat
```

Next up, we’ll initiate our project by using the `npx hardhat` command:

```text
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.0.0-rc.1 👷‍

✔ What do you want to do? · Create a sample project
✔ Hardhat project root: · /src/super-awesome-project
✔ Do you want to add a .gitignore? (Y/n) · y
✔ Help us improve Hardhat with anonymous crash reports & basic usage data? (Y/n) · true
✔ Do you want to install the sample project's dependencies with yarn (@nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers)? (Y/n) · y
```

And we have a sample project set up! You can run **npx hardhat test** to check if everything is working.

